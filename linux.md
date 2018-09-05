## linux

> 操作系统的内核，多用户，多任务的支持远程操作的系统

### 浏览器作用

- 呈现内容        解析内容和样式    -webkit-

- 实现交互逻辑            v8引擎=>解析JS

- 进行数据传递            chorme  net 引擎

### ubuntu

> 计算机操作系统，是linux最受欢迎的发行版

### linux命令

/  根目录

~   家目录

shift+ctrl+t    终端分屏

alt+1   切换第一分屏

#### cd 目录切换      

> 跟文件夹名字或路径

- cd ..  上一级目录

- cd ../../  上上级目录

- cd -   退回到最近的一次

ls 

> 查看目录

- ls -a   查看全部目录
- ls -l    列出文件的详细信息

clear  清除屏幕

#### 目录

bin    重要的二进制应用程序

sbin   超级管理员

boot   启动项

dev   设备文件（硬件设备）

etc   配置文件    启动脚本等

home   家目录

lib  系统库文件

lost+found    遗失查找目录

media      管理移动的设备

mnt   管理文件系统

opt     提供一个供可选的应用程序安装目录

proc   存放进程产生的垃圾

root    关于超级管理员的东西

sys   系统文件

tmp   临时文件存放

usr   绝大多数用户的配置文件

var   经常变换的文件

run  内存



#### 查看文档命令

- man   f->翻页   q->退出

which   命令的存放位置

pwd       当前的位置  输出为绝对位置

#### 操作文件

##### 创建文件

- echo   输出

> echo 123 > "1.txt"    写入   会覆盖原来的
>
> echo  456>>"1.txt"  追加

- touch    创建文件   文件存在则不执行

##### 预览文件

- cat  

- gedit   编辑文件

##### 删除文件

rm   

##### 重命名文件

mv 1.txt 2.txt     文件1重命名为2

##### 复制文件

cp 1.txt 2.txt           把1.txt复制并命名为2.txt

#### 操作目录

- mkdir   创建目录
- rmdir   删除空目录
- rmdir -p a/b   连续删除目录  a不空b为空
- rm -rf 

##### 重命名文件夹

mv  a aaa     文件夹a重命名为aaa

##### 复制文件夹

cp  a  -r  b

