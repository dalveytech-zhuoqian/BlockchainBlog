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



