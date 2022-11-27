# 什么是typechain

Ethereum智能合约的TypeScript绑定
TypeChain是一个代码生成器-提供ABI文件和区块链访问库的名称（ethers/truffle/web3.js），您将获得与给定库兼容的TypeScript类型。

静态类型-您将不再调用不存在的方法

IDE支持-适用于任何支持Typescript的IDE

可扩展-使用多种不同的工具：ether.js、hardhat、truffle、Web3.js或您可以创建自己的目标

无摩擦-适用于简单的JSON ABI文件以及Truffle/Hardhat工件

---

需要添加tsconfig.json

```JSON
{
  "compilerOptions": {
    "target": "es5",
    "module": "commonjs",
    "strict": true,
    "esModuleInterop": true,
    "outDir": "dist",
    "resolveJsonModule": true
  },
  "include": ["./scripts", "./test", "./typechain-types"],
  "files": ["./hardhat.config.ts"]
}
```




需要在hardhat.config.ts里面添加

```TS
typechain: {
    target: 'truffle-v5',
  }
  ```

