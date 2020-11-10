### Typescript
- Typescript是由微T软开发的一款开源的编程语言
- Typescript是Javascript的超集，遵循最新的ES5/ES6规范。TypeScript扩展了Javascript语法
- TypeScript更像后端Java、C#这样的面向对象语言可以让JS开发大型企业应用
- 越来越多的项目是基于TS的，比如VSCode、Angular6、Vue3、React16
- TS提供的类型系统可以帮助我们在写代码的时候提供更丰富的语法提示
- 在创建前的编译阶段经过类型系统的检查，就可以避免很多线上的错误

#### 环境
```typescript
1. npm i typescript -g
2. tsc -init
3. tsc  将ts文件转化为js
4. npm i ts-node -g  // 通过vscode右键run code执行

// 通过构建工具来执行
npm i rollup typescript rollup-plugin-typescript2 @rollup/plugin-node-resolve rollup-plugin-serve -D
```

```typescript
let name = '';
// 在全局下是有name变量的，一般在自己的代码末加上export {}，防止模块间干扰
```

#### 类型

> 所有的类型， :后面的都是类型， =后面的都是值
- 基础类型
  - string
  - number
  - boolean
  
- 元组 表示长度以及个数都限制好了
  ```js
    // 可以向元祖中push数据，不可以通过索引来修改属性
    let tuble:[string,number,boolean] = ['231',12, true]
  ```
  
- 数组 存放一类类型的集合
  ```typescript
    let arr:number[] = [1,3,3]
  ```

- 枚举

  - 枚举默认下标是从0开始
  - 枚举可以进行反举
  - 可以为枚举指定不同的数据类型,如果指定的数据不是number类型，需要为下一条数据指定下标
  - 常量枚举不可以进行反举

  ```typescript
  enum USER_ROLE {
      ADMIN,
      USER = 'a',
      MANAGER = 1
  }
  console.log(USER_ROLE.ADMIN) // 0
  console.log(USER_ROLE[0]) // ADMIN
  
  const enum USER_ROLE1 {
      ADMIN,
      USER = 'a',
      MANAGER = 1
  }
  ```

- any类型

  > 不进行类型校验，相当于没有指定类型

- null   undefined

  > null   undefined 是任何类型的子类型，可以为其他类型赋值，但是在严格模式下不允许有空值，所有会报错，赋值时 null -> null undefined -> undefined

  ```typescript
  let str:string | number | null = null
  ```

- void 类型

  > 表示空类型，原则上可以将null  indefined赋值给void，但是严格模式下，null会报错

  ```typescript
  let v:void = undefined;
  console.log(v) // undefined
  ```

- never类型

  > never类型是任何类型的子类型，可以为任何类型赋值
  >
  > 有3种情况会得到never

  ```typescript
  // 1.函数报错，返回值是never
  function error():never {
      throw new Error('aaa')
  }
  let e:never = error()
  // 2.循环体陷入死循环
  function Twhile():never {
      while(true) {}
  }
  let a:never = Twhile()
  // 3.判断类型出现never
  function byType(val:number|string){
    if (typeof val === 'string') {
      val
    } else if(typeof val === 'number') {
      val
    } else {
      val
    }
  }
  ```

- symbol

  > symbol 可以做key，但是取不到值,除非转成any

  ```typescript
  let s1 = Symbol('213');
  let obj = {
    s1: 123
  }
  // console.log(obj[s1])
  ```

- ```typescript
  // BigInt
  let num1 = BigInt(Number.MAX_SAFE_INTEGER) + BigInt(1)
  let num2 = BigInt(Number.MAX_SAFE_INTEGER) + BigInt(1)
  console.log(num1 === num2)
  
  // 对象类型 非原始数据类型 object
  
  const create = (obj: object) => {};
  create({});
  ```

- 联合类型

  ```typescript
  /**
   * 联合类型 并集
   * 当没有初始化的时候，只能调用两者类型中的共同方法;
   * 会根据赋值，来推倒后续的方法
  */
  
  let str1:string|number;
  str1 = 1;
  str1.toFixed(2)
  ```
  
- 字面量类型

  ```typescript
  let direcrion: 'up'|'left'|'right'|'down'
  direcrion = 'up'
  ```

#### 函数

> 函数要考虑入参以及返回值

- funtion函数关键字声明
- const 表达式方式声明

```typescript
function sum(a:string, b:string):string {
    return a+b
}
// 如果使用函数表达式，你给他定义了类型，你可以把一个可以兼容的函数赋值给他
type Sum = (a:string, b:string) =>string
const sum1:Sum = (a:string, b:string) => { return a + b }

// 可选参数

let sum2 = (a:string, b?:string) => {
    return a
}
// 默认值
let sum3 = (a:string, b:string = '2') => {
    return a + b
}

// 剩余参数
let sum4 = (...args:number[]) => {}
sum4(1,2,3,4)
```

#### 类

- 三个运算符
  - as   断言成 xxx
  - !    非空断言
  - ？ 链运算判断符，有值取值，没有返回undefined

```typescript
class Person {
    x:number //表示实例上有这个属性
    constructor (x:number, y:number, ...args:number[]) { //这些参数跟函数使用方式一样
        this.x = x
        this.y = 2 // 因为上面没有定义y，直接this.y 会报  类型“Person”上不存在属性“y”
    }
}
let p = new Person(1)
console.dir(p)
```

- 类修饰符

  - public : 父类，子类，外面都可以访问到
  - protected：父类，子类可以访问
  - private：只有自己可以访问
  - readonly：初始化之后就不可以更改了

  > 如果constructor被标志成protected,private;则此类不可以被new，被标记成private，则不可以被继承

- 静态方法和静态属性
  - 通过类来调用的方法或者属性，就是静态方法或者静态属性
  - 静态方法或者静态属性可以被继承
  
- 属性访问器是原型属性，可以通过属性访问器来访问私有属性

```typescript
// construtor和静态方法中的super指向的是父类,原型上的方法指向的是父类的prototype
```

```typescript
class Animal {
    age:number
    constructor (public name:string, age:number) {
        this.name = name;
        this.age = age
    }
    static getName () {
        console.log('Animal')
    }
    say () {
        console.log('animal say')
    }
}

class Cat extends Animal{
    constructor (name:string, age:number, public address: string) {
        super(name, age);  // 指向父类
        this.address = address
    }
    static getName() {
        super.getName()  // 指向父类
        console.log('cat')
    }
  	private _eat = '';
  	get eat () {
      return this._eat
    }
  	set eat (value) {
      this._eat = value
    }
    say() {
        super.say(); // 指向父类的prototype
        console.log('cat say')
    }
}

Cat.getName()
let c = new Cat('Tom', 12, 'bj');
c.eat = 'hello'
console.log(c.eat)
c.say()
```

##### 抽象类

> 抽象类不能被实例化,只有抽象类里面的内容，可以标记`abstract`，子类必须实现

```typescript
abstract class Animal { // 抽象类可以包含抽象方法和抽象属性
  abstract name:string //可以没有实现
  eat() {
    console.log('eat')
  }
}

class Cat extends Animal{
  name!: string;
}
```



#### 装饰器

> 在不改变原结构的前提下，扩展新的方法，可以对类，属性，方法进行装饰

```typescript
// 对类进行装饰
function modifer (target:any) {
    target.prototype.say = (
        function () {
            console.log('say constructor')
        }
    )()
}

// 对属性进行装饰
function toUppCase(target: any, key:string) {
    let value = target[key];
    Object.defineProperty(target, key, {
        get () {
            return value.toUpperCase()
        },
        set (newValue) {
            value = newValue
        }
    })
}
// 支持扩展参数
 function double(num:number) {
    return function (target:any, key:string) {
        let value = target[key]
        Object.defineProperty(target, key, {
            get () {
                return value * num
            },
            set (newValue) {
                value = newValue
            }
        })
    }
 }
// 对方法进行装饰
 function beforeGetName(target:any, key: string, descriper:PropertyDescriptor){
     let value = descriper.value
     descriper.value = function () {
         console.log('before getName')
         value.call(target)
     }
     return descriper
 }

@modifer
class Person{
    say!:Function;
    @toUppCase
    name:string = 'hyh';
    @double(3)
    age:number = 12
    @beforeGetName
    getName () {
        console.log('getname')
    }
}

let p = new Person()
console.log(p.name)
console.log(p.age)
p.getName()
export {}
```

#### 接口

> TypeScript的核心原则之一是对值所具有的*结构*进行类型检查。 它有时被称做“鸭式辨型法”或“结构性子类型化”。 在TypeScript里，接口的作用就是为这些类型命名和为你的代码或第三方代码定义契约。

> 接口可以用来描述属性，方法，类，可以被实现，被继承

- 描述属性

```typescript
interface Fullname {
    firstname:string, 
    lastname:string
}
// 利用接口来描述属性，别人看到依赖接口，可以规范自己的传参
function fullname (obj:Fullname) {
    return obj.firstname + obj.lastname
}
fullname({firstname:'string', lastname:'string'})
```

- 描述方法

```typescript
interface FullName {
    (firstName:string,lastName:string):string
}
const fullName:FullName = (firstName:string, lastName:string):string => {
    return firstName + lastName
}
```

##### 混合类型

> 一个对象可以同时做为函数和对象使用，并带有额外的属性。

```typescript
interface Counter {
    (start: number): string;
    interval: number;
    reset(): void;
}

function getCounter(): Counter {
    let counter = <Counter>function (start: number) { };
    counter.interval = 123;
    counter.reset = function () { };
    return counter;
}

let c = getCounter();
c(10);
c.reset();
c.interval = 5.0;
```

##### 特性

> 被描述的属性，方法，类中的参数不能比接口定义的多
>
> 解决办法有四种

- 采用断言，直接断言成对应的接口

  ```typescript
  interface Potato {
      color:string,
      size: number
  }
  const potato:Potato = ({
      color: '',
      size: 10,
      address: 'bj'
  } as Potato)
  ```

- 多个重名的接口会合并，但是这样会破坏原有的接口

  ```typescript
  interface Potato {
      color:string,
      size: number
  }
  interface Potato {
      address:string
  }
  const potato:Potato = {
      color: '',
      size: 10,
      address: 'bj'
  }
  ```

- 在原接口上扩展新的接口

  ```typescript
  interface Potato {
      color:string,
      size: number
  }
  interface EPotato extends Potato{
      address:string
  }
  const potato:EPotato = {
      color: '',
      size: 10,
      address: 'bj'
  }
  ```

- 为接口添加自定义的属性

  ```typescript
  interface Potato {
      color:string,
      size: number,
      [key:string]: any
  }
  const potato:Potato = {
      color: '',
      size: 10,
      address: 'bj'
  }
  ```

  