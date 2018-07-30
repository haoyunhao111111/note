# 页面重构（html & css）

## 一、定义：

- html:超文本标记语言
- css:层叠样式表

## 二、html语法：

1、单标签

​	<标签名>   只有开始标签称之为单标签

2、双标签

​	<标签名>  </标签名>  有开始标签也有结束标签的称之为双标签

### 三、属性的语法：

​	语法：

​		属性名="属性值"

​		属性名="属性值1 属性值2"

​	注意：

​	1、	标签名和属性名之间要有空格

​	2、多个属性之间要有空格

​	3、多个属性值之间要有空格

### 四、路径：

​	绝对路径：从盘符开始一条完整的路径

​	相对路径：两个文件的位置关系

### 五、命名规范

​	1、严格区分大小写

​	2、可以采用字母、数字、下划线、$  （数字不开头）

​	3、命名语义化

​	4、可以采用驼峰命名法

### 六、标签在页面中的效果分类：

​	1、行内元素

​		定义：在一行内显示，不可以设置宽高,只可以设置左右间距，不可以设置上下间距eg:span del i em b 	strong a ....

​	2、块元素

​		定义：可以设置宽高，独占一行。       eg：标题标签(h1-h6) 列表标签(ul>li  \ ol>li \ dl>dt+dd)    段落标签.(p  pre).. div	()

​	3、行内块元素

​		定义：可以设置宽高，在一行内显示     eg：img 表单控件

### 七、元素的转换：

​	转换为块元素：display:block;

​	转换为行内元素： display:inline;

​	转换为行内块元素：display:inline-block;

元素的级别：

块元素>行内块元素>行内元素

### 八、元素嵌套的规范：

1、同一级别可以相互嵌套

2、级别高的元素可以嵌套级别低的元素

3、段落标签只能嵌套行内元素

4、a标签不可以嵌套a标签	

### 九、css样式表的引入方式

1、外链接    

```html
<link rel="stylesheet" href="index.css">
```

2、嵌入式    

```html
<style></style>
```

3、行内样式------------------------------很少使用

```html
<div style="width:200px;height:200px"></div>
```

### 十、布局

第一步：清除默认样式

第二步：划分模块

第三步：设置模块的大小以及位置

第四步：划分下一级模块

#### 移动端布局的步骤：

1. 修改视口

   ```html
   <meta name="viewport"  content="width=device-width">
   ```

2. 引入rem.js

   ```html
   <script src=""></script>
   ```

3. 修改rem.js设计稿的宽度



text-indent---------首行缩进    em为单位  2em--首行缩进2个字符

1em=1*font-size；

### 十一、a标签：

title:标题

target:用来控制新页面打开的位置

​		_self:在本窗口打开

​		_blank:在新窗口打开

### 十二、选择器

#### 选择器：一个能够选择html文档中一个或多个标签的规则

#### （1） 标签选择器：作用选择页面中所有的**标签

​		语法：

​			标签名{

​				样式名：样式值;

​				.......

​				}

#### （2）类名选择器：选择类名为**的标签

​		语法：

​			.类名{

​				样式名：样式值;

​				....

​			      }

#### （3）交叉选择器：

​		语法：

​			div.box{

​				样式名：样式值;

​				....

​			      }

#### （4）群组选择器：选择页面中所有的E1,E2,E3

​		 E1，E2，E3{

​			样式名：样式值;

​				....

​			      }

####  (5) 通用选择器：选择所有的元素

​			*{

​				}

####  (5) 后代选择器：选择E1的后代E2

​			E1 E2{ }

####  (6) ID选择器:id="box"  选择页面中id为box的唯一标签

​                       \#box{

​                              样式值：样式名

​                               ........

​                               }

#### （7）伪类选择器：

​                            E：hover{}----------------选择鼠标移入状态

#### （8）伪结构选择器：

​			E:first-child{}--------------作为第一个孩子的E标签

​			E:first-of-type{}--------------选中作为子元素的同类型的第一个元素

​			E:last-child{}--------------作为最后一个孩子的E标签

​			E:last-of-type{}--------------选中作为子元素的同类型的最后一个元素

​			E:nth-child(n){}-----------作为第n个孩子的E标签

​			E:nth-of-type(n){}----------选中作为子元素的同类型的第n个元素 

​				偶数（even） 

​				奇数（odd）

​				表达式（3n）---选中3的倍数

​			E:nth-last-child(n){}-----------作为倒数第n个孩子的E标签

​			E:nth-last-of-type(n){}----------选中作为子元素的同类型的第n个元素

#### (9)伪元素选择器

::after{}    -----------------在元素内容之前插入元素

::before{}  ----------------在元素内容之后插入一个元素

::after{}  ::brfore{}伪元素content：" "  必须写   

#### （10）相邻兄弟选择器

E1+E2{}：  选择E1的下一个兄弟元素E2

#### （11）子类选择器

E1>E2{}     选择E1的子类元素	

#### （12）属性选择器

1. [attr]{}----------选择所有拥有attr属性的元素
2. [attr="value"]------选择拥有attr属性并且属性值为value的元素
3. E[attr="value"]-----选择拥有attr属性并且属性值为value的E元素
4. E[attr~="value"]-----选择拥有attr属性并且属性值(一个或多个)其中一个属性值为value的E元素
5. E[attr^="v"]-----选择拥有attr属性并且属性值为(一个或多个)其中一个属性值以v开头的E元素
6. E[attr$="v"]-----选择拥有attr属性并且属性值(一个或多个)其中一个属性值以v结尾的E元素
7. E[attr*="v"]-----选择拥有attr属性并且属性值(一个或多个)其中一个属性值包含v的E元素

#### 选择器优先级：宗旨（越具体的优先级越高）

1. id                100
2. class           10
3. 标签名         1

a b c d e 

a------- 行内样式

b------- id选择器

c--------类名选择器  伪类选择器  属性选择器

d--------标签选择器   伪元素选择器

e--------通用选择器

### 十三、盒子模型

#### 盒子模型：四部分组成

1、margin     外间距：盒子与盒子之间的距离

2、border     边框

3、padding    内填充（内间距）边框与内容之间的距离 

4、content    内容

#### margin

​	margin-top(上间距)\margin-right\margin-left\margin-buttom

​	margin:50px---------------------------上右下左都是50

​	margin:50px 100px---------------------上下50   左右100

​	margin :0 auto------------------------上下为0，左右（auto）自动调节

​	margin:50 px 100px 150px--------------上50 左右100 下50

​	margin:50 px 100px 150px 200px--------上 右 下 左（顺时针方向）

#### padding 设置方法同margin

width：auto（默认值）  |百分比|数值

height：auto（默认值） |百分比|数值

width:auto         参照于子元素的宽度           

height:auto       参照于内容的高度    

#### 一个元素实际的宽高为

实际宽度=border-left+padding-left+width+padding-right+border-right

实际高度=border-top+padding-top+height+padding-buttom+border-buttom

#### 盒子模型的问题：

- 大部分元素的margin padding默认为0，但有一些元素的margin padding 不为0  

  ​                                                                       eg:body、 标题标签 、列表标签 、段落标签

- 相邻的两个块元素的margin会重合，值会取最大值。

- margin值可以设置为负数，padding不可以。

- 行内元素margin值只有左右，没有上下。

- 两个发生嵌套关系的元素，如果父元素没有padding值,父元素与子元素之间没有别的内容，此时子元素的margin会作用在父元素上

  - 用父元素的padding值代替margin值(首选)

    父元素{

    ```
    				padding-top:50px;
    
    				box-sizing:border-box
    
    			}
    ```

  - 给父元素添加overflow:hidden;

### 十四、定位

1. 定位的元素脱离文档层，到达定位层（高于浮动层）。

2. 定位的元素会多出5个元素（top right buttom  left z-index(层级)）
   1.相对定位：相对于自身来定位，在文档层中保留原来的位置

   ​	positon:relative;

   2.绝对定位：相当于最近的，定位的，祖先元素来定位，完全脱离文档流。

   ​	position:absolute;

   3.固定定位：相对于浏览器的四条边，完全脱离文档流。

   ​	position:fixed;

   ### 4.top与bottom同时定义哪个样式会作用到元素身上

   top的权重比bottom大

   left权重比right大

   ### 5.定位元素居中方式：

   1. #### 水平居中：

      left:50%;

      margin-left:-100px(自身宽度的一半)

      left:0

      right:0

      margin:0 auto;

   2. #### 垂直居中：

      top：50%；

      margin-top:-100px(自身高度的一半)

      bottom:0

      top:0

      margin:auto 0;

   3. #### 绝对居中：

      left:50%;

      margin-left:-100px(自身宽度的一半)

      top：50%；

      margin-top:-100px(自身高度的一半)

      top:0

      bottom:0

      left:0;

      right:0;

      margin:auto;

### 十五、动画

#### 动画规则：

@keyframes animation1(动画名，任意){

from{

}

to{

}

}

#### 挂载动画：

animation:animation1 1s(动画名，时间)

animation-name:animation1-----------------------动画名称

animation-duration：1s----------------------------时间

animation-timing-function:linnerl-----------------时间函数(匀速)

 animation-delay:1s-----------------------------延迟

animation-iteration-count: 3----------------------旋转3次

animation-direction:alternate----------------------指定下一次动画是否为常规

animation-fill-mode:backwards--------------------返回一开始的状态

​                               forwards-----------------------保持当前状态

animation-play-state:paused-----------------------暂停

​                                 running-----------------------运动

### 十六、flex布局

#### 容器的属性：

- flex-direction:主轴方向

  - row    主轴在水平方向，从左到右；
  - row-reverse   主轴在水平方向，从右到左；
  - column   主轴在垂直方向，从上到下；
  - column-reverse    主轴在垂直方向，从下到上；

- flex-wrap:  决定项目换行

  - wrap  项目换行
  - nowarp  项目不换行（默认值）

- justify-content   决定项目在主轴方向的对齐方式

  - flex-strat   主轴的起点
  - flex-end    主轴的终点
  - center        主轴的中心
  - spac-between  两端对齐
  - space-around   项目的两侧距离相等

- align-items   定义项目在交叉轴上的对齐方式（适用于一根轴线和多跟轴线）

  - flex-start   交叉轴的起点
  - flex-end    交叉轴的终点
  - center       交叉轴的中心
  - baseline  基线对齐（文本底部）

- align-content:定义项目在交叉轴上的对齐方式（适用于多跟轴线）

  - flex-start   交叉轴的起点

  - flex-end    交叉轴的终点

  - center       交叉轴中心

  - space-between   两端对齐

  - space-around    两侧距离相等

    

    #### 项目属性

    - order:定义项目的排列顺序，数值越小越靠前，默认为0；
    - flex-grow:定义项目的放大比例，默认为0，即使存在剩余空间也不放大，
    - flex-shrink:定义项目的缩小比例，默认值为1，空间不足，项目缩小；值为0，空间不足，项目不缩小
    - flex-basis:定义项目占据的主轴空间
    - align-self:定义项目在交叉轴上的对齐方式

    



