解构，顾名思义就是拆分结构。在JS中，结构就是拆分‘一整坨值’，然后赋值给对应的变量

# 最简单的解构-数组的解构

```js
//before es6
var a = 1,
    b = 2,
    c = 3;

//es6
var [a,b,c]=[1,2,3]

a//1
b//2
c//3
```

## React Todo Sample Code中用到的一个解构-对象的解构

数组的元素是按次序排列的，变量的取值由它的位置决定；而对象的属性没有次序，变量必须与属性同名，才能取到正确的值。

```js
let { foo:foo, bar:bar } = { foo: "aaa", bar: "bbb" };
foo // "aaa"
bar // "bbb"

//高级版，利用对象的shorthand语法
let {foo,bar} = {foo:"aaa",bar:"bbb"}
```

### 实际应用场景

假设在Component中需要用到大量的属性，并且我们知道这些属性的属性名，那我们就可以使用this.props.todos, 但是代码中充斥着成片的this.props.todos, this.props.id, this.props.age显然不如todos,id,age来的简单明了。针对这一点，可以利用对象的shorthand和解构来实现:

```js
const {
        todos,
        visibilityFilter,
        //如果有其他属性，可以继续加上去
} = this.props;
```

上面的代码片段从this.props对象中解构出了todos和visibilityFilter两个值，如果变量的值props中不存在，那就会赋予undefined

