# TodoAPP

### 代码结构

###### 重构前的代码结构：![](/assets/todoAPP结构图.png)

###### 重构后的代码结构（优点，将展示组件从Redux中解耦，减少了未来如果迁移框架而带来的成本。reduce没有改变\)：![](/assets/todoAPP重构后的代码.png)

### 具体代码举例：

重构前：

```js
class ToDoView extends React.component{
    ....
    render(){
        ....
        return(
        ...
           <ul>
            {visibleTodo.map(todo=>(
                <li key={todo.id} 
                    onClick={()=>{
                        store.dispatch({
                            type:"TOGGLE_TODO",
                            id:todo.id
                        })
                    }} 
                    style={{
                        textDecoration:
                            todo.completed?
                                'line-through':
                                'none'
                    }}>
                    {todo.text}
                </li>
            ))} 
        </ul> 
        )
    }
}
```

重构后：

```js
const Todo = ({//为什么要花括号
    text,//将要渲染的数据放进参数中
    completed,
    onClick
})=>(
    <li 
        onClick={onClick}//这样修改后，todo的点击行为就灵活多了
        style={{textDecoration:completed?'line-through':'none'}}
    >
    {text}
</li>
)

const TodoList = ({
    todos,//和todo一样，将要传入的方法和参数作为参数传入组件，todoList只做展示
    onTodoClick
})=>(
    <ul>
        {todos.map(todo=>
            <Todo
                key={todo.id}
                {...todo}//{id: 1, text: "", completed: false} react传入state和对象解构
                onClick = {()=>onTodoClick(todo.id)}
            />)       
        }
    </ul>
)

...

class ToDoView extends React.component{
    ....
    render(){
        ....
        return(
            ...
            <TodoList todos={visibleTodo} 
                    onTodoClick={id=>store.dispatch({
                        type:"TOGGLE_TODO",
                        id
            })}
            ...
        )
    }
}
```



