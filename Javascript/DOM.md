# DOM(文档对象模型)

## 获取元素：

- 获取ID名的元素

```js
let box=document.getElementById("idname")    box:变量名     idname:ID名
//返回值为类数组的集合
```

- 获取类名的元素  集合

```js
let obj=document.getElementByClassName("classname");
```

- 获取标签名的元素   集合  下标   遍历

```js
let obj=document.getElementByTagName("tagname")
```

- 获取选择器选中的第一个元素

```js
let obj=document.querySelector("选择器")
```

- 获取选择器选中的集合  下标   forEach

```js
let obj=document.querySelectorAll("选择器")
```

## 操作属性：

### 标准属性：obj.attr

### 自定义属性：

- 获取：obj.getAttribute(name)
- 设置：obj.setAttribute(name,value)

## 操作样式：

### 获取样式的方式：

- 行内样式：obj.style.attr
- css样式：getComputedStyle(obj,null).attr

### 设置：

- 行内样式：

```js
obj.style.属性名=属性值；
```

- 批量样式：

```js
obj.className="box" 
obj.classList.add("box")      添加类
obj.classList.remove("box")   删除类
obj.classList.toggle("box")   切换类
obj.id="box"
```



## 操作内容：

- innerText
- innerHTML:识别标签对

## 元素的尺寸和位置

- obj.offsetWidth:   获取元素的真实宽度（width+padding+border）

- obj.offsetHeight: 获取元素的真实高度 （width+padding+border）

- obj.offsetTop:获取当前元素的外边框到距有定位属性的父元素的内边框的距离。

- obj.offsetLeft:获取当前元素的外边框到距有定位属性的父元素的内边框的距离。

- ##### obj.scrollTop:有滚动条的元素，浏览器滚动时在垂直方向的拉动距离

```js
document.body.scrollTop || document.documentElement.scrollTop     兼容
```

- ##### obj.scrollLeft:有滚动条的元素，浏览器滚动时在水平方向的拉动距离

```js
document.body.scrollLeft || document.documentElement.scrollLeft     兼容
```



### 动态创建元素：

```js
document.creatElement('TagName')
```

插入到页面：

```js
父元素.appendChild(子元素)
document.body.appendChild(div)
```

