# 对象字面量shorthand语法创建对象

示范代码：

```js
var a=1;
var b=2;
var newObj ={a,b};//本质上就是 var newObj ={a:a,b:b}
newObj//{a:1,b:2}
```

这里要注意两点：

1. 使用shorthand之前，变量必须已经声明过
2. 属性的键对应的值与属性名相同



