[视频链接](http://www.html5train.com/kecheng/detail_1029018)

### 数据类型

#### 基本数据类型(进行值操作)

> 直接按值操作，例如 var a=12;直接把12赋予变量a

- number
- string
- null
- undefined
- boolean

#### 引用数据类型(按引用地址操作)

> js中遇到对象，会严格按照以下步骤进行
>
> 1、浏览器为其开辟一个新的内存空间，为了方便后期可以找到这个空间，浏览器为其分配一个16进制的地址
>
> 2、按照顺序依次把键值对放入内存空间
>
> 3、把开辟内存的地址赋予变量，变量可以通过地址找到该空间，进行操作

- 对象
  - {}  普通对象
  - []  数组
  - /^/  正则
  - Math   
  - ...
- 函数
  - function  普通函数
  - 类
  - ...

```javascript
function aa(){
    var aa=Array.prototype.slice.call(arguments);
    return eval(aa.join('+'));
}
```
##### 函数的操作

1. 创建函数

   1. 先开辟一个内存空间(分类一个16进制的地址)
   2. 把函数体中编写的js代码当做`字符串`存储到空间中(函数只创建不执行，没有意义)
   3. 把分配的地址赋值给声明的函数值(function fn 和 var fn 操作原理其实相同，都是在当前作用域当中申明了一个名字，此处两个名字是重复的)

2. 执行函数

   > 目的：执行函数体中的代码

   1. 函数执行的时候，浏览器会形成一个新的私有作用域 (只能执行函数体中的代码执行) 供函数体中的代码执行
   2. 执行代码之前，先把创建函数存储的那些字符串编程真正的js表达式，按照从上到下的顺序在私有作用域中执行

   > 一个可以被执行n次，每一次执行相互之间互不干扰

   > 形成的私有作用域把函数体中的私有变量保护起来，在私有作用域中操作私有变量和外界没有关系，外界也无法直接操作私有变量，我们把函数执行形成的这种保护机制叫做`闭包`

### 栈内存、堆内存

> 在项目中，内存越少性能越好，我们需要把一些没用的内存处理掉

- 栈内存

  > 俗称叫做作用域（全局作用域/私有作用域）

  - 为js代码提供执行的环境
  - 基本数据类型直接存放在栈内存中

- 堆内存

  >储存引用对象类型值的（相当于一个存储的仓库）

  - 对象存储的是键值对
  - 函数存储的是代码字符串

#### 内存释放

- 堆内存

```javascript
var o={}  //当前对象对应的堆内存被变量o占用，堆内存无法销毁
o=null    //null空对象指针(不指向任何堆内存)，此时上一次的堆内存就没有被占用了
// 谷歌浏览器会在空闲时间把没有被占用的堆内存自动释放
// ie:计数机制
```

- 栈内存

  > 一般情况下，函数执行形成栈内存，函数执行完，浏览器会把形成的栈内存自动释放，有时候执行完成，栈内存不能被释放

  > 全局作用域在加载页面的时候执行，关闭页面时销毁

### 变量提升(预解析)

> 在`当前作用域`中，js代码自上而下执行之前，浏览器会把所有带`var,function`关键字的进行提前`声明或者定义`

- 声明(declare)：var num  在当前作用域中声明我有num这个名了
- 定义(defined)：num=12  把声明的名字赋一个值
- 带var关键字的只是提前声明一下，带function关键字的在变量提升阶段把声明和定义都完成了

```javascript
console.log(num)  =>undefined
console.log(fn)   =>函数本身
var num=13;
function fn(){
    console.log(a)   =>undefined
    var a=10;
    console.log(a)   =>   10
}
fn()
console.log(num)   =>13
```

#### 定义变量带var和不带var的区别

##### 全局作用域

> 在全局作用域中，我们声明一个变量，相当于给全局对象window增加了一个属性名

- 带var 在当前作用域中声明一个变量，如果当前是全局作用域，也相当于给全局作用域设置了一个属性叫做a
- 不带  在全局作用域中，如果不带var ，仅仅是给全局对象设置了一个新的属性名(把window省略了)

##### 私有作用域

- 带var

```javascript
function fn(){
    console.log(a)  // =>undefined
    var a=12
    console.log(a)  // =>12
}
fn()
console.log(a)   //  =>报错
//闭包机制：私有作用域保护里面的私有变量不受外界的干扰
```

- 不带var

```javascript
function fn(){
    a=12
    console.log(a)  // =>12
}
fn()
console.log(a)  //=>12
```

#### 作用域链

> 函数执行形成一个私有的作用域链（保护私有变量），进入到私有作用域中，首先变量提升（什声明过的变量私有的）接下来代码执行

1. 执行的时候遇到一个变量，如果这个变量是私有变量，闭包机制
2. 如果当前变量不是私有变量，我们需要向他的上级作用域进行查找，上级如果也没有，则继续向上查找，一直到window全局作用域为止，我们把这种查找机制叫做`作用域链`
   1. 如果上级作用域有，我们当前操作的就是上级作用域中的变量（加入我们在当前作用域值改了，相当于把上级作用域中的这个值修改了）
   2. 如果上级作用域没有这个变量(window也没有)
      1. 变量=值  相当于给上级作用域,相当于给window设置了一个属性
      2. alert(变量)   想要输出这个变量，但是此时是没有的，所以会报错

```javascript
console.log(x,y)  //  undefind  undefind
var x=10,
    y=20;
function fn(){
    console.log(x,y);  // undefind 20
    var x=y=100; // -> var x=100;y=100
    console.log(x,y);  // 100 100
}
fn();
console.log(x,y);  // 10 100
```

#### 只对等号左边的进行变量提升

> 赋值，左边是变量，右边应该都是值
>
> 匿名函数：函数表达式(把函数当做一个值赋值给变量或者其他内容)

```javascript
console.log(fn);  //undefined
var fn=function(){
    
};
console.log(fn);  // 函数本身
```

真实项目当中，应用这个原理，我们创建函数的时候可以使用函数表达式得方式。原因如下：

1. 因为只能对变量左边的进行提升，所以变量提升完成后，当前函数只是声明了，没有定义，想要执行函数`只能放在复制的代码之后执行`
2. 这样让我们的代码逻辑更加严谨，以后想要知道一个执行的函数做了什么功能，只需要查找定义的部分即可(不会存在定义的代码在执行下面的情况)

#### 不管条件是否成立都要进行变量提升

- 不管条件是否成立，判断体中出现的var/function都要进行变量提升，但是在最新版浏览器中，function声明的变量只能提前声明不能定义了（前提：函数是在判断体中）

  ```javascript
  console.log(num);   //undefined
  console.log(fn);    //undefined
  if (1===1){
      var num=12;
      function fn(){
          
      }
  };
  ```

- 代码执行到条件判断地方

  - 条件不成立，进入不到判断题中,复制的代码执行不了，此时之前声明的变量或者函数依然是`undefined`

  - 条件成立,进入条件判断体中的第一件事情不是执行代码，而是把之前变量提升没有定义的函数首先定义了(进入到判断体中函数就定义了，迎合ES6中的块级作用域)

    ```javascript
    console.log(num);   //undefined
    console.log(fn);    //undefined
    if (1===1){
        console.log(num)  // undefinede
        console.log(fn)  //  函数体本身
        var num=12;
        function fn(){
            
        }
        console.log(num)  //12
        console.log(fn)   //  函数体本身
    };
    console.log(fn)   //  函数体本身
    ```

```javascript
f=function(){return true;};
g=function(){return false};
~function(){
    if(g() && []==![]){
        f=function(){return false;};
        function g(){return true};
    };
}();
console.log(f());
console.log(g());
```

#### 关于重名的处理

> 在变量提升阶段，如果名字重复了，不会重新的进行声明，但是会重新的进行定义(后面赋的值会把前面赋的值给替换掉)

```javascript
fn();  // =>4
function fn(){console.log(1);}
fn();   // =>4
function fn(){console.log(2);}
fn();   // =>4
var fn=13;
fn();  // => 报错
function fn(){console.log(3);}
fn();
function fn(){console.log(4);}
fn();
```

### 闭包

#### 作用域

> 全局作用域：window
>
> 私有作用域：函数执行
>
> 块级作用域：使用Let创建变量存在块级作用域

#### 查找私有变量

js中私有变量有且只有两种

1. 在私有作用域变量提升阶段声明过的变量(或者函数)
2. 形参也是私有变量

##### 函数执行的完整步骤

> 形参赋值->变量提升->代码自上而下执行->当前私有作用域销毁或者不销毁

```javascript
var x=10,
    y=20,
    z=30;
function fn(x,y){
    console.log(x,y,z);  
    var x=100;
    y=200;
    z=300;
    console.log(x,y,z);
}
fn(x,y,z);
console.log(x,y,z);
```

```javascript
function fn(b){
    console.log(b);
    function b(){
        console.log(b);
    };
    b();
};
fn(1);
```

`函数执行形成一个私有作用域(A),A的上一级作用域跟它在哪执行没有关系，只跟在哪定义的有关`

#### 作用

##### 保护

> 形成私有作用域，保护里面的私有变量不受外界的干扰

- jQuery实现全局调用里层方法

```javascript
(function(window,undefiend){
     var jQuery=function(){
        ....
    }
	window.jQuery=window.$=jQuery
 })(window)
jQuery()
$()
```

> 真实项目中，我们利用闭包保护机制，实现多人协同开发(避免多人同一个命名导致代码冲突的问题)

##### 保存

> 函数执行形成一个私有作用域，函数执行完成之后，形成的这个栈内存一般会自动释放

```javascript
function fn(){
    var i =1;
    return function(n){
        console.log(n+i++)
    }
}
var f=fn()
f(10) // 11
fn()(10) // 11
f(20) //22
fn()(20) //21
```

> 先进行的全局的变量提升，然后自上而下代码执行，`var f = fn()`把fn()的返回值赋值给f，因为返回值为函数，执行时开辟内存空间，f执行新开辟的内存空间，因为f占用新开辟的内存空间，因此执行后不会被销毁，
>
> fn()(10) 先执行fn(),把fn的返回值进行二次执行

### this

> 当前函数执行的主体(谁执行的函数，this指向谁)
>
> ```this是跟它在哪定义的以及在哪执行的没有任何关系```

- 函数以外的this是window

```javascript
function fn(){
	console.log(this)  //window
}
fn()
// fn() == window.fn()
function fn(){
	function b(){
		console.log(this) //window
	}
	b()
}
fn()
```

#### 规律

- 在js非严格模式下(默认模式就是非严格模式)
  - 自执行函数中的this就是widow

    ```javascript
    var obj={
    	fn:(function(){
    		console.log(this)  // this
    		return function(){}
    	})()
    }
    ```

- 给元素的某个事件绑定方法，当事件丑法执行对应方法的时候，方法中的this一般都是当前元素操作的元素本身

  ```javascript
  obox.onclick = function(){
      // this -> obox
  }
  ```

- 当方法执行，看看方法名前面是否有`.`,有的话`.`前面是谁，this指向谁，没有的话，this一般指向window

  ```javascript
  var obj={
  	fn:function(){
  		console.log(this)
  	}
  }
  obj.fn() // this -> obj
  var f = obj.fn
  f() // this -> window
  ```

- 在js严格模式下(让js更加严谨)

  > 开启严格模式：在当前作用域的第一行加`use strict`,name当前模式执行的js代码，就是按照严格模式处理的

  ```javascript
  <script>
  "use strict"; //整个js代码开启严格模式
  </script>
  <script>
  	~function(){
  		"use strict"; // 只是把当前私有作用域开启了严格模式，对外面全局没有影响
  	}()
  </script>
  ```

  - 在js严格模式下，如果执行主体不明确，this指向undefined

    ```javascript
    <script>
    "use strict"; //整个js代码开启严格模式
    function fn(){
    	console.log(this)
    }
    fn()  // this->undefined
    window.fn() // this->window
    </script>
    ```


#### 闭包、this指向、作用域综合练习

```javascript
var num=1,
	obj={
		num:2,
		fn:(function(num){
			this.num*=2
			num+=2;
			return function(){
				this.num*=3;
				num++;
				console.log(num) 
			}
		})(num)
	}
var fn=obj.fn;
fn()
obj.fn()
console.log(num,obj.num)
```

解析过程

1. 全部作用域下变量提升

   > num -> undefined , obj->undefined, fn -> undefined

2. 代码自上而下执行

   > 1. 解析obj(obj为引用类型，开辟内存空间：aaa000)
   >
   >    1. num=2
   >
   >    2. fn：自执行函数(引用类型，开辟内存空间：aaa111)
   >
   >       1. 形参赋值 num=1
   >
   >       2. 变量提升 无
   >
   >       3. 代码执行
   >
   >          > this.num*=2  // this指向window；window.num->2
   >          >
   >          > num+=2  // 形参num+=2 -> 3
   >          >
   >          > return aaa222 // function为函数，开辟内存空间：aaa222
   >
   >    3. 将自执行函数的返回值赋予fn；fn->aaa222  // 因为aaa111开辟的堆内存aaa222被aaa111以为的占用，所以aaa111不销毁
   >
   > 2. fn = obj.fn ; // fn指向aaa222
   >
   > 3. fn()  // 开辟一个内存空间aaa333，将aaa222中的代码复制执行
   >
   >    1. this.num**=3 // this指向window；window.num*=3 ->window.num=6
   >    2. num++   // num不是aaa222私有的，向上一级aaa111查找 ，num++ -> num=4
   >    3. console.log(4)
   >    4. aaa333销毁
   >
   > 4. obj.fn() // 开辟一个内存空间aaa444，将aaa222中的代码复制执行
   >
   >    1. this.num*=2  //this指向obj；obj.num*=3  ->  obj.num = 6
   >    2. num++    // num不是aaa222私有的，向上一级aaa111查找 ，num++ -> num=5
   >    3. console.log(5)
   >    4. aaa444销毁
   >
   > 5. console.log(6,6)


## 面向对象

### 属性类型

#### 数据属性

- [[configurable]]:表示能否通过delete删除属性从而重新定义属性，能否通过修改属性的特性，或者能否把属性修改为访问器属性

  ```javascript
  // 该属性配置为false之后，便不可以再改为true，否则会报错
  var object = {}
  Object.defineProperty(object,'name',{
  	configurable:false,
  	writeable:false,
  	value:'bb'
  })
  object.name = 'aa'
  Object.defineProperty(object,'name',{ // 报错 Cannot redefine property: name
  	configurable:true,
  })
  ```

- [[Enumberable]]:表示能否通过for-in循环返回属性
- [[Writable]]:能否修改该属性值
- [[Value]]:属性的数据值，默认为undefined

```javascript
// 使用ECMAScrite5中的Object.defineProperty()方法，可修改数据属性------单个属性
var object = {}
Object.defineProperty(object,'name',{
	writeable:false,
	value:'bb
})
object.name = 'aa' // 非严格模式下，该操作被忽略,严格模式下，该操作报错,其他数据属性同理
console.log(object.name) // 'bb'
// Object.defineProperties() ------多个属性 (IE9+、Firefox 4+、Safari 5+、Opera 12+、Chrome)  
Object.defineProperties(object,{
    name:{
        writable:false
    },
    age:{
        ...
    }
})
```

#### 访问器属性

> 访问器属性不包含数据值，包含getter(读取访问器属性时调用，返回有效的值)和setter函数(写入访问器属性时调用)

- [[configurable]]:表示能否通过delete删除属性从而重新定义属性，能否通过修改属性的特性，或者能否把属性修改为访问器属性
- [[Enumberable]]:表示能否通过for-in循环返回属性
- [[get]]:读取属性时调用的函数，默认值为undefined
- [[set]]:写入属性时调用的函数，默认值为undefined

```javascript
var object = {
	_age:10,
	year:''
}
Object.defineProperty(object,'age',{
	get:function(){
		return this._age
	},
	set:function(newvalue){
        if (newvalue <=19) {
        	this.year = '00后'
        } else {
        	this.year = '90后'
        }
	}
})
object.age = 20
console.log(object.year)
```

#### 读取属性的特性

> Object.getOwnPropertyDescriptor()

```javascript
Object.getOwnPropertyDescriptor(Object,'prototype')
// configurable: false
// enumerable: false
// value: {constructor: ƒ, __defineGetter__: ƒ, __defineSetter__: ƒ, hasOwnProperty: ƒ, __lookupGetter__: ƒ, …}
// writable: false
```

#### 构造函数模式

> var Person = function(){}
>
> var person = new Person()

使用new创建实例，会经历一下4步

1. 创建一个新的对象
2. 构造函数的作用域赋值给新对象(this指向这个新对象)
3. 执行构造函数中的代码
4. 返回这个新对象

### 单例模式

我们把对象数据类型实现`把描述同一件事务的属性或者特征归纳汇总在一起，以此来避免全局变量的冲突问题`的方式和思想就是`单例设计模式`

> 在真实项目中，为了实现模块化开发或者团队协作开发，我们经常应用单例模式(一般业务逻辑部分的代码都是依托单例模式设计规划的)

> 由来：很久很久以前，js中都是值类型，没有引用数据类型

```javascript
var name = '张三'
var name = '李四'
// 全局变量污染 全局变量冲突
```

> 对象数据类型：把描述同一件事务的特征或者属性，进行汇总（放在一起），以此来避免全局变量之间的冲突

### 原型与原型链

#### 原型

1. 函数中的prototype属性,是一个指针，指向一个对象(Object空对象)

   1. 每一个函数都有一个prototype属性，他默认指向一个object空对象(即称为：原型对象)

      ```javascript
      function Fn(){}
      console.log(Fn.prototype)
      ```

   2. 原型对象有一个属性constructor，他指向函数对象

      ```javascript
      console.log(Fn.prototype.constructor)  // 输出为Fn
      ```

   3. 通过isPrototypeOf()来确定实例与原型对象之间的关系

      ```javascript
      function Fn(){}
      let fn = new Fn()
      Fn.prototype.isPrototypeOf(fn) // true
      Object.getPrototypeOf(fn) == Fn.prototype // true
      ```

2. 给原型对象添加属性(一般是方法)

   1. 作用:函数的所有实例对象自动拥有原型中的属性(方法)

      ```javascript
      Fn.prototype.test=function(){
          console.log('test')
      }
      var fn = new Fn()
      fn.test()
      ```

3. 每一个函数都有一个prototype属性`定义函数时自动添加的`，称为显式每一个实力对象有一个__proto__(传教关键对象时自动添加的)，称为隐式原型，隐式原型的值即为其构造函数的显式原型的值

   ```javascript
   function Fn(){}
   console.log(Fn.prototype) 
   var fn = new Fn()
   console.log(fn.__proto__)
   console.log(Fn.prototype === fn.__proto__)  // true
   ```

4. 通过hasOwnPrototype()判断某一属性是存在于实例还是原型

   > 返回值为true->属性存在于实例，false->属性存在于原型

   ```javascript
   var descriptor = Object.getOwnPropertyDescriptor(Object,'prototype')
   function Fn(){
   	
   }
   Fn.prototype.name = 'aa'
   let fn = new Fn()
   fn.name = 'bb'
   console.log(fn.hasOwnProperty('name'))  // true
   ```

   原型的动态性

   > 在原型查找值的过程是一次搜索，因此我们对原型对象所做的任何修改(重写除外)能够立即从实际上反应出来，即使是先创建了实例，后修改原型
   >
   > ```javascript
   > function Fn(){}
   > var fn=new Fn()
   > Fn.prototype.name = 'aa'
   > console.log(fn.name)
   > ```
   > 应用
   >
   > ```javascript
   > // 只需要在初始化构造函数的时候为其添加方法，不必要每次添加
   > function Fn(){
   > 	this.name= 'aa'
   > 	if (!(this.say instanceof Function)){
   > 		alert('first')
   > 		Fn.prototype.say=function(){
   > 			alert(this.name)
   > 		}
   > 	}
   > }
   > var fn1 = new Fn()
   > var fn2 = new Fn()
   > fn2.name='bb'
   > fn1.say() // first aa
   > fn2.say() // bb
   > ```
##### 原型与In操作符
###### in的用法

   - for-in循环

     > 访问所有能通过对象访问的，可枚举的属性,既包括实例也包括原型

     ```javascript
     var obj = new Object()
     Object.prototype.age = 12
     obj.name = 'aa'
     for (var item in obj){
     	console.log(item) // name age
     }
     ```

   - 单独使用in，可通过对象访问到给定的属性时返回true，不论属性在原型还是实例(原型链查找机制)

     ```javascript
     function Fn(){
         name:'a'
     }
     var fn = new Fn()
     fn.name = 'bb'
     console.log('name' in fn) //true
     console.log('name' in Fn) //true
     
     //与hasOwnprototype配合判断属性存在于对象还是原型
     function hasPrototypeProperty(object,name){
     	return !object.hasOwnProperty(name) && (name in object)
     }
     hasPrototypeProperty(fn,'name') // false
     ```


##### 原型的问题：

- 构造函数无法传参

- 原型中属性值为引用类型是，实例一改全改(多个实例的__proto__指向同一个地址)

  ```javascript
  function Fn(){}
  Fn.prototype.friends=['a','b','c']
  let fn1 = new Fn()
  let fn2 = new Fn()
  fn1.friends.push('d')
  console.log(fn1.friends) // ['a','b','c','d']
  console.log(fn2.friends) // ['a','b','c','d']
  
  //解决方法:将引用类型的值放入构造函数中
  function Fn(){
      this.friends=['a','b']
  }
  Fn.prototype={
      constructor:Fn,
      name:'aa',
  }
  var fn1 = new Fn()
  var fn2 = new Fn()
  fn1.friends.push('c')
  console.log(fn1.friends) //[a,b,c]
  console.log(fn2.friends) // [a,b]
  ```


#### 原型链

访问一个对象属性时，访问的路径：

1. 现在自身属性中查找，找到返回
2. 如果没有，再沿着__proto__这条链线上查找，找到返回
3. 如果没又找到，返回undefinde(Object.prototype.__proto__为null

## promise

> Promise是异步编程的一种解决方案

```javascript
new Promise((resolve,reject)=>{
	setTimeout(()=>{
		resolve('第一次访问成功,进行第二次访问')
	},1000)
})
.then(res => {
	console.log(res)
	return new Promise((resolve,reject) => {
		setTimeout(()=>{
			reject('第二次访问成功')
		},1000)
	})
	.then(data =>{
		console.log(data)
	})
	.catch(()=>{
		console.log('第二次访问失败')
	})

})
.catch(()=>{
	console.log('第一次访问失败')
})

// 若第二次没有进行网络请求，上面可简写为
new Promise((resolve,reject)=>{
	setTimeout(()=>{
		resolve('第一次访问成功,进行第二次访问')
	},1000)
})
.then(res => {
	console.log(res)
	return Promise.resolve('第二次访问成功')
	.then((res)=>{
         console.log(res)
	})
})
.catch(()=>{
	console.log('第一次访问失败')
})
```

### promise.all

> 一个需求需要访问两个级以上接口

```javascript
Promise.all([   // Promise.all接收一个数组，数组内存放要进行的网络请求
    new Promise((resolve,reject)=>{
    	setTimeout(()=>{
    		resolve('第一次访问成功')
    	},1000)
    }),
    new Promise((resolve,reject)=>{
    	setTimeout(()=>{
    		resolve('第二次访问成功')
    	},1000)
    })
// 得到的res为一个数组，将多个网络请求的成功结果存放，只要有一个请求失败，不会调用then，会直接调用catch，
]).then(res => {  
	console.log(res)
})
```
