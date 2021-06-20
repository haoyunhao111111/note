[官方文档](https://vue3js.cn/docs/zh/guide/migration/introduction.html)

#### setup

- 新的option,所有的组合api函数都在此使用，只在初始化的时候调用一次
- 函数如果返回一个对象，那么对象中的属性以及函数，模板中可以直接使用
- setup的执行时机
  - 在beforecreate之前执行，此时组件对象还没有创建
  - this是undefined，不能通过this来访问data/method/watch/coomputed
  - 其实所有的composition API相关回调函数也都有不可以取到this
- setup返回值
  - 一般返回一个对象，为模版提供数据，
  - 返回对象的属性会与data函数返回数据合并成为组件对象的属性
  - 返回对象中的方法会与method中的方法合并成为组件对象的方法
  - 如果有重名，setup优先
  - 一般setup/data以及setup/method不要混用
  - setup不能是一个async函数
- setup的参数
  - props: 包含props配置声明且传入了的所有的属性和对象
  - context:
    - attrs: 包含没有在props中声明的属性的对象，相当于this.$attrs
    - slots:包含所有传入的插槽内容的对象，相当于this.$slots
    - emit: 用来分发自定义事件的函数，相当于this.$emit

#### ref

- 作用：定义一个数据的响应式
- 语法： const xxx= ref(initValue);
  - 创建一个包含响应式数据的引用
  
  - js中操作数据xxx.value

  - 模板中不需要.value

- 一般用来定义一个基本数据类型的响应式数据
- 如果用ref处理对象或者数组，内部会自动的将对象/数组转换为reactive的代理对象
- ref内部是通过给value属性添加getter/setter来实现对数据的劫持
- reactive内部是通过使用proxy来实现对对象内部所有数据的劫持，并通过reflect操作对象内部数据

```js
<template>
  <h3>{{count}}</h3>
  <button @click="updateData">更新数据</button>
</template>
<script>
	import {ref} from 'vue';
	export default {
		setup() {
			const count = ref(0);
			updateData() {
				count.value += 1
			}
			return {
				count,
				updateData
			}
		}
	}
</script>
```



#### reactive

- 作用： 定义多个数据的响应式
- const proxy = reactive(obj)，接受一个普通的对象然后返回该普通对象的响应式代理器对象
- 响应式转换是深层的，会影响对象内部所有嵌套的属性
- 内部基于es6的proxy实现，通过代理对象操作源对象内部对象都是响应式的

```js
<template>
  <h3>name:{{user.name}}</h3>
  <h3>age:{{user.age}}</h3>
  <h3>wife:{{user.wife}}</h3>
  <button @click="updateData">更新数据</button>
</template>
<script lang="ts">
import { defineComponent, ref, reactive } from 'vue'
export default defineComponent({
  setup () {
    let obj = {
      name: 'hyh',
      age: 26,
      wife: {
        name: 'yhs',
        age: 23,
        cars: ['a', 'b', 'c']
      }
    }
    const user = reactive(obj)
    function updateData () {
      user.name += '=='
      user.age += 2
      user.wife.name += '+='
      user.wife.cars.push('e')
      // count.value++
    }
    return {
      user,
      updateData
    }
  }
})
</script>
```

#### 响应式原理

##### vue2

- 基本类型以及对象类型，通过Object.defineProperty来劫持，为每一个属性添加getter/setter来实现响应式
- 对于数据，通过改写push,pop,shift,unshift,reserve,splice,sort这七个方法来实现对数据的监听

- 缺点
  - 对象直接添加或者删除属性，页面不是更新
  - 对于数组来说，直接通过下标替换或更新length，页面不会更新

##### vue3

- 通过Proxy拦截对data任意属性的任意操作(属性值的读写，添加，删除)
- 通过Reflect动态对被代理的相应属性进行特定的操作
- Proxy的监听的深层次的
- ie不兼容Proxy,所以vue3放弃了支持ie

#### 生命周期

| vue2          | vue3          | Components api | 说明 |
| ------------- | ------------- | -------------- | ------------- |
| beforeCreate  | beforeCreate  | setup          |  |
| created       | created       | setup          |  |
| beforeMount   | beforeMount   | onBeforeMount  |  |
| mounted       | mounted       | onMounted      |  |
| beforeUpdate  | beforeUpdate  | onBeforeUpdate |  |
| updated       | updated       | onUpdated      |  |
| activated     | activated     | onActivated |  |
|  deactivated            |deactivated|onDeactivated|  |
| beforeDestroy | beforeUnmount | onBeforeMounted |  |
| destroyed     | unMounted     | onUnmounted |  |
| errorCaptured | errorCaptured | onErrorCaptured | 子孙组件错误时被调用(错误对象，错误组件，错误字符串) |
|  | renderTracked | onRenderTracked | 跟踪虚拟dom重新渲染时调用 |
|  | renderTriggered | onRenderTriggered | 虚拟dom重新渲染被触发时调用 |

`3.0的生命周期会比2.O的先执行，vue3的生命周期是一个函数，参数是一个回调函数`

#### toRefs

> 可以把一个响应式的对象，转换成普通对象，改普通对象的每一个属性都是一个ref

- 当从合成函数返回响应式数据时，toRefs非常有用，这样消费组件就可以在不丢失响应式的情况下对返回的对象进行分解使用

#### 其他的api

##### shallowReactive && shallowRef

shallowReactive：这两个都是浅的响应式，只会对对象本身进行响应，不会进行的深度的响应

shallowRef:如果是对一个对象进行响应式，不会进行reactive处理

##### readonly && shallowReadonly

readonly：深度只读数据

shallowReadonly： 浅的只读数据

##### toRaw && markRaw

toRaw: 返回由reactive | ref 方法转换的响应式代理的普通对象

markRaw： 标记一个对象，使其永远不能被转换成代理对象，返回对象本身
