# 以太坊的状态树
因此这些状态并非直接存储在区块链上，而是将这些状态维护在默克尔前缀树中，在区块链上仅记录对应的树 Root 值。使用简单的数据库来维护树的持久化内容，而这个用来维护映射的数据库叫做 StateDB。

以太坊每个节点提供evm给智能合约运行,这些智能合约的storage等一些状态发生改变的信息需要保存下来(包括之前的状态,为了失败的时候rollback)
那么以太坊不可能每次把所有人所有账户信息都重新生成一颗新的树, 那样会造成新增数据非常困难, 重新生成一棵树复杂度极高
所以以太坊设计了一种存储的数据结构叫做modified Merckle Particial Trie(也就是修改过的默克尔字典压缩树)
这种树有几个特点, 
* 第一, 因为我们的地址或者hash值都是非常稀疏的, 所以查找路径很大部分可以极度压缩
* 第二, 我们需要保证节点上传的信息和原来的树是吻合的, 所以采用了hash值作为路径进行查找遍历
* 第三, 我们需要修改数据的代价极小, 这种树的结构只用修改一小部分分支即可,不用整个树重构

从程序设计角度，StateDB 有多种用途：

维护账户状态到世界状态的映射。
支持修改、回滚、提交状态。
支持持久化状态到数据库中。
是状态进出默克尔树的媒介。

实际上 StateDB 充当状态（数据）、Trie(树)、LevelDB（存储）的协调者。可以从以下三个角度思考

打包block的时候, 不需要上传这个statedb, 只要上传block信息就行

```go
//core/state/statedb.go
type StateDB struct {
	//操作状态的底层数据库，在实例化 StateDB 时指定 ②。
	db         Database//这是一个interface, 数据库存储的地方,修改数据库真实的value的
	prefetcher *triePrefetcher
	trie       Trie//世界状态所在的树实例对象，现在只有以太坊改进的默克人前缀压缩树。
	originalRoot common.Hash // 原来的root,状态修改之前

	// This map holds 'live' objects, which will get modified while processing a state transition.
	// 活跃的对象储存在object里面, 在状态转移的时候, 这些数据会发生改动
	// use 账户地址as key的账户状态对象，能够在内存中维护使用过的账户。
	stateObjects        map[common.Address]*stateObject
	stateObjectsPending map[common.Address]struct{} // State objects finalized but not yet written to the trie
	//stateObjectsDirty： 标记被修改过的账户。
	stateObjectsDirty   map[common.Address]struct{} // State objects modified in the current execution
  //...
}
```
可以看到 stateObject 中维护关于某个账户的所有信息，涉及账户地址、账户地址哈希、账户属性、底层数据库、存储树等内容。
```go
// core/state/state_object.go
type stateObject struct {
	address  common.Address//对应的账户地址
	addrHash common.Hash  // 账户地址的哈希值
	data     types.StateAccount//账户属性
	db       *StateDB //底层数据库

	// 写缓存
	trie Trie // storage树, 第一次访问的时候是空. storage trie, which becomes non-nil on first access
	code Code // 合约字节码, 当代码载入的时候会被调用. contract bytecode, which gets set when code is loaded
	//...	
}

//core/types/state_account.go
// 状态账户信息
type StateAccount struct {
	Nonce    uint64
	Balance  *big.Int 
	Root     common.Hash // merkle root of the storage trie
	CodeHash []byte
}

```

```go
// core/state/statedb.go:408
// getStateObject retrieves a state object given by the address, returning nil if
// the object is not found or was deleted in this execution context. If you need
// to differentiate between non-existent/just-deleted, use getDeletedStateObject.
// 通过地址获取state obj.
func (self *StateDB) getStateObject(addr common.Address) (stateObject *stateObject) {
	if obj := self.stateObjects[addr]; obj != nil {//①先从缓存查询
		if obj.deleted {
			return nil
		}
		return obj
	}
 
	enc, err := self.trie.TryGet(addr[:])//②从树里面获取
	if len(enc) == 0 {
		self.setError(err)
		return nil
	}
	var data Account
	if err := rlp.DecodeBytes(enc, &data); err != nil {//③取到的value反序列化
		log.Error("Failed to decode state object", "addr", addr, "err", err)
		return nil
	}
	obj := newObject(self, addr, data)//④组装
	self.setStateObject(obj)//设置缓存
	return obj
}
```
```go

// core/state/database.go
// 这是一个接口, 因为不同节点的作用不同(有的只获取数据, 有的要挖矿), 所以轻节点使用odrDatabase, 正常
// 正常节点使用带缓存的cachingDB, 因为轻节点不存储数据, 而是通过向其他节点请求来获得数据
// 因此odrDATabase只是一个封装
// 一个普通节点已经内置levelDB, 为了提高读写性能, 在上面包了一层cache缓存
// Database wraps access to tries and contract code.
type Database interface {
	// OpenTrie opens the main account trie.
	//打开指定状态版本(root)的含世界状态的顶层树。
	OpenTrie(root common.Hash) (Trie, error)

	// OpenStorageTrie opens the storage trie of an account.
	//打开账户(addrHash)下指定状态版本(root)的账户数据存储树。
	OpenStorageTrie(addrHash, root common.Hash) (Trie, error)

	// CopyTrie returns an independent copy of the given trie.
	//深度拷贝树。
	CopyTrie(Trie) Trie

	// ContractCode retrieves a particular contract's code.
	//获取账户（addrHash）的合约，必须和合约哈希(codeHash)匹配。
	ContractCode(addrHash, codeHash common.Hash) ([]byte, error)

	// ContractCodeSize retrieves a particular contracts code's size.
	//获取指定合约大小
	ContractCodeSize(addrHash, codeHash common.Hash) (int, error)

	// TrieDB retrieves the low level trie database used for data storage.
	//获得 Trie 底层的数据驱动 DB，如: levedDB 、内存数据库、远程数据库
	TrieDB() *trie.Database
}
```

```go
// trie/trie.go
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

-----------------------------

#### example#1
读取以太坊账户balance
```go
db := state.NewDatabase(levelDB)
block = blockchain.CurrentBlock()
statedb,err := state.New(block.Root(), db)
balance := statedb.GetBlance(addr1)

// core/state/statedb.go
// GetBalance retrieves the balance from the given address or 0 if object not found
func (s *StateDB) GetBalance(addr common.Address) *big.Int {
	stateObject := s.getStateObject(addr) // 根据地址获取stateobj
	if stateObject != nil {
		return stateObject.Balance() // 如果存在就返回balance
	}
	return common.Big0
}

//core/state/state_object.go
func (s *stateObject) Balance() *big.Int {
	return s.data.Balance
}
```
#### example#2
张三转账给李四 100 ETH
```go
db: = state.NewDatabase(levelDB)
block = blockchain.CurrentBlock()
statedb, err := state.New(block.Root(), db)
 
statedb.SubBalance(张三,100 ETH)
statedb.AddBalance(李四,100 ETH)
statedb.Commit()//把当前内存中的trie写入数据库

// core/state/state_object.go
func (s *stateObject) SetBalance(amount *big.Int) {
	//写入日志
	s.db.journal.append(balanceChange{
		account: &s.address,
		prev:    new(big.Int).Set(s.data.Balance),
	})
	s.setBalance(amount)
}
//修改stateobjec里面的数据
func (s *stateObject) setBalance(amount *big.Int) {
	s.data.Balance = amount
}
```

commit方法, 把数据存到数据库
```go
// core/state/statedb.go:680
func (s *StateDB) Commit(deleteEmptyObjects bool) (root common.Hash, err error) {
	defer s.clearJournalAndRefund()
	
	 //因为在修改某账户信息是，将会记录变更流水（journal），因此在提交保存修改时只需要将在流水中存在的记录作为修改集①。 
	for addr := range s.journal.dirties {//①⑧⑨⑩
		s.stateObjectsDirty[addr] = struct{}{}
	}
	
	//所有访问过的账户信息，均被记录在 stateObjects 中，只需要遍历此集合 ② 便可以提交所有修改。
	for addr, stateObject := range s.stateObjects {//②
		_, isDirty := s.stateObjectsDirty[addr] // 查询数据是否被修改(如修改,则commit)
		switch {
		//如果数据自杀了,或者是空数据
		case stateObject.suicided || (isDirty && deleteEmptyObjects && stateObject.empty()):
			//③
			//当合约账户被销毁或者外部账户余额为 0 时可以从树中移除该账户，避免空账户影响树操作性能 ③。 
			//这里仅仅是从树中移除，并不能直接从持久层抹除。因为旧 State 依然依赖此账户，
			//一旦缺失将因为数据不完整而导致 OpenTrie 无法加载。同时，可方便其他节点同步 State 时不会缺失数据。
			s.deleteStateObject(stateObject)
		case isDirty://如果数据需要修改
			// 另外，如果集合中的账户有变更（isDirty），则需要提交此账户。如果该账户是刚部署的新合约(dirtyCode)④，
			if stateObject.code != nil && stateObject.dirtyCode {//④
				//把新部署的合约代码插入数据库
				s.db.TrieDB().InsertBlob(common.BytesToHash(stateObject.CodeHash()), stateObject.code)
				stateObject.dirtyCode = false
			}
			//则需要根据合约代码 HASH 作为键，存储对应的合约字节码。同时还将该账户专属的存储树提交⑤，
			//把合约专属的storage trie插入数据库
			if err := stateObject.CommitTrie(s.db); err != nil {//⑤
				//如果插入数据出错
				return common.Hash{}, err
			}
			//而账户属性也许有被修改，因此需要将此信息也更新到账户树中⑥。
			s.updateStateObject(stateObject)//⑥
		}
		delete(s.stateObjectsDirty, addr) // 从statedb脏数据中删除这个key
	}
	//至此, 每个objects都处理完了
	//...
	//提交账户trie
	root, err = s.trie.Commit(func(leaf []byte, parent common.Hash) error {//⑦
		//提交过程中, 涉及账户内容作为叶节点的, 在发送change的时候, 会变更账户节点和father节点的关系
		//记录关系的原因是用于在树的缓存使用, 尽可能的快速定位所需数据的位置和快速释放, 降低内存垃圾回收的压力
		var account Account
		if err := rlp.DecodeBytes(leaf, &account); err != nil {
			return nil
		}
		if account.Root != emptyRoot {
			s.db.TrieDB().Reference(account.Root, parent)
		}
		code := common.BytesToHash(account.CodeHash)
		if code != emptyCode {
			s.db.TrieDB().Reference(code, parent)
		}
		return nil
	})
	return root, err
}
```
** 如下图, 只有statedb commit的时候, 才会把数据写入leveldb. 上半部分都属于内存操作 **
![image](https://user-images.githubusercontent.com/1460432/205443024-c23c1f38-9913-43e8-8118-c7a64ea228ae.png)

----------------------------
以下信息需要打包上传到区块链
```go
// core/type/block.go
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

// core/type/block.go
// Block represents an entire block in the Ethereum blockchain.
type Block struct {
	//区块的数据结构
	header       *Header // 区块头
	uncles       []*Header
	transactions Transactions
}

// core/type/block.go
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
// core/types/receipt.go
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
布隆过滤器的实现
```go
// core/types/bloom9.go
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

// core/types/bloom9.go
// 私有方法(把布隆过滤器加起来)
// add is internal version of Add, which takes a scratch buffer for reuse (needs to be at least 6 bytes)
func (b *Bloom) add(d []byte, buf []byte) {
	i1, v1, i2, v2, i3, v3 := bloomValues(d, buf)
	b[i1] |= v1
	b[i2] |= v2
	b[i3] |= v3
}

// core/types/bloom9.go
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

// core/types/bloom9.go
// 查找
// BloomLookup is a convenience-method to check presence in the bloom filter
func BloomLookup(bin Bloom, topic bytesBacked) bool {
//碰撞测试,如果返回true,可能在里面
	return bin.Test(topic.Bytes())
}

```






