```solidity
contract C {
    struct S { uint16 a; uint16 b; uint256 c; }
    uint x;
    mapping(uint => mapping(uint => S)) data;
}
 ```
 让我们计算data[4][9].c的存储位置。
 
 mapping本身的位置是1（前面有32个字节的变量x）。
 
 这意味着data[4]存储在`keccak256（uint256（4）.unt256（1））`。 
 
 data[4]的类型也是mapping， data[4][9]的数据从slot `keccak256（uint256（9）.kecak256（duint256（4）.unt256（1））`开始。
 
 结构S内成员c的slot偏移量为1，因为a和b被压缩在一个slot中。
  
 c是`keccak256（uint256（9）.kecak256（duint256（4）.uint256（1））+1`
 
 值的类型是uint256，因此它使用单个插slot。
