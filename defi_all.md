## defi大全一览

#### compound
```
compound是一个银行类协议, 可以吧钱存进去,
在compound有存钱的可以把资产按照抵押率抵押给池子
从池子借出其他或者同一种资产
利息的计算方式是浮动利率,并且按照block数量计算需要支付多少利息
compound的borrow index的更新方式是比较多有人诟病的
因为每次用户调用totalBorrowsCurrent/borrowBalanceCurrent/exchangeRateCurrent...之类的查询信息或者其他函数
不论成功与否,都会更新这个index
这造成一些用户的不爽, 我虽然这gas是要负的,
但是为啥要让我又没成功,又要帮你用额外的gas更新这个index
```

#### aave
```
aave和compound差不多, 但是有两种利率方式, 一种是固定利率, 一种是浮动利率
固定利率的意思是, 按照借钱的时候约定的利息借钱, 后期如果市场利率因为资金率上升而涨价了
负债者的利率不会变化
浮动利率的计算方式和compound基本差不多
aave的利息是按照时间差计算的,比compound要更精准.
aave的interest rate更新就比较合理, 只有在pool withdraw/repay/borrow/deposit的时候会更新
```

