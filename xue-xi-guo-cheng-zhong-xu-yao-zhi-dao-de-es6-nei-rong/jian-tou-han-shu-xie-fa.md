# 箭头函数

箭头函数的英文：Arrow function，准确的说叫fat arrow function（瘦箭头-&gt;,胖箭头=&gt;\)

## 箭头函数的语法

一个参数，有返回值

```
//es5
var fn = function(x){
    return x*x
}

//es6
var fn = (x) => {x*x} //not right!
var fn = (x) => x*x   //okay
var fn = x => x*x     //good!
```

## 最简单的箭头函数

* 省略了包裹参数的圆括号（）
* 省略了包裹函数体的花括号{}
* 省略了return

```js
var fn = function(x){
    return x*x
}
//等同于

var fn = x =>x*x;
var b = fn(2);
b//4
```



