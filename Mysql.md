## 数据库

> 关系型数据库(MySQL)          非关系型数据库(redis)          数据仓库

安装mysql服务      1.命令行  2.软件   3.程序存入数据

### 数据库操作

```mysql
#简单的数据库操作

show databases;   #查看数据库
create datebase  demo;   #创建名为demo的数据库
use demo;            #使用demo数据库
show tables;        #查看demo中的表
create table stu (
    id int(10) auto_increment primary key,   #表头名 数据类型  自增  主键
    name  varchar(10),
    age varchar(10),
    sex varchar(10))default charset=utf8;    #指定字符编码类型
desc stu;    #查看数据表的结构
insert into sut(name,age,sex) values("张三","20","男")   #插入数据
update stu set sex="女" where id=1;   #修改数据
delete from stu where id=1;    #删除数据
drop table stu     #删除表
drop database demo   #删除数据库
```
