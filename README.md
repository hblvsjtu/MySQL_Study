# MySQL_Study


## 作者：冰红茶  
## 参考书籍：《MySQL5.7从入门到精通》 [W3school](http://www.w3school.com.cn/sql/index.asp)
    
------    
    
无论是学习前端也好，还是后端，数据库知识作为一种计算机基础知识值得每个程序员去学习。本文从MySQL为例，学习SQL语言，学习CRUD，点亮此技能，对以后的职业发展有利无害^_ ^

## 目录
## [一、MySQL常用命令大全](#1)
### [1.1 准备工作](#1.1)
### [1.2 表的增删改查](#1.2)
### [1.3 字段的增删改查](#1.3)
### [1.4 数据的增删改查](#1.4)
### [1.4 浏览器数据持久化存储技术](#1.4)
## [二、前端与协议](#2)
### [2.1 HTTP协议简介](#2.1)
### [2.2 HTTP版本](#2.2)
### [2.3 HTTP2.0](#2.3)
### [2.4 Web安全机制](#2.4)
### [2.5 HTTPS协议通讯过程](#2.5)
### [2.6 前端实时协议](#2.6)
### [2.7 RESTful数据协议规范](#2.7)
### [2.8 与Native交互协议](#2.8)
## [三、前端三层结构与应用](#3)
### [3.1 结构层HTML、表现层CSS和行为层JavaScript](#3.1)
### [3.2 前端结构层演进](#3.2)
### [3.3 浏览器脚本演进历史](#3.3)
### [3.4 前端表现层基础](#3.4)
### [3.5 响应式网站开发技术](#3.5)
## [四、现代前端交互框架](#4)
### [4.1 直接DOM操作时代](#4.1)
### [4.2 MV*交互模式](#4.2)
### [4.3 数据变更检测](#4.3)
### [4.4 Virtual DOM交互模式](#4.4)
## [五、前端项目与技术实践](#5)
### [5.1 前端开发规范](#5.1)
### [5.2 自动化构建](#5.2)
### [5.3 前端性能优化](#5.3)
### [5.4 前端用户数据分析](#5.4)
### [5.5 前端搜索引擎优化基础](#5.5)
## [六、渲染方式](#6)
### [6.1 前后端分离](#6.1)
### [6.2 数据渲染](#6.2)

        
        
------      
        
<h2 id='1'>一、MySQL常用命令大全</h2>
<h3 id='1.1'>准备工作</h3>  
        
#### 1) mysql连接数据库
> - 添加mysql的环境变量 我的电脑-属性-高级-环境变量-PATH-浏览（打开MySQL server文件夹里面的bin文件夹）
> - 打开PowerShell 键入
                
                PS C:\WINDOWS\system32> mysql -h localhost -u root -p
                Enter password: ********
                Welcome to the MySQL monitor.  Commands end with ; or \g.
                Your MySQL connection id is 10
                Server version: 5.7.20-log MySQL Community Server (GPL)

                Copyright (c) 2000, 2017, Oracle and/or its affiliates. All rights reserved.

                Oracle is a registered trademark of Oracle Corporation and/or its
                affiliates. Other names may be trademarks of their respective
                owners.

                Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
#### 2) 修改密码
> - mysqladmin命令用来修改用户密码
> - 命令格式： mysqladmin -u 用户名 -p 旧密码  password 新密码
#### 3) 退出
> - quit
#### 3) 使用
> - use <数据库名>; 
> - 把目标数据库当作默认的数据库使用
#### 4) 打印
> - select 
> - 打印版本号、时间、计算
                
                mysql> select version();
                +------------+
                | version()  |
                +------------+
                | 5.7.20-log |
                +------------+
                1 row in set (0.01 sec)

                mysql> select now();
                +---------------------+
                | now()               |
                +---------------------+
                | 2019-07-06 22:13:52 |
                +---------------------+
                1 row in set (0.00 sec)

                mysql> select "welcome to my blog";
                +--------------------+
                | welcome to my blog |
                +--------------------+
                | welcome to my blog |
                +--------------------+
                1 row in set (0.00 sec)

                mysql> select (4*4)/10+10;
                +-------------+
                | (4*4)/10+10 |
                +-------------+
                |     11.6000 |
                +-------------+
                1 row in set (0.01 sec)
#### 5) 备份数据库
> - mysqldump -h 主机名 -u 用户名 -p 密码 备份数据库名称 > 全路径名.sql;
                
                PS C:\WINDOWS\system32> mysqldump -h localhost -u root -p test_db > C:\Users\hblvs\Desktop\123.sql
                Enter password: ********
#### 6) 还原数据库
> - mysql -h 主机名 -u 用户名 -p 密码 备份数据库名称 < 全路径名.sql;
> - 注意：执行前必须保证数据库已创建在服务器中，否则会出错
> - 如果已经登入服务器了。可以使用source命令导入本地备份文件

            
<h3 id='1.2'>表的增删改查</h3>  
        
#### 1) 创建
> - create 
> - create database
> - create table
> - 创建表时，必须指定以下信息
>> - 要创建表的名称，不区分大小写，不能使用SQL里面的关键字
>> - 数据表中每一列（字段）的名称和数据类型，如果创建多个列，需要用逗号隔开
                
                mysql> create database test_db;
                Query OK, 1 row affected (0.01 sec)

                mysql> use test_db;
                Database changed

                mysql> create table tb_emp1(id INT(11), name VARCHAR(25), deptId INT(11), salary FLOAT);
                Query OK, 0 rows affected (0.05 sec)

                mysql> show tables;
                +-------------------+
                | Tables_in_test_db |
                +-------------------+
                | tb_emp1           |
                +-------------------+
                1 row in set (0.00 sec)
#### 2) 删除数据表
> - drop database 数据库名;
> - drop table [if exists] 表1, 表2,..., 表n
                
                mysql> drop table if exists tb_emp1;
                Query OK, 0 rows affected (0.01 sec)

                mysql> show tables;
                Empty set (0.00 sec)
#### 3) 修改表名
> - alter table 旧表名 rename 新表名;
                
                mysql> alter table tb_emp1 rename tb_emp;
                Query OK, 0 rows affected (0.02 sec)

                mysql> show tables;
                +-------------------+
                | Tables_in_test_db |
                +-------------------+
                | tb_emp            |
                +-------------------+
                1 row in set (0.00 sec)
#### 4) 显示
> - show;
> - show databases;
> - show tables;
                
                mysql> show databases;
                +--------------------+
                | Database           |
                +--------------------+
                | information_schema |
                | jsp_db             |
                | mysql              |
                | performance_schema |
                | sakila             |
                | sys                |
                | world              |
                +--------------------+
                7 rows in set (0.01 sec)

                mysql> show tables;
                +-------------------+
                | Tables_in_test_db |
                +-------------------+
                | tb_emp1           |
                +-------------------+
                1 row in set (0.00 sec)

            
<h3 id='1.3'>字段的增删改查</h3>  
        
#### 1) 增加字段
> - alter table 表名 add 新字段名 数据类型 约束条件
                
                mysql> alter table tb_emp1 add age INT(11);
                Query OK, 0 rows affected (0.08 sec)
                Records: 0  Duplicates: 0  Warnings: 0

                mysql> update tb_emp1 set age=26 where id=0001;
                Query OK, 1 row affected (0.01 sec)
                Rows matched: 1  Changed: 1  Warnings: 0

                mysql> select age from tb_emp1 where id=0001;
                +------+
                | age  |
                +------+
                |   26 |
                +------+
                1 row in set (0.00 sec) 
#### 2) 删除字段
> - 
#### 3) 修改字段
> - 
#### 4) 查询字段
> - describe或者show create table
                
                mysql> describe tb_emp1;
                +--------+-------------+------+-----+---------+-------+
                | Field  | Type        | Null | Key | Default | Extra |
                +--------+-------------+------+-----+---------+-------+
                | id     | int(11)     | YES  |     | NULL    |       |
                | name   | varchar(25) | YES  |     | NULL    |       |
                | deptId | int(11)     | YES  |     | NULL    |       |
                | salary | float       | YES  |     | NULL    |       |
                +--------+-------------+------+-----+---------+-------+
                4 rows in set (0.01 sec)

                mysql> show create table tb_emp1;
                | Table   | Create Table                                                                                                                                                                                 |
                +---------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
                | tb_emp1 | CREATE TABLE `tb_emp1` (
                  `id` int(11) DEFAULT NULL,
                  `name` varchar(25) DEFAULT NULL,
                  `deptId` int(11) DEFAULT NULL,
                  `salary` float DEFAULT NULL
                ) ENGINE=InnoDB DEFAULT CHARSET=utf8 |
                +---------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
                1 row in set (0.03 sec)

             
<h3 id='1.4'>数据的增删改查</h3>  
        
#### 1) 向表中插入数据
> - insert into 表名称 values
                
                mysql> insert into tb_emp1 values(0001, 'lvhongbin', 0001, 19000);
                Query OK, 1 row affected (0.01 sec)
#### 2) 删除记录
> - delete from table 
                
                mysql> select id from tb_emp1;
                +------+
                | id   |
                +------+
                |    1 |
                |    2 |
                +------+
                2 rows in set (0.00 sec)

                mysql> delete from tb_emp1 where id=0002;
                Query OK, 1 row affected (0.01 sec)

                mysql> select id from tb_emp1;
                +------+
                | id   |
                +------+
                |    1 |
                +------+
                1 row in set (0.00 sec)
#### 3) 修改表中的数据
> - update tableName set column1=value1,column2=value2, ...columnN=valueN where  conditions;
                
                mysql> update tb_emp1 set name='lvhongchao' where id=1;
                Query OK, 1 row affected (0.01 sec)
                Rows matched: 1  Changed: 1  Warnings: 0
                
                mysql> select name from tb_emp1;
                +------------+
                | name       |
                +------------+
                | lvhongchao |
                +------------+
                1 row in set (0.00 sec)
#### 4) 查询表中的数据
> - select [字段1, 字段2, ...字段n] from [表/视图] where [查询条件]
                
                mysql> select id from tb_emp1;
                +------+
                | id   |
                +------+
                |    1 |
                +------+
                1 row in set (0.00 sec)

                mysql> select name from tb_emp1;
                +-----------+
                | name      |
                +-----------+
                | lvhongbin |
                +-----------+
                1 row in set (0.00 sec)