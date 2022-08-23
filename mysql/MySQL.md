# Mysql基础

### 	入门

 * 启动MySQL服务

   ``` /mysql
   mysql -u root -p
   enter passwoed:xxxxxx
   ```

### 	数据库管理

 * 查看数据库

   ``` /mysql
   show databases;
   ```

 * 创建数据库

   ``` /mysql
   create database db_name
   default character set utf8; #指定默认字符集创建数据库
   ```

* 查看数据库的默认字符集

  ``` /mysql
  show create database db_name;
  ```

* 删除数据库

  ``` /mysql
  drop database db_name;
  ```

 * 修改数据库

   ``` /mysql
   alter database db_name default character set gbk;
   ```

### 表管理

* 选择数据库

  ``` /mysql
  use db_name;
  ```

* 查看当前使用的数据库

  ``` /mysql
  select database();
  ```

* 查看所有表

  ``` /mysql
  show tables;
  ```

* 创建表

  ``` /mysql
  create table tb_name(
  	id int,
  	name varchar(10)
  );
  ```

* 查看表结构

  ``` /mysql
  desc tb_name
  ```

* 删除表

  ``` /mysql
  drop table tb_name;
  ```

* 修改表

  ``` /mysql
  #添加字段
  -alter table tb_name add column column_name column_type;
  #删除字段
  -alter table tb_name drop cloumn column_name;
  #修改字段类型
  -alter table tb_name modify column column_name column_type;
  #修改字段名称
  -alter table tb_name change column column_name column_newname column_type;
  #修改表名称
  -alter table tb_name rename to tb_newname;
  ```

### 增删改查数据

* 增加数据

  ``` /mysql
  #插入数据一一对应
  -insert into tb_name(column1,column2,column3) values (...,...,...);
  ```

* 修改数据

  ``` /mysql
  #带条件修改数据
  -update tb_name set columnX = '...' where columnY = '...';
  #可同时修改多个字段的值
  ```

* 删除数据

  ``` /mysql
  #带条件的删除
  -delete from tb_name where columnX = '...';
  ```

#### drop ,delete,truncate的区别

 * drop只能删除表，删除数据库，删除表中的字段
 * delete只能删除数据与where搭配使用，删除的数据不能回滚
 * truncate也是删除表中所有的数据，删除的数据不能回滚

### 查询数据

* 查询列

  ``` /mysql
  #查询所有列
  -select *from tb_name;
  #查询指定列
  -select column1,column2 from tb_name;
  #查询是添加一个常量列
  -select column1,column2，'......' as '...' from tb_name;
  #查询合并列
  -select (column1+column2) from tb_name
  #去除重复数据
  -select DISTINCT columnX from tb_name
  ```

* 条件查询

  ``` /mysql
  #where
  #逻辑条件：and（与）、or（或）
  #比较条件：> < >= <= = <>（不等于）between and（等价于>= 且 <=)
  #判空条件：is null、is not null
  
  #模糊条件：like
  	#%：表示任意字符
  	#_：表示一个字符
  	
  #聚合查询：聚合函数
  	#sum()
  	#avg()
  	#max()
  	#min()
  	#count()	
  ```

* 分页查询

  ``` /mysql
  #limit(起始行，查询行数)
  ```

* 查询排序

  ``` /mysql
  #order by
  	#asc 升序
  	#desc 倒序
  #多个排序条件
  	order by column1 asc，column2 desc；
  ```

* 分组查询

  ``` /mysql
  #group by
  #分组查询后筛选（having）
  	#分组之前条件使用where关键字，分组之后条件使用having关键字
  ```

* 备份数据库

  ``` /mysql
  mysqldump -u root -p db_name>c:\db_name.sql
  enter password:xxxxxxx
  
  #恢复数据库
  	create database db_name;
  	use db_name;
  	source c:\db_name.sql;
  ```

  



