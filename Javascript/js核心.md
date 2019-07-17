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

- 声明(declare)：var num  在当前作用域中吼一嗓子我有num这个名了
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
    conaole.log(a)  // =>undefined
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
    var x=y=100;
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
f(10)
fn()(10)
f(20)
fn()(20)
```

> 先进行的全局的变量提升，然后自上而下代码执行，`var f = fn()`把fn()的返回值赋值给f，因为返回值为函数，执行时开辟内存空间，f执行新开辟的内存空间，因为f占用新开辟的内存空间，因此执行后不会被销毁，
>
> fn()(10) 先执行fn(),把fn的返回值进行二次执行

![](https://image.coolcustomer.cn/19c9ff5c-10f5-4399-b1bb-92a3007f8b12)

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

   

   ![](https://image.coolcustomer.cn/cb3a9b24-d357-4273-a71c-25ac4a02ac47 )