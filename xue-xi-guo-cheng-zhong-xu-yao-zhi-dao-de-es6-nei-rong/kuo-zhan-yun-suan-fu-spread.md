Sample1

假设ViewTodoApp组件中需要用到两个props（或者说外部传入的两个子state），正常的写法是

```js
    ReactDOM.render(
        <ViewTodoApp 
            todos={store.getState().todos
            visibilityFilter={store.getState().visibilityFilter}
        }/>,
        document.getElementById("root")
    )
```

```js
const render=()=>{
    console.log(store.getState())
    ReactDOM.render(
        <ViewTodoApp 
        {...store.getState()}/>,
        document.getElementById("root")
    )
}
```

 {todos: Array\(0\), visibilityFilter: "SHOW\_ALL"}

