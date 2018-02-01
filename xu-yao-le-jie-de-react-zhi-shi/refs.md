# Refs

Refs是获取DOM元素的好帮手！

适合使用Refs的地方

1. 管理focus行为，文本选中行为，媒体播放行为
2. 触发动画
3. 与第三方DOM lib整合

React官方提到：在可以使用声明的方法解决的场景中，避免使用Refs。why？

## 添加refs到DOM元素上

refs可以添加到任何的DOM 元素上，并且绑定一个回调函数。并且, 当该元素mount或者unmount的时候就会**即刻触发**一个回调函数。

如

```js
<input type="textarea" ref={node=>{console.log('1111')}}/>//首次渲染的时候就会打印出1111
```

## 



