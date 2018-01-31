# Store

## store.subscribe\(\){}

只要有动作被分发，那么store就会执行subscribe里面的**函数（注意，必须得是一个function）**

```js
store.subscribe(render)
```

上面这条代码的意思是：当stroe中有action发生时，render函数就会自动执行



# Reducer，Store，Render，Action，State的关系![](/assets/屏幕快照 2018-02-01 上午12.04.12.png)

* Reducer, Render是具体的处理函数
* Store是链接Reducer和Render的‘胶水’
* State，Action是Reducer和Render所处理的对象
* State是这些处理的最终目的



