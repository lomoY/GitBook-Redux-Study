## 如何传递函数？比如一个onClick函数

我拿Redux教学中的Sample举例：

先创建Filter组件

```js
const Filter = ({
    children,
    onClick
}) => {
    return(
        <a href="#" 
            onClick={ e => {
                e.preventDefault();
                onClick()             //注意这个onClick
        }}>{children}
        </a>
    )
};
```

调用Filter的时候我们这样做

```js
<Filter active={
    props.filter==state.visibilityFilter
     }
    onClick={()=>store.dispatch({       //注意这个onClick
        type:"SET_VISIBILITY_FILTER",
        filter:props.filter
    })}>
    {props.children}
</Filter>
```

需要注意，这里的onClick是一个函数名，从技术上而言，把它写成'onFilterClick'也是可以的。但是在这个例子中，Filter只包含了一个点击事件，所以作者直接把属性名写成了’onClick‘，实际开发中我认为因当避免这样做，以防止和markup的内置属性混淆。

