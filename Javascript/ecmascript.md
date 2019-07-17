##  js

### 优势

> 单线程异步机制的语言   js最基本的特性，极少得资源，做更多的事，用单线程模拟多线程
>
> 单线程：程序同一时间做一件事
>
> 异步机制：把需要耗费时间以及不确定时间的代码，放到异步执行

## 一、组成：

- ECMAscript

  > 变量、数据类型、运算符、数组、函数、对象
- BOM  浏览器对象模型

  > windows对象、history对象、location对象
- DOM文档对象模型

  > 元素获取、操作属性、操作样式、节点、事件、事件对象

## 二、作用：

- 数据验证
- 动态创建、删除元素
- 操作元素的内容和样式
- 模拟动画drc
- 创建cookie
- ajax 
- JSON格式的数据处理

## 三、特征：

- 客户端脚本语言、实验用户交互
- 基于`对象`和`事件`驱动的`松散型`、`解释型`语言

## 四、js的引入方式：

1. 外部引入方式：

   ```html
   <script src="index.js"></script>>
   ```

2. 嵌入式：

   > 在html页面中用`script`标签引入js

3. 事件后：

   ```html
   <div onclick="alert(1)"></div>
   ```

### 注意：

- js的几种引入方式是相互关联的，可以相互操作与访问
- 外部js中不能添加script标签对
- 嵌入式js中不能添加src属性

## 五、输出/输入工具：

#### 输出工具：

- 弹出框

  ```javascript
  alert(1);    alert('a');
  ```

- 输出到控制台(不可以识别标签对)

  ```javascript
  console.log(1);
  ```

- 输出到页面中(可以识别标签对)

  ```javascript
  document.writer("<b>加粗</b>");document.writer("<i>倾斜</i>");
  ```

#### 输入工具：

```javascript
prompt(提示文本，默认值)
```



## 六、注释：

- //         单行注释
- ctrl++shift+/   块级注释

## 七、变量：

>  一个容器,存储数据

### 命名规范：

> 数字，字母，$，_

- 不能以数字开头；
- 区分大小写；
- 不能以关键字(js中已经用到的)命名；
- 不能以保留字(js将来会用到的)命名；
- 有意义
- 首字母大写   Array  String Object
- 驼峰命名法   getElementByld

### 赋值：

- 先声明，后赋值。

  ```javascript
  var num; num=10
  ```

- 声明的同时赋值;

  ```javascript
  var a=10;
  ```

- 一次性先声明多个变量，再赋值；

  ```javascript
  var a,b,c;  a=1;b=2;c=3;
  ```

- 一次性声明多个变量并赋值

  ```javascript
  var a=1,b=2,c=3;
  ```

#### 注意事项：

- 变量先声明后访问，变量的默认值为`undefided`
- 新值覆盖旧值；
- 变量可以重复声明；
- 不用var关键字声明变量，但赋值，不会报错，此变量为全局变量
- 不用var关键字声明，也不赋值，会报错
- 先访问后声明变量，值为`undefined`,预解析(var function);

### 数据类型：

> 根据数据在内存中的存储位置划分，基本类型存放在栈中，引用数据类型存放在堆中(指针存放在栈中，内容存放在堆中)。

#### 基本数据类型（值类型）：

- undefined

- null

- string

- boolean

- number

  > 八进制：以0o开头，0-7
  >
  > 二进制：以0b开头
  >
  > 十六进制：以0x开头，0-9   a-f
  >
  > NaN:not a number  本来期望返回数值的操作但并未返回数值的操作

#### 引用数据类型：

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

#### typeof

> 用来判断变量的数据类型,结果为字符串。

```html
var str="abc";
console.log(typeof str);
```

> | 数据类型            | 值                                           | 情况 | typeof    |
> | ------------------- | -------------------------------------------- | ---- | --------- |
> | undefined           | undefined                                    |      | undefined |
> | null                | null，空占位符                               |      | object    |
> | boolean 布尔型      | true/false                                   |      | boolean   |
> | string     字符串型 | 带引号“ ”  ‘ ’                               |      | 字符串    |
> | number              | 整数、小数、八进制、十进制、十六进制、特殊值 |      | number    |
> | object              |                                              |      |           |

## 八、运算符：

> 表达式：能够求值的语句

### 算术运算符：

`+ - * / %   ++var  var++  --var  var--`

`+`:

- 操作数都是数值型进行四则运算
- 操作数中包含字符串，进行拼接

`++var  var++`

- ++var:先算++；再执行本行中的其他语句
- var++：先执行本行中的其他语句，再执行++;

### 关系运算符：

> 返回值为布尔值  true flase

`>  <  >=  <=  ==  ===  !=  !==`

- 如果两个操作数都是字符串(数字型字符串)，按照ASCII进行比较大小；
- 如果两个操作数都是数字，直接比大小。
- 如果有一个操作数是布尔值，则在比较相等性之前先将其转换为数值——false转换为0，而true转换为1
- 如果一个操作数是字符串，另一个操作数是数值，在比较相等性之前先将字符串转换为数值
- 如果一个操作数是对象，另一个操作数不是，则调用对象的valueOf()方法，用得到的基本类型值按照前面的规则进行比较，如果对象没有valueOf()方法，则调用 toString()
- `==`:先转化，再比较
- `===`:仅比较，不转化
- `undefined==null`

### 赋值运算符：

`=  +=  -=  *=  /=   %=`

```js
var num=5;
num+=10;    //num=num+10
```

### 逻辑运算符：

> 测量值与变量之间的逻辑关系
>
> 0、false、undefined、null  NaN  ""  为false

- &&  与
- ||    或
- ！    非    取反

#### 逻辑运算符的真值表

| A     | B     | A&&B  | A\|\|B | !A    |
| ----- | ----- | ----- | ------ | ----- |
| true  | true  | true  | true   | false |
| true  | flase | flase | tue    | false |
| false | true  | false | true   | true  |
| false | false | false | false  | true  |

返回值：

- &&

> 同真为真，返回第一个假值

- ||

> 同假为假，返回第一个真值

- ！

> 取反 ，返回值为 true/false

### 三元运算符：

```js
表达式？语句1：语句2；
```

> 如果表达示结果为真，执行语句1，如果表达1式结果为假，执行语句2；
>
> ```
> confirm  在页面弹出提示框
> ```

## 九、流程控制

> 代码按照指定条件的顺序执行

- 顺序结构
- 分支结构
- 循环结构

### 顺序结构：

> 语句按照指定条件的执行顺序

### 分支结构:

> 当条件成立时执行响应的语句

- 单分支结构

```js
if(条件){
    条件成立时，执行的语句
}
```

- 双分支结构

```js
if(条件){
    条件成立时，执行的语句
}
else{
    条件不成立时，执行的语句
}
```

- 多分支结构

```js
if(条件1){
    条件1成立时，执行的语句
}
else if(条件2){
        条件1不成立，但是条件2成立时执行的语句
 }
else if(){
    
}
else{
    以上条件都不成立时，执行的语句
}
```

- 嵌套分支

```js
if(){
   if(){}else{}
}
   else{
   
   }
```

switch

```js
switch(表达示){
        case 值1：语句1；break；
        case 值2：语句2；break；
        。。。
        default:语句；
}
```

## 十、循环结构

> 单当满足条件时，重复不断的执行一段代码。

### for循环：明确知道次数

```js
for(初始条件；终止条件；步进值){
    循环体；
}
```

执行顺序:

- 初始条件
- 终止条件
- 循环体
- 步进值
- 重复以上2,3,4步，直到不能满足终止条件，跳出循环;

### while循环：

```js
while(条件){
    当满足条件时，执行的语句；
}
```

### do while循环：

```js
do{
    循环体；
}while(条件)
```

### 循环终止：

`break`:终止所有循环

`continue`:终止本次循环,如果后面的语句仍满足条件，继续执行。

## 十一、数学方法：

- Math.pow(x,y)         x的y次幂
- Math.random()       产生0-1的随机数
- Math.floor()             向下取整
- Math.ceil()               向上取整
- Math.round()          四舍五入取整

## 十二、数组：

> 按照顺序排列的一组相关数据。每一个数组元素都有特定的键名(下标)。

### 初始化数组元素：

- 先声明后赋值 `var  arr=[]; arr[0]="a" arr[1]="3";`

- 声明的同时赋值   `var arr=[1,2,3,4];`

### 数组的下标：

> 访问数组元素。

### 数组的长度：

`arr.length`

清空数组：`arr.length=0`

#### 注意事项：

- 默认值为undefined;
- 数组长度是可变的;
- 数组元素可以是任意数据类型;

### 遍历数组元素：

- 用for循环遍历数组

```js
for(var i=0;i<arr.length;i++){
    arr[i]
}
```

- 用 for  in 遍历数组

```js
for(var i in arr){
    i;下标
    arr[i];元素
}
```

### 二维数组：

#### 访问：`arr[i][j]`

#### 遍历：

```js
for(var i=0;i<arr.length;i++){
    for(var j=0;j<arr[i].length;j++){
        arr[i][j]
    }
}
```

## 十三、函数

> 把实现某一特定功能的代码块封装起来，并且能够重复调用。

- 函数本身
- 是一个对象
- 构造函数（类）

### 定义函数：

- 基本语法(function关键字)

```js
function functionName([形参1],[形参2],...){
    函数体；
    [return 返回值];
}
```

- 字面量，自变量

```js
var variable=funciton(){
    函数体；
}
variable()
```

> 用字面量声明的函数必须要先声明后调用，用关键字function声明的函数，可以在声明前也可以在声明后（预解析）。

- 对象的方式





### 函数的调用：

- 函数名()

```json
functionName()
```

- 自变量+()

### 参数：

> 动态改变函数体的变量，是函数更加灵活。

- 形参：

> 定义函数时写在括号中的变量，形参的作用是接收实参

- 实参：

> 函数调用时写在括号中的值，实参的作用是给形参传值。

#### 参数的传递：

- 参数可以是任意的数据类型
- 参数的传递是按照顺序传递
- 形参=实参：一一对应传递
- 形参>实参：多余的形参赋值为undefined
- 形参<实参：实参由`argunments`对象来接收

#### arguments对象：

- 用来接收参数的详细信息
- 每声明一个函数，在其内部自动生成arguments对象，arguments对象只在函数内部起作用；
- argunments[i]      argunments.length      遍历  类似数组但不是数组

### 返回值：return

- 返回值可以是任意的数据类型
- return  终止函数  return语句后面的代码不执行
- 一个函数内部可以有多条return分支语句，但最终只执行一条return语句；
- 如果一个函数没有返回值，返回undefined

### 作用域：

> 变量起作用的范围

- 全局作用域   

- 局部作用域

- 块级作用域

#### 全局作用域：

> 在整个js代码中，都能访问的变量，凡是修改，变量的值就会改变

- 在函数外部用`var`声明的变量，拥有全局作用域
- 不用`var`声明，但赋值的变量，拥有全局作用域

#### 局部作用域：

- 形参是局部变量，拥有局部作用域
- 在函数内部用`var`关键字声明的变量，拥有局部作用域

#### let:

- 声明变量，用法和`var`一样；
- 识别块级作用域，var不识别
- 不能重复声明变量，不存在变量提升（先访问后声明）

#### const:

- 声明常量，一旦声明。不能被改变
- 声明变量的同时赋值，否则会报错
- 可以识别块级作用域
- 不能重复声明
- 不存在变量提升

### 回调函数

形参高阶函数

返回值高阶函数

### 内置顶层函数：

> 内置：ECMAscript自带的函数，只要知道如何使用，不用关心如何封装
>
> 顶层：在代码中任意位置均能使用

- escape():  

> 将输入的字符串进行编码

- unescape()

> 将编码的字符串就行解码

- Boolean()

> 将其余数据类型转化为布尔型
>
> 0 undefined null NaN false ""

- String()

> 将任意数据类型转化成字符串型

- Number()
  - null->0     ""->0     "  "->0
  - flase->0   true->1
  - undefined->NaN
  - 进制数转化为十进制
  - 去掉没有意义的后导0
  - 字符串：规范的浮点数，数值型字符串

- parseInt()

> 将字符串转化为整数
>
> 第一个字母是数字（+，-，空格 ）转化不成功，转化为NaN

- parseFloat()

> 将字符串转化为浮点型
>
> 只能转化规范的浮点数，如果不成功，返回NaN

- isNaN

> 判断值是否能够转化为数值型，能转化为数值型返回false,不能转化为数值型返回true

#### 数据类型转化：

- 强制类型转化
- 隐式数据类型转换：算术运算符  逻辑运算符  条件if()  while()

### 箭头函数：

```js
let aa=(item)=>{
    console.log(123)
    console.log(456)
    console.log(item,"item")
}
aa(小白)
```

## 十四、对象：

### 概念：

- 类：一群具有相同特征对象集合的描述
- 对象：具体存在的对象个体
- 属性：对对象基本信息的描述
- 方法：对象功能的描述

### 定义对象：

- 构造函数（类），实例化对象

```json
function Computer(color){
    this.color=color;
    this.play=function(){
        console.log("上网")
    }
}
let ASUS=new Computer
    
```

- json(没有面向对象的特质，js独有的一种存储数据的对象)

```js
let asus=
    {
        属性名：属性值，
        属性名：属性值，
        方法名：function(){
    },
    }
```



- class定义类，实例化对象

```javascript

```



### 属性：

> 对象.属性名=属性值

### 方法：

> 对象.方法名=函数

### 增删改查：

- 增加：对象.属性名=属性值
- 删除：delete  对象.属性名
- 修改：对象.属性名=属性值
- 访问：对象.属性名         对象['属性名']     对象.方法

### 遍历：

```js
for(let i in apple){
    
    i;//属性名
    apple[i];//属性值
}
```

### constructor:

对象的属性，返回该对象的构造函数。

### instanceof:

`对象 instanceof 构造函数` 判断函数是否是对象的构造函数，是返回true,否返回false   



## 十五、字符串方法:

### 查找对应字符以及字符编码

```js
 let str =new string("山西农业大学")
    str.chatAt(0)      //访问字符串中第几个的元素
    str.charCodeAt(b)     //第几个元素的编码
    string.fromCharCodeAt()   //类上的方法   括号里填字符编码
```

### 查找下标

```js
	str.indexOf()     //从前往后查找对应字符的下标。如果有返回下标，如果没有返回-1
    str.lastIndexOf()  //从后往前查找对应字符的下标。如果有返回下标，如果没有返回-1
    str.search()   //查找对应字符的下标。如果有返回下标，如果没有返回-1   可以使用正则·
    str.match()   //返回一个数组，  所查的字   下标    所在数组      如果没有返回null
```

### 字符串的截取

```js
    str.substr("star,[length]")     //从star开始截取，长度为length
    str.substring("star,end")     //从star开始截取，到end结束，不会截取到end
    str.slice(star,end)   //从star开始截取，到end结束，不会截取到end
```

### 字符串大小写转换

```js
 let str1="ancEfGh"
 str1.toLowerCase()   //转化为小写
 str1.toUpperCase()   //转化为大写
```

### 字符串的替换

```js
let str="山西";
str.replace("山"，"陕");
```

### 字符串转化为数组

```js
let str="1,2,3,4,5"
arr=str.split(",")
```

## 十六、数组的方法：

### 增加删除：

```js
let arr=[1,2,3,4,5]
arr.push()     //在数组最后插入内容
arr.pop()      //删除数组最后一位
arr.unshift()  //在数组之前插入
arr.shift()    //在数组之前删除一位
arr.splice(3,4,"gour")  //在下标为3的位置删除，删除长度为4，在删除的位置添加gour
arr.includes(5)  //判断是否包含某个数
```

### 截取：

```js
arr.slice(star,end)
```

### 连接多个数组：

```js
newarr=arr.concat()
```

### 取反：

```js
arr.reverse()
```

### 数组转化为字符串：

```js
arr.join("-")
```

### 排序：

```js
let arr=[1,2,3,0,4,5,6,7,9,8,4];
arr.sort((x,y)=>y-x)
console.log(arr)
```

### 查找

> 返回第一个满足条件的元素

```js
 let arr=[1,2,3,0,4,5,6,7,9,8,4];
 let num=arr.find(item=>item%2==0)
 console.log(num)
```

### arr.some()

> 判断是否满足条件(有就可以),返回值为boolean

```js
 let bb=arr.some(item=>item>10);
 console.log(bb)
```

### arr.every()

> 判断每个元素是否满足某种条件,返回值为boolean

```js
let cc=arr.every(item=>item>6);
console.log(cc)
```

### arr.filter()

> 筛选或过滤

```js
 let dd=arr.filter(item=>item>6);
 console.log(dd)
```

### arr.forEach()

> 让数组中每一个元素都执行一个函数，不会影响原数组

### arr.map()

> 让数组中每一个元素都执行一个函数，	返回一个新数组

## 十七、节点：

### 节点的分类

- 文档节点
- 元素节点
- 属性节点
- 文本节点
- 注释节点

|          | nodeName     | nodeValue | nodeType |
| -------- | ------------ | --------- | -------- |
| 文档节点 | #document    | null      | 9        |
| 元素节点 | 大写的标签名 | null      | 1        |
| 属性节点 | 大写的属性名 | 属性值    | 2        |
| 文本节点 | #text        | 文本      | 3        |
| 注释节点 | comment      | 注释内容  | 8        |

### 节点的获取属性：

>  childNodes     子节点
>
> parentNodes   父节点
>
> previousSibling   上一个兄弟节点
>
> nextSiblling         下一个兄弟节点
>
> previousElementSibling    上一个兄弟元素节点
>
> nextElementSibling    下一个兄弟元素节点

### 节点的方法：

#### 创建节点

```js
let div =document.createElement("div")
```

```js
//创建文本节点
let text1=document.createTextNode("这是span标签")
span.appendChild(text1)
```

```js
//创建注释节点
let comment1=document.createComment("这是注释节点")
box.appendChild(comment1)
```

#### 插入节点

```js
//在最后插入节点
let box=document.querySelector(".box")
box.appendChild("div")
```

```js
//在之前插入节点  inserBefore(要插入的元素，插入位置之后的元素)
let sapn=document.createElement("span")
box.inserBofore(span,div)
```

#### 属性节点

```js
//创建属性节点
let attr=document.createAttribute("id")
attr.nodeValue="box"
//设置属性节点
box.setAttributeNode(attr)
```

#### 删除节点：

```js
//删除标签节点
box.removeChild("div")
//删除属性节点
box.removeAttribute("id")
```

## 十八、事件

### 事件添加方式：

- 节点：onclick=function()
- 节点.addEventListener("事件"，事件处理程序，事件类型)

### 事件构成：

事件源：谁去触发事件，谁就是事件源；

事件：

事件处理程序:

事件对象：用来保存事件触发时的信息

>  w3c：事件处理程序的形参中

>  ie：window.event

```js
//解决兼容问题
box.onmouseenter=function(e){
    let event=e || window.event
}
```



### 常用事件:

#### web端：

##### 鼠标事件：

- onclick                              单击
- ondblclick                         双击
- onmousedown                按下
- onmouseup                     抬起
- onmousemove                鼠标移动
- onmouseover                  移入
- onmouseout                    移出
- onmouseenter                 移入
- onmouseleave                 移出  
- oncontextmenu               右击

```js
document.oncontextmenu=function(e){
    e.preventDefault();        //阻止浏览器默认行为
}
```

##### 鼠标滚轮事件：onmousewheel

```js
box.onmousewheel=function(){
    console.log(123)
}
```



##### 鼠标事件对象常用的属性：

clientX:距离浏览器的X偏移

clientY:距离浏览器的Y偏移

offsetX:距离事件源的X偏移

offsetY：距离事件源的Y偏移

screenX:距离屏幕的X偏移

screenY:距离屏幕的Y偏移

##### 键盘事件：

onkeydown    键盘按下

onkeyup         键盘抬起

onkeypress    键盘按下（按下功能键ctrl  shift delete esc等不会触发）

##### 键盘事件对象常用属性：

keyCode:   键盘码

ctrlKey    是否按下crtl

shiftKey   是否按下shift

altKey    是否按下alt

key         键盘名

##### 表单事件：

oninput   输入

onchange     内容发生改变，并且失去焦点

onblur       失去焦点

onfocus     获得焦点

onsubmit     提交表单

onselect      文本选中

##### 窗口事件：

##### 事件流：

当触发一个事件时，由这个事件的容器到整个文档都会按照特定的顺序进行依次触发；

##### 事件的分类：

捕获型事件：true    从不具体的事件源到具体的事件源;

冒泡型事件：false   从具体的事件源到不具体的事件源；

##### 阻止事件流：

event.stopPropagation()

```js
//解决兼容问题
let event=event || window.event
event.stopPropagation();  //w3c
event.returnValue=true;   //IE
```

##### 事件委派：

```js
event.target     //目标事件源
```

#### 移动端事件：

- ontouchstart     按下
- ontouchmove   移动
- ontouchend      抬起

## 十九、日期对象

### 获取当前时间

```js
let ay=new Date("2018/8/8 12:00:00")
let ay1=new Date("12:00:00 2018/8/8")
let ay2=new Date("2018/8/8")  //月份从0开始   0-11
```

### 设置时间

```js
//获取格林尼治时间
let now=new Date()
now.setFullYear(2020)  //设置年份
now.setMonth(5)  //设置月份
now.setDate(26)  //设置日期
now.setHours()  //设置小时
now.setMinutes()  //设置分钟
now.setSeconds()  //设置秒数
now.setMillliseconds()  //设置毫秒
//获取世界协调时
let now=new Date()
now.setUTCFullYear(2020)  //设置年份
now.setUTCMonth(5)  //设置月份
now.setUTCDate(26)  //设置日期
now.setUTCHours()  //设置小时
now.setUTCMinutes()  //设置分钟
now.setUTCSeconds()  //设置秒数
now.SetUTCMillliseconds()  //设置毫秒
```

### 获取时间

```js
let now=new Date()
now.getFullYear()  //获取当前年份
now.getMonth()  //获取当前月份
now.getDate()  //获取当前日期
now.getHours()  //设置小时
now.getMinutes()  //设置分钟
now.getSeconds()  //设置秒数
now.getMillliseconds()  //设置毫秒
now.getTime()    //当前时间到1970年1月1日00:00
```

## 二十、正则

>  正则就是用来描述或者匹配一系列规则的字符串

### 作用：

- 数据验证
- 内容检索
- 内容替换
- 内容过滤

### 创建正则对象：

- 通过实例化对象

```js
let red=new RegExp("正则表达式"，"模式修正符")   ``
let red=new RegExp("uek"，"g")  
//模式修正符      g全局    i不区分大小写      m换行
```

- 通过字面量的方式

```js
let reg=//         //代表定界符，里面写正则表达式，外面写模式修正符
```



### 正则表达式常用方法:

- test(str)   检测正则对象是否匹配str   返回值     true|| false
- exec(str)   检测正则对象是否能够匹配str   返回值    如果能匹配，返回一个拥有特定属性的数组，  如果不能匹配  返回null

### 正则表达式：

- 原子：正则表达式中最小的规则，只返回一个

```js
\d   匹配0-9
\w   匹配任意的数字 字母 下划线
\s   空白  \n  \r   \f
\D   除了0-9以外的字符
\W   除了数字，字母，下划线以外的字符
\S   除了空白以外的字符
```

- 原子表，[]只返回一个

```js
[a-c]   a-c
```

- 元字符

```js
.   所有字符
|   或
```

- 原子组()

> 默认存储到内存中，可以使用\1  \2等方式来引用
>
> (?:) 可以使原子组不在内存中存储，不可以引用

```js
//第一种用法
let str1="山西优逸客"
let str2="陕西优逸客"
let reg=/(山西|陕西)优逸客/g
//第二种用法    (?:)=>找不见
原子组可以用于存储
let str="<div>div</div>";
let reg=/<(div)>\1<\/\1>/g
```

### 正则中的数量

```js
*  0个或多个    >=0
+  一个或多个   >=1
?  0个或1个
//贪婪
{11}  11个
{15,18}    15到18个
{6，}   至少6个
//吝啬
//边界判断
^  开始
$  结束
\b   单词边界
\B   非单词边界
```

### 使用场景：

- 正则对象
- str.split("正则表达式")
- str.replace(正则对象、替换的内容)
- str.search(正则表达式)