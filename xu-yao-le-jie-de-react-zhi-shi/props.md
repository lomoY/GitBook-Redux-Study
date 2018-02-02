# props

在组件Render的时候，属性名就是props中的key，属性值就是key对应的value

```js
ReactDOM.render(
        <ViewTodoApp 
        todos={store.getState().todos}
        dogs={123}/>,
        document.getElementById("root")
    )

//此时,this.props={todos: Array(0), dogs: 123}
```

高级一点的写法{...store.getState\(\)}

```js
ReactDOM.render(
        <ViewTodoApp 
        {...store.getState()}/>,
        document.getElementById("root")
    )
```

所以这里就有了一个问题，store中的state到底是在哪儿添加上去的？[看这里](/chapter1/store.md)

