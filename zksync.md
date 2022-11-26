#### zk的意思就是零知识证明

zkroll利用默克尔树在链下存储账户状态, operator收集用户的交易, 交易完成之后, operator会执行
每个交易(包括校验balance,nounce,sign,执行状态转换), 交易执行完成之后, 生成一个新的默克尔tree,
为了证明链下状态转移是正确的, operator会在交易完成之后, 生成一个零知证明的proof.operator在执行交易后,
本地默克尔树root会由prev state root转换成横post state root

#### zksync的基本架构
1. zksync smart contract:     部署在eth mainnet,用于管理用户的balance, 验证zksync network操作的正确性
2. prover app:    
```
为a worker application,用于创建a proof for an executed block
prover application从server app中获取有效jobs,当有新的区块的时候,server app将提供a witness(input data to generate a proof),
然后prover application 开始工作, 当proof生成后, prover application会将该proof报告给server application
server application再讲该proof发布给zksync只能合约
proverapplication可以看成是ondemand worker, 当server application负载很高的时候, 允许多个prover applications
当没有交易数的入的, 则没有prover application,生成proover是非常消耗资源的
```
3. server application
```
运行zksync网络节点,server application的职能主要有
1. 监测智能合约上的onchain operations(如存款)
2. 接收交易
3. 生成zksyncv区块
4. 为executed blocks发起proof生成申请
5. 把数据发布到zksync 智能合约
```

#### 操作流程
zksync交易可以是layer1或者L2操作发起,经理三个状态 1/req 2/committed 3/verified. 
只有verified操作才是确定性状态
