## \[\].filter

语法：

```js
array.filter(function(currentValue,index,arr), thisValue)
```

* **currentValue（必须）**：当前操作的数组元素
* index：当前操作的数组元素在数组中的索引
* arr：调用filter方法的数组本身
* **function函数体内应当是做判断的，filter应当返回符合判断条件的元素，作为一个新的数组；如果没有元素符合判断条件，则返回空数组；**

_经过我的实验，我发现它本质上就是在遍历的时候判断当前return的语句是true还是false，true就return，false就不return。_

范例：

```js
var arr = [1,2,3,4,5]
//正确
var b=arr.filter(function(ele){
    return ele==1;
});
b//[1]

//不正确,函数不会自己回调，需要加上return
var c =arr.filter(function(ele){
     ele==1;
    })

//不正确,filter函数是通过比较来返回的，而不是让我们对元素本身进行操作的
var d =arr.filter(function(ele){
     return ele+1;
    })
```

Redux官方教程中有一个函数的形参命名成了filter，使其与操作数组的filter方法同名，这样的行为应当避免

```js
const filterTodos = (todos,filter) => {
    console.log(todos)
    console.log(filter)
    switch (filter){
        case "SHOW_ALL":
            return todos;
        case "SHOW_COMPLETED":
            return todos.filter(
                t=>t.completed
            );
        case "SHOW_ACTIVE":
            return todos.filter(
                t=>!t.completed
            );
        default:
            return todos;
    }
}
```



