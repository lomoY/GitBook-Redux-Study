# Reducer

## Reducer基本概念

含义：to cause \(someone\) to be in a specified state or condition。因此，reducer的含义并不是'减少者',而是‘状态改变者'

当一个函数作为reducer使用时，他所return的对象，一定是一个state，例如：

```js
const todoAPP = (state=[],action) =>{
    return {a:1}
}
//此时，state已经被更新为了{a:1}
```

## Reducer的合并

一个APP会有有一个根State，本质上也是唯一的state，这个state包含了许多子state节点，然后形成了一个state tree。为了管理这个tree中的state，并且有针对地回应对应的action，reducer也会被拆成许多个。而最终，所有的reducer都会被合并到一个根reducer中。Reducer的合并就诞生于这样的设计思路中。

举例：官方todo sample中的示范代码

```js
const todoAPP = (state=[],action) =>{
    return {
        todos:todo(state.todos,action),//todos reducer只处理state中的todos
        visibilityFilter:visibilityFilter(state.visibilityFilter,action)//如果写成了state.vis,那就相当于输入了undefiend
    }
}
```



