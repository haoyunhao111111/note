

## mvvm

> model ->模型->数据  view->视图->html+css    数据到视图，视图到数据，双向数据绑定  优点>缺点

```vue
<div class="app">  //指定vue的作用范围
    <input type="text" v-model="one">+<input type="text" v-model="two">=<span v-text="result()"></span>
</div>
</body>
<script>
    new Vue({
        el:".app",  //说明vue的作用范围
        
        
        
        data:{        //设置数据，json格式
            one:0,
            two:0
        }
        
        
         methods:{     //方法  存放逻辑
            result(){
                return this.one*1+this.two*1
            }
        },
            
            
             computed:{    //只运行有关于自己的
             result(){
                return this.one*1+this.two*1
            }
        },
            
            
             watch:{
            one(one,two){    //one：改变后的值；two:改变前的值
                console.log(one,two)
            }
         }
    })
    
    :style="background:(item.isdone?red:none)"
</script>
```

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



## 指令

- v-model  只能用于表单
- v-text      用于表单以外

## 路由

## 状态

## 组件化开发

> 完整的数据，逻辑，组件

```vue
Vue component("car",        //函数名
	template:'aa',         //aa:html代码
	data(){return(bb)}，     //bb:数据   data后跟一个函数，返回值为JSON对象
	methods:{},
	。。。
) 
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

- create

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
        beforeCreate() {
            console.log(this.msg)  //输出  hello
            this.show()     //输出  我是show方法
        }
    })
</script>
```

- beforeMount

> 接着下来，vue开始编辑模板，执行vue的代码，最终会在内存中生成一个编译好的最终模板字符串，紧接着渲染为内存中的DOM，也就是说，此函数在执行的时候，只是在内存中渲染好了模板，而没有`把模板挂载到真正的页面中去`，这个阶段，页面还是旧的 

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



2

vue  init  webpack    aaaa

use   no  

 set up  no

e2e  no

npm run dev



3

@vue/cli

vue create bbb



babel  vuex   router  y y

npm run serve



## http协议下的URL标准格式

URL：统一资源定位符

URI：统一资源标识符



url格式:    协议：//主机地址：端口/路径/文件名?查询字符串#锚链接