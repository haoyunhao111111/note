## jQuery

>  本质：javascript  框架
>
> 宗旨：  write  Less,do More
>
> 作用：优化js的操作、dom操作、页面交互效果、事件、Ajax、动效
>
> 特性：隐式循环，链式调用

### jQuery核心函数

- 传入选择器：返回jQuery对象

```js
jQuery(".box")
```

- 传入函数：给document    添加  ready 事件  

```js
jQuery("document").ready(function(){})==jquery(function（）{})==jQuery().ready(function(){})
```

- 传入dom对象：返回jQuery对象
- 传入字符串： "<div></div>"  创建新节点    appendTo

### jQuery常用方法：

- .css("样式属性","样式值")

```js
//单个样式
$(".box").css("background-color","blue")
//批量样式
$(".box").css({
        backgroundColor:"blue",
        borderRadius:"50%"
    })
```

#### 筛选的方法：

- .eq(index)   返回对应下标的jQuery对象
- .get(index)   返回对应下标的DOM对象
- .hasClass("类名")   判断jQuery数组中是否有一个类名为***对象；  返回值为bool
- .filter([选择器]，[元素]，[函数])   筛选出符合条件的对象
- .is("选择器)   判断是否为某个对象,
- .map(fn)  生成一个新的数组或集合
- .has("选择器“)   返回一个选中的jquery对象、
- .not("选择器")   从jQuery 数组中删除选中的元素。
- .slice(start,[end])  截取指定位置的jquery对象
- .each(index,item)   遍历jQuery数组，index在前，item在后
- .index()  返回jQuery 对象在数组中的下标

#### 操作属性的方法：

- attr()

- removeAttr()
- prop()
- removeProp()

#### 操作类名的方法：

- addClass()    增加类名
- removeClass()   移出类名
- toggleClass()    切换类名

#### 操作内容的方法：

- .text()
- .html()
- .val()       表单

#### jQuery对象元素的位置信息

- .offset()     返回一个位置信息的对象 {left:**,top:**}  相对于浏览器的位置
- .position()     返回一个位置信息的对象 {left:**,top:**}  相对于定位的祖先元素的位置
- .scrollTop()     滚动条的高度
- .scrollLeft()

#### 常用方法：

- findIndex:获取第一个符合条件的下标
- toArray():将jQuery对象转化为原生数组对象

#### 事件对象：

- e.offsetX
- e.offsetY
- e.pageX
- e.pageY
- e.target
- e.currentTarget      ==this
- e.stopPropagetion()
- e.preventDefault()

#### 事件源：

- one()
- on()
- trigger()   自动触发事件
- triggerHander    自动触发事件，并且清除浏览器默认行为

