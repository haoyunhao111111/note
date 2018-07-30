## BOM(浏览器对象模型)

> 完成窗口与窗口之间的通信，`window`是其核心对象

- history
- location
- dom
- screen
- frames
- navigation

### window对象

#### 属性：

- 浏览器宽高
  - window.innerWidth    获取浏览器的宽度
  - window.innerHeight  获取浏览器的高度
  - document.documentElement.clientWidth  获取浏览器的宽度
  - document.documentElement.clientHeight  获取浏览器的高度

- 浏览器左上角距屏幕左上角的偏移量
  - window.screenTop    垂直偏移量
  - window.screenLeft    水平偏移量

#### 方法：

- alert()     弹出框
- prompt   输入框    
- confim    弹出确定取消框
- close()    关闭页面
- open(“url”，“width=300,height=200”)     打开页面
- setInterval(fn,1000)    隔一定时间重复不断的执行一个函数    fn:时间函数；   1000 ：间隔时间，单位毫秒
- clearInterval(t)  清除时间函数
- setTimeout(fn,1000)    隔一定的时间，只执行一次函数   fn:时间函数；   1000 ：间隔时间，单位毫秒
- clrearTimeout(t)    清除时间函数

#### 获取表单的值：obj.value

### history对象：

#### 属性：

- history.length      用来显示历史记录的长度

#### 方法：

- history.forward()    前进
- history.back()          后退
- history.go(0)            刷新

### location对象：

#### 属性：

- lacation.ref   设置或获取页面的地址；
- location.host   主机名＋端口号
- location.hostname     主机名
- location.port      端口号
- location.protocol     协议
- location.pathname     路径
- location.search   问号后的搜索路径

#### 方法：

- location.reload()     重新加载
- location.replace(“history.html”)    页面替换，不会增加历史记录
- location.assign("history.html")      页面替换，能够增加历史记录