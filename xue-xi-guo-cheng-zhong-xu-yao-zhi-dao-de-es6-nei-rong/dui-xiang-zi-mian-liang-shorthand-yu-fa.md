# 对象字面量shorthand语法创建对象

示范代码：

```js
var a=1;
var b=2;
var obj1 ={a,b};//本质上就是 var newObj ={a:a,b:b}
obj1//{a:1,b:2}

var obj2={c:1,a}//这样也可以哟！
obj2//{c: 1, a: 1}
```

这里要注意两点：

1. 使用shorthand之前，变量必须已经声明过
2. 属性的键对应的值与属性名相同

## shorthand配合变量的结构\(我不确定我这个说法对不对\)

```js
//简单版
const full = ({ first, last }) => first + ' ' + last;
//等同于

function full(person) {
  return person.first + ' ' + person.last;
}
```

```js
//高级版，引用Redux教程中的sample code

//在component中，调用Filter组件
<Filter filter="SHOW_COMPLETED">SHOW_COMPLETED</Filter>

const Filter = (props) => (//打印props得到{filter: "SHOW_COMPLETED", children: "SHOW_COMPLETED"}
    <a href="#" onClick={ e => {
        e.preventDefault();
        store.dispatch({
            type:"SET_VISIBILITY_FILTER"
        })
    }}>{props.children}
    </a>
);
//等价于
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

（\*高级版代码片段中用到了children或者说props.children，详情请看对应[小节](/children)）

