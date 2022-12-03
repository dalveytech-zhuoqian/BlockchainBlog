# 以太坊的状态树
以太坊每个节点提供evm给智能合约运行,这些智能合约的storage等一些状态发生改变的信息需要保存下来(包括之前的状态,为了失败的时候rollback)
那么以太坊不可能每次把所有人所有账户信息都重新生成一颗新的树, 那样会造成新增数据非常困难, 重新生成一棵树复杂度极高
所以以太坊设计了一种存储的数据结构叫做modified Merckle Particial Trie(也就是修改过的默克尔字典压缩树)
这种树有几个特点, 
* 第一, 因为我们的地址或者hash值都是非常稀疏的, 所以查找路径很大部分可以极度压缩
* 第二, 我们需要保证节点上传的信息和原来的树是吻合的, 所以采用了hash值作为路径进行查找遍历
* 第三, 我们需要修改数据的代价极小, 这种树的结构只用修改一小部分分支即可,不用整个树重构


打包block的时候, 不需要上传这个statedb, 只要上传block信息就行
```go
//MPT
type Trie struct {
	root  node
	owner common.Hash

	// Keep track of the number leaves which have been inserted since the last
	// hashing operation. This number will not directly map to the number of
	// actually unhashed nodes.
	unhashed int

	// db is the handler trie can retrieve nodes from. It's
	// only for reading purpose and not available for writing.
	db *Database

	// tracer is the tool to track the trie changes.
	// It will be reset after each commit operation.
	tracer *tracer
}
```

```go
type StateDB struct {
	db         Database//这是一个interface, 数据库存储的地方,修改数据库真实的value的
	prefetcher *triePrefetcher
	trie       Trie//这也是一个interaface
  originalRoot common.Hash // 原来的root,状态修改之前

  //...
}
```
----------------------------
以下信息需要打包上传到区块链
```go
type Header struct {
	// 区块头的数据结构
	ParentHash common.Hash `json:"parentHash"       gencodec:"required"`
	// 叔叔哈希, 就是父节点的相邻节点(也可能比父节点要大)
	UncleHash   common.Hash    `json:"sha3Uncles"       gencodec:"required"`
	Coinbase    common.Address `json:"miner"`
	// 状态树的根节点
	Root        common.Hash    `json:"stateRoot"        gencodec:"required"` 
	// 交易的根节点
	TxHash      common.Hash    `json:"transactionsRoot" gencodec:"required"`
	//收据的根节点
	ReceiptHash common.Hash    `json:"receiptsRoot"     gencodec:"required"`
	// 整个区块的布隆区块, 多个收据的bloom filter合并在一起得到的
	Bloom       Bloom          `json:"logsBloom"        gencodec:"required"`
}
```

```go
// Block represents an entire block in the Ethereum blockchain.
type Block struct {
	//区块的数据结构
	header       *Header // 区块头
	uncles       []*Header
	transactions Transactions
}
```

## core/types/block.go
```go
//创建了交易trie和收据trie
func NewBlock(header *Header, txs []*Transaction, uncles []*Header, receipts []*Receipt, hasher TrieHasher) *Block {
	b := &Block{header: CopyHeader(header)}

	// 创建交易数----------------------
	if len(txs) == 0 {
		b.header.TxHash = EmptyRootHash
	} else {
		// 跟哈希值
		b.header.TxHash = DeriveSha(Transactions(txs), hasher)
		b.transactions = make(Transactions, len(txs))
		copy(b.transactions, txs)
	}

	// 创建收据树---------------------
	if len(receipts) == 0 {
		b.header.ReceiptHash = EmptyRootHash
	} else {
		// root 哈希值
		b.header.ReceiptHash = DeriveSha(Receipts(receipts), hasher)
		// 创建bloom filter, 每个交易执行完之后, 会得到一个收据, 所以交易列表的长度应该和收据列表的长度一样
		b.header.Bloom = CreateBloom(receipts)
	}

	// 叔父区块---------------------
	if len(uncles) == 0 {
		b.header.UncleHash = EmptyUncleHash
	} else {
	//计算hash
		b.header.UncleHash = CalcUncleHash(uncles)
		b.uncles = make([]*Header, len(uncles))
		//构造trie
		for i := range uncles {
			b.uncles[i] = CopyHeader(uncles[i])
		}
	}

	return b
}
```

```go
//收据
// Receipt represents the results of a transaction.
type Receipt struct {
	// Consensus fields: These fields are defined by the Yellow Paper
	Type              uint8  `json:"type,omitempty"`
	PostState         []byte `json:"root"`
	Status            uint64 `json:"status"`
	CumulativeGasUsed uint64 `json:"cumulativeGasUsed" gencodec:"required"`
	// 布隆过滤器, 根据logs产生的
	Bloom             Bloom  `json:"logsBloom"         gencodec:"required"`
	// 每个收据可以包含多个log
	Logs              []*Log `json:"logs"              gencodec:"required"`

	// Implementation fields: These fields are added by geth when processing a transaction.
	// They are stored in the chain database.
	TxHash          common.Hash    `json:"transactionHash" gencodec:"required"`
	ContractAddress common.Address `json:"contractAddress"`
	GasUsed         uint64         `json:"gasUsed" gencodec:"required"`

	// Inclusion information: These fields provide information about the inclusion of the
	// transaction corresponding to this receipt.
	BlockHash        common.Hash `json:"blockHash,omitempty"`
	BlockNumber      *big.Int    `json:"blockNumber,omitempty"`
	TransactionIndex uint        `json:"transactionIndex"`
}
```

```go
// 私有方法, 布隆函数, 映射到布隆的计算
// bloomValues returns the bytes (index-value pairs) to set for the given data
func bloomValues(data []byte, hashbuf []byte) (uint, byte, uint, byte, uint, byte) {
	sha := hasherPool.Get().(crypto.KeccakState)
	sha.Reset()
	sha.Write(data)
	sha.Read(hashbuf)
	hasherPool.Put(sha)
	// The actual bits to flip
	v1 := byte(1 << (hashbuf[1] & 0x7))
	v2 := byte(1 << (hashbuf[3] & 0x7))
	v3 := byte(1 << (hashbuf[5] & 0x7))
	// The indices for the bytes to OR in
	i1 := BloomByteLength - uint((binary.BigEndian.Uint16(hashbuf)&0x7ff)>>3) - 1
	i2 := BloomByteLength - uint((binary.BigEndian.Uint16(hashbuf[2:])&0x7ff)>>3) - 1
	i3 := BloomByteLength - uint((binary.BigEndian.Uint16(hashbuf[4:])&0x7ff)>>3) - 1

	return i1, v1, i2, v2, i3, v3
}

// 私有方法(把布隆过滤器加起来)
// add is internal version of Add, which takes a scratch buffer for reuse (needs to be at least 6 bytes)
func (b *Bloom) add(d []byte, buf []byte) {
	i1, v1, i2, v2, i3, v3 := bloomValues(d, buf)
	b[i1] |= v1
	b[i2] |= v2
	b[i3] |= v3
}

// 
// CreateBloom creates a bloom filter out of the give Receipts (+Logs)
func CreateBloom(receipts Receipts) Bloom {
	buf := make([]byte, 6)
	var bin Bloom
	//对每个收据调用, 生成bloom
	for _, receipt := range receipts {
	//所有的收据的布隆加起来
		for _, log := range receipt.Logs {
		// 所有的logs的布隆 加起来
			bin.add(log.Address.Bytes(), buf)
			for _, b := range log.Topics {
			//所有的主题的布隆 加起来
				bin.add(b[:], buf)
			}
		}
	}
	return bin
}

// 查找
// BloomLookup is a convenience-method to check presence in the bloom filter
func BloomLookup(bin Bloom, topic bytesBacked) bool {
//碰撞测试,如果返回true,可能在里面
	return bin.Test(topic.Bytes())
}

```






