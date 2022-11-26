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

#### Euler也是一个借贷平台(允许用户19倍杠杆做空或者挖矿)
与其他借贷平台的区别, 从holder的角度,他们希望存入token,获取利息
从借款方的角度看,用户需要减少波动风险,并且建立空头仓位

这部分没看懂
问题一: 做空必须借到币, 用户是从哪里借的币
问题二: 做空应该要把借到的币在市场上先抛掉, 然后低价的时候再买回, 这一步怎么操作的

#### liquidity Liquity 是一种去中心化的借贷协议，只用 ETH 作抵押提取无息贷款。 是比较早期的项目.
#### makerdao 拍卖清算(鼻祖)
#### yfi 构建策略,提供dex搬砖,策略构建者分成





