## zksync demo源码阅读

## 部署Greeter
```ts
import { Deployer } from "@matterlabs/hardhat-zksync-deploy"; // 导入zksync的库

//准备工作
const wallet = new Wallet("<private key>");
const deployer = new Deployer(hre, wallet);//这是zk的部署人
const artifact = await deployer.loadArtifact("Greeter");


// 往部署人的zk wallet存入0.001个eth,否则无法完成部署操作
const depositAmount = ethers.utils.parseEther("0.001");
const depositHandle = await deployer.zkWallet.deposit({
  to: deployer.zkWallet.address,
  token: utils.ETH_ADDRESS,
  amount: depositAmount,
});
//等待存款操作完成
await depositHandle.wait();

// 部署Greeter, 并且设置greeting信息为`Hi there!`
const greeting = "Hi there!";
const greeterContract = await deployer.deploy(artifact, [greeting]);

//打印部署完成的信息
const contractAddress = greeterContract.address;
console.log(`${artifact.contractName} was deployed to ${contractAddress}`); // 打印地址
```

## 部署完成后, app.vue看看greeting信息是否是`Hi there!`
```js
// 这里填入上一步部署的智能合约地址
const GREETER_CONTRACT_ADDRESS = '<your smart contract address>'; // TODO: Add smart contract address
const GREETER_CONTRACT_ABI = require("./abi.json"); //这是编译的时候生成的json abi信息
const provider = new Provider('https://zksync2-testnet.zksync.dev'); // 这里填入zk的地址,而不是eth mainnet地址了
const signer = (new Web3Provider(window.ethereum)).getSigner();
const contract = new Contract(
          GREETER_CONTRACT_ADDRESS,
          GREETER_CONTRACT_ABI,
          this.signer
      );
await contract.greet();

```
