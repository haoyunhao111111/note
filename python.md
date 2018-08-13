## python

### 输出：print()

单个输出，多个输出，表达式

格式化打印    %d（整数）  %f（浮点数）  %s（字符串）

print("str",end="str")

### 变量：

没有声明符

不需要声明

由数字 字母 下划线组成     不能使用$符号   不能以数字开头  区分大小写

不支持自增，自减   a+=1

不可以使关键字，保留字

#### 数据类型：

### 数字   

- 整数（二进制  0b    八进制  0o    十六进制 0x   科学计数法8e2）

- 浮点数

- 复数    

#### 浮点数，整数的转化：float()   int()

#### 将十进制转化为二进制 八进制  十六进制：bin()     oct()      hex()				

### 字符串:不可变量

#### 内建函数：

- string.capitalize()    字符串的第一个字符大写
- str.lower()    字符串小写
- str.upper()   字符串大写
- str.center(扩充后的长度，扩充的内容)   str在中间
- str.ljust(扩充后的长度，扩充的内容)   str在左边
- str.rjust(扩充后的长度，扩充的内容)   str在右边
- string.count("str",start,end)  从start到end间str出现的次数
- str.encode(encoding="utf-8",errors="ignore")   编码
- str.decode(encoding="utf-8",errors="ignore")   解码
- str.endswith()     是否是以某一字符结尾   返回值为bool
- str.find("a",start,end)  从start到end之前查找a   找到返回 下标，找不到返回-1     左->右
-  str.rfind("a",start,end)  从start到end之前查找a   找到返回 下标，找不到返回-1    右->左
- str.index("a",start,end)  从start到end之前查找a   找到返回 下标，找不到报错    左->右
-  str.rindex("a",start,end)  从start到end之前查找a   找到返回 下标，找不到报错    右->左
- str.isalnum()   不为空  且所有字符都是数字  字母    返回值为  bool
- str.isalpha()   不为空  且所有字符都是字母  
- str.isdecima()  是否字符都是十进制的数字
- str.isdigit()  是否字符都是数字
- str.islower()   是否都是小写
- str.isupper()   是否都是大写
- str.isspace()  至少有一个字符str是否全为空    返回值为bool
- str.join(seq)   将列表对象用str进行分割组合成字符串
- str.split("，",num)   将str通过“,”进行分割，num指定分割次数
- str.spiltlines()   将str通过\n进行分割
- str.strip(["str"])    在字符串前后删除空格，或者删除str

#### 定义方式：

- 单引号  '''str'''
- 双引号 “”“ str"""

#### 转义字符：

- r   之后写的为普通字符   \n  \r  \t
- b  后面的字符串是byte (二进制)  在python2中  print()函数操作的全部为byte型数据 在 python3中是Unicode数据
- u  为了python2兼容到python3

### 列表

>  mylist=[1,2,3,4,5]

#### 注意：

- 列表可以保存惹你类型数据
- 列表可以使用切片
- 列表是可变的，字符串不可变
- 可以创建空列表，也可以创建只有一个元素的列表
- 可以创建多维列表

#### 内建函数：

- arr.append(“a”)   在列表最后插入元素

- arr.insert(index,"a")  在任意位置插入元素,如果没有index默认最后插入
- list.extend(list1)   将两个列表进行合并

```python
arr+[4,5,6]+[7,8,9]   #合并多个
```

- list.pop()   删除最后一个元素
- list.count()   查看某元素在list 的次数
- list.index()  查看某元素在list中的第一个下标，如果不存在就报异常
- list.remove(item)  删除list中的item，有相同的删除第一个
- list.reverse()   反转list
- list.sort(reverse=True)   排序   默认升序，reverse=True    降序
- list.copy()  浅拷贝
- list.clear()  清空数组
- 

### 元组 

> mytuple=(1,2,3,4)

#### 注意：

- 元组和列表相似，区别就是元组不能改变

```python
mytuple=([1,2],[3,4])
mytuple[0][0]="a"
```

- 元组通过圆括号定义
- 可以使用切片
- 元组可以定义只有一个元素的元组，mytuple=(1,)，逗号不能少
- 空元组

#### 操作list/tuple的内建函数：

- len(list)   数组的最大长度
- max()   数组的最大值
- min()   数组的最小值
- list()   将元组转换为列表
- tuple()  将列表转换为元组
- enumerate()   返回下标和元素

### 字典：

#### 创建方式

- json格式

> mydict={1:"a",2:"b",3:"c"}

- 通过内建函数

> mydict=dict(name="小红"，age="10")

- 通过映射函数

> mydict=dict(zip["a","b"],[1,2])

- 可迭代对象方式

> mydict=dict([("a","b"),(1,2)])

- 批量创建

> mydict=dict.fromkeys([1,2,2,3],"a")

#### 访问方式：

mydict[键]

#### 删除字典和属性:

del ,mydict["name"]

#### 内建函数：

- dict.get("key","info")  返回key对应的value    没有为None   info指定没找到的
- dict.keys()    返回字典中所有的key
- dict.values()  返回字典中的所有value
- dict.itemd()   返回字典中所有的key:value形式的数据
- dict.setdefault(key,value)    添加数据
- dict.pop(key)   删除key
- dict.popitem()   删除最后一位的key:value
- dict.clear()    清空dict

### 集合

布尔值

空

### 切片

str[start: end: step]   step默认为1  可以为负数；

### 循环：

##### for

```python
mylist=[1,2,3,4,5]
for item in mylist:
    print(item,end="   ")
    print(mylist.index(item))
```

##### enumerate()

> 将列表转换为下标和值的序列

```py
for i,v in enumerate(mylist)
```

### 浅拷贝与深拷贝：

```python
import copy
copy.copy(arr)   浅拷贝
copy.deepcopy(arr)  深拷贝
```

