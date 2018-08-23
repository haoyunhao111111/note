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
- string.count("str",start,end)  从start到end间string3出现的次数
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

- list.append(“a”)   在列表最后插入元素

- list.insert(index,"a")  在任意位置插入元素,如果找不到index默认最后插入
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

del .mydict["name"]

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

> + - * /

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
- .>>右移运算符： 运算符的二进制位全部右移若干位,由>>右边的数字指定了移动的位数,高位丢弃，低位补0

### 赋值运算符：

> =  +=  -=  *=  /=  %=  **=  //=

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
lambda 参数:表达式
参数可以有多个；
表达式不需要return,自动return;只能写一行
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
cc(4)(5)
```

### 文件操作

#### 读文件：

```python
f=open("filename",mode)
# filaname:文件路径
# mode:操作方式；
```



#### 打开模式：

- r  读操作（默认）
  - read     读取文件
  - read([num])     num代表读取的字符数量，默认为全部；
  - readline()          读取行
  - readline([num])    文件读取每一行,num代表读取本行的字符数量
  - readlines         列表形式的多行，返回值为列表
- rb  以二进制的方式读取文件
- w   写入     会覆盖之前的内容；路径不对会创建新文件
  - write(str)   把str写入文件，在str后不会加换行符；
  - f.flush()     把缓冲区的内容写入硬盘
- a    写入     不会覆盖之前的内容；路径不对会创建新文件
- r+    读写（不会创建新文件，每次读写文件在文件开头）
- w+   读写（创建新文件，会覆盖原内容）
- a+    读写（创建新文件，每次读写追加）

#### 指针：

seek():移动文件读取指针到指定位置

```python
f.seek(p,0)  移动到文件第p个字节处，绝对位置
f.seek(p,1)  移动到相对于当前位置之后的p个字节，文件以二进制的方式打开
f.seek(p,2)  移动到相对文章尾之后的p个字节，文件以二进制的方式打开
```

tell()：返回文件读取指针的位置

#### 捕获异常：

```python
try:
    f=open("note.txt","r")
except:
    print("发生错误")
    
    
    
try:
    f=open("note.txt","r")
finally:                    #不管会不会出错，都会执行下面的内容；
    if f:                   #如果f存在
        f.close()
```

```python
#python3语法糖
with open("note1.txt","r") as f:        #自动关闭文件
```



### os模块：

os 可以操作文件、系统

os.path     操作文件路径

os.system()     命令控制台

os.listdir()   显示目录下的内容

os.mkdir()   创建文件夹

os.path.isfile()       是否为文件

os.path.isdir()        是否为路径



### pickle模块常用方法

```python
#写入数据
import pickle
obj=[{"name":"xb","sex":"男","tel":12345678}]
with:open("node.txt","wb") as f:
          pickle.dump(obj,f)
#读数据
import pickle
with open("node.txt","rb") as f:
    obj=pickle.load(f)
    print(obj[0]["name"])         
```



### csv存储数据：

> 电子表格和数据库常用的导入导出格式

```python
import csv
#列表写入数据
with open("dome.csv","w",newline="") as f:
    writer=csv.writer(f,dialect="excel")
    for i in range(10):
        writer.writerows([[1,2,3,4,5],["a","b","c","d","e"]])
#字典写入数据
with open("dome.csv","w",newline="") as c:
    writer=csv.DictWriter(c,[1,2,3,4,5])
    writer.writeheader()
    writer.writerow({1:"a",2:"b",3:"c",4:"d",5:"e"})
    writer.writerows([{1:"a",2:"b",3:"c",4:"d",5:"e"},{1:"a",2:"b",3:"c",4:"d",5:"e"}])
#列表方式读数据
with open("dome.csv","r") as d:
    reader=csv.reader(d)
    for item in reader:
        print(item)
 #字典方式读数据
with open("dome.csv","r") as b:
    read=csv.DictReader(b)
    for i in read:
        print(dict(i))

```

### 面向对象：

静态方法和类方法都可以通过类或者实例来调用，其两个的特点都是不能够调用实例属性

类属性与类方法是类固有的方法与属性，不会因为实例不同而改变

### 继承和派生：

继承的目的是延续旧的类的功能

继承：任何类都是直接或者间接继承object类，objects是一切基类父类

派生：派生就是子类在继承父类的基础上衍生出新的属性，子类独有的，父类没有的，或者子类定义与父类同名的东西，子类也叫派生类

派生的目的是在旧类的基础上派生新功能



#### 继承和派生常用的内建函数：

- issubclass(sub,parent)   判断sub是否为parent的子类  返回bool
- isinstance(ins,class)   判断ins是否为class的实例      返回bool
- hasattr(obj,"attr")     判断obj中是否有attr属性    返回bool
-  getattr(obj,"attr")     获取obj中的attr属性
- setattr(obj,"attr")     设置obj中的attr属性
- delattr(obj,"attr")     删除obj中的attr属性
- dir()   以列表的形式列出类或实例的属性和方法
- super()  寻找父类信息super(type[,object-or-type])

​              python3和python2的一个区别就是python3可以直接使用

- super().***    代替super(Class,self).***
- vars(object)    以字典的形式返回类或实例的属性

#### 封装：

> 对内部数据进行保护（隐藏），或合理的暴露

  

### 异常

> 因为程序出现了错误而在正常控制流以外采取的行为

#### 错误

- 软件方面（错误是语法或者逻辑上的）

语法错误：软件结构上的错误，导致不能被解释器解释或者编译器无法编译，这些错误必须在程序执行前纠正

逻辑错误：不完整或者不合法得输入导致，也可能是逻辑无法生成，计算，或者输出结果需要的过程无法执行

#### except捕获多个异常

当捕获多个异常时，可以把要捕获异常的名字，放到except后，并使用元组的方式进行存储

```python
try:
    print("----test1-----")
    open("123.txt","r")  #如果123.txt不存在，那么会产生IOError异常
    print("----test1-----")
    print(num)     #如果num没有定义，那么会产生NameError异常
except(IOError,NameError):
    #如果想通过一次except捕获到多个异常可以用一个元组的方式
    #errorMsg里会保存捕获到的错误信息
```

#### 总结

- except语句不是必须的，finally语句也不是必须的，但是二者必须要有一个，否则就没有try的意义
- except语句可以有多个，python会按照except语句的顺序依次匹配你指定的异常，如果异常已经处理就不会进入后面的except语句
- except语句可以以元组的形式同时指定多个异常
- except语句后面如果不指定异常类型，则默认捕获所有异常，你可以通过logging或sys模块获取当前异常
- 如果要捕获异常后重复抛出，请使用raise,后面不要任何参数或信息
- 不建议捕获并抛出同一个异常

#### 异常种类

```python
BaseException
 +-- SystemExit  解释器请求退出
 +-- KeyboardInterrupt  用户中断执行（ctr + c）
 +-- GeneratorExit   生成器发生异常来通知退出
 +-- Exception   常规错误基类
      +-- StopIteration 	迭代器没有更多的值
      +-- StopAsyncIteration
      +-- ArithmeticError   数值计算错误基类
      |    +-- FloatingPointError   浮点计算错误
      |    +-- OverflowError    数值运算超出最大限制
      |    +-- ZeroDivisionError    除(或取模)零 (所有数据类型)
      +-- AssertionError    断言语句失败
      +-- AttributeError    对象没有这个属性
      +-- BufferError   
      +-- EOFError  没有内建输入，到达EOF标记
      +-- ImportError   导入模块失败
      |    +-- ModuleNotFoundError
      +-- LookupError   无效数据查询基类
      |    +-- IndexError 序列中没有此索引(index)
      |    +-- KeyError 映射中没有这个键
      +-- MemoryError   内存溢出错误
      +-- NameError 未声明未初始化的本地变量
      |    +-- UnboundLocalError 	访问未初始化的本地变量
      +-- OSError   操作系统错误
      |    +-- BlockingIOError 操作阻塞设置为非阻塞操作的对象（例如套接字）时引发
      |    +-- ChildProcessError 子进程上的操作失败时引发
      |    +-- ConnectionError 连接相关的问题的基类
      |    |    +-- BrokenPipeError
      |    |    +-- ConnectionAbortedError
      |    |    +-- ConnectionRefusedError
      |    |    +-- ConnectionResetError
      |    +-- FileExistsError 尝试创建已存在的文件或目录时引发
      |    +-- FileNotFoundError    在请求文件或目录但不存在时引发
      |    +-- InterruptedError 系统调用被输入信号中断时触发
      |    +-- IsADirectoryError 在目录上请求文件操作时引发
      |    +-- NotADirectoryError 在对非目录的os.listdir()事物请求目录操作（例如）时引发
      |    +-- PermissionError 尝试在没有足够访问权限的情况下运行操作时引发 - 例如文件系统权限。
      |    +-- ProcessLookupError 当给定进程不存在时引发
      |    +-- TimeoutError 系统功能在系统级别超时时触发。
      +-- ReferenceError    弱引用(Weak reference)试图访问已经垃圾回收了的对象
      +-- RuntimeError  一般的运行时错误
      |    +-- NotImplementedError  	尚未实现的方法
      |    +-- RecursionError
      +-- SyntaxError 一般的解释器系统错误
      |    +-- IndentationError 缩进错误
      |         +-- TabError    Tab 和空格混用
      +-- SystemError Python 语法错误
      +-- TypeError     对类型无效的操作
      +-- ValueError    传入无效的参数
      |    +-- UnicodeError  Unicode 相关的错误
      |         +-- UnicodeDecodeError  	Unicode 解码时的错误
      |         +-- UnicodeEncodeError  Unicode 编码时错误
      |         +-- UnicodeTranslateError   Unicode 转换时错误
      +-- Warning   警告的基类
           +-- DeprecationWarning   关于被弃用的特征的警告
           +-- PendingDeprecationWarning    关于特性将会被废弃的警告
           +-- RuntimeWarning   可疑的运行时行为(runtime behavior)的警告
           +-- SyntaxWarning    可疑的语法的警告    
           +-- UserWarning  用户代码生成的警告
           +-- FutureWarning    关于构造将来语义会有改变的警告
           +-- ImportWarning
           +-- UnicodeWarning
           +-- BytesWarning
           +-- ResourceWarning
```

### 模块和包

#### 包

> 文件夹(里面必须有初始化)

##### 引入方法

单个引入

```python
#第一种引入方式
import bao.a
bao.a.aa()
#第二种引入方式
from bao import a
a.aa1()
#第三种引入方式
from bao import a as a1
a1.aa2()
#第四种引入方式
from bao.a import aa3
aa3()
```

一次性导入

```python
from bao.a import *         #一般不用
在包中子模块添加变量__all__   列表
```

#### 使用相对路径导入包中子模块

- .  当前目录
- ..上一级目录

##### 注意:

- 使用.这种模式从不是包的目录中导入将会引发错误
- 在顶层的脚本的简单模块中，他们将不起作用
- 包的部分将作为脚本直接执行，那他们将不起作用

#### 重新加载模块

```python
import imp
import spam
imp.reload(spam)
```

#### 运行目录或压缩文件

> 应用程序中有多个文件，可以把应用程序放进自己的目录并添加一个__main__.py文件

```python
myapplianction/
spam.py
bar.py
__main__.py
```

#### 读取位于包中的数据文件

```python
import pkgutil
data=pkgutil.get_data(__package__,"somedata.dat")   #结果为字节型数据
```

#### 通过字符串名导入模块

```python
import importlib
math=importlib.import_module('math')
math.sin(2)
mod=importlib.import_module("urllib.request")
u=mod.urllopen('http:www.pyhton.org')
```





