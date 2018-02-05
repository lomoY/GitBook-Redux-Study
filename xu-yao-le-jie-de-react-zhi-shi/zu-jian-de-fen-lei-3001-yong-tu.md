## React Component

当一个组件是纯展示，又不需要用到React Component的内置函数的时候，就没有必要把它声明为一个class然后去继承Component，直接用函数式组件即可

## 函数式组件（又叫无状态组件）

```js
//简单版
const Button = ({ children, ...props }) => (
        <button {...props}>{children}</button>
 );
```

```js
//高级版，引用Redux教程中的sample code

//在component中，调用Filter组件
<Filter filter="SHOW_COMPLETED">SHOW_COMPLETED</Filter>

const Filter = ({filter,children}) => (
    <a href="#" onClick={ e => {
        e.preventDefault();
        store.dispatch({
            type:"SET_VISIBILITY_FILTER"
        })
    }}>{children}
    </a>
);
```

函数式组件又称为无状态（stateless）组件，它不存在自身的状态，并且没有普通组件中的各种生命周期方法，同时其函数式的写法决定了其渲染只由属性决定；

优点：

* 简化代码、专注于 render；
* 组件不需要被实例化，无生命周期，提升性能；?
* 输出（渲染）只取决于输入（属性），无副作用；pure component
* 视图和数据的解耦分离；?

缺点：

* 无法使用 ref；
* 无生命周期方法；
* 无法控制组件的重渲染，因为无法使用 shouldComponentUpdate 方法，当组件接受到新的属性时则会重渲染；

参考文章：

* [https://medium.com/@joshblack/stateless-components-in-react-0-14-f9798f8b992d](https://medium.com/@joshblack/stateless-components-in-react-0-14-f9798f8b992d)
* [https://qiutc.me/post/component-of-react.html](https://qiutc.me/post/component-of-react.html)



