# gmx数据分析
https://api.thegraph.com/subgraphs/name/gmx-io/gmx-stats/graphql

# 订单总统计
```
{
    orderStat(id: "total") {
      openSwap
      openIncrease
      openDecrease
      executedSwap
      executedIncrease
      executedDecrease
      cancelledSwap
      cancelledIncrease
      cancelledDecrease
    }
  }
```


```json
{
  "data": {
    "orderStat": {
      "openSwap": 354,
      "openIncrease": 466,
      "openDecrease": 4583,
      "executedSwap": 2922,
      "executedIncrease": 29943,
      "executedDecrease": 50232,
      "cancelledSwap": 2196,
      "cancelledIncrease": 32040,
      "cancelledDecrease": 81293
    }
  }
}
```


# trading数据统计
```
{
  tradingStat(id: "total") {
    profit
    loss
    profitCumulative
    lossCumulative
    longOpenInterest
    shortOpenInterest
    liquidatedCollateral
    liquidatedCollateralCumulative
    timestamp
    period
  }
  orders
}
```
```json
{
  "data": {
    "tradingStat": {
      "profit": "253693508315453369468815923958815808115",
      "loss": "296008145653788506271436583940485719454",
      "profitCumulative": "253693508315453369468815923958815808115",
      "lossCumulative": "296008145653788506271436583940485719454",
      "longOpenInterest": "117459874341722020922772793923415312333",
      "shortOpenInterest": "28188194332496828199504886534335725806",
      "liquidatedCollateral": "38229372571880981942513689770322037159",
      "liquidatedCollateralCumulative": "38229372571880981942513689770322037159",
      "timestamp": 1673654400,
      "period": "total"
    }
  }
}
```


# 累计开订单总数大于1000的用户
```
query MyQuery {
  orders( where: {index: "1000"}) {
    index
    account
  }
}
```
```json
{
  "data": {
    "orders": [
      {
        "account": "0x597da53a39ea634be355e6028136b5e5f28c25d9"
      },
      {
        "account": "0x7f1e9629089b90c676463aaefb4a2bf6a79c5429"
      },
      {
        "account": "0x8305bdf7f6b3f5af53223d31783fb34f42de42a1"
      },
      {
        "account": "0xfde4a6c95020b7f9772f022fff3d5b9eec91df0c"
      }
    ]
  }
}
```



# 累计开订单总数大于100的用户
```
query MyQuery {
  orders( where: {index: "100"}) {
    index
    account
  }
}
```
```json
{
  "data": {
    "orders": [
      {
        "account": "0x0017dfe08bcc0dc9a323ca5d4831e371534e9320"
      },
      {
        "account": "0x0035502c012494172b2bb45117394267700ab6f1"
      },
      {
        "account": "0x0090be9ba80a5750264f938f0966c93d3dc47698"
      },
      {
        "account": "0x02add1377d59137bfc5eb358c2136ba9aee1e011"
      },
      {
        "account": "0x04d52e150e49c1bbc9ddde258060a3bf28d9fd70"
      },
      {
        "account": "0x055ddc40fbe329e3b43cb06f56a9ecdaca3ad521"
      },
      {
        "account": "0x05ff25c26352ce316c183fa226ed4de4b07e9e6f"
      },
      {
        "account": "0x08138243c8b2c5bb825763a7b065280a57af79e5"
      },
      {
        "account": "0x08b9f59f12ac64f93a6e2ff8015e8543648c1ff4"
      },
      {
        "account": "0x09216e1c6defe4405ac0d8337027c5909dc18ca2"
      },
      {
        "account": "0x09330039dc1e6be97d9c76da55535fc80962976c"
      },
      {
        "account": "0x0952615cd36904d97c736a0b0a5eea75c75e26d8"
      },
      {
        "account": "0x0baef0414391b623343b397466cf9921fbd391ef"
      },
      {
        "account": "0x0bbb9d764e6f4f6468a251ebd4bd50f008f7db21"
      },
      {
        "account": "0x0fc15b3b60fc55ad726abf575b8068ad0ddb9e65"
      },
      {
        "account": "0x1124aa0616ec8216539a14cdf25519115345658a"
      },
      {
        "account": "0x12571fddb14763492e9cd0e49fe56f3bed277f2c"
      },
      {
        "account": "0x129f4bd852fd04bf32ad28ae686e022dec008ed6"
      },
      {
        "account": "0x12b2946224aa50cc88cd026b9bdc19631a96564e"
      },
      {
        "account": "0x1470de04c1d42a13a950facf85cbdcecb86e98f0"
      },
      {
        "account": "0x1470de04c1d42a13a950facf85cbdcecb86e98f0"
      },
      {
        "account": "0x15e875bd7de4c3d1f57a9837c411a30ff5f12b38"
      },
      {
        "account": "0x15e875bd7de4c3d1f57a9837c411a30ff5f12b38"
      },
      {
        "account": "0x164e9765e50495b0a19770682cb30d442bda9c64"
      },
      {
        "account": "0x1890aaecd560d8c2aac3eeb2de3ced9c67ae5599"
      },
      {
        "account": "0x1acd5821cc6857d366a9b08aff1ee39a9d04c283"
      },
      {
        "account": "0x1b1a4fb64b5bb26dbd5a4b8a291e4de1bd5d58f9"
      },
      {
        "account": "0x1d8066e2ebdf5ead7ec52d92cea5d0b7d0278263"
      },
      {
        "account": "0x1e5fa3786d297a67c618d9a060fa0056ff058aef"
      },
      {
        "account": "0x1e8ebaa6d9bf90ca2800f97c95afedd6a64c91e2"
      },
      {
        "account": "0x222a227a5dc77c643e836556e573cb266998a870"
      },
      {
        "account": "0x22a7155442d22547379079dae7d4629bf0fc8260"
      },
      {
        "account": "0x22b2b18d2406daea73d59b59267efe781e3a2a3f"
      },
      {
        "account": "0x22b2b18d2406daea73d59b59267efe781e3a2a3f"
      },
      {
        "account": "0x23c9db00cd2c000679aa98113d3223c5a467dd1f"
      },
      {
        "account": "0x2406d61812bbe600767fce3392e868f14c9b67f0"
      },
      {
        "account": "0x24a3856c4e66292c875271a064aacb73ff3004b8"
      },
      {
        "account": "0x2542fc7f04fa388e06527bf819fe8d5d05e51d4b"
      },
      {
        "account": "0x26257b69b1050eed26d69f688c3be54a8073a703"
      },
      {
        "account": "0x266559ff8500fdae9675647c81531b1c0f2efa1c"
      },
      {
        "account": "0x2797ff1c04a20abec5b8bc2a5b76a41d70d097c3"
      },
      {
        "account": "0x2797ff1c04a20abec5b8bc2a5b76a41d70d097c3"
      },
      {
        "account": "0x28ead95628610b4ee91408cfe1c225c71ab6e7a8"
      },
      {
        "account": "0x290bffbe2803bb4c1fee41d03f2beffe6ddcbac3"
      },
      {
        "account": "0x290bffbe2803bb4c1fee41d03f2beffe6ddcbac3"
      },
      {
        "account": "0x29766cc82eab4ed00a0c7f287a07cee72d7705cc"
      },
      {
        "account": "0x29f8c091a17a75c98f95b079067ffd23639b7f91"
      },
      {
        "account": "0x2afa70ab8b5f36753d2f3e26576dff0d91254a44"
      },
      {
        "account": "0x2afa70ab8b5f36753d2f3e26576dff0d91254a44"
      },
      {
        "account": "0x2b11db55e500916217e5b8f73d3bdb8501374200"
      },
      {
        "account": "0x2c9c3393156329641b11a8132e013edbbb0f087c"
      },
      {
        "account": "0x2cbf930fcf88a3dde079a516b534138e088c4651"
      },
      {
        "account": "0x2d617f438116d107e07c49d61d4d7217bb924c2f"
      },
      {
        "account": "0x2deeca909787b9553dba4ade8f78f67dbe22d5b9"
      },
      {
        "account": "0x300e780479437092cd0a40a6f3b7eae5dcd33226"
      },
      {
        "account": "0x31d75ac26642f0dc3367d3ec5da7e592eff42577"
      },
      {
        "account": "0x31f1f8b1c5ed47b8ecc941e55f46251303b2d782"
      },
      {
        "account": "0x333c91876481f9e913367abc67ede7b46985f7f7"
      },
      {
        "account": "0x33b670487eb6942a6964e730660aae1a25b23ce3"
      },
      {
        "account": "0x34e809e36f37c4be3f0b8448ac0447f0c3173789"
      },
      {
        "account": "0x356cd07b0b96860ac6c592de434772de9bd5b60f"
      },
      {
        "account": "0x365f32001609c990b2c50e7e9eea67f2f5867805"
      },
      {
        "account": "0x37106760d6c250df1e366e0749c17ee14dc65652"
      },
      {
        "account": "0x37c2a74bf47bf2295127bca9fabcc7b334823c27"
      },
      {
        "account": "0x3819546fd6f02baa624cb7baf0265c032d546071"
      },
      {
        "account": "0x38866c8e75e91709d92a78a7ba8a3f5d87027808"
      },
      {
        "account": "0x396891fced4c401ea9527cbdb2e753aafdf45ade"
      },
      {
        "account": "0x3b36997337d9bc290af1c3fb924a85b32d94b880"
      },
      {
        "account": "0x3c045d92b7c3bb83e2018e2e296f6a0bc0e2eb07"
      },
      {
        "account": "0x3c7406f59035671ddb9b1bfa81d735d065bea88c"
      },
      {
        "account": "0x3c7648e3526f64aa13bb28206edecb9200dfbf4d"
      },
      {
        "account": "0x3d10d2029ac65a5057c0358de6f72da1f4d39d9f"
      },
      {
        "account": "0x4188d6d3a476affd6781fd8d68d280e0d8ab774f"
      },
      {
        "account": "0x4188d6d3a476affd6781fd8d68d280e0d8ab774f"
      },
      {
        "account": "0x4207696e4a13f1b0733174dde8d314f801add847"
      },
      {
        "account": "0x42e4880442814a2c6e86453144c16fcb3e0e52f2"
      },
      {
        "account": "0x439db15ee11f448bb05b257230f36221bee23b29"
      },
      {
        "account": "0x4594de64d7ffcabf324d6420f186b6325bce5c64"
      },
      {
        "account": "0x47a3e0e190c44252305424ef5c1257036bfc0aec"
      },
      {
        "account": "0x47cfb486c9e04bf9113f0b5a68d5b681947d98fd"
      },
      {
        "account": "0x48008b2060d9b948d6ef38238cda3065554492ed"
      },
      {
        "account": "0x48202a51c0d5d81b3ebed55016408a0e0a0afaae"
      },
      {
        "account": "0x4944b51e22d94840b0e86551b4dfb0b67d1cd487"
      },
      {
        "account": "0x498a1e3d13b5640e2eae64cc62d185b22d9a9298"
      },
      {
        "account": "0x4b94480c5cfc9ccb6beebc36ba82f67901b22461"
      },
      {
        "account": "0x4cee629583e2eeff509e2b5c17910c3d0c55eccf"
      },
      {
        "account": "0x4ebe485c1df060f6fc6e3c3b200ebc21fe11a94d"
      },
      {
        "account": "0x5221e4a2e1face94bf61d7b6d8534d66d633bd01"
      },
      {
        "account": "0x52b84469dbf38fe5edeb79a5171ea101a3e0b1a9"
      },
      {
        "account": "0x5378e749d3c7f7507bb6cd40d4b4a4e806e5af35"
      },
      {
        "account": "0x53d8edf6a54239eb785ec72213919fb6b6b73598"
      },
      {
        "account": "0x53d8edf6a54239eb785ec72213919fb6b6b73598"
      },
      {
        "account": "0x54278ce843a5e0763e6c3ff4ebecc840e238240f"
      },
      {
        "account": "0x54278ce843a5e0763e6c3ff4ebecc840e238240f"
      },
      {
        "account": "0x54789c6961317e9fe15c957adedec53069e9cc32"
      },
      {
        "account": "0x5481484616fd5bcc97dd5bbb4f58daadf34d099d"
      },
      {
        "account": "0x5765cd5e418ac64b13cf7c4fe22c25ed6885c24f"
      },
      {
        "account": "0x57790b0b998ba2c9dfe55e73300ffc1d3e457169"
      },
      {
        "account": "0x585020d9c6b56874b78979f29d84e082d34f0b2a"
      },
      {
        "account": "0x58c364ed8bc1c17e4e14cbe07ae112582004a32e"
      }
    ]
  }
}
```

# 金额大于1,000,123的订单
```
query MyQuery {
  orders(where: {
    size_gt: "10010231978679208721213980045706490000"
    type: "increase"
    status:"executed"
  }) {
    account
    size
    type
    status
  }
}
```
```json
{
  "data": {
    "orders": []
  }
}
```


# 金额大于100,123的订单
```
query MyQuery {
  orders(where: {
    size_gt: "1010231978679208721213980045706490000"
    type: "increase"
    status:"executed"
  }) {
    account
    size
    type
    status
  }
}
```
```json
{
  "data": {
    "orders": [
      {
        "account": "0x15e875bd7de4c3d1f57a9837c411a30ff5f12b38",
        "size": "1308468646288209606986688000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x1a2f2405ba4d5f3c68c413d136ad81617dbacf58",
        "size": "1181725488999999999999374080000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x1a4bb4eca30a9e332f363d3cbdf40848c176279a",
        "size": "1437841088318115305822642400000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x1a4bb4eca30a9e332f363d3cbdf40848c176279a",
        "size": "1543406247228232896650858750000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x1a4bb4eca30a9e332f363d3cbdf40848c176279a",
        "size": "1233584737248697221040305400000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x254ca3c9c98cdb37a642d23a9946d1f1a929cd87",
        "size": "1080135456170376396784359600000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x254ca3c9c98cdb37a642d23a9946d1f1a929cd87",
        "size": "1010605373208738572690680880000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x2a9c628f9b1b06a881407ae457ffb0e51fb7e752",
        "size": "5656804673267326732671700000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x2a9c628f9b1b06a881407ae457ffb0e51fb7e752",
        "size": "5647619405940594059405115000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x2d62bd2bbc36db52040e3dca97afbe12c9773354",
        "size": "2951737020863658418242372500000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x2d62bd2bbc36db52040e3dca97afbe12c9773354",
        "size": "2941176470588235294116625000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x2fba909aed4345ac0c67c75c51d955f822b14629",
        "size": "1147201586560000000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x2fba909aed4345ac0c67c75c51d955f822b14629",
        "size": "1452649764884999999999456880000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x346ccfdee95c7bd36b60bfe028d0f40d3517f22f",
        "size": "1032070530297029702969540000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x3f5504ecd6dc1d7c978b5812b2e38d251ce7167c",
        "size": "1449419239551275687481344000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x5152746bbc7d75c23d3982a563f01af55806c718",
        "size": "1081107523725662850991960500000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x55913786aceedee35144def52a9e9a65bd24279d",
        "size": "1200474214582098399525270000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x55913786aceedee35144def52a9e9a65bd24279d",
        "size": "1551724137931034482758384300000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x55913786aceedee35144def52a9e9a65bd24279d",
        "size": "2498054054054054054053395000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x55913786aceedee35144def52a9e9a65bd24279d",
        "size": "2929999999999999999999484580000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x55913786aceedee35144def52a9e9a65bd24279d",
        "size": "2498849557522123893804143900000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x5b16557f1b63f981d1b4cfad18e7a4d5283fefc6",
        "size": "3589084581119999999996660000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x5b16557f1b63f981d1b4cfad18e7a4d5283fefc6",
        "size": "1143914468430359999997055000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x5dc77c46bc02ed80a9c7d0a5bf277068e2c2cbb2",
        "size": "1180576419213973799126160000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x6150dffebb529b87c90bc350c7dae2765a06a429",
        "size": "4352682370908086249998200000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x65b1b96bd01926d3d60dd3c8bc452f22819443a9",
        "size": "4591384123291654550740964000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x65b1b96bd01926d3d60dd3c8bc452f22819443a9",
        "size": "1178335653209220000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x65b1b96bd01926d3d60dd3c8bc452f22819443a9",
        "size": "2851290811367390000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x65b1b96bd01926d3d60dd3c8bc452f22819443a9",
        "size": "3295318247472315840153214400000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x65b1b96bd01926d3d60dd3c8bc452f22819443a9",
        "size": "2099533437013996889578972000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x65b1b96bd01926d3d60dd3c8bc452f22819443a9",
        "size": "4298203011136320000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x65b1b96bd01926d3d60dd3c8bc452f22819443a9",
        "size": "3300733496288040000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x65b1b96bd01926d3d60dd3c8bc452f22819443a9",
        "size": "4546492957672640000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x6be5b497578d2260bc27afb91af26666dafe3a47",
        "size": "3031259353858221394253195700000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x6de4d784f6019aa9dc281b368023e403ea017601",
        "size": "1175266911139199999996590000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x8376070c2a30b3174c7da50fa03095239953be16",
        "size": "1075140243902439024389820000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x8376070c2a30b3174c7da50fa03095239953be16",
        "size": "1160757241959067458385685000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x852237393f7cb573a62165101670a703bf08a1b8",
        "size": "2876992634643377001454314500000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x88cdd4e3fa3585a364c30d217f6a31c52afa3f1f",
        "size": "1380670611439842209072178000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x88cdd4e3fa3585a364c30d217f6a31c52afa3f1f",
        "size": "1367478866235703630034673000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x89261103fa88a913c8d0debd00574fd16895407d",
        "size": "2023693318920000000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x89261103fa88a913c8d0debd00574fd16895407d",
        "size": "7403754599999999999997411000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x8e3ef6f89fe04a306dc6aaa44b7fd551e288a801",
        "size": "5775650907590588235293850000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x8e3ef6f89fe04a306dc6aaa44b7fd551e288a801",
        "size": "2535428475247524752475238000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x8e3ef6f89fe04a306dc6aaa44b7fd551e288a801",
        "size": "4534876009411764705881822000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x8e3ef6f89fe04a306dc6aaa44b7fd551e288a801",
        "size": "3887070551568627450980310000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x8e3ef6f89fe04a306dc6aaa44b7fd551e288a801",
        "size": "3352723152709359605909930000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x8e3ef6f89fe04a306dc6aaa44b7fd551e288a801",
        "size": "2929117647058823529411200000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x8e3ef6f89fe04a306dc6aaa44b7fd551e288a801",
        "size": "2054058652550805882352290000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x8e3ef6f89fe04a306dc6aaa44b7fd551e288a801",
        "size": "2080127133529411764705762000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x8e3ef6f89fe04a306dc6aaa44b7fd551e288a801",
        "size": "2212102339178664705881160000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x8e3ef6f89fe04a306dc6aaa44b7fd551e288a801",
        "size": "2298420301568627450980320000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x8e3ef6f89fe04a306dc6aaa44b7fd551e288a801",
        "size": "3921568627450980392155853000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x8e3ef6f89fe04a306dc6aaa44b7fd551e288a801",
        "size": "3888779739666666666666262500000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x8e3ef6f89fe04a306dc6aaa44b7fd551e288a801",
        "size": "6092509891431751456310600000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x926f31d9d9416234e50d5bba96b8f86dee82e87e",
        "size": "1198494769920000000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x926f31d9d9416234e50d5bba96b8f86dee82e87e",
        "size": "1301029522433100000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x9cdfecedee9bdee998e7ae615910b714715e1e06",
        "size": "1152073632398000000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x9f898a9baa8b69b7ee29702ca5a3cd03f31e848a",
        "size": "1141116707805155089221795000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x9f898a9baa8b69b7ee29702ca5a3cd03f31e848a",
        "size": "1817377257589054183266675000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x9f898a9baa8b69b7ee29702ca5a3cd03f31e848a",
        "size": "1442227717441710000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x9f898a9baa8b69b7ee29702ca5a3cd03f31e848a",
        "size": "3028140000661500000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x9f898a9baa8b69b7ee29702ca5a3cd03f31e848a",
        "size": "1270165304087736789630030000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x9f898a9baa8b69b7ee29702ca5a3cd03f31e848a",
        "size": "2004807157077443758709780000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x9f898a9baa8b69b7ee29702ca5a3cd03f31e848a",
        "size": "1014596893667861409795465000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x9f898a9baa8b69b7ee29702ca5a3cd03f31e848a",
        "size": "2083504278606965174128428000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x9f898a9baa8b69b7ee29702ca5a3cd03f31e848a",
        "size": "1024770402717127607956100000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x9f898a9baa8b69b7ee29702ca5a3cd03f31e848a",
        "size": "3019634394752534287416780000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x9f898a9baa8b69b7ee29702ca5a3cd03f31e848a",
        "size": "2032947893269613699720920000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x9f898a9baa8b69b7ee29702ca5a3cd03f31e848a",
        "size": "2066733094384707287932612500000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x9f898a9baa8b69b7ee29702ca5a3cd03f31e848a",
        "size": "1780055373580394500895288000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x9f898a9baa8b69b7ee29702ca5a3cd03f31e848a",
        "size": "2648749885833416062740875000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0xa688bc5e676325cc5fc891ac48fe442f6298a432",
        "size": "6639108910891089108910884000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0xa75fb3bd645a02b59a9963c3cc12f34dc86b9660",
        "size": "4660000000000000000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0xa75fb3bd645a02b59a9963c3cc12f34dc86b9660",
        "size": "1165000000000000000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0xa75fb3bd645a02b59a9963c3cc12f34dc86b9660",
        "size": "2056262863775000000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0xa75fb3bd645a02b59a9963c3cc12f34dc86b9660",
        "size": "1479864143566000000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0xb396e2490a505104c310e2e8c799a391480f6828",
        "size": "2099453658536585365852354000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0xb5beb7b5aa8430a43a516d583e498ce1788446b9",
        "size": "3182711198428290766207590000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0xb6734a7597cfa9ae7e7c6409bbbd4ec2c0a76332",
        "size": "1277018827146000000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0xb6734a7597cfa9ae7e7c6409bbbd4ec2c0a76332",
        "size": "2238022751517000000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0xb8e56d497ca6432b93ed59c4d357b98e144d27be",
        "size": "1983359483610536200000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0xb8e56d497ca6432b93ed59c4d357b98e144d27be",
        "size": "3290293216444291202837055000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0xb8e56d497ca6432b93ed59c4d357b98e144d27be",
        "size": "2838385722453629629628512000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0xbd2670d4253103efd9272ead153b0ce82182f3e5",
        "size": "1980198019801980198019072000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0xc7748db7338cc106aeb041b59965d0101eda8636",
        "size": "1153455039733920000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0xc7748db7338cc106aeb041b59965d0101eda8636",
        "size": "1057157109303416470588036000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0xc7748db7338cc106aeb041b59965d0101eda8636",
        "size": "1176470588235294117646947000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0xcb696fd8e239dd68337c70f542c2e38686849e90",
        "size": "1479864143619602134885490000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0xcb696fd8e239dd68337c70f542c2e38686849e90",
        "size": "1617852294191250000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0xd2acf36f772074172a20394282ec6d96b79ace3c",
        "size": "4415252045074442257872576000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0xd5c6767df4e33cc8d6a67097b982ee48357106c0",
        "size": "1085877905840984567298253000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0xda6e7ff7f96ac290bf8a040d03bd0b114beeb7dc",
        "size": "1619381516190476190475108000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0xe1249fc86c7e52130e9ab75c14f10b310cf6280d",
        "size": "1367126035175629268292456000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0xe1249fc86c7e52130e9ab75c14f10b310cf6280d",
        "size": "1558564590830439856268000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0xe1249fc86c7e52130e9ab75c14f10b310cf6280d",
        "size": "1123044584956156862744391000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0xe1249fc86c7e52130e9ab75c14f10b310cf6280d",
        "size": "1586509831010063414632944000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0xe2e8369ec7de1a6021edc7045cd3a51040998922",
        "size": "2757528203677826297912640000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0xe2e8369ec7de1a6021edc7045cd3a51040998922",
        "size": "2417830356466763706938025000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0xe5ce9e5d7787a07a0d8f4b87b6f782edd79c1162",
        "size": "2118625342830000000000000000000000000",
        "type": "increase",
        "status": "executed"
      }
    ]
  }
}
```

# 金额大于10123的订单(已经被执行的开仓订单)
```
query MyQuery {
  orders(where: {
    size_gt: "101231978679208721213980045706490000"
    type: "increase"
    status:"executed"
  }) {
    account
    size
    type
    status
  }
}
```
```json
{
  "data": {
    "orders": [
      {
        "account": "0x000015e5428b2500006830afcd519800585fa6b3",
        "size": "196078431372549019606466000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x000015e5428b2500006830afcd519800585fa6b3",
        "size": "196078431372549019607610000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x000015e5428b2500006830afcd519800585fa6b3",
        "size": "392156862745098039215081000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x000015e5428b2500006830afcd519800585fa6b3",
        "size": "248258356251334303735685000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x000015e5428b2500006830afcd519800585fa6b3",
        "size": "134626028837171000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0035502c012494172b2bb45117394267700ab6f1",
        "size": "112170000000000000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0035502c012494172b2bb45117394267700ab6f1",
        "size": "111899000000000000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0035502c012494172b2bb45117394267700ab6f1",
        "size": "110790000000000000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0035502c012494172b2bb45117394267700ab6f1",
        "size": "117499000000000000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0035502c012494172b2bb45117394267700ab6f1",
        "size": "116900000000000000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0035502c012494172b2bb45117394267700ab6f1",
        "size": "120000000000000000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0035502c012494172b2bb45117394267700ab6f1",
        "size": "120077000000000000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0035502c012494172b2bb45117394267700ab6f1",
        "size": "119595000000000000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0035502c012494172b2bb45117394267700ab6f1",
        "size": "404761904761904761904050000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0035502c012494172b2bb45117394267700ab6f1",
        "size": "238446916285714285714110000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0035502c012494172b2bb45117394267700ab6f1",
        "size": "128131000000000000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0035502c012494172b2bb45117394267700ab6f1",
        "size": "126300000000000000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0035502c012494172b2bb45117394267700ab6f1",
        "size": "125800000000000000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0035502c012494172b2bb45117394267700ab6f1",
        "size": "126600000000000000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0035502c012494172b2bb45117394267700ab6f1",
        "size": "125600000000000000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0035502c012494172b2bb45117394267700ab6f1",
        "size": "125050000000000000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0035502c012494172b2bb45117394267700ab6f1",
        "size": "126800000000000000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0035502c012494172b2bb45117394267700ab6f1",
        "size": "246120000000000000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0499d821624288509cad73b17f57cc528f066ca5",
        "size": "183528039049032933491850000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x04d52e150e49c1bbc9ddde258060a3bf28d9fd70",
        "size": "193582037697599999997360000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x04d52e150e49c1bbc9ddde258060a3bf28d9fd70",
        "size": "109493725311359999999696000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0561a78021d8966ddd20c28c6c4318d8675ee1f0",
        "size": "109964326913676801251280000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0916ea6008118f1ffe4f4a971e1684c1f741f7eb",
        "size": "505078505117623723097500000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0916ea6008118f1ffe4f4a971e1684c1f741f7eb",
        "size": "512240430197061451404555000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0a0357e50db54027f39373db16ef3461ce770feb",
        "size": "103138141600000000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0a53d9586dd052a06fca7649a02b973cc164c1b4",
        "size": "120557355801067442988800000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0a53d9586dd052a06fca7649a02b973cc164c1b4",
        "size": "284472729334684568930700000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0a53d9586dd052a06fca7649a02b973cc164c1b4",
        "size": "317066210277535177098091500000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0ab7e750416bb5e6006cdf86fab1a88486b51dd1",
        "size": "212735524970507274870345000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0ab7e750416bb5e6006cdf86fab1a88486b51dd1",
        "size": "300634331571736151887560000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0c2db7cb6d59b0f68c72480460b1d225e71740b4",
        "size": "103681860137399999999650000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0e4f8dbc7b060c53849f6c1e29066df876e771ce",
        "size": "641658440276406712733618000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0e4f8dbc7b060c53849f6c1e29066df876e771ce",
        "size": "148514851485148514850834000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0e4f8dbc7b060c53849f6c1e29066df876e771ce",
        "size": "241694847821762482592760000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0e4f8dbc7b060c53849f6c1e29066df876e771ce",
        "size": "151455157394575331616912000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0e4f8dbc7b060c53849f6c1e29066df876e771ce",
        "size": "361571272691201269714899000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0e4f8dbc7b060c53849f6c1e29066df876e771ce",
        "size": "240093695100527034939740000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0e4f8dbc7b060c53849f6c1e29066df876e771ce",
        "size": "402240825233088672881475000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0e4f8dbc7b060c53849f6c1e29066df876e771ce",
        "size": "348929421094386849671360000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0e4f8dbc7b060c53849f6c1e29066df876e771ce",
        "size": "242124034079651277986800000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0e4f8dbc7b060c53849f6c1e29066df876e771ce",
        "size": "102929532858273950909496000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0e4f8dbc7b060c53849f6c1e29066df876e771ce",
        "size": "308788598574821852730425000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0e4f8dbc7b060c53849f6c1e29066df876e771ce",
        "size": "245073769581830000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0e4f8dbc7b060c53849f6c1e29066df876e771ce",
        "size": "389980305111920000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0e4f8dbc7b060c53849f6c1e29066df876e771ce",
        "size": "254874789666435712164416000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0e4f8dbc7b060c53849f6c1e29066df876e771ce",
        "size": "497237756231851324010432000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0e4f8dbc7b060c53849f6c1e29066df876e771ce",
        "size": "167197452120500000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0e4f8dbc7b060c53849f6c1e29066df876e771ce",
        "size": "236220472368840000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0e4f8dbc7b060c53849f6c1e29066df876e771ce",
        "size": "276898734177215189872514000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0e4f8dbc7b060c53849f6c1e29066df876e771ce",
        "size": "333004440059200789342572000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0e4f8dbc7b060c53849f6c1e29066df876e771ce",
        "size": "315955766024060000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0e4f8dbc7b060c53849f6c1e29066df876e771ce",
        "size": "467797757769507591813490000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0e4f8dbc7b060c53849f6c1e29066df876e771ce",
        "size": "438849636724290000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0e4f8dbc7b060c53849f6c1e29066df876e771ce",
        "size": "240170347628008319301095000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0e4f8dbc7b060c53849f6c1e29066df876e771ce",
        "size": "247524752475247524751476000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0ec17322313209a2f6c04b5cf8dacac78b2383b2",
        "size": "295972828611900000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0efe81db03b6a7828d2097418b8d804393277727",
        "size": "731104000000000000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0f2cd0c6474594b2d3830e1076f40d6828641a0f",
        "size": "134146341463414634145120000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0f2cd0c6474594b2d3830e1076f40d6828641a0f",
        "size": "291262135802824000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0f4bc970e348a061b69d05b7e2e5c13eb687e5e3",
        "size": "156460788587478983284373000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0f4bc970e348a061b69d05b7e2e5c13eb687e5e3",
        "size": "190375264563346849964418000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0f4bc970e348a061b69d05b7e2e5c13eb687e5e3",
        "size": "106495238095238095237440000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x0f4bc970e348a061b69d05b7e2e5c13eb687e5e3",
        "size": "106417142857142857141850000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x12a3051760ec32abe13d8d45af00e0cc4f292ccd",
        "size": "294561576354679802954940000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x12a3051760ec32abe13d8d45af00e0cc4f292ccd",
        "size": "296287853413456802284192000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x12a3051760ec32abe13d8d45af00e0cc4f292ccd",
        "size": "597482701825510959309940000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x12a3051760ec32abe13d8d45af00e0cc4f292ccd",
        "size": "147236453201970443349605000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x12d3d411d010891a88bff2401bd73fa41fb1316e",
        "size": "528800000000000000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x12d3d411d010891a88bff2401bd73fa41fb1316e",
        "size": "537400000000000000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x12d3d411d010891a88bff2401bd73fa41fb1316e",
        "size": "273100000000000000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x12d3d411d010891a88bff2401bd73fa41fb1316e",
        "size": "278700000000000000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x12d3d411d010891a88bff2401bd73fa41fb1316e",
        "size": "380636342602098267998676000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x12d3d411d010891a88bff2401bd73fa41fb1316e",
        "size": "275700000000000000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x12d3d411d010891a88bff2401bd73fa41fb1316e",
        "size": "281400000000000000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x12d3d411d010891a88bff2401bd73fa41fb1316e",
        "size": "503762715709913651198856000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x138dd537d56f2f2761a6fc0a2a0ace67d55480fe",
        "size": "645300000000000000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x138dd537d56f2f2761a6fc0a2a0ace67d55480fe",
        "size": "716550000000000000000000000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x14dd1939fed9623569c2bf7c92145a5d94cbf8b4",
        "size": "101949915866574284864535000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x14dd1939fed9623569c2bf7c92145a5d94cbf8b4",
        "size": "150925116360545519006295000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x1501cf2e9afd2624a485e675427609a1932772ec",
        "size": "214927327528466175485593500000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x15e875bd7de4c3d1f57a9837c411a30ff5f12b38",
        "size": "147986414361960213487740000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x15e875bd7de4c3d1f57a9837c411a30ff5f12b38",
        "size": "147986414361960213487660000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x15e875bd7de4c3d1f57a9837c411a30ff5f12b38",
        "size": "147986414361960213487660000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x15e875bd7de4c3d1f57a9837c411a30ff5f12b38",
        "size": "145063106796116504853300000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x15e875bd7de4c3d1f57a9837c411a30ff5f12b38",
        "size": "147572052401746724890696000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x15e875bd7de4c3d1f57a9837c411a30ff5f12b38",
        "size": "147409267345948568655833000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x15e875bd7de4c3d1f57a9837c411a30ff5f12b38",
        "size": "147986414361960213488002950000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x15e875bd7de4c3d1f57a9837c411a30ff5f12b38",
        "size": "147986414361960213487535910000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x15e875bd7de4c3d1f57a9837c411a30ff5f12b38",
        "size": "147986414361960213487510440000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x15e875bd7de4c3d1f57a9837c411a30ff5f12b38",
        "size": "147986414361960213487500000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x15e875bd7de4c3d1f57a9837c411a30ff5f12b38",
        "size": "147986414361960213488400000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x15e875bd7de4c3d1f57a9837c411a30ff5f12b38",
        "size": "147986414361960213488085000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x15e875bd7de4c3d1f57a9837c411a30ff5f12b38",
        "size": "147986414361960213487526000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x15e875bd7de4c3d1f57a9837c411a30ff5f12b38",
        "size": "147986414361960213487500000000000000",
        "type": "increase",
        "status": "executed"
      },
      {
        "account": "0x15e875bd7de4c3d1f57a9837c411a30ff5f12b38",
        "size": "147986414361960213488490000000000000",
        "type": "increase",
        "status": "executed"
      }
    ]
  }
}
```

