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
const Todo = ({    //为什么要花括号？因为直接在参数中进行解构
    text,            //将要渲染的数据放进参数中
    completed,
    onClick        //点击事件参数的命名有两种方式。1.onClick，表示该Todo行为更灵活 2.onToggleClick，表明该点击是一个特定行为
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

## 小结

1.表现组件，应当关注于视觉的展示，与行为相分离，具体执行什么功能，可以在调用的时候来决定

2.参数的传递不应当过深，比如Filter需要一个叫currentFilter的值，为了获得这个值，就要先传入Footer，再从Footer传入Filter，而Footer自身并不会使用到这个值。过深的另外一个弊端就是父组件需要知道子组件需要哪些值，这样就使得组件缺乏封装性。

