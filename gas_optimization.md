原文: https://hackmd.io/@totomanov/gas-optimization-loops
#### 总结:
* 不要使用<= and >=
* for循环的i++这种可以使用unchecked, 从for那行拿到最下面
* 一些简单的函数尽量用Yul(也就是assembly) [如何使用Yul](https://docs.soliditylang.org/en/latest/yul.html)
* for循环中, 每次都要使用length, 可以把length存成变量, 放入stack中
* 除了storage类型, 其他情况uint8并不会比uint256更省,反而还要多做一次cast

批量转账的时候
----------
可以用yul把函数选择器存入内存



把数组转成数字(太麻烦不推荐)
---------
```
原来数组[1, 6, 13, 22, 24, 25, 30, 33, 94, 215]
假设每个数字都是8个字节, 那么最大也就是2^8=255
那么我们可以把这串数组转换为一个uint256
每个数字是两个16hex
转换完成后0x00000000000000000000000000000000000000000000d75e211e1918160d0601
从右开始读01,06,0d,16,…,d7. 

```

原来的函数
```solidity
function loopArray_cached(uint256[] calldata ns) public returns (uint256 sum) {
    uint256 length = ns.length;
    for(uint256 i = 0; i < length;) {
        sum += ns[i];
        unchecked {
            i++;
        }
    }
}
```

```solidity
function loop_arr_magic(uint256 encoded_ns, uint256 length) public returns (uint256 sum) {
    for(uint256 i = 0; i < length;) {
        sum += encoded_ns & 0xff;
        encoded_ns >>= 8; // mask移动2^8,8个byte
        unchecked {
            i++;
        }
    }
}
```
