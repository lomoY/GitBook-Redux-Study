# Store

## store.subscribe\(\){}

只要有动作被分发，那么store就会执行subscribe里面的**函数（注意，必须得是一个function）**

```js
store.subscribe(render)
```

上面这条代码的意思是：当stroe中有action发生时，render函数就会自动执行

