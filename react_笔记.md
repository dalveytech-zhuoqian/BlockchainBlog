* useState和useRef的区别
* * useState会引起视图刷新, ref不会
* * usestate是受控组建,useref是不受控组建(一般在编辑框里面使用)
* 纯静态的组建, 为了防止父组件更改状态,导致自己被刷新, 可以使用memo
* 子组建想调用父组件的方法, 可以使用usecallback
