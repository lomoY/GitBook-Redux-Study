# 箭头函数

箭头函数的英文：Arrow function，准确的说叫fat arrow function（瘦箭头-&gt;,胖箭头=&gt;\)

## 箭头函数的语法

* 可省略包裹参数的**圆括号**（）。当参数数量为一个的时候可省略，无参数及多个参数的情况不可省略

* 可省略函数声明的**花括号**。若省略花括号，则return函数声明，弱函数声明是一个对象，则可用圆括号包裹；

* 无花括号或者包裹圆括号的情况省略了显示的**return**

无参数/一个参数，有返回值

```js
//es5
var fn = function(x){
    return x*x
}

//es6
var fn = (x) => {x*x} //not right!因为需要添加return
var fn =(x) => (x*x)  //okay
var fn = (x) => x*x   //okay
var fn = x => x*x     //good!
var fn = x =>({x:x})  //good!

//传入一个方法的时候
var fn = ({onAddClick})=> (<button type="button" onClick={()=>{onAddClick(input.value)}}>)

//没有参数
var fn=()=>4
fn()//4

//多个参数
var fn = (x,y)=>x+y;
fn(1,2)//3

var fn = ({x,y})=x+y;
```

上面的代码可以看出，如果在**函数声明**外包裹了**花括号**，那么就需要**显示**地添加 return；而圆括号或者只有表达式则**默认添加return。**

## 箭头函数对于this绑定的影响

ongoing....

