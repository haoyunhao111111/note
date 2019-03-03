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

##### 查看历史

history

history -c   清空历史

##### 软连接

ln -s       ln -s  原文件的绝对路径  原文件名    目标文件的绝对路径   目标文件名

ln           ln 原文件 目标文件

区别：

- 硬链接    占用内存空间    不能做文件夹的快捷方式     一改全改
- 软连接    基本不占内存空间     可以做文件夹的快捷方式     一改全改

##### 查找文件

find    查找文件    find   aa*   查找以aa开头的所有文件

grep   查找内容

grep a *.txt   从所有txt文件里面查找内容包含a的

##### 管道

|   ps -aux | grep 112

##### 文件解压缩

前提->打包  解包

打包：tar  -cvf    目标文件   原文件

> target  目标    c  create  创建    v   view   视图    f   file  文件

解包 ：tar -xvf    打包文件 -C   目标文件夹

压缩    tar  -zcvf   目标文件   原文件

解压    tar   -zxvf    压缩文件   -C   目标文件夹

zip压缩    zip  目标文件  原文件

​		 unzip   目标文件

#### ssh协议

> secure shell

##### 特点

体积小，速度快

文件加密

对口令

#### 文件传输

文件上传：scp  aa.html  hyh @192.168.184.128:/home/hyh      

> scp  目标文件  服务器名@服务器地址:要存放的地址

文件下载：scp hyh@192.168.184.128:/home/hyh/1.txt a

> scp 服务器名@服务器地址：下载文件的存放地址  

#### 磁盘管理

df  查看磁盘使用信息    -h

du  查看家目录使用情况    -h

#### 网络通讯

ifconfig eth0     修改IP

ifconfig   netmask    修改子网掩码

ifconfig   broadcast    修改广播地址

UDP协议  视频

TCP协议   浏览器

netstat  -aup  

> a  所有   u   udp 协议    p   端口

netstat -atp

> a  所有   t  tcp协议    p  端口

ping  检测对方主机能不能通信

#### 软件安装和管理

##### apt-get方式安装   



sudo apt-get update      获取新的软件列表

sudo add-apt repository  ppa:webupd8team/java   添加包地址

sudo apt-get install packagename    安装软件包

sudo apt-get remove packagename   删除软件

apt-get --purge remove mysql-server mysql-client   删除软件包包括配置文件

apt-get autoremove mysql-server mysql-client    删除该软件的依赖包

apt-get clean && sudo apt-get autoclean   清除无用的包



##### 源码安装

- 下载源码
  - wget  url
  - wget -0 filrname url
- 解压
- 进入解压的目录
- 找到Configure并执行以下命令
  - ./configure --prefix=/usr/local/test  [--enable-optimizations]     prefix=/安装目录  [优化安装]
- 编译   make all
- 安装   make intall

##### 多版本共存

sudo update-alternatives --install /usr/name/python python3 /opt/python3.7/bin/python3.7 5000     

> sudo update-alternatives --install  链接  名称  路径  优先级

#### 关机

- halt   关机
- poweroff  立刻关机
- shutdown  -h  now  立刻关机（root使用）
- shutdown  -h  10  10分钟以后关机

#### 重启

- reboot
- shutdown  -r  now
- shutdown -r  10
- shuedown -r 20:35
- shutdown -c 取消重启

#### 进程

ps -aux  显示所有包含使用者的进程

top   动态显示所有进程

kill pid     杀死进程

kill -9 pid  强制杀死进程

sudo etc/init.d/mysql         stop   start   restart  

>  进程保护机制存放地址   关闭    运行   重启

#### 权限管理

- whoami   查看当前目录
- who   查看用户
- su      切换用户
- useradd   添加用户
  - -m  自动创建家目录
  - -d   指定用户登录的起始目录 
  - -g    指定新创用户的组
  - -G    追加组
- passwd   为新用户设置密码

> sudo passwd first

- usermod

> usermod first -d /home/first/some



##### 检测是否添加成功的三个方法

- home ls
- cat etc/passwd
- 从window用新用户登录ubuntu





#### 组

- groupadd   创建组
- groupdel    删除组
- groupmod  demo -n demo1   修改
- gpasswd   -d  first first    从组中删除用户名  （该组不是用户名的主组）
- gpasswd   -a   first first    把用户名添加到组中



##### 让新建用户拥有sudo权限

usermod -a -G sudo first

usermod -a -G adm  first



#### 更改文件的所有者

chown   first:first  aaa       修改当前目录的拥有者

>  chown    用户名:组名  目录

chown  -R first:first  aaa    修改当前目录及其子目录的拥有者



#### 更改文件权限

chmod   u=rwx  g=rwx  o=rwx

1->x  2->w  3->xw   4->r  5->rx  6->rw  7->rwx



表明用python执行文件

#! /usr/bin/env  python



### 添加全局变量

- export PATH=$PATH:/
- vim ~/.profile
- 软链  sudo ln -s /usr/local/nginx/sbin/nginx  /usr/bin/nginx





