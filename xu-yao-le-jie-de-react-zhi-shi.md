# key

React需要数组中的子元素都拥有一个key。如果没有添加key，就会报错`558 Warning: Each child in an array or iterator should have a unique "key" prop.`（虽然叫Warning，但是报出来是一个error，也是很棒棒的）。

这里的子元素，可以是一串li，可以是一堆div。

## 添加key的两种思路

以遍历操作li为例

### 在属性中增加额外的值

```js
const todoItems = todos.map((todo) =>//这里的todo参考官方todo sample中的代码
  <li key={todo.id}>
    {todo.text}
  </li>
);
```

### 利用元素在素组中的索引

只有在item没有合适ID的时候才采用该方法

```js
const todoItems = todos.map((todo, index) =>
  <li key={index}>
    {todo.text}
  </li>
);
```

















参考资料：[https://reactjs.org/docs/lists-and-keys.html\#keys](https://reactjs.org/docs/lists-and-keys.html#keys)

