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

## 路由

## 状态

## 组件化开发

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





## localStorage

localStorage.setITem("aa","bb")    存入

locolStorage.removeItem("aa")     删除

locolStorage.clear    清空

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
