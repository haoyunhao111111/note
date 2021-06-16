[官方文档](https://vue3js.cn/docs/zh/guide/migration/introduction.html)

#### setup

- 新的option,所有的组合api函数都在此使用，只在初识化的时候调用一次
- 函数如果返回一个对象，那么对象中的属性以及函数，模板中可以直接使用

#### ref

- 作用：定义一个数据的响应式
- 语法： const xxx= ref(initValue);
  - 创建一个包含响应式数据的引用
  
  - js中操作数据xxx.value

  - 模板中不需要.value

- 一般用来定义一个基本数据类型的响应式数据

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

