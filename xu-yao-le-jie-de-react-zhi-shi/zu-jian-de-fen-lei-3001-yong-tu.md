## 表现型组件 Presentational Component

我的表现型组件关心以下几点

* 关心做出来的东西是长什么样子的
* 组件内部可能同时包含了表现型及容器型子组件，并且它们拥有自己的DOM结构和样式？
* 通常允许通过this.props.children进行控制？
* 对于app的其余部分没有依赖，比如Redux的action和store
* 并不规定数据如何被加载或者改变
* 仅通过props来获取数据以及回调函数？
* 很少拥有他们自己的state。如果有，那也是UI state，而不是data state
* 通常被写成函数式无状态组件，除非它们需要state，生命周期函数，或者性能优化等
* 例子：page，sidebar，story，userinfo，list等

## 容器组件 Container Component

一个容器组件会进行数据的获取，然后渲染（render）它所对应的子组件。

子组件在这里意味着有着相似命名的组件：

```js
StockWidgetContainer =>StockWidget
TagCloudContainer =>TagCloud
PartyPooperListContainer =>PartyPooperList
```

#### 为什么要使用容器组件？

让我举一个例子：

我有一个用来展示评论（comment）的组件，在我不知道使用容器组件前，我会这样写：

```js
class CommentList extends React.Component {
  this.state = { comments: [] };

  componentDidMount() {
    fetchSomeComments(comments =>
      this.setState({ comments: comments }));
  }
  render() {
    return (
      <ul>
        {this.state.comments.map(c => (
          <li>{c.body}—{c.author}</li>
        ))}
      </ul>
    );
  }
}
```

这个组件负责了数据的获取以及数据的表现，这并没有什么错误，但是忽略了利用React的一些优点

##### 重用性

现有的组件除非运行在相同的上下文中，否则无法被重用

##### 数据结构

现有的组件必须获得所指定的数据结构。如果所获得的json数据结构发生了变化，那么这个组件就挂掉了。

#### 利用了容器组件后

这次，我们把上面的组价加以改进，利用一个外层的容器组件来进行数据获取

```js
class CommentListContainer extends React.Component {
  state = { comments: [] };
  componentDidMount() {
    fetchSomeComments(comments =>
      this.setState({ comments: comments }));
  }
  render() {
    return <CommentList comments={this.state.comments} />;
  }
}

const CommentList = props =>
  <ul>
    {props.comments.map(c => (
      <li>{c.body}—{c.author}</li>
    ))}
  </ul>
```

这么做了之后，有以下几个好处：

1. 我们将数据获取及渲染分离了。
2. 我们使得CommentList组件变的可重用。
3. 我们允许CommentList来设置PropTypes的能力。

#### 小结：容器型组件关心的内容

* 关心做出来的东西是如何工作的。
* 在内部可能同时会包含表现型和容器型子组件，但它们通常没有DOM标记，除了一些用来包裹的div，并且没有任何样式。
* 向表现型组件或者其它的容器型组件提供数据。
* 调用Redux actions作为表现型子组件的回调函数？
* 通常是有状态的，因为容器型组件通常是作为数据的提供方
* 通常由高阶组件（higher order components），比如connect...
* 例子：UserPage，FollwersSideBar，StoryContainer，FollowedUserList等

在工作中，我将表现型组件和容器型组件会放在不同等目录下，以区别两者等不同。

#### 什么时候来使用容器型组件？

我建议你在编写你的app时，先从表现型组件入手。最终，你会意识到你要向下传递许多的props。当一些组件仅仅是帮忙将props的组件下传给更下面的组件，而自身并不去使用这些props的时候，你会发现，只要子组件需要的数据发送变化，那么就需要来重写这些夹在中间的组件。这时候就可以引入一些容器型组件了。

由于这是一个不断优化、重构的过程，所以不用指望第一次就能全部搞定。当你按照这个模式不断的试验时，你就会培养出一种直觉，这种直觉会告诉你什么场景下需要提取一个容器型组件。

#### 其他的区别

表现型组件和容器型组件的区别，在本质上并不是一种技术区别，而是目的的区别。

但是相反的，这里有一些相关的技术区别：

* 有状态与无状态。有一些组件会使用React的setState（）方法，而一些组件并不会去使用。尽管容器型组件趋向于有状态，而表现型组件趋向于无状态，但这并不是一条定死的规律。表现型组件想写成有状态也是完全ok的
* class和function。组件可以被声明为class或者function。函数式组件更容易定义，但缺乏一些只有在class从才有的一些特点。由于函数式组件更容易被理解，因此我建议你优先使用它们，除非你发现你需要使用状态、声明周期或者性能优化。
* 纯以及不纯。纯函数可以被定义成有状态或者无状态，也可以被定义成class或者function。

## 

## 

## 

## React Component

当一个组件是纯展示，又不需要用到React Component的内置函数的时候，就没有必要把它声明为一个class然后去继承Component，直接用函数式组件即可

## 函数式组件（又叫无状态组件）

```js
//简单版
const Button = ({ children, ...props }) => (
        <button {...props}>{children}</button>
 );
```

```js
//高级版，引用Redux教程中的sample code

//在component中，调用Filter组件
<Filter filter="SHOW_COMPLETED">SHOW_COMPLETED</Filter>

const Filter = ({filter,children}) => (
    <a href="#" onClick={ e => {
        e.preventDefault();
        store.dispatch({
            type:"SET_VISIBILITY_FILTER"
        })
    }}>{children}
    </a>
);
```

函数式组件又称为无状态（stateless）组件，它不存在自身的状态，并且没有普通组件中的各种生命周期方法，同时其函数式的写法决定了其渲染只由属性决定；

优点：

* 简化代码、专注于 render；
* 组件不需要被实例化，无生命周期，提升性能；?
* 输出（渲染）只取决于输入（属性），无副作用；pure component
* 视图和数据的解耦分离；?

缺点：

* 无法使用 ref；
* 无生命周期方法；
* 无法控制组件的重渲染，因为无法使用 shouldComponentUpdate 方法，当组件接受到新的属性时则会重渲染；

参考文章：

* [https://medium.com/@joshblack/stateless-components-in-react-0-14-f9798f8b992d](https://medium.com/@joshblack/stateless-components-in-react-0-14-f9798f8b992d)
* [https://qiutc.me/post/component-of-react.html](https://qiutc.me/post/component-of-react.html)



