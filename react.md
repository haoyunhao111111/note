###  安装脚手架

1. npm install -g create-react-app
2. create-react-app test  ->项目名称
3. cd test
4. npm start ->项目启动

### 生命周期函数

![16.0之前的生命周期](https://img2018.cnblogs.com/blog/331769/201903/331769-20190314070341633-1595341780.png )

![最新版的生命周期](https://s0.lgstatic.com/i/image/M00/5D/D9/CgqCHl-FVVeAaMJvAAKXOyLlUwM592.png)

- constructor:仅仅在挂载阶段被调用一次
  - 可以进行this.state的初始化
- componentWillMount: 在组件渲染之前执行(新版本弃用)
- render
  - render的执行过程并不会去操作真实的dom,只是把需要渲染的内容返出来
  - 渲染真实dom是在挂载阶段由eactDOM.render()完成
- componentDidMount: 在组件渲染之后执行
  - ui渲染完成后调用
  - 只执行一次
  - 典型场景：获取外部资源
- componentWillReveiceProps: props发生改变执行(新版本弃用)
  - 并不是由 props 的变化触发的，而是由父组件的更新触发的
- shouldComponentUpdate: 返回true或false,true代表允许改变，false代表不允许改变
  - 决定VIrtual DOM是否要重绘
  - 一般可以由pureComponent自动实现
  - 典型场景：性能优化
- componentWillUpdate: 数据在改变之前执行(state, props)(新版本弃用)
- componentDidUpdate: 数据修改完成(state, props)
  - 每次ui更新时被调用
  - 常常用做子组件更新完毕来通知父组件
- 典型场景：页面根据props变化重新获取数据
- componentWillUnmount: 组件卸载前执行
  - 组件移除时调用
  - 典型场景：资源释放
- getDerivedStateFromProps：当state需要从props初始化时使用
  - 是一个静态方法，获取不到this
  - 尽量不要使用：维护两者的状态一致性会增加复杂度
  - 每次render都会调用
  - 新版本(16.3版本)用来取代componentWillReveiceProps
  - 典型场景：表单控件获取默认值
- getSnapshotBeforeUpdate
  - 在页面render之前调用，state已更新
  - 典型场景：获取render之前的dom状态

##### state注意

1. 不能直接修改state

   > 构造函数是唯一可以给 `this.state` 赋值的地方： 

   ```react
   this.steta.name = 'hyh' // 错误
   this.setState({name:'hyh'}) // 正确
   ```

2. State 的更新可能是异步的

   > 因为 `this.props` 和 `this.state` 可能会异步更新，所以不要依赖他们的值来更新下一个状态。 

   ```react
   // Wrong
   this.setState({
     counter: this.state.counter + this.props.increment,
   });
   // 要解决这个问题,this.setState要接收的是一个函数而不是对象
   this.setState((state,porps)=>({
       counter = state.a+props.b
   }))
   ```

### 组件

#### 函数定义/类定义组件

```react
// 两种方法一样
function Test(props){
    return <h1>My name is {props.name}</h1>
}

class Test extends React.Component(
    render(){
    	<h1>My name is {this.props.name}</h1>
    }
)
```

#### props的只读性

> 无论是函数或者类声明一个组件,都绝不能修改自身的props

```react
// 纯函数
function sum(a,b){
    return a+b
}
// 非纯函数,改变了自己的入参
function sub(accound,amount){
    accound -= amount
}
```

> 所有 React 组件都必须像纯函数一样保护它们的 props 不被更改。

#### 组件的类型检查

[官方文档](https://react.docschina.org/docs/typechecking-with-proptypes.html)

```javascript
import React,{Component} from 'react'
import PropTypes from 'prop-types'
const Demo1 = (props) => {
  return (
  	<div>{peops.color}<div/>
  )
}
Demo1.PropTypes = {
  color:PropTypes.string.isRequired
}
```

#### 高阶组件

高阶组件是`参数为组件`，返回值为`新组件`的`函数`



### Virtual DOM和key属性的作用

> diff算法时间复杂度为O(n)

#### 虚拟dom的两个假设

1. 组件得dom结构是相对稳定的
   1. diff算法在遇到跨层级的组件移动时会直接删掉原来的dom及其子节点，不会考虑其在别的地方是否会用到
2. 类型相同的兄弟节点可以被唯一标示
   1. 节点位置，顺序发生变化时，方便比较

### Redux

- [中文文档](https://www.redux.org.cn)
- [英文文档](https://redux.js.org/)
- [Github](https://github.com/reactjs/redux)

#### 安装redux 

```
npm install redux --save
```

#### 目录结构

- src
  - store
    - index.js
    - reducer.js

```javascript
// index.js
import { createStore } from 'redux'  //  引入createStore方法
import reducer from './reducer'    
const store = createStore(reducer) // 创建数据存储仓库
export default store   //暴露出去

// reducer.js
const defaultState = {}  //默认数据
export default (state = defaultState,action)=>{  //就是一个方法函数
    return state
}
```



1. 页面使用store

   ```javascript
   constructor(props){
       super(props)
        this.state = store.getState()   // getState() -> 获取reducer中的state
     }
   ```

2. 通过action更改store

   1. 定义action

      ```javascript
      function changeInput(){
          const action = {
              type:'changeInput',
              value:'aaa'
          }
      }
      ```

   2. store.dispatch(action)

      ```javascript
      function changeInput(){
          const action = {
              type:'changeInput',
              value:'aaa'
          }
          store.dispatch(action)
      }
      ```

   3. reducers根据action做相应的逻辑

      ```javascript
      const defaultState = {}  //默认数据
      export default (state = defaultState,action)=>{  //就是一个方法函数
          // reducer中只能接受state,不能更改state,需要将state进行深拷贝，做相应的逻辑，然后return
          if (action.type === 'changeInput'){
              let newState = JSON.parse(JSON.stringify(state))
              newState.inputvalue = action.value
              return newState  // return之后，store中数据改变，但是视图未改变，需要重新获取store中的state
          }
          return state
      }
      ```

   4. 页面订阅store

      ```javascript
      constructor(props){
          super(props)
           this.state = store.getState()
           store.subscribe(this.getStore)
        }
        getStore = () => {
          this.setState(store.getState())
        }
      ```

      ```javascript
      //实际开发中，常常把action中type属性单独放在一个文件中以常量的方式定义，然后在页面和reducer中分别引用，这样做是为了防止前后定义的type不一致，导致报错
      //实际开发中，把action存放在一个文件中，便于管理
      ```
#### 三个坑

1. store必须是唯一的

2. reducer中只能接受state,不能更改state

3. reducer必须是一个纯函数

#### thunk中间件

> 因为reducer必须是一个纯函数，所以网络请求不能放在reducer中，thunk可以使网络请求发生在reducer中

##### 配置

```javascript
// store/index.js
import {createStore,applyMiddleware,compose} from 'redux'
import thunk from 'redux-thunk'
import reducer from './reducer'
const compostEnHancers = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__?
  window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__({}):compose  // 增强函数
const enhancer = compostEnHancers(applyMiddleware(thunk))
const store = createStore(reducer,enhancer)
export default store
```

##### 使用

```javascript
// createActions.js
export const getListAction = (data) => ({
  type:GET_LIST,
  data
})
export const getList = () => {
  return (dispatch) => {
    axios.get('/oms/channel/getAllChannel').then((res)=>{
      const data = res.data
      const action = getListAction(data)
      dispatch(action)
    })
  }
}
```

#### react-redux

> React生态中常用组件，它可以简化`Redux`流程 
>
> ```
> npm install --save react-redux
> ```

##### Provider  

> 提供器：只要使用了这个组件，组件里边的其它所有组件都可以使用`store`了 

```javascript
//         src/index.js
import React from 'react';
import ReactDOM from 'react-dom';
import TodoList from './TodoList'
//---------关键代码--------start
import { Provider } from 'react-redux'
import store from './store'
//声明一个App组件，然后这个组件用Provider进行包裹。
const App = (
   <Provider store={store}>
       <TodoList />
   </Provider>
)
//---------关键代码--------end
ReactDOM.render(App, document.getElementById('root'));
```

##### connect

> 连接器

```javascript
import React,{Component,Fragment} from 'react'
import Item from './item'
import {changeInputAction,addListAction,delItemAction} from '../store/createActions'
import {connect} from 'react-redux'  // 引入connect
class fragement extends Component{
  // constructor(props){
  //   super(props)
  // }
  render() {
    // const {list} = this.state;
    return (
      <Fragment>
        <div>
          <input type="text" value={this.props.inputvalue} onChange={this.props.change}/>
          <button onClick={this.props.addList}>增加服务</button>
        </div>
        <div>
          <ul>
            {
              this.props.list.map((item,index) => {
                return <Item key={index+item} index={index} delFun={this.props.deleteItem} content={item}>{item}</Item>
              })
            }
          </ul>
        </div>
      </Fragment>
    )
  }
}

const stateToProps = (state) => {
  return {
    inputvalue:state.inputvalue,
    list:state.list
  }
}

const dispatchToProps = (dispatch) => {
  return {
    change(e){
      const action =changeInputAction(e.target.value);
      dispatch(action)
    },
    addList () {
      const action = addListAction();
      //this.props.inputvalue
      dispatch(action)
    },
    deleteItem (index){
      const action = delItemAction(index);
      dispatch(action)
    }
  }
}
export default connect(stateToProps,dispatchToProps)(fragement)

```

### react-router

> ```
> npm install --save react-router-dom
> ```

```javascript
import React from "react";
import { BrowserRouter as Router, Route, Link } from "react-router-dom";

function Index() {
  return <h2>JSPang.com</h2>;
}

function List() {
  return <h2>List-Page</h2>;
}

function AppRouter() {
  return (
    <Router>
        <ul>
            <li> <Link to="/">首页</Link> </li>
            <li><Link to="/list/">列表</Link> </li>
        </ul>
        <Route path="/" exact component={Index} />
        <Route path="/list/" component={List} />
    </Router>
  );
}
export default AppRouter;
```

### react-hooks

```javascript
import React,{ useState } from 'react'

function Count(){
  const [count,addCount] = useState(0)
  return(
    <div>
      <div>你点击了{count}次</div>
      <button onClick={()=>{addCount(count+1)}}>点击</button>
    </div>
  )
}
export default Count

```

#### useEffect

```javascript
import React,{ useState,useEffect } from 'react'

function Count(){
  const [count,addCount] = useState(0)
  useEffect(()=>{  //  将react中的ComponentDidMount和ComponentDidUpdate结合起来，是异步操作
    console.log(`useEffect=>${count}`)
  })
  return(
    <div>
      <div>你点击了{count}次</div>
      <button onClick={()=>{addCount(count+1)}}>点击</button>
    </div>
  )
}
export default Count
```
#### useContext

> 父子组件传值

```javascript
import React,{ useState,useEffect,createContext,useContext } from 'react'
const CountContent = createContext()

function CountComponent(){
  let count = useContext(CountContent)
  return (
    <h2>{count}</h2>
  )
}
function Count(){
  const [count,addCount] = useState(0)
  useEffect(()=>{
    console.log(`useEffect=>${count}`)
  })
  return(
    <div>
      <div>你点击了{count}次</div>
      <button onClick={()=>{addCount(count+1)}}>点击</button>
      <CountContent.Provider value = {count}>
        <CountComponent></CountComponent>
      </CountContent.Provider>
    </div>
  )
}
export default Count
```
