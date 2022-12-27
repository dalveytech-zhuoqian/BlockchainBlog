* useState和useRef的区别
* * useState会引起视图刷新, ref不会
* * usestate是受控组建,useref是不受控组建(一般在编辑框里面使用)
* 纯静态的组建, 为了防止父组件更改状态,导致自己被刷新, 可以使用memo
* 子组建想调用父组件的方法, 可以使用usecallback
* array.prototype.reduce遍历数组,最后给出一个结果
* * reduce() 方法对数组中的每个元素执行一个由您提供的reduce函数(升序执行)，将其结果汇总为单个返回值。reduce方法可做的事情特别多，就是循环遍历能做的，reduce都可以做，比如数组求和、数组求积、数组中元素出现的次数、数组去重等等。




----------------------------

### reduce
```js
arr.reduce(function(prev,cur,index,arr){
...
}, init);
```

```js
const arr = [1,2,3,4,5];
const sum = arr.reduce(function(prev,cur,index,arr){
    console.log(prev,cur,index);
    return prev + cur;
});
console.log('arr:',arr,'sum:',sum);
```

```js
const array1 = [1, 2, 3, 4];

// 0 + 1 + 2 + 3 + 4
const initialValue = 0;
const sumWithInitial = array1.reduce(
  (prev, cur) => prev + cur,
  initialValue
);

console.log(sumWithInitial);
// expected output: 10

```

