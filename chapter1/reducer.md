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
        todos:todos(state.todos,action),//todos reducer只处理state中的todos
        visibilityFilter:visibilityFilter(state.visibilityFilter,action)//如果写成了state.vis,那就相当于输入了undefiend
    }
}
```

由于Reducer的合并是必然也是必要的，Redux专门提供了一个方法:`combineReducers(reducers)`

# combineReducers\(reducers\) {#-combinereducers-reducers}

这个函数将不同的子state和子reducer匹配到一起，最终返回一个整合的reducer。参数是一个对象，对象的键表示了子reducer所要处理的子state

```js
const todoAPP = combineReducers({
    todos:todos,
    visibilityFilter:visibilityFilter
})
```

由于es6中对象字面量的[_shorthand_](/xue-xi-guo-cheng-zhong-xu-yao-zhi-dao-de-es6-nei-rong/dui-xiang-zi-mian-liang-shorthand-yu-fa.md)语法，我们可以将上面的代码改写如下。但是这里有一个约定，那就是’**reducer的名字必须和所对应子state的名字一致**‘。

```js
const todoAPP = combineReducers({
     todos,
     visibilityFilter
})
```

#### combineReducer的实现原理

了解实现原理前，应当了解下面的两个函数

##### Object.key\(对象\)

该函数并返回一个包含所传入对象所有属性名的数组

```js
var obj1 ={a:1,b:2}
Object.keys(obj1);//得到["a", "b"]
```

##### 数组.reduce\(\)

语法：`arr.reduce(callback,[initialValue)`

* callback （执行数组中每个值的函数，包含四个参数）

* * previousValue （上一次调用回调返回的值，或者是提供的初始值（initialValue））
  * currentValue （数组中当前被处理的元素）
  * index （当前元素在数组中的索引）
  * array （调用 reduce 的数组）
* initialValue （作为第一次调用 callback 的第一个参数，即previousValue。）

```js
const combineReducers=(reducers)=>{
    return (state={},action)=>{
        return Object.keys(reducers).reduce(
            (nextState,key)=>{ //官方SAMPLE中的key就是todos和visibilityFilter
                nextState[key]=reducers[key](
                    state[key],
                    action
                );
                return nextState;
            },
            {}
        )
    }
}
```



