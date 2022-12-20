https://blog.csdn.net/astar2022/article/details/127864325
简单的说
promis是同步, 因此先运行, promise是微任务,异步运行, 但是需要主线程运行完毕之后才运行, setTime是宏任务, 异步运行,优先级小于微任务
```js
  setTimeout(() => {
    console.log(4);
  }, 0); // async

  new Promise((resolve,reject)=>{
    console.log(1) // main
    resolve(3) // async, main > micro task > setTimeout  
  }).
  then((a)=>{
    console.log(a)
  }) // async

  console.log(2)
  ```
