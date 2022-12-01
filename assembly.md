# 内联汇编小汇总
## compound
`CErc20.sol`保证转账成功函数
```solidity
function doTransferIn(address from, uint amount)virtual override internal returns(uint){
  //省略...
  token.transferFrom(from, address(this), amount);
  bool success;
  assembly{
    switch returndatasize() // Pushes the size of the return data buffer onto the stack将返回值缓冲区的大小压入堆栈
      case 0 {
        success := not(0)//非运算
      }
      case 32 {
        returndatacopy(0, 0, 32)//Copies data from the return data buffer to memory将数据从返回值缓冲区复制到内存
        success := mload(0)// 从内存读取
      }
      default {
        revert(0, 0)
      }      
  }
  require(success, "TOKEN_TRANSFER_IN_FAILED");
  //省略...
}
```
`returndatacopy`函数源码
```go
func opReturnDataCopy(pc *uint64, interpreter *EVMInterpreter, scope *ScopeContext) ([]byte, error) {
	var (
		memOffset  = scope.Stack.pop() // 出栈, 内存下标
		dataOffset = scope.Stack.pop() // 出栈, 数据
		length     = scope.Stack.pop() // 出栈, 数据长度
	)

	offset64, overflow := dataOffset.Uint64WithOverflow()
	if overflow { // 检查数据是否溢出2^64
		return nil, ErrReturnDataOutOfBounds
	}
	// we can reuse dataOffset now (aliasing it for clarity)
	var end = dataOffset // 复制一份
	end.Add(&dataOffset, &length) // 计算end位置
	end64, overflow := end.Uint64WithOverflow()
	if overflow || uint64(len(interpreter.returnData)) < end64 {
    // 检查溢出
		return nil, ErrReturnDataOutOfBounds
	}
  // 从interpreter的bytes数组中取切片
  // 把切片放入内存中
	scope.Memory.Set(memOffset.Uint64(), length.Uint64(), interpreter.returnData[offset64:end64])
	return nil, nil
}
```

