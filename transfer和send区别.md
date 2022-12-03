address.transfer(amount)     汽油2300

失败的时候会revert,会导致连锁型回滚

address.send(amount)    汽油2300

失败的时候返回false

---------------------

address.call.value(amount)() 也可以转账

call的本意是发动函数调用, 当然也可以用来转账, 

但是一般没有人会这么写, 因为这样代码编译之后size\会变大

也不会引起连锁回滚

还有一个最大不同, call合约发起转账的时候, 

会把剩余的所有gas都发送过去, 

而上面两个合约是发送2300个基础gas, 

对面合约收到转账之后, 啥也干不了

所以如果对面合约有receive函数或者fallback函数, 

那么我们调用的时候应该使用address.call.value

如果我们想安全的调用,那么应该使用send,

然后取返回值对面合约是不是想干点坏事, 结果gas不够报错了

ERC20的转账
-------------------------

```solidity
function safeTransfer(   IERC20 token,  address to,   uint256 value   ) internal {
    //我们需要在这里执行一个低级调用，
    //以绕过Solidity的返回数据大小检查机制，
    //因为我们是自己实现的。
    //我们使用｛Address functionCall｝来执行此调用，
    //该调用验证目标地址是否包含约定代码，并断言在低级调用中是否成功。
    bytes memory returndata = address(token).functionCall(abi.encodeWithSelector(token.transfer.selector, to, value), "SafeERC20: low-level call failed");
    if (returndata.length > 0) {
        require(abi.decode(returndata, (bool)), "SafeERC20: ERC20 operation did not succeed");
    }
}
```


