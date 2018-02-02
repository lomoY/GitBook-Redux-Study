# children

props.children 用在函数中，this.props.children用在对象中

```js
const Filter = ({filter,children}) => (
    <a href="#" onClick={ e => {
        e.preventDefault();
        store.dispatch({
            type:"SET_VISIBILITY_FILTER",
            filter
        })
    }}>{children}
    </a>
);

...
<Filter filter="SHOW_ALL">夹在两个标签中间的任何东西都可以是children！</Filter>
<Filter filter="SHOW_ALL">比如字符串ALL</Filter>
```



参考资料：

* https://reactjs.org/docs/react-api.html\#react.children
* https://codeburst.io/a-quick-intro-to-reacts-props-children-cb3d2fce4891





