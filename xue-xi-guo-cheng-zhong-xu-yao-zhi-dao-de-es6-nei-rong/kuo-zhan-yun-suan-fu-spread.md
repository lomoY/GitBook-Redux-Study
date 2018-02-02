Sample1

假设ViewTodoApp组件中需要用到两个props（或者说外部传入的两个子state），正常的写法（也就是**显式地传递**）是

```js
//store.getState()获得 {todos: Array(0), visibilityFilter: "SHOW_ALL"} 
ReactDOM.render(
    <ViewTodoApp 
        todos={store.getState().todos}
        visibilityFilter={store.getState().visibilityFilter}
    }/>,
    document.getElementById("root")
)
```

但如果这时候有10个、20个props呢？显示的声明显然比较低效。这时就可以利用**扩展运算符**来实现

```js
//store.getState()获得 {todos: Array(0), visibilityFilter: "SHOW_ALL"} 
ReactDOM.render(
    <ViewTodoApp 
    {...store.getState()}/>,
    document.getElementById("root")
)
```

上面的代码利用了扩展运算符，将state对象中的每一个字段（如何添加字段请看这）作为属性传递给了该组件

上面的代码片段拆分开来就是：

1. store.getState\(\)返回对象：{todos:\[\], visibilityFilter: "SHOW\_ALL"}
2. 我们通过
   ```js
   todos={store.getState().todos}
   visibilityFilter={store.getState().visibilityFilter}
   ```

   的方式向组件传递props及对应的值；或者通过`{...store.getState()}`这样的方式

3. 不论第二步中采取哪种方式，我们执行`console.log(this.props)`都会获得`{todos: Array(0), visibilityFilter: "SHOW_ALL"}`

4. 第3步的结论表明，传入组件的属性都会变成this.props对象的属性。因此给组件添加属性其实就是给this.props对象赋值

5. 底层....



