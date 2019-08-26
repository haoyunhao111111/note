### 安装脚手架

1. npm install -g create-react-app
2. create-react-app test  ->项目名称
3. cd test
4. npm start ->项目启动

### jsx简介

> 一种 JavaScript 的语法扩展。 我们推荐在 React 中使用 JSX 来描述用户界面。JSX 乍看起来可能比较像是模版语言，但事实上它完全是在 JavaScript 内部实现的。 

```react
const element = <h1>hello</h1>
```

#### jsx本身是一种表达式

```react
function test(user){
  return user.name+' '+user.age
}
let user={name:'hyh',age:21}
const element = ( <h1>hello!{test(user)}</h1> )  // 单标签需要</>结束。eg:<br/>、<img/>；元素中引用变量需要用{}包裹
ReactDOM.render(
  element, // 要渲染的元素
  document.getElementById('root') // 渲染的位置
)
```

#### 属性

> SX 的特性更接近 JavaScript 而不是 HTML , 所以 React DOM 使用 `camelCase` 小驼峰命名 来定义属性的名称，而不是使用 HTML 的属性名称。
>
> 例如，`class` 变成了 `className`，而 `tabindex` 则对应着 `tabIndex`

```react
const element = <div className = 'test'>test</div>
// css文件
// .test{color:red;}
```

#### 防注入

```react
const title = response.potentiallyMaliciousInput;
// 直接使用是安全的：
const element = <h1>{title}</h1>;
```

#### jsx代表Object

> Babel转译器会把JSX转义成一个React.createElement()方法调用

```react	
const ele = <h1 className='test'>hello</h1>

const ele = React.createElement(
	'h1',
    {className::test},
    'hello'
)

// 以上两个ele是等价的
```

### 元素渲染

> 元素是构成React的最小元素
>
> 与浏览器的 DOM 元素不同，React 当中的元素事实上是普通的对象，React DOM 可以确保 浏览器 DOM 的数据内容与 React 元素保持一致 



- 用React 开发应用时一般只会定义一个根节点。但如果你是在一个已有的项目当中引入 React 的话，可能会需要在不同的部分单独定义 React 根节点。 
- 将React元素渲染到根DOM节点中，我们通过把它们都传递给 `ReactDOM.render()` 的方法来将其渲染到页面上

```react
const ele = <h1>hello</h1>
ReactDOM.render(ele,document.getELementById('root'))
```

#### 元素更新

> React元素都是不可变的，创建成功后，无法改变其内容以及属性，唯一办法就是创建一个新的元素，传入ReactDOM.render()重新渲染

> React DOM 首先会比较元素内容先后的不同，而在渲染过程中只会更新改变了的部分。 

```react
function test(){
  const ele = (
    <div style={{color:'red'}}>It's {new Date().toLocaleTimeString()}</div>
  )
  ReactDOM.render(ele,document.getElementById('root'))
}
setInterval(test,1000)
```

### 组件

> 组件从概念上看就像是函数，它可以接收任意的输入值（称之为“props”），并返回一个需要在页面上展示的React元素。 

> 组件名称必须以大写字母开头。
>
> 例如，`<div />` 表示一个DOM标签，但 `<Welcome />` 表示一个组件，并且在使用该组件时你必须定义或引入它。

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

#### 渲染组件

> react元素不仅可以使dom元素,也可以是组件

```react
const ele = <Test name='郝云浩' /> //引用组件时，其标签最后必须加 '/'
ReactDOM.render(ele,document.getElementById('root'))
```

实现过程

1. 对`<Test name='aaa'/>` `元素` 调用`ReactDOM.render()`方法
2. React将`{name: 'aaa'}`作为props传入并调用`Test`组件。
3. `Test`组件将`<h1>Hello, aaa</h1>`元素作为结果返回。
4. React DOM将DOM更新为`<h1>Hello, aaa</h1>`。

#### 组合组件

> 组件的返回值只能有一个根元素。这也是我们要用一个`<div>`来包裹所有`<Test />`元素的原因。 

```react
function Test(props){
    return <h1>My name is {props.name}</h1>
}
function App(){
    return (
        <div>
        	<Test name='Tom' />
            <Test name='Jack'>
        </div>)
}
ReactDOM.render(<App/>,document.getElementById('root'))
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

> **所有 React 组件都必须像纯函数一样保护它们的 props 不被更改。** 

### state和生命周期函数

> react不允许修改已经渲染的元素，只能通过重新渲染元素来修改，但这样是耗费资源的

```react
function Clock(props) {  // 封装CLock组件
  return (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {props.date.toLocaleTimeString()}.</h2>
    </div>
  );
}

function tick() {
  ReactDOM.render(
    <Clock date={new Date()} />, // 渲染CLock组件
    document.getElementById('root')
  );
}
setInterval(tick, 1000); 
```

> Clock需要设置一个定时器，并且每秒重新渲染ui

#### 利用state来解决问题

> State 与 props 类似，但是 state 是私有的，并且完全受控于当前组件。

```react
class Clock extends React.Component{
    render(
    	 return (
          	<div>It's {this.props.date.tolocaleTimeString()}</div>
         )
    )
}
```

#### 向 class 组件中添加局部的 state

1. 把 `render()` 方法中的 `this.props.date` 替换成 `this.state.date`  

   ```react
   class Clock extends React.Component{
       render(
       	 return (
             	<div>It's {this.state.date.tolocaleTimeString()}</div>
            )
       )
   }
   ```

2. 添加一个 [class 构造函数](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Classes#Constructor)，然后在该函数中为 `this.state` 赋初值

   ```react
   class Clock extends React.Component{
       constructor(props){
           super(props)
       	this.state = {date:new Date()}
       }
       render(){
           return (
             	<div>It's {this.state.date.tolocaleTimeString()}</div>
            )
       }
   }
   ```

3. 移出<CLock/>属性中date

   ```react
   class Clock extends React.Component{
       constructor(props){
           super(props)
       	this.state = {date:new Date()}
       }
       render(){
           return (
             	<div>It's {this.state.date.tolocaleTimeString()}</div>
            )
       }
   }
   ReactDOM.render(
   	<CLock/>,
       document.getElementById('root')
   )
   ```

##### 生命周期方法

   - `componentDidMount()` 方法会在组件已经被渲染到 DOM 中后运行 
   - `ComponentWillUnmount()`在组件被卸载和销毁之前立即调用。在此方法中执行任何必要的清理，例如使计时器无效、取消网络请求或清除在*组件* 

```react
class Clock extends React.Component{
  constructor(props){
    super(props);
    this.state = {date:new Date(),name:'郝云浩'}
  }
  componentDidMount() {
    this.timeId = setInterval(  // 将定时器ID保存在this中
      ()=>this.tick(),1000
    )
  }
  componentWillUnmount() {
    clearInterval(this.timeId)
  }
  tick(){
    this.setState({
      date:new Date()
    })
  }

  render(){
    const ele = <div className='test'>
      <span>hello，{this.state.name}</span>
      <br/>
      <span>it's {this.state.date.toLocaleString()}</span>
      <br/>
    </div>
    return ele
  }
}
ReactDOM.render(<Clock />,document.getElementById('root'))
```

##### state注意

1. 不能直接修改state

   > 构造函数是唯一可以给 `this.state` 赋值的地方： 

   ```react
   this.steta.name = 'hyh' // 错误
   this.setState({name:'hyh'}) // 正确
   ```

2. State 的更新可能是异步的

   > 因为 `this.props` 和 `this.state` 可能会异步更新，所以你不要依赖他们的值来更新下一个状态。 

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




### 组件的三大属性

1. props ---  组件外部传入，只读，不可变

2. state --- 组件内部的状态，可变

3. refs----标识组件内的元素

   ```react
   class Test_ref extends React.Component{
         constructor(props){
           super(props)
           this.show = this.show.bind(this)
         }
         show(){
           alert(this.input.value)
           return
           const con = this.refs.content.value
           if (con === '' || con === null || con === undefined) {
             alert('暂未填写')
             return
           }
           alert(con)
         }
         blur(event){
           console.log(event.target.value)
         }
         render(){
           return(
             <div>
               // react 不建议 旧版本的方法,未摒弃，但是不建议
               <input type="text" ref="content"></input> &nbsp;&nbsp;&nbsp;
               // react 建议
               <input ref={input => this.input = input}></input> // 形参`input`是input元素
               <input type="button" value="按钮" onClick={this.show.bind(this)}></input>
               <br/>
               <input type="text" onBlur={this.blur.bind(this)}></input>
             </div>
           )
         }
       }
       ReactDOM.render(<Test_ref/>,document.getElementById('test'))
   ```

   #### 组件的组合使用

   ```javascript
   // 主框架
   class App extends React.Component{
       constructor(props){
           super(props)
           this.state = {
               todoList:['aaa','bbb','ccc']
           }
           this.addTodo = this.addTodo.bind(this) // react函数需要手动绑定this
       }
       addTodo(item){
           const {todoList} = this.state
           todoList.unshift(item)
           this.setState({todoList})
       }
       render(){
           const {todoList} = this.state
           return (
               <div>
               <h1>TodoList</h1>
               <Add count={todoList.length} add={this.addTodo}></Add>
               <List list={todoList}></List>
               </div>
           )
       }
   }
   // todoList
   class List extends React.Component{
       render(){
           const {list} = this.props
           return(
               <div>
               <ul>
               {list.map((item,index)=>{ return (<li key={index}>{item}</li>) })}
               </ul>
               </div>
           )
       }
   }
   List.propTypes = {
       list: PropTypes.array.isRequired
   }
       // add按钮
       class Add extends React.Component{
         addItem(){
           const value = this.input.value.trim()
           this.props.add(value)
           this.input.value = ''
         }
         render(){
           const { count } = this.props
           return (
             <div>
               <input type="text" ref={input => this.input = input}/>
               <button onClick={this.addItem.bind(this)}>添加 #{count+1}</button>
             </div>
           )
         }
       }
       // 声明父组件传入的值，并类型校验  isRequired->该变量是否可以为空
       Add.propTypes = {
         count:PropTypes.number.isRequired,
         add:PropTypes.func.isRequired
       }
       ReactDOM.render(<App/>,document.getElementById('test'))
   ```

   > 组件的propTypes类型
   >
   > ![数据类型声明](https://image.coolcustomer.cn/0dbf0f1a-4be9-4b59-929b-0985993f259d )

#### React绑定this的三种方法

> 如果不绑定this指向为undefined

1. 在constructor中绑定

   ```javascript
   class App extends React.Component{
       constructor(props){
           super(props)
           this.add = this.add.bind(this)
       }
       add(){
           console.log(this)
       }
       render(){
           return (
           	<div onClick={this.add}></div>
           )
       }
   }
   ```

2. 调用函数时绑定

   ```javascript
   class App extends React.Component{
       constructor(props){
           super(props)
       }
       add(){
           console.log(this)
       }
       render(){
           return (
           	<div onClick={this.add.bind(this)}></div>
           )
       }
   }
   ```

3. 利用箭头函数不改变this指向

   ```javascript
   class App extends React.Component{
       constructor(props){
           super(props)
       }
       add(){
           console.log(this)
       }
       render(){
           return (
           	<div onClick={()=>this.add()}></div>
           )
       }
   }
   ```