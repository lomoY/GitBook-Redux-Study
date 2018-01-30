# 在pure function中更新状态的方法

Object.assign\(\)及扩展运算符

Object.assign\(\)

特点：浅拷贝、对象属性合并

语法：`Object.assign(targetObj, ...sourcesObj)`

  
克隆对象（单个源对象时）

```js
var obj1={a:1}
var obj2 = Object.assign({},obj1)
//也可以写成:var obj3 = Object.assign(obj1)
obj2//输出{a:1}
```

### 合并对象（多个源对象时）

```
var obj1={a:1}
var obj2={b:1}
var obj3 = Object.assign({},obj1,obj2)
//如果写成:var obj3 = Object.assign(obj1,obj2),
//那么除了obj3会获得合并后的对象，obj1也会被添加obj2的属性
obj3//{a: 1, b: 1}
```

 Object.assign\(\)

同

样

可

以

作

用

于

数

组

  


## 扩展运算符

`...`

  


  


被

复

制

的

对

象

必

须

是

可

遍

历

的

：

如

对

象

、

数

组

  


  


### 复制数组

```
const a = [1,2]
；


const b1 = [...a];//
得
到
[1,2]


const b2 = [a]//
得
到
[[1,2]]


b1===a//false,
说
明
是
对
象
的
复
制
```

### 复制对象

```
var obj1={a:1,b:2}


var obj2={...obj1}//
得
到
{a:1,b:1}


obj1===obj2//false,
说
明
是
对
象
的
复
制
```

### 合并数组

```
var a =[1,2];


var b = [3,4];


var c = [...a,...b];//[1,2,3,4]


//
效
果
等
同
于
var c = a.concat(b);


//
上
述
操
作
并
不
改
变
原
数
组
```

### 合并对象

```
var a = {a: 1, b: 2}


var b = {b: 3, c: 4}


var c = {...a,...b};//{a: 1, b: 3, c: 4}


var d ={...a,...b,x:5}//{a: 1, b: 3, c: 4, x: 5}


//
上
述
操
作
并
不
改
变
原
对
象
```



