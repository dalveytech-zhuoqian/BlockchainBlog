# 自编面试题
 - 为什么bytes在函数传参的时候,必须定义calldata/memory
 - - 因为bytes是数组类型,也叫引用类型,占用空间大
 - external和public有什么区别
 - - external只能外部调用,内部需要加上`this`.method_name()
 - calldata和memory区别
 - - calldata的数据不能更改, 一般用在函数入参的引用类型, 比如bytes[], uint[]
 - memory赋值给memory, 如果我改变原变量, 新赋值的变量会变吗?
 - - 会, 因为是创建了引用
 - 以下代码编译能成功吗? 为什么报错? 应该怎么改?
 ```
 contract C {
    function f() public pure {
        g([1, 2, 3]);
    }
    function g(uint[3] memory) public pure {
        // ...
    }
}
 ```
  - - [1, 2, 3]的数组默认是uint8类型, 而定义的uint默认是uint256类型, 这里需要对第一个数组元素进行cast, `g([uint(1),2,3]);`
