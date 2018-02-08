## 组件分类成容器型组件和表现型组件的案例



旧代码，包含关系：Footer---&gt;Filter

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

```js
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
                onClick(filter)
        }}>{children}
        </a>
    )
};
```

```js
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
            <Filter active={
                        props.filter==state.visibilityFilter
                    }
                    onClick={store.dispatch({
                        type: "SET_VISIBILITY_FILTER",
                        filter: props.filter
                    })}
            >
            {props.children}
            </Filter>
        )

    }
}
```





