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
- str.isalpha()    不为空  且所有字符都是字母  
- str.isdecima() 是否字符都是十进制的数字
- str.isdigit()      是否字符都是数字
- str.islower()    是否都是小写
- str.isupper()   是否都是大写
- str.isspace()   至少有一个字符，str是否全为空    返回值为bool
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

- 列表可以保存任意类型数据
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
- list.clear()  清空列表

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
- dict.items()   返回字典中所有的key:value形式的数据
- dict.setdefault(key,value)    添加数据
- dict.pop(key)   删除key
- dict.popitem()   删除最后一位的key:value
- dict.clear()    清空dict

### 集合

> 唯一的，不可变的对象的一种无序集合·，一个项只能出现一次

#### 集合的添加：

- add("abc")         添加数据
- update("abc")   添加集合

#### 删除：

- myset.remove()

#### 集合的操作：

- 差集：-    
- 并集：|
- 交集：&

### 布尔值

True  False 

### 空

None

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

## 运算符：

### 算数运算符：

#### 基本算数运算符

> + - *  /    

##### 注意：

- python3中除法无论有无复杂类型，结果精确到浮点数
- +
  - 操作两个数字型数据=>加法运算
  - 操作一个数字型数据=>正数
  - 操作的str  list  tuple  起到连接作用
- -减法运算和负数
- *
  - 操作两个数字型数据=>乘法运算
  - 操作的str list tuple=>重复

#### 复杂算数运算符

> %  取余         //向下取整    **幂运算

### 逻辑运算符

>  and  与         or或                not 非

### 关系运算符

- ==  等于  比较对象是否相等
- !=   不等于   比较两个对象是否不相等

### 位运算符

- &  按位与 :参加运算的两个值，如果两个相应位都为1，则该位的结果位为1·，否则为0；
- |  按位或 :参加运算的两个值，如果两个相应位有一个为1，则该位的结果位为·1，否则为0；
- ^  按位异或：当两个对应的二进制相异时，结果为1
- ~ 按位取反：对数据的每个二进制位取反，即1->0,0->1
- <<  左移运算符：运算符的二进制位全部左移若干位,由<<右边的数字指定了移动的位数，高位丢弃，低位补0
- .>>右移运算符：运算符的二进制位全部右移若干位,由>>右边的数字指定了移动的位数,高位丢弃，低位补0

### 赋值运算符：

> =  +=  -=  *=  /=  &=  **=  //=

### 成员运算符

- in   如果在指定序列中找到值返回True ,否则返回False
- not in    如果在指定序列中没有找到值返回True ,否则返回False

### 身份运算符

-  is  按照地址判断两个标识符是否相等
- is not

### 运算符优先级

> 幂运算>正负>算数运算符>关系运算符>赋值运算符>身份>成员>逻辑

## 流程控制

### 选择结构：

```python
if 1>2:
    print("1>2")
elif 1=2:
    print("1=2")
else
	print("1<2")
```

#### 三元表达式

```python
结果1 if 表达式 else 结果2
```

### 循环结构

range(start,end,step)                start->开始下标    end->结束下标         step->步进值

在循环里，干预循环的语句：

continue:结束本次循环，继续下次循环

break:终止整个循环

## 函数

> 将完成某一特定功能的代码集合起来，可以重复使用这些代码块

```python
def add(a,b):
    return a+b
print(add(45,7))
```

### 参数

> 必选参数>默认参数>可变参数>关键字参数

#### 可变参数：

在参数前面加*，数据类型为元组

```python
def add(*arr):
    num=0
    for i in arr:
        num+=i
    print(num)
add(1,2,3,4,5,6,6)
```

#### 关键字参数：

在参数前面加**

```python
def fn(name,age,**arr):
    print("name:%s"%name)
    print("age:%s"%age)
    print(arr)
fn("xb",18,tel=12345678,sex="男")
```

### 返回值

#### 注意：

- return后续代码不会被执行
- 之内返回一次
- 要返回多个数据，整体返回

### 高阶函数：

### 特殊函数：

#### 匿名函数：

```python
lambda 参数:表达式(只能写一行)
参数可以有多个；
表达式不需要return,自动return;
num=(lambda a,b:a+b)(1,2)       ##自调用
print(num)
fn=lambda a,b:a+b               ##字面量
fn(1,2)
```

##### 使用场合:map reduce filter

map(函数，序列)   

```python
arr=map(lambda x:x*2,range(1,11))
print(list(arr))

arr=map(lambda x,y:x*y,range(1,11),range(1,11))
print(list(arr))
```

filter(函数，序列)

```python
arr=filter(lambda x:x>4,range(1,11))
print(list(arr))
```

reduce(函数，序列)

```python
import functools
arr=functools.reduce(lambda x,y:x+y,range(1,11))
print(arr)

x:不是序列中的某一项，是表达式的结果
函数返回的是值，不是序列
```

#### 闭包函数

> 在函数中，可以（嵌套）定义另一个函数时，如果内部的函数引用了外部的函数变量，则可能产生闭包，闭包可以用来在一个函数与一组“私有”变量之间创造关联关系，在给定函数被多次调用的过程中，这些私有变量能够保持其持久性

```python
def fn():
    x=4
    action=lambda n:x**n
    return action
x=fn()
print(x(2))
```

### 递归函数：

> 如果一个函数在内部不调用其他函数，而是调用自己本身的话，这种函数就是递归函数

### 局部变量和全局变量

global  告诉python准备生成一个或多个全局变量名    先声明后使用，不能声明的同时使用

nonlocal   

### 装饰器

>  给某程序增添功能

#### 三个原则

1. 不能修改被装饰的函数的源代码
2. 不能修改被装饰函数的调用方式
3. 满足1、2的情况下增添新功能

#### 定义公式

> <函数+实参高阶函数+返回值高阶函数+嵌套函数+语法糖=装饰器>

```python
import time
def aa(fn):
    def bb():
        start=time.time()
        fn()
        end=time.time()
        print("程序运行时间：",end-start)
    return bb
def test():
    time.sleep(1)
    print("skjgareiu")
test=aa(test)
test()
```

#### 函数的柯里化:

```python
def cc(a):
    def dd(b):
        print(a+b)
    return dd
cc(4)(5)hanshudehanshuhanshudekellliluhua
```

