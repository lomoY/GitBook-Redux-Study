# Reducer

含义：to cause \(someone\) to be in a specified state or condition。因此，reducer的含义并不是'减少者',而是‘状态改变者'

当一个函数作为reducer使用时，他所return的对象，一定是一个state，例如：

```js
const todoAPP = (state=[],action) =>{
    return {a:1}
}
//此时，state已经被更新为了{a:1}
```



