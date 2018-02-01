# Refs

Refs是获取DOM元素的好帮手！利用ref的回调函数将DOM元素设置成class或者说component的属性，是实现访问DOM元素的常见模式。

适合使用Refs的地方（我还没体会到）

1. 管理focus行为，文本选中行为，媒体播放行为
2. 触发动画
3. 与第三方DOM lib整合

React官方提到：在可以使用声明的方法解决的场景中，避免使用Refs。why？

## 添加refs到DOM元素上

当refs属性被添加到一个HTML DOM元素上后，它实现了两件事情：

1. 获取了被添加refs DOM元素的DOM对象
2. 给该DOM元素增加了一个回调函数（这个回调函数是干嘛的呢？和{}有啥区别呢？）

### refs获取DOM对象

如下面这行代码，ref所添加的回调函数所传入的**参数**就是所绑定的DOM对象。可以在回调函数中通过`this.input=node`的方式将当期的input添加到整个Component的属性中，从而使其可以被其他函数所访问。

```js
<input type="textarea" ref={node=>{console.log(node)}}/>//<input type="textarea">
```

### refs的回调函数

refs可以添加到任何的DOM 元素上，并且绑定一个回调函数。并且, 当该元素mount或者unmount的时候就会**即刻触发**一个回调函数。

如

```js
<input type="textarea" ref={node=>{console.log('1111')}}/>//首次渲染的时候就会打印出1111
```

## 



