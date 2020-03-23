## mvvm

> model ->模型->数据  view->视图->html+css    数据到视图，视图到数据，双向数据绑定  优点>缺点

## 双向数据绑定的原理

```vue
<script>
    var obj={};
    var aa;
    Object.defineProperty(obj,"name",{
        //value:100,        //设置
        //writable:true,   //可写
        configurable:true,   //可删
        enumerable:true,   //可遍历
        set:function (val) {
            if(aa!=val){
                document.querySelector("div").innerHTML=val
            }
            aa=val;
        },
        get:function () {
            return aa
        }
    })
    obj.name="zhangsan"
    console.log(obj.name)
    obj.name="lisi"
</script>
```

## 过滤器

> 原数据不变的情况下，只改变显示的效果

```html
<div id="app">
    <div>{{a+b | toFixed(3)}}</div>
</div>
```

```javascript
<script>
   new Vue({
    el:'#app',
    data:{
      a:0.1,
      b:0.2
    },
    filters:{
      toFixed(input,params){  // input:过滤器前面的结果,params:过滤器所传入的参数,当前的this指向window
        return input.toFixed(params)
      }
    }
   })
</script>
```

```javascript
// 将方法挂载到Vue原型上，在new出的每一个实例都具有该方法
<script>
    Vue.filter('toFixed',function(data){
    	return data+'全局过滤器'
	})
   new Vue({
    el:'#app',
    data:{
      a:0.1,
      b:0.2
    },
   })
</script>
```

## 修饰符

### 修饰符

- .number

```html
<input type="number" v-model.number='number'>  <!-- 只允许输入数字 -->
```

- .lazy

```html
<input type="number" v-model.lazy='number'>  <!-- 输入框失去焦点后才进行数据才发生变化 -->
```



### 按键修饰符

- .enter
- .ctrl
- .keyCode

### 事件修饰符

- .stop  阻止事件的冒泡行为

> 作用相当于`e.cancelBubble=true`和`e.stopPropagation()`

```javascript
<div id="app">
    <div @click='zuxian'>祖先元素
      <div @click='fu'>父元素
        <div @click.stop='zi'>子元素</div>
      </div>
    </div>
  </div>
  <script src="vue.js"></script>
  <script>
    new Vue({
      el:'#app',
      data:{},
      methods:{
        zuxian(){
          alert('zuxian')
        },
        fu(){
          alert('fu')
        },
        zi(e){
          // alert('zi',e.cancelBubble=true)
          // alert('zi',e.stopPropagation())
          alert('zi')
        }
      }
    })
  </script>
```

- .captrue

> `捕获事件`，以下代码弹出顺序为 zuxian->zi->fu

```javascript
<div id="app">
    <div @click.capture='zuxian'>祖先元素
      <div @click='fu'>父元素
        <div @click='zi'>子元素</div>
      </div>
    </div>
  </div>
  <script src="vue.js"></script>
  <script>
    new Vue({
      el:'#app',
      data:{},
      methods:{
        zuxian(){
          alert('zuxian')
        },
        fu(){
          alert('fu')
        },
        zi(e){
          alert('zi')
        }
      }
    })
  </script>
```

- .prevent

> 阻止默认行为

```javascript
<div id="app">
    <div @click.capture='zuxian'>祖先元素
      <div @click='fu'>父元素
        <div @click='zi'>子元素</div>
      </div>
    </div>
    <a href="http://www.baidu.com" @click.prevent='zuxian'></a>
  </div>
  <script src="vue.js"></script>
  <script>
    new Vue({
      el:'#app',
      data:{},
      methods:{
        zuxian(){
          alert('zuxian')
        }
      }
    })
  </script>
```

- .once  该事件只执行一次

> 第一次点击zi：弹框顺序 zi->fu->zuxian  第二次点击zi：弹框顺序 zi->zuxian 

```javascript
<div id="app">
    <div @click='zuxian'>祖先元素
      <div @click.once='fu'>父元素
        <div @click='zi'>子元素</div>
      </div>
    </div>
  </div>
  <script src="vue.js"></script>
  <script>
    new Vue({
      el:'#app',
      data:{},
      methods:{
        zuxian(){
          alert('zuxian')
        },
        fu(){
          alert('fu')
        },
        zi(e){
          alert('zi')
        }
      }
    })
  </script>
```

- .self 只有点击自己时才会执行，不受冒泡影响

```javascript
<div id="app">
    <div @click='zuxian'>祖先元素
      <div @click.self='fu'>父元素
        <div @click='zi'>子元素</div>
      </div>
    </div>
  </div>
  <script src="vue.js"></script>
  <script>
    new Vue({
      el:'#app',
      data:{},
      methods:{
        zuxian(){
          alert('zuxian')
        },
        fu(){
          alert('fu')
        },
        zi(e){
          alert('zi')
        }
      }
    })
  </script>
```



## axios

```javascript
// 默认配置
axios.defaults.baseUrl = ''
axios.defaults.timeout = 5000 // 请求时间，超时报错
```



```javascript
axios.get('/app/sdfkof',{})
    .then(function(res){
    	console.log(res)
    })
    .catch(function(error){
    	console.log(error)
    })
// axios.请求方式('请求地址',传入的参数).访问成功的函数.访问失败的函数
```

### promise-axios

```javascript
let a=''
function buy(){
    setTimeout(()=>{
        a='buy'
    },2000)
}
buy()
function get(){
    console.log(a)
}
//异步：首先想到回调函数(将后续要处理的逻辑传入到当前要做的事，事情做好后再调用此函数)
let a=''
function buy(callback){
    setTimeout(()=>{
        a='buy';
        callback
    },2000)
}
buy(function get(val){
    console.log(val)
})

```

> promise:解决回调逻辑,成功态，失败态，等待态。
>
> js原生自带

```javascript
// resolve:代表的是转向成功态
// reject:代表的是转向失败态
// Promise的实例就一个then方法，then方法有两个参数
let p = new Promise((resolve,reject)=>{
    setTimeout(function(){
        let a ='buy';
        resolve(a)
    },2000)
});
p.then((res)=>{console.log(res)},()=>{})
```

## computed

> 计算`属性`,不是方法,不能与data,methods重名

> 里面的对象会有get(),set()方法，都指向实例

```javascript
<div id="app">
    <div v-if='isTrue'>true</div>
<div v-else>false</div>
</div>
<script src="vue.js"></script>
<script>
    new Vue({
    el:'#app',
    data:{
        all:[{a:true},{a:true},{a:true}]
    },
    computed:{
        isTrue:{ // 如果计算属性是函数，默认调用get()
            get(){ // get和set都指向实例，默认获取isTrue的值，所以会调用get()方法
                return this.all.every(p=>p.a)
            },
            set(val){
                this.all.forEach(p=>p.a=val)
            }
        }
    }
})
</script>
```



- 方法不会有缓存，computed会根据依赖(归vue管理的数据，可以响应式)

## 指令

### 常用的内部指令

> dom元素的行间属性，vue提供了内置的指令，必须以v-开头，后面的值均为变量

- v-model  只能用于表单，会忽略掉value,checked,selected,将数据绑定到视图上，数据修改后会影响视图的变化
  - 如果是复选框，只有一个复选框的时候，会把此值转化为boolean类型，true代表选中。
  - 如果是多个checkbox，要增加value属性，并且数据类型是数组
- v-text      用于表单以外
- v-if 操作的是dom，不满足条件，里面的代码不会执行
- v-show:操作的是样式

> 如果频繁的切换dom，用v-show更好，如果一开始数据就能确认下来，用v-if更好

### 自定义指令(Vue.directive())

#### 用法

```javascript
<template>
  <div>
    <div v-hyh="color">{{num}}</div>
    <div>
      <button @click="add">add</button>
    </div>
  </div>
</template>
<script>
import Vue from 'vue'
Vue.directive('hyh', function (el, binding) { 
  /*
  el: 自定义指令的dom
  binding:{
  	name:'hyh',   自定义的指令名
  	value:'red',  自定义指令绑定的data值
  	expression:'color'  自定义指令绑定的变量
  }
  */
  el.style = 'color:' + binding.value
})
export default {
  data () {
    return {
      num: 10,
      color: 'red'
    }
  },
  methods: {
    add () {
      this.num++
    }
  }
}
</script>
<style lang="less" scoped></style>
```

#### 生命周期

- bind:只调用一次，指令第一次绑定到元素时调用，用这个钩子函数可以定义一个绑定时执行一次的初始化动作。
- inserted:被绑定元素插入父节点时调用（父节点存在即可调用，不必存在于document中）。
- update:被绑定于元素所在的模板更新时调用，而无论绑定值是否变化。通过比较更新前后的绑定值，可以忽略不必要的模板更新。
- componentUpdated:被绑定元素所在模板完成一次更新周期时调用。
- unbind:只调用一次，指令与元素解绑时调用。

```javascript
Vue.directive('hyh', {
    bind:function(){//被绑定
     console.log('1 - bind');
     el.style = 'color:' + binding.value
    },
    inserted:function(){//绑定到节点
        console.log('2 - inserted');
    },
    update:function(){//组件更新
        console.log('3 - update');
    },
    componentUpdated:function(){//组件更新完成
        console.log('4 - componentUpdated');
    },
    unbind:function(){//解绑
        console.log('1 - bind');
    }
})
```

## 组件化开发

### 脚手架安装

```javascript
vue-cli2   vue init webpack my-project
vue-cli3   vue create my-project
```

### 父组件->子组件

> props：在组件中，用props来定义父组件传递的值

- 简单写法->不建议

  ```javascript
  props:['name','age']
  ```

- 对象写法：

  ```javascript
  props:{
  	name:{
  		type:String,
  		required:true,  // 是否是必传, true->父组件不传会报错
  		default:'张三', // 默认值->基本数据类型
  	}
  	hoppy:{
  		type:Array,
  		required:true,  // 是否是必传, true->父组件不传会报错
  		default:function(){   // 如果默认值是对象或者数组，必须从工厂函数中获取
  			return ['aa','bb']
  		}
  	}
  }
  ```

### 子组件->父组件

>  $emit：自定义事件

- 在子组件中，通过$emit()来触发事件。 
- 在父组件中，通过v-on来监听子组件事件 。

### 父子组件的访问方式

- $children

  > 获取到父组件页面中所有的子组件，以列表形式，当子组件过多时，往往不能确定它的索引值，甚至还可能会发生变化。 

  ```javascript
  // 子组件
  <div id='app'>
      <div>
      	<cpn></cpn>
          <cpn></cpn>
          <cpn></cpn>
          <cpn></cpn>
  	</div>
  </div>
  // 父组件
  mounted(){
      console.log(this.$children)
  }
  
  ```

- $refs

  > $refs和ref指令通常是一起使用的。 ref类似于一个特定的id，$refs返回值为object

  ```javascript
  // 子组件
  <div id='app'>
      <div>
  		<cpn ref="first"></cpn>
  		<cpn ref="second"></cpn>
  		<cpn></cpn>
  		<cpn></cpn>
  	</div>
  </div>
  // 父组件
  mounted(){
  	console.log(this.$refs.first)
  }
  ```


### 插槽

> 组件的插槽也是为了让我们封装的组件更加具有扩展性 

#### 具名插槽

```javascript
// 子组件
<div>
	<slot name="left">
		<div>默认插槽</div>
	</slot>
	<slot name="right"></slot>
</div>
//父组件
<div id='app'>
	<cpn>
		<div slot="left">左插槽</div>
		<div slot="right">右插槽</div>
	</cpn>
	<span>----------</span>
	<cpn></cpn>
</div>
```

#### 作用域插槽

```javascript
//子组件
<template id="cpn">
	<div>
		<slot :data="list"></slot>
	</div>
</template>
// 父组件
<div id='app'>
	<cpn>
		<template slot-scope="scope">
			<ul>
				<li v-for="item in scope.data">{{item}}</li>
			</ul>
		</template>
	</cpn>
	<cpn>
		<template slot-scope="aaa">
			<span v-for="item in aaa.data">{{item}}--</span>
		</template>
	</cpn>
</div>
```

## 生命周期函数

- beforeCreate

> 在它之前刚初始化了一个空的vue实例对象，在这个阶段，实例对象身上只有默认的一些生命周期函数和默认的事件，其他的东西都未创建，`在这个生命周期函数执行的 时候，data和methods中的数据都还没有初始化 `

```vue
<div id="app"></div>
<script>
    var vm = new Vue({
        el: "#app",
        data: {
            msg: "hello"
        },
        methods: {
            show() {
                console.log("我是show方法")   
            }
        },
        beforeCreate() {
            console.log(this.msg)   //输出undefined
            this.show()     //报错，this.show不是一个函数
        }
    })
</script>
```

- created

> 在created中，data和methods等都已经被初始化好了，所以`如果要用到methods中的方法或者操作data中的数据，最早只能在created中操作 `

```vue
<div id="app"></div>
<script>
    var vm = new Vue({
        el: "#app",
        data: {
            msg: "hello"
        },
        methods: {
            show() {
                console.log("我是show方法")  
            }
        },
        created() {
            console.log(this.msg)  //输出  hello
            this.show()     //输出  我是show方法
        }
    })
</script>
```

- beforeMount

> 接着下来，vue开始编辑模板，执行vue的代码，最终会在内存中生成一个编译好的最终模板字符串，紧接着渲染为内存中的DOM，也就是说，此函数在执行的时候，只是在内存中渲染好了模板，而没有`把模板挂载到真正的页面中去`，这个阶段，页面还是旧的 

```vue
<div id="app">
    <h1 id="aa">{{msg}</h1>
</div>

<script>
    new Vue({
        el: "#app",
        data: {
            msg: "hello"
        },
        beforeMount:{
            var aa=document.querySelector("#aa").innerHTML
            console.log(aa)   //输出   {{msg}}
        }
    })
</script>
```

- Mounted

> 这个时候已经将在内存中编译好的模板，`真正的替换到浏览器的页面中去`，如果要操作页面上的DOM节点，最早要在mounted中进行。`只要执行完了mounted，就表示整个vue实例已经初始化完毕了`。此时，组件已经脱离了创建阶段，进入到了运行阶段  

```vue
<div id="#app">
    <h1 id="aa">{{msg}</h1>
</div>

<script>
    new Vue({
        el: "#app",
        data: {
            msg: "hello"
        },
        mounted:{
            var aa=document.querySelector("#aa").innerHTML
            console.log(aa)   //输出   hello
        }
    })
</script>
```

- beforeUpdate

>  当执行beforeUpdate的时候，页面中显示的数据还是旧的，不过这个时候data中的数据是最新的，`页面尚未和最新的数据保持同步 `

```vue
<div id="#app">
    <h1 id="aa">{{msg}</h1>
    <button @click="msg='yes'"></button>
</div>

<script>
    new Vue({
        el: "#app",
        data: {
            msg: "hello"
        },
        beforeUpdate:{
            console.log("页面中h1的内容："+document.querySelector("#aa").innerHTML)  //输出 hello
            console.log("msg中的内容"+this.msg)   //输出  yes
        }
    })
</script>
```

- updated

> ###### 到达这个时候，会先根据data中最新的数据， 在内存中重新渲染出一份最新的DOM树，更新完后紧接着把这份最新的DOM树重新渲染到真实的页面中去，这样就完成了data（model层）到view（视图层）的更新。updated事件执行的时候，页面和data中的数据已经保持同步了，都是最新的了

```vue
<div id="#app">
    <h1 id="aa">{{msg}</h1>
    <button @click="msg='yes'"></button>
</div>

<script>
    new Vue({
        el: "#app",
        data: {
            msg: "hello"
        },
        updated:{
            console.log("页面中h1的内容："+document.querySelector("#aa").innerHTML)  //输出 yes
            console.log("msg中的内容"+this.msg)   //输出  yes
        }
    })
</script>
```

- beforeDestroy

> 当执行beforeDestroy的时候，vue实例就已经从运行阶段，进入到了销毁阶段。这个时候实例身上的data和methods以及component等等都处于可用状态，还没有真正执行销毁的过程 

- destroyed

> 当执行到destroyed函数的时候，组件已经被完全销毁了，此时组件中的data,methods等等都已经不可用了 

## 路由(vue-router)

### 发展阶段

1. 后端路由->后端渲染

   > 当我们页面中需要请求不同的路径内容时, 交给服务器来进行处理, 服务器渲染好整个页面, 并且将页面返回给客户

   缺点：

   1. 一种情况是整个页面的模块由后端人员来编写和维护的. 
   2. 另一种情况是前端开发人员如果要开发页面, 需要通过PHP和Java等语言来编写页面代码. 
   3. 而且通常情况下HTML代码和数据以及对应的逻辑会混在一起 

2. 前后端分离->前端渲染

   > 后端只提供API来返回数据, 前端通过Ajax获取数据, 并且可以通过JavaScript将数据渲染到页面中

   优点：

   1. 前后端责任的清晰, 后端专注于数据上, 前端专注于交互和可视化上

3. 单页面富应用阶段(SPA：Single page Web application)

   > 在前后端分离的基础上加了一层前端路由 

### vue-router

> npm install vue-router --save

```javascript
// router/index.js

// 配制路由相关信息
import Vue from 'vue'
import VueRouter from 'vue-router'

// 通过Vue.use(插件)，安装插件 
Vue.use(VueRouter)

// 创建VueRouter实例
const routes = [
    {
    path: '',
    redirect: '/home' // 重定向路径
  },
  {
    path: '/home',
    component: Home
  },
  {
    path: '/about',
    component: About
  }
] // 配置路由和组件的映射关系
const router = new VueRouter({
  routes
})
// 将router传入到vue实例
export default router

// main.js
import Vue from 'vue'
import App from './App'
import router from './router'
Vue.config.productionTip = false

/* eslint-disable no-new */
new Vue({
  el: '#app',
  router,
  render: h => h(App)
})

```

#### router-link

> 组件支持用户在具有路由功能的应用中 (点击) 导航 

- to -> 跳转路由
- replace -> 启用history.replaceState
- tag -> 生成一个别的标签
- active-class -> 当导航处于活跃状态的class,可在`router/index.js`下统一配置

```vue
<router-link to="about" tag="button" replace>关于</router-link>
<router-link to="home" tag="button" replace>首页</router-link>
```

#### 路由懒加载

> 当打包构建应用时，Javascript 包会变得非常大，影响页面加载 ，路由懒加载的主要作用就是将路由对应的组件打包成一个个的js代码块。

##### 懒加载的方式

> 引入组件时以函数的方式引入

```javascript
{
  path: '/about',
  component: () => import('../components/about'),
  meta: {
    title: '关于'
  }
}
```

#### 嵌套路由

> 一个路径映射一个组件, 访问这两个路径也会分别渲染两个组件 

```javascript
// router/index.js
{
  path: '/home',
  component: () => import('../components/home'),
  children: [
    {    // 默认路径
      path:'/home',
      redirect:'news'
    },
    {
      path: 'news',
      component: () => import('../components/news')
    },
    {
      path: 'message',
      component: () => import('../components/message')
    }
  ],
  meta: {
    title: '首页'
  }
},
// home.vue
<div>
    <h2>我是home</h2>
    <router-link to="/home/news">新闻</router-link>
    <router-link to="/home/message">消息</router-link>
    <router-view></router-view>
</div>
```

#### 组件传参

1. params
   1. 配置路由格式: /router/:id 
   2. 传递的方式: 在path后面跟上对应的值 
   3. 传递后形成的路径: /router/123, /router/abc
   4. 获取数据:this.$route.params.id
2. query
   1. 配置路由格式: /router, 也就是普通配置 
   2. 传递的方式: 对象中使用query的key作为传递方式 
   3. 传递后形成的路径: /router?id=123, /router?id=abc 
   4. 获取数据:this.$route.query.id

#### 路由守卫

> vue-router提供的导航守卫主要用来监听监听路由的进入和离开的

[官方文档](<https://router.vuejs.org/zh/guide/advanced/navigation-guards.html> )

- 全局前置守卫(router.beforeEach(to,from,next))

  - to: 即将要进入的目标路由对象
  - from:当前导航正要离开的路由
  - next:一定要调用该方法来 resolve这个钩子。执行效果依赖 `next` 方法的调用参数 
    - next() -> 进行管道中的下一个钩子，跳转路由
    - next(false)  ->中断路由
    - next('/')  ->next传入一个路由，表示跳转到该路由

  ```javascript
  router.beforeEach((to, from, next) => {
    document.title = to.matched[0].meta.title
    next()
  })
  ```

- 全局后置钩子(router.afterEach(to,from))  ->  不会接受next函数，也不会改变导航本身

- 组件内路由守卫

  ```javascript
  new Vue({
      data(){
          return {}
      },
      methods:{},
      beforeRouteEnter (to, from, next) {
          // 在渲染该组件的对应路由被 confirm 前调用
          // 不！能！获取组件实例 `this`
          // 因为当守卫执行前，组件实例还没被创建
      },
      beforeRouteUpdate (to, from, next) {
          // 在当前路由改变，但是该组件被复用时调用
          // 举例来说，对于一个带有动态参数的路径 /foo/:id，在 /foo/1 和 /foo/2 之间跳转的时候，
          // 由于会渲染同样的 Foo 组件，因此组件实例会被复用。而这个钩子就会在这个情况下被调用。
          // 可以访问组件实例 `this`
      },
      beforeRouteLeave (to, from, next) {
          // 导航离开该组件的对应路由时调用
          // 可以访问组件实例 `this`
      }
  })
  ```

##### 路由守卫流程解析

1. 导航被触发。
2. 在失活的组件里调用离开守卫。
3. 调用全局的 `beforeEach` 守卫。
4. 在重用的组件里调用 `beforeRouteUpdate` 守卫 (2.2+)。
5. 在路由配置里调用 `beforeEnter`。
6. 解析异步路由组件。
7. 在被激活的组件里调用 `beforeRouteEnter`。
8. 调用全局的 `beforeResolve` 守卫 (2.5+)。
9. 导航被确认。
10. 调用全局的 `afterEach` 钩子。
11. 触发 DOM 更新。
12. 用创建好的实例调用 `beforeRouteEnter` 守卫中传给 `next` 的回调函数。

#### keep-alive

>  keep-alive 是 Vue 内置的一个组件，可以使被包含的组件保留状态，或避免重新渲染。
>
> 它们有两个非常重要的属性: 
>
> - include - 字符串或正则表达，只有匹配的组件会被缓存 
> - exclude - 字符串或正则表达式，任何匹配的组件都不会被缓存 

## 状态(vuex)

> 状态的集中处理，存储多个页面都需要的状态

### Vuex核心概念

#### state

  > vuex提出单一状态树(Single Source of Truth)概念,所有的状态放在一个store中，不要有多个store

#### getters

  >类似于computed中的get方法

  ```javascript
getters: {
    // 基本用法：第一个参数是state
    moreTo20 (state) {
      return state.student.filter(item => item.age > 20)
    },
    // 调用getters内其他方法：第二个参数是getters
    moreTo20length (state, getters) {
      return getters.moreTo20.length
    },
    // 根据外部传入的参数处理:getters中的方法只能接受两个参数(state,getters),如果外部传参，只能返回函数来处理
    moreToAge (state) {
      return function (age) {
        return state.student.filter(item => item.age > age)
      }
    }
  },
  ```

#### mutation

> vuex提供的唯一的更新state的方式：提交mutation
>
> 里面的方法必须是同步的

- 普通方式

  ```javascript
  // store/index.js
  mutations: {
    increment (state,payload) {
       console.log(payload)
    }
  },
  // 页面
  this.$store.commit('increment' ,{ name: '张三', age: 10 })
  ```

- 带type属性的对象

  ```javascript
  // store/index.js
  mutations: {
    increment (state,payload) {
       console.log(payload)
    }
  },
  // 页面
      this.$store.commit({
          type:'increment',
          info:{ name: '张三', age: 10 }
      })
  ```

##### mutation响应规则

- 提前在store中初始化好所需的属性
- vue.set(object,key,value)
- vue.delete(object,key)

#### action

> 处理异步的请求

```javascript
// store/index.js
actions: {
    increment (context) {  // context:执行上下文，相当于$store
        return new Promise((resolve, reject) => {
            setTimeout(() => {
                context.commit(INCREMENT)
                resolve('action处理完成')
            }, 1000)
        })
    }
},
// 页面 -> 调用actions用dispatch
this.$store.dispatch('increment').then(res => {
    console.log(res)
})
```

## vue中动画

### css动画原理

> vue中用<transition></transition>标签将需要进行动画的元素包裹起来，指定name属性(可不进行指定)
>
> transition会对包裹元素元素加载的瞬间赋予类(v-enter,v-enter-active,v-leave-to,v-leave-active)
>
> v-enter,v-enter-active 元素由消失到出现过程，元素加载完成进行第一帧动画时v-enter会被remove,动画完成后v-enter-active被remove
>
> v-leave-to,v-leave-active 元素由出现到消失过程，元素加载完成进行第一帧动画时v-leave-to会被remove,动画完成后v-leave-active被remove

```vue
html
<transition>
    <el-form-item label="定金金额" v-show="ruleForm.consumptionType == 2">
        <el-input :disabled="createUserId != userId" type="number" v-model="ruleForm.earnestMoney"
                  placeholder="请输入定金金额"></el-input>
    </el-form-item>
</transition>
css
.v-enter,.v-leave-to{
  opacity: 0;
}
.v-enter-active,.v-leave-active{
  transition:opacity 1s;
}
```

### 在vue中使用anmiate.css动画

```html
/*
* appear 首次进入页面 开始动画
* appear-active-class  首次进入页面  执行的类
* enter-active-class 开始进入时执行的类
* leave-active-class 离开时执行的类
* type  当animate跟transition同时存在时，以type指定的动画时长为标准时长
* :duration='10000'  动画时长为10000毫秒
* :duration='{entry:5000,leave:100000}'  入场动画时长  5000毫秒  出场动画时长10000毫秒
*/
<link href='animate.css'>
<transition appear enter-active-class='animated swing' leave-active-class='animated swing' appear-active-class='animated swing'>
</transition>
```

### Vue.js中js动画与Velocity.js结合

```vue
<transition @before-enter='handleBeforeEnter' @enter='handleEnter' @after-enter='afterEnter' @befoer-leave='' @leave='' @after-leave=''>
    <div></div>
</transition>
<script>
    methods:{
        handleBeforeEnter (el) {
            // el : transition标签所包裹的dom元素
            console.log('handleBeforeEnter')
        },
        handleEnter （el,done） {
           // done： 回调函数
            setTimeout(()=>{
                el.style.color = 'red'
                done() // 回调函数执行，表明动画执行完成，然后会调用after-enter钩子函数
            },2000)
        }，
        afterEnter (el) {
            el.style.color = '#000'
        }
    }
</script>
```

### 列表动画

```vue
<transiton-group>
	<div v-for="(item,index) in arr" :key='index'>{{item}}</div>
</transiton-group>
<button @click='add'>添加</button>
data () {
    return {
		arr: []
    }
}
methods: {
    add () {
		this.arr.push('aa')
    }
}
```

