# BlockchainBlog
什么是重入漏洞
```
interface ReiceveInterface{
  function onReceive() external{}
}
contract MyContract{
  function withDraw(uint amount) external{
  // 检查是否有用户的代币还有多少个
  // 扣掉要提取的部分
  ReiceveInterface(msg.sender).onReceive();
  }
}
```
用于攻击的合约

```
contract Attactor{
  uint count =0;
  function start() external{
    onReceive();
  }
  
  function onReceive() external{
    if(time<9){
      count+=1;
      MyContract(0x...).withDraw(1 ether);
    }
  }
}
```

这样就会出现循环调用，导致取款的时候，检查用户余额出错，导致可能已经没钱了，但是依旧可以取钱。
解决方法就是用openzeppelin的nonReentrent修饰符。

