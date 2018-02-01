# Component

在React中，一个Component就是一个单独的视觉组件

## React.Component VS. Component

在React中，我们会看到别人的代码中有两种继承方式：

```js
class ViewTodoApp extends React.Component{} 
class ViewTodoApp extends Component{}
```

这两种方式是一致的，我们可以通过下面的这行代码来检验

```js
console.log(Component===React.Component)//true
```

## 为什么需要通过extends Component来实现？

因为通过继承React.Component，就会具有一些React Component的公有方法，如生命周期函数

## 继承Component的要点

1. Component是要被继承的，继承的对象应当是一个class
2. Component应当包含一个render函数\(\)
3. React开发中不建议自定义基类Class

## 组合VS.继承

官方文档：[https://reactjs.org/docs/composition-vs-inheritance.html](https://reactjs.org/docs/composition-vs-inheritance.html)

## 给props赋值

## component 、



小结，component是用来构建React组件的一种方式，而在开发中组件的形式有许多中，具体请看下一章节



