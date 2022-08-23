# MySQL加强

### 数据约束

* 默认值：default

  ``` mysql
  create table student(
  	id int,
  	name varchar(10),
  	address varchar(20) default '深圳宝安'
  );
  #注意
  	对默认值字段插入null是可以的
  	对默认值字段插入非null
  ```

* 非空：not null

  ``` mysql
  create table student(
  	id int,
  	name varchar(10),
  	gender varchar(2) not null
  )
  #注意
  	非空字段必须复制
  	非空字段不能插入null
  ```

* 唯一：unique

  ``` mysql
  create table student(
  	id int unique,
  	name varchar(10)
  )
  #注意
  	唯一字段可以插入null
  	唯一字段可以插入多个null
  ```

* 主键：primary key

  ``` mysql
  #非空+唯一
  create table student(
  	id int primary key,
  	name varchar(10)
  )
  #注意
  	通常情况下，每张表都会设置一个主键字段，用于标记表中每条记录的唯一性
  	建议不要选择表的包含业务含义的字段作为主键，建议给每张表独立设计一个非业务含义的字段
  ```

* 自增长：auto_increment

  ``` mysql
  #ZEROFILL 自增长，从零开始
  create table student(
  	id int primary key auto_increment,
  	name varchar(10)
  )
  #自增长字段可以不赋值，自动递增
  ```

* 外键约束：foreign key

  ``` mysql
  #部门表（主表）
  create table department(
  	id int primary key,
  	dept_name varchar(20)
  )
  
  #员工表（副表）
  create table employee(
  	emp_id int primary key,
  	name varchar(10),
  	dept_id int,
  	foreign key(dept_id) references department(id)
  	#       外键          引用       参考表（参考字段）
  )
  
  #注意
  	被约束的表称为副表，约束别人的表称为主表，外键设置在副表上的
  	主表的参考字段通用为主键
  	添加数据：先添加主表，后添加副表
  	修改数据：先修改副表，后修改主表
  	删除数据：先删除副表，后删除主表
  ```

* 级联操作

  ``` mysql
  #当有了外键约束的时候，必须先修改或删除副表中的所有关联数据，才能删除主表！
  #我们希望直接修改或删除主表数据，从而影响副表数据，可以使用级联操作实现
  
  #级联修改
  ON UPDATE CASCADE
  #级联删除
  ON DELETE CASCADE
  
  #员工表（副表）
  create table employee(
  	emp_id int primary key,
  	name varchar(10),
  	dept_id int,
  	foreign key(dept_id) references department(id)
  	#       外键          引用       参考表（参考字段）
  	ON UPDATE CASCADE ON DELETE CASCADE
  )
  ```
  
* 三大范式

  ``` mysql
  #设计原则：建议设计的表尽量遵守三大原则
  #第一范式：
  	要求表的每个字段必须是不可分割的独立单元
  #第二范式：
  	在第一范式的基础上，要求每张表只表达一个意思。表的每个字段和主键有依据
  #第三范式：
  	在第二范式的基础上，要求每张表的主键之外的其他字段都只能和主键有直接决定依赖关系
  ```

* 关联查询（多表查询）

  ``` mysql
  #交叉查询
  	不推荐，产生笛卡尔积现象
  	
  #内连接查询：
  	只有满足条件的结果才会显示
  	select tb1.column1 col1,tb2.column col2 from tb1,tb2
  	where (连接条件)
  	select tb1.column1,tb2.column from tb1 inner join
  	tb2 on (连接条件)
  	
  #外连接
  	 左[外]连接查询： 使用左边表的数据去匹配右边表的数据，如果符合连接条件的结果则显示，如果不符合连接条件则显示null -- （注意： 左外连接：左表的数据一定会完成显示！）
  	 select tb1.column1 col1,tb2.column col2 from tb1 left outer
  	 tb2 join on (连接条件)
  	  右[外]连接查询: 使用右边表的数据去匹配左边表的数据，如果符合连接条件的结果则显示，如果不符合连接条件则显示null -- （注意： 右外连接：右表的数据一定会完成显示！）
  	 select tb1.column1 col1,tb2.column col2 from tb1 right outer 
  	 tb2 join on (连接条件)
  	 
  #自连接查询
  	 select tb1.column1 col1,tb2.column col2 from tb1 a right outer 
  	 tb1  join on (连接条件)
  	
  	
  ```
  
* 视图

  ```mysql
  #视图可以被看成是一种虚拟表，但是其物理上是不存在的，即MySQL并没有专门的位置为视图存储数据。根据视图的概念可以发现其数据来源于查询语句
  create 创建视图
  	create VIEW viewname as select_statement(sql语句)
  desc 查看视图信息
  	desc viewname
  show 查看创建的视图
  	show tables
  	show create table|view viewname
  update 更新视图数据
  	update viewname set ... where ... 
  alter 修改视图
  	alter VIEW viewname as select_statement(sql语句)
  drop 删除视图
  	drop VIEW viewname
  	
  
  ```

* 存储过程

  ```mysql
  #存储过程，带有逻辑的sql语句,之前的sql没有条件判断，没有循环,存储过程带上流程控制语句（if  while）
  存储过程的特点
      1）执行效率非常快！存储过程是在数据库的服务器端执行的！！！
      2）移植性很差！不同数据库的存储过程是不能移植。
      
  DELIMITER$	-- 声明存储过程的结束符
  CREATE PROCEDURE pro_test()
  BEGIN
  	-- 可以写入多个SQL语句
  	select * from employee;
  END$
  -- 执行存储过程
  CALL pro_test();
  
  #--------------------------------------带有输入参数的存储过程---------------------------------------
  DELIMITER$	-- 声明存储过程的结束符
  CREATE PROCEDURE pro_test(IN eid INT) -- IN：输入参数
  BEGIN
  	-- 可以写入多个SQL语句
  	select * from employee where id = eid;
  END$
  -- 执行存储过程
  CALL pro_test(4);
  
  #--------------------------------------
  -- 3.2 带有输出参数的存储过程
  DELIMITER $
  CREATE PROCEDURE pro_testOut(OUT str VARCHAR(20))  -- OUT：输出参数
  BEGIN
          -- 给参数赋值
  	SET str='helljava';
  END $
  
  
  
  
  ```

  





