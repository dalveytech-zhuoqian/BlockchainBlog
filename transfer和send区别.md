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

如果我们想安全的调用,那么应该使用send,

然后取返回值对面合约是不是想干点坏事, 结果gas不够报错了

那么我们调用payable的时候应该使用address.call.value

ERC20的转账
-------------------------

```solidity
function safeTransfer(
        IERC20 token,
        address to,
        uint256 value
    ) internal {
    
    bytes memory data = abi.encodeWithSelector(token.transfer.selector, to, value)
    address target = address(token)
    require(address(this).balance >= value, "Address: insufficient balance for call");
    (bool success, bytes memory returndata) = target.call{value: value}(data);

    if (success) {
        if (returndata.length == 0) {
            require(isContract(target), "Address: call to non-contract");
        }
    } else {
        if (returndata.length > 0) {
            assembly {
                let returndata_size := mload(returndata)
                revert(add(32, returndata), returndata_size)
            }
        } else {
            revert(errorMessage);
        }
    }

    if (returndata.length > 0) {
        // Return data is optional
        require(abi.decode(returndata, (bool)), "SafeERC20: ERC20 operation did not succeed");
    }
}

```


