# 在pure function中更新状态的方法

## Object.assign\(\)及扩展运算符

Object.assign\(\)

特点：浅拷贝、对象属性合并

语法：`Object.assign(targetObj, ...sourcesObj)`

#### 克隆对象（单个源对象时）

```js
var obj1={a:1}
var obj2 = Object.assign({},obj1)
//也可以写成:var obj3 = Object.assign(obj1)
obj2//输出{a:1}
```

#### 合并对象（多个源对象时）

```
var obj1={a:1}
var obj2={b:1}
var obj3 = Object.assign({},obj1,obj2)
//如果写成:var obj3 = Object.assign(obj1,obj2),
//那么除了obj3会获得合并后的对象，obj1也会被添加obj2的属性
obj3//{a: 1, b: 1}
```

Object.assign\(\)

同样可以作用于数组

## 扩展运算符spread

`...`

被复制的对象必须是可遍历的：

如对象、数组

注意：如果要在当前开发中使用扩展运算符，需要在`.babelrc`中进行配置，否则在编译过程中会出现`SyntaxError: Unexpected token`我的配置是:

```
"plugins":["transform-es2015-destructuring", "transform-object-rest-spread"]
```

#### 复制数组

```js
const a = [1,2]；
const b1 = [...a];//得到[1,2]
const b2 = [a]//得到[[1,2]]
b1===a//false,说明是对象的复制
```

#### 复制对象

```js
var obj1={a:1,b:2}
var obj2={...obj1}//得到{a:1,b:1}
obj1===obj2//false,说明是对象的复制
```

#### 合并数组

```js
var a =[1,2];
var b = [3,4];
var c = [...a,...b];//[1,2,3,4]
//效果等同于var c = a.concat(b);
//上述操作并不改变原数组
```

#### 合并对象

注意示范代码中的newObj3和newObj4，通过这两个对象的结果可以知道，... 本质上是将靠后的对象的属性的值覆盖到靠前的对象的对应属性的值上面。

```js
var obj1 = {a: 1, b: 2}
var obj2 = {b: 3, c: 4}
var obj3= {a:2}
var newObj1 = {...obj1,...obj2};//{a: 1, b: 3, c: 4}
var newObj2 = {...a,...b,x:5}//{a: 1, b: 3, c: 4, x: 5}
var newObj3 = {...obj1,...obj3}//*{a:2,b:2};
var newObj4 = {...obj3,...obj1}//*{a:1,b:2};
//上述操作并不改变原对象
```

#### 

#### 原对象基础上修改属性

```js
var a = {id:1,sex:'male',age:19};
var b = {...a,id:30};//或者var b = {id:30, ...a}
b//{id:30,sex:'male',age:19};
```

## Map方法处理数组

* map\(\)方法返回一个新数组，数组中的元素为原始数组元素调用函数处理的后值。
* map\(\)方法按照原始数组元素顺序依次处理元素
* map不会改变原始数组

```js
var arr = [1,2,3];
var arrSqure = arr.map(function(num){
    return num*2;
})
arrDouble//得到[2,4,6]，同时不改变原数组
```

例子：希望通过map函数只改变指定id的completed值

```js
var state=[{id:0,completed:true},
           {id:1,completed:true},
           {id:2,completed:true}];

var action={id:2,completed:false};

/**
*state.map的逻辑是:将发生action的item的ID与state中每个item的id进行比较,
*如果比较结果为false,那就将元素原样返回；
*如果比较结果为true,那就修改需要修改的属性，然后返回
*整个map操作将返回一个新的数组
**/
state.map(todo=>{
    if(todo.id!==action.id){
        return todo;
    }
    return{
        ...todo,
        completed:!action.completed
    };
});
```



