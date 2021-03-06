## 组件分类成容器型组件和表现型组件的案例

旧代码，包含关系：Footer---&gt;Filter

```js
<Footer
    visibilityFilter={visibilityFilter}
    onFilterClick={filter=>store.dispatch({
            type:"SET_VISIBILITY_FILTER",
            filter
        })
    }
/>
```

```js
const Footer = ({
     visibilityFilter,
     onFilterClick
 })=>{
   return <div>
        SHOW:
        <Filter
            filter="SHOW_ALL" 
            selectedFilter={visibilityFilter}
            onClick={onFilterClick}
            >ALL</Filter>
        <Filter 
            filter="SHOW_ACTIVE" 
            selectedFilter={visibilityFilter}
            onClick={onFilterClick}
            >SHOW_ACTIVE</Filter> 
        <Filter 
            filter="SHOW_COMPLETED" 
            selectedFilter={visibilityFilter}
            onClick={onFilterClick}
            >SHOW_COMPLETED</FilterContainer>
    </div>
}
```

```js
const Filter = ({
    filter,
    children,
    selectedFilter,
    onClick
}) => {
    if(filter==selectedFilter){
        return <span>{children}</span>
    }

    return(
        <a href="#" 
            onClick={ e => {
                e.preventDefault();
                    store.dispatch({
                     type:"SET_VISIBILITY_FILTER",
                      filter
                  })
                onClick(filter)
        }}>{children}
        </a>
    )
};
```

在这部分代码中：

* 父组件本身不使用参数中的两个值，仅仅是给子组件用的
* 子组件自己指明了具体的行为，表现和行为分离不透彻
* 子组件在展示时，需要知道filter和selectedFilter的值才能确定如何展示，表现不单纯

新代码，包含关系：Footer---&gt; FilterContainer----&gt;Filter

```
<Footer/>
```

```js
/*
* Footer
* 该组件现在只需用最简单的方式通过FilterContainer来使用Filter
* 修改点1 传参。visibilityFilter,onFilterClick 这两个值Footer本身不使用，也不关心，仅仅是Filter使用到了，所以删除
* 修改点2 从直接调用Filter改为调用FilterContainer
* 修改点3 只需要传入filter属性和children属性
*/

const Footer = ()=>{
   return <div>
    SHOW:
        <FilterContainer filter="SHOW_ALL">ALL</FilterContainer>
        <FilterContainer filter="SHOW_ACTIVE">SHOW_ACTIVE</FilterContainer> 
        <FilterContainer filter="SHOW_COMPLETED">SHOW_COMPLETED</FilterContainer>
    </div>
}
```

```js
/*
* Filter
* 该组件只负责数据的展示，提供了一些参数，使得在调用的时候给它指派具体的数据和行为
* 修改点1 不需要知道filter的值和当先选择的filter的值来进行判断从而决定要展示什么内容，把判断的过程交给父级，父级判断的结果作为active的值传入
* 修改点2 喊出原先所指定的动作行为，将动作的指定交给父级
* 修改点3
*/
const Filter = ({
    active,
    children,
    onClick
}) => {
    if(active){
        return <span>{children}</span>
    }
    return(
        <a href="#" 
            onClick={ e => {
                e.preventDefault();
                onClick()
        }}>{children}
        </a>
    )
};
```

```js
/*
* FilterContainer
* 该组件负责数据的获取，并且告诉Filter子组件使用什么数据，发生什么行为
* 修改点1 利用this.props获得父组件传入的属性，而父组件不需要再考虑Filter具体需要哪些参数，实现了解耦
* 修改点2 通过store的订阅来获得store里对应的状态，而非通过父组件传入
* 修改点3 forceUpdate
* 修改点4 在Container中判断Filter的显示效果，而非在Filter的内部进行判断
* 
*/
class FilterContainer extends React.Component{
    componentDidMount(){
        this.unsubscribe=store.subscribe(()=>this.forceUpdate)
    }
    componentWillUnmount(){
        this.unsubscribe();
    }
    render(){
        const props=this.props;
        const state=store.getState();
        return(
            <Filter 
                active={
                        props.filter==state.visibilityFilter
                    }
                onClick={store.dispatch({
                                type: "SET_VISIBILITY_FILTER",
                                filter: props.filter
                            })
                        }
            >
            {props.children}
            </Filter>
        )
    }
}
```

小结：

* Filter可以从store中订阅到的属性，不再从父组件中一一传入，而是直接订阅



