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



