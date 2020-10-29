1.数据库的好处:实现数据持久化、使用完整的管理系统统一管理，易于查询
2.数据库的相关概念
	2.1 DB(database:数据库)---->存储数据的“仓库”。它保存了一系列有组织的数据（保存一组有组织的数据的容器）
	2.2 DBMS:数据库管理系统(Database Management System)、数据库软件(产品)--->数据库是通过DBMS创建和操作的容器（用于管理DB中的数据）
	2.3 SQL:结构化查询语言(Structure Query Language)---->专门用来与数据库通信的语言（用来与DBMS通信的语言）
3.SQL的优点
	3.1 不是某个特定数据库供应商专有的语言，几乎所有DBMS都支持SQL
	3.2 简单易学
	3.3 虽然简单，但实际上是一种强有力的语言，灵活使用其语言元素，可以进行非常复杂和高级的数据库操作。
4.数据库的特点
	4.1 将数据放到表中，表再放到库中
	4.2 一个数据库中可以有多张表，每张表都有一个名字，用来标识自己，表名具有唯一性
	4.3 表具有一些特性，这些特性定义了数据在表中如何存储，类似于java中”类“的设计
	4.4 表由列组成，我们也称为字段。所有表都是由一个或多个列组成的，每一列类似java中的"属性"
	4.5 表中的数据是按行存储的，每一行类似于java中的"对象"
5.MySQL的背景
	5.1 前身是一家瑞典的公司、MySQL AB
	5.2 08年被sun公司收购
	5.3 09年sun公司被oracle公司收购
5.MySQL的优点
	5.1 成本低:开放源代码，一般可以免费试用
	5.2 性能高、移植性好:执行很快
	5.3 简单:很容易安装和使用
	5.4 体积小
6.DBMS分为两类
	6.1 基于共享文件系统的DBMS（ Access ）
	6.2 (CS)基于客户机-----服务器的DBMS( MySQL、Oracle、SqlServer   )
7.MySQL的配置文件重要选项	
	[mysql]

​    #  设置mysql客户端默认字符集

​	default-character-set=utf8 
​	[mysqld]
​	# 设置3306端口
​	port = 3306 
​	# 设置mysql的安装目录
​	basedir=D:\\softnew\\MYSQL\\mysql-5.7.20-winx64
​	# 允许最大连接数
​	max_connections=200
​	# 服务端使用的字符集默认为8比特编码的latin1字符集
​	character-set-server=utf8
​	# 创建新表时将使用的默认存储引擎
​	default-storage-engine=INNODB
8.MySQL服务的停止与启动
​	8.1 停止（Windows）: net stop "MySQL服务名"
​	8.2 启动（Windows）： net start "MySQL服务名"
9.MySQL服务的登录和退出(Windows)
​	9.1 登录:mysql -h (主机) -P (端口号) -u (用户名) -p(密码)
​	9.2 退出：exit
10.MySQL的常见命令
​	10.1 显示存在的数据库: show databases;
​	10.2 打开指定数据库: use "数据库名";
​	10.3 显示当前数据库中存在的表: show tables;
​	10.4 显示指定库的表: show tables from "数据库名"；
​	10.5 查看当前所在的库:select database();
​	10.6 创建表 create table “表名”(字段名 字段类型，字段名 字段类型(字段长度));
​	10.7 查看表的结构:desc "表名"；
​	10.8 查看数据：select * from “表名”；
​	10.9 插入数据:insert into “表名" (字段名，字段名) values（字段值，字段值）；
​	10.10 修改数据: update “表名” set 字段名=字段值 where 条件；
​	10.11 删除数据: delete from “表名” where 条件； 
​	10.12 查看数据库的版本：在客户端(select version())、不在客户端(mysql --version/mysql -V);

​	10.13 查看字符集：show variables like '%char%';

11.SQL的语法规范
	11.1 不区分大小写，但建议关键字大写，表名、列名小写
	11.2 每条命令最好用分号结尾
	11.3 每条命令根据需要，可以缩进或换行
	11.4 注释
		单行注释：#注释文字
		单行注释：-- 注释文字
		多行注释：/* 注释文字 */
12.DQL(data query language)语言学习
	12.1 基础查询
		12.1.1 语法:select 查询列表(表中的字段、常量值、表达式、函数) from 表名；
		12.1.2 查询结果是一个虚拟表格；
		12.1.3 起别名(便于阅读、区分不同表的相同字段)：as "别名"、as可以省略
		12.1.4 去重：distinct 字段名(select distinct department_id from departments)
		12.1.5 +号的作用:仅仅只有运算符的功能，其中一方为字符型，试图将字符型数值换成数值型，如果转换成功，则继续做加法运算，如果转换失败，则将字符型的数值转换为0，只要一方为null,结果肯定为null
		12.1.6 concat(可变参数)字符连接函数：只要拼接的参数中一个为null,整个结果都为null
		12.1.7 ifnull(可能为空的字段,字段为空时所取的值)
		12.1.8 isnull(字段)：如果字段的值为null返回1，不为null返回0
	12.2 条件查询
		12.2.1 select 查询条件 from 表名 where 筛选条件；
		12.2.2 分类:按条件表达式筛选(>、<、=、!=、<>、<=、>=)、按逻辑表达式筛选(&&、||、!、and、or、not)、模糊查询(like、between and、in、is null、is not null)
		12.2.3 like和通配符一起使用:%(任意多个字符，包含0个字符)、_(任意单个字段)、\(转义符)、
escape '符号'(把指定符号定义为转移符)、可以判断数值型
		12.2.4 between and:可以提高语句的简洁度、包含边界值、两个值的顺序不能颠倒
		12.2.5 in:可以提高语句的简洁度、值类型必须统一(兼容)、不支持通配符
		12.2.6 is null/is not null:=和<>不能判断null值
		12.2.7 安全等于( <=> ): 可以用于判断null值和普通类型的值

​	12.3 排序查询

​		12.3.1 语法：select 查询列表 from 表 where 筛选条件 order by 排序列表(字段、别名、表达式、函数) asc(升序)|desc(降序)

​		12.3.2  特点：默认是升序

​		12.3.3 length(字段)：获取字段的长度

​		12.3.4 order by 一般放在最后，limit 子句除外

​	12.4 常见函数

​		12.4.1 分类：单行函数、分组函数

​		12.4.2 单行函数：字符函数、数字函数、日期函数、其他函数、流程控制函数

​		12.4.3 字符函数

```
length(字段)：获取字符的长度(字节数)
concat(字符，字符，.....)：拼接字符
upper(字符)：把小写变为大写
lower(字符)：把大写变为小写
substr(字符,索引,长度):截取字符，索引从1开始
instr(字符，字串): 返回字串在字符中第一次出现的索引、不存在返回0
trim(字符)：去掉前后空格
trim(字符 from 字符1)：去掉字符1前后的指定字符
lpad(字符，长度，字段1)：在字符前面添加多个字符1使总长度为指定长度、字符长度超过制定长度会进行截取字符
rpad(字符，长度，字段1)：在字符后面添加多个字符1使总长度为指定长度、字符长度超过制定长度会进行截取字符
replace():把字符的指定字符用指定字符替换
```

​		12.4.4 数学函数

```
round(数值)：四舍五入
round(数值，位数)：小数点保留几位
ceil(数值)：向上取整
floor(数值)：向下取整
truncate(小数，位数)：小数后面保留指定位数
mod(数值，数值)：取余数
rand():取随机数，放回0~1之间的小数
```

​		12.4.5 日期函数

```
now(): 返回当前系统时间
curdate()：返回当前系统日期
curtime(): 返回当前系统时刻
year(日期)：获取年
month(日期)：获取月
monthname(日期)：获取月(英文)
str_to_date(日期，格式)：把字符日期转化为指定格式的日期格式
date_format(日期，格式): 把日期转换为指定格式的字符串
datediff(日期,日期):两个日期相差的天数
```

​	12.4.6 其他函数

```
version(): 查询数据库版本号
database(): 查看当前数据库
user():查看当前用户
password(字符)，返回当前字符的密码形式(加密)
md5(字符)：加密
```

​	12.4.6 流程控制函数

```
if(表达式，表达式为true返回的值，表达式为false返回的值)
case函数：
	case 要判断的字段和表达式
	when 常量1 then 要显示的值1或语句1；
	when 常量2 then 要显示的值2或语句2；
	......
	else 要显示的值n或语句n;
	end
	--------------------------------
	case 
	when 条件1 then 要显示的值1或语句1；
	when 条件2 then 要显示的值2或语句2；
	.......
	else 要显示的值n或语句n;
	end
```

​	12.4.7 分组函数(用作统计使用，又称为聚合函数或统计函数或组函数)

```
sum(字段):求和      数值型、忽略null值、可以和distinct一起使用
avg(字段):平均值    数值型、忽略null值、可以和distinct一起使用
max(字段):最大值    任何类型、忽略null值、可以和distinct一起使用 max(distinct 字段)
min(字段):最小值    任何类型、忽略null值、可以和distinct一起使用
count():统计个数    任何类型、使用具体字段时忽略null值、可以和distinct一起使用
	引擎
		MYISAM ：count(*) 的效率高
		INNODB : count(*) 和 count(1) 效率差不多,比count(字段)高
和分组函数一同查询的字段要求是group by后的字段
```

​	12.4.8 分组查询

````
having:在分组后进行筛选，放在 group by 之后
特点：1.分组查询的筛选分为分组前筛选和分组后筛选
						数据源        位置                关键字
	分组前筛选：	  原始表      group by 子句的前面	  where
	分组后筛选   分组后的结果集   group by 子句的后面 	havings
	2.分组函数做条件肯定是放在having中
	
3.group by 支持表达式分组、多个字段分组、函数分组
4.可以添加排序(放在分组查询之后)
````

  12.4.9 连接查询(当查询的字段涉及多个表时)

```
笛卡尔乘积(全连接)：各表条数的乘积

分类：
	按年代：sq1192标准(仅仅支持内链接)、sql199标准(支持内连接+外连接(左外连接+右外连接)+交叉连接)
	按功能：
		内链接：等值连接、非等值连接、自连接
		外连接：左外连接、右外连接、全连接
		交叉连接

为表起别名：提高语言的简洁度，区分多个重名字段
	如果为表起了别名，则查询的字段就不能使用原来的表明去限定

等值连接：select 字段1,字段2,.... from 表1,表2 where 表1.字段1 = 表2.字段2
		特点：
			多表等值连接的结果为多表的交集部分
			n表连接，至少需要n-1个连接条件
			多表的顺序没有要求
			一般需要为表起别名
			可以搭配前面介绍所有来一起使用
			
			
非等值连接：select 字段1,字段2,... from 表1,表2 where 表1.字段1 (>=、<=、<、>、between and...) 表2.字段2

自连接: select a.字段1,b.字段1,... from 表1 as a,表1 as b where a.字段3 = b.字段4


sql99语法：
	select 查询列表
	from 表1 别名 连接类型(内连接：inner,左外连接：left(outer),右外连接:right(outer),全连接:full(outer),交叉连接:cross)
	join 表2 别名
	on 连接条件
  【where 筛选条件】
  【group by 分组】
  【having 筛选条件】
  【order by 排序条件】

特点：inner 可以省略

外连接：
	应用场景：用于查询一个表中有，另一个表中没有的记录
	特点：外连接的查询结果为主表中的所有记录，如果从表中有和它匹配的，则显示匹配的值，如果从表中没有和它匹配的，则显示null,外连接查询结果=内连接结果+主表中有而从表中没有的记录
	左外连接：left  join 左边的是主表
	右外连接：right join 右边的是主表
	左外和右外交换两个表的顺序，可以实现同样的效果
	全外连接：全外连接结果=内连接结果+表1中有表2中没有+表1中没有表2中有的
	
交叉连接：
	结果为笛卡尔乘积
	
sql92与sql99:
	功能：sql99支持更多
	可读性：sql99实现连接条件与筛选条件分离
```

12.4.10 子查询

```
分类：
	按子查询出现的位置：
      select后面：标量子查询
      from后面：表子查询
      where或having后面：标量子查询、列子查询、行子查询
      exists后面(相关子查询:查询结果为Boolean类型，有值结果为1,没有值返回0)：表子查询
      	语法： select exists(select * from "表名")；
   按结果集的行列数不同：
   	标量子查询(结果集只有一行一列)
   	列子查询(结果集只有一列多行)
   	行子查询(结果集一行多列或多行多列)
   	表子查询(结果集一般为多行多列)
   	
特点：
	子查询优的执行先于主查询的执行，主查询的条件用到了子查询的查询结果

多行子查询：
	使用的操作符：
		in/not in:等一列表中的任意一个
		any/some:和子查询返回的某一个值比较
		all:和子查询返回的所有值比较
		in 等价于 =any/not in 等价于 <>all
		<any 等价于 <max()/ <all 等价于 <min()

行子查询：
	将多行字段当成一个虚拟的字段来用
```

12.4.11 分页查询 

```
语法：
	select 查询列表
	from 表
  【join type in 表2】
   on 连接条件
   where 筛选条件
   group by 分组字段
   having 分组后的筛选
   order by 排序的字段】
   limit offset(要显示条目的起始索引，从0开始),size(要显示的条目个数)
 
特点：
 	放在查询语句的最后
```

 12.4.12 联合查询

```
union/union all:
应用场景：要查询的结果来自于多个表，且多个表没有直接的连接关系，但查询的信息一致时
特点：
	要求多条查询语句的查询列数是一致的
	要求多条查询语句的查询的每一列的类型和顺序最好一致
	union会去重、union all 不会去重
```

13. DML语言(数据操作语言)：插入(insert)、修改(update)、删除(delete)

    13.1 插入语句

    ```
    语法：
    	方式一(支持插入多行,支持子查询)：insert into “表名”（字段1、字段2....） values(字段1的值、字段2的值.....) 【select 查询列表】
    	方式二：insert into "表名" set 列名 = 值,列名 = 值
    注意：
    	插入的值的类型要与列的类型一致或兼容
    	不可以为null的列必须插入值，可以为null的可以插入null值或者不写
    	列的位置可以调换
    	列数和值的个数必须一致
    	可以省略列名，默认是所有列
    ```

    13.2 修改语句

    ```
    语法：
    	单表：update "表名" set 列名 = 值,列名 = 值,.... where 筛选条件 
    	多表：
    		sql92: update 表1 别名,表2 别名 set 列=值,.... where 连接条件 and 筛选条件
    		sql99: update 表1 别名 inner|left|right|full|cross join 表2 别名
    		on 连接条件 set 列=值,...... where 筛选条件
    ```

    13.2 删除语句

    ```
    语法：
    	方式一：
    		单表：delete from  “表名” where 筛选条件
    		多表：delete 别名 from 表1 inner|left|right|full|cross join 表2 别名 on 连接条件
    		where 筛选条件
    	方式二：删除所有数据
    		truncate table 表名
    
        假如删除的表中有字增长列，如果用delete删除后，再插入数据，自增长列的值从断点开始，而truncate删除后，再插入数据，自增长列的值从1开始。
        truncate删除没有返回值，delete删除有返回值。
        truncate删除不能回滚，delete删除有回滚。
    ```
    
14. DDL(数据定义语言)：库和表的管理

    14.1 库的管理

    ```
    库的创建：create database (if not exists)库名 【character set 字符集】；
    库的修改：
    	更改库的字符集：alter database 库名 character set 字符集；
    库的删除：drop database 库名；
    ```

    14.2 表的管理

    ```
    表的创建：
    	语法：create table 【if not exists】 表名(
		列名 列的类型(长度) 约束,
    		列名 列的类型(长度) 约束,
    		列名 列的类型(长度) 约束,
    		.....
    		列名 列的类型(长度) 约束
    	);
    	
    表的修改:
    	修改列名：alter table 表名 change 【column】 旧列名 新列名 类型；
       修改列类型: alter table 表名 modify column 列名 类型；
       添加列: alter table 表名 add column 列名 类型 【first|after 列名】;
       删除列: alter table 表名 drop column 列名；
       修改表名: alter table 表名 rename 【to】 新表名；
       
    表的删除:
    	drop table 【if exists】 表名；
    	
    复制表:
    	仅仅结构: create table 表名 like 表名；
       结构和数据: create table 表名  select * from 表名 where 筛选条件；
       复制部分结构: create table 表名 select 字段1,字段2,... where 1 = 2;
    ```
    
    14.3 常见的数据类型
    
    ```
    数值型：(unsigned:无符号) (zerofull:长度不够用0填充，使用默认为无符号)
    	整型：
    		tinyint：1个字节、有符号(-128～127)、无符号(0~255)
    		smallint：2个字节、有符号(-32768~32767)、无符号(0～65535)
    		mediumint：3个字节
    		int、integer：4个字节
    		bigint：8个字节
    	小数：
    		定点数：
    			dec(m,d):
    			decimal(m,d):
    		浮点数：
    			float(m,d):4个字节
    			double(m,d):8个字节
    字符型：
    	较短的:
    		char(m)：固定长度的字符
    		varchar(m)：可变长度的字符
    		binary：保存二进制
    		varbinary：保存二进制
    		enum：保存枚举
    		set：保存集合
    	较长的:
    		text：
    		blob：
    日期型：
    	date：4个字节，日期
    	datetime：8个字节，日期时间
    	timestamp(时间戳)：4个字节，日期时间，值受时区影响
    	time：3个字节，时间
    	year：1个字节，年
    
    选择类型的原则：所选择的类型越简单越好，能保存数值的类型越小越好
    
    整型特点：
    	如果不设置无符号还是有符号，默认是有符号，如果要设置无符号添加unsigned关键字
    	如果插入的数值超出范围，回报out of range 异常，并且插入临界值
    	如果不设置长度，会有默认的长度
    	长度代表显示的最大宽度，长度不够使用0来填充，但必须和zerofull来搭配使用
    
    小数特点：
    	1、m为整数部位+小数部位，d为小数部位，超出范围则为临界值
    	2、m和d可以省略，如果是decimal，则m默认为10,d默认为0,如果是float和double,则会根据插入的数据来决定精度
    	3、定点型的精度较高
    ```
    
    14.4 常见的约束
    
    ``` 
    分类：六大约束
    	not null：非空，保证该字段的值不能为空
    	default：默认，用于保证该字段有默认值
    	priamry key：主键，用于保证该字段的值具有唯一性，并且非空
    	unique：唯一，用于保证该字段的值具有唯一性，可以为空
    	check：检查约束【mysql中不支持】
    	foreign key：外键，限制两个表的关系
    	
    查看索引：show index from 表名；
    	
    create table if not exists 表名(
    	id int primary key,
    	stuName varchar(20) not null,
    	gender char(1) check(gender='男' or gender = '女'),
    	seat int unique,
    	age int default 18
    	majorId int,
    	
      【constraint 约束名】 primary key(id),
      【constraint 约束名】 unique(seat),
      【constraint 约束名】 check(gender='男' or gender='女'),
      【constraint 约束名】 foregin key(id) references 表名(id)
    );
    
    约束分类：
    	列级约束：六大约束都语法上都支持，但是外键约束没有效果
    	表级约束：除了非空、默认，其他的都支持
    	
    主键与唯一的区别：
    					唯一性       是否允许为空    一个表中可以有多少个   是否允许组合
    	主键：		唯一				 不可以				多个						允许
    	唯一：      唯一            可以				 一个					 允许
    	
    外键：
    	1、要求在从表设置外键关系
    	2、从表的外键列的类型和主表的关联列的类型要求一致或兼容，名称无要求
    	3、主表中的关联列必须是一个key(主键、唯一键)
    	4、插数据时，先插入主表后插从表，删数据时，先删从表后删主表
    	
    删除主键约束：
    	alter table 表名 drop primary key;
    删除唯一约束：
    	alter table 表名 drop index 约束名;
    删除外键约束：
    	alter table 表名 drop foregin key 约束名;
    ```
    
      14.5 标识列(自增长列)
    
    ```
    可以不用手动的插入值，系统提供默认的序列值
    auto_increment
    
    show variables like '%auto_increment%';
    
    set auto_increment_increment = 3;
    
    特点：
    	1、必须和key(主键、唯一键)搭配使用
    	2、一个表至多一个标识列
    	3、标识列的类型必须是数值型
    	4、可以通过 set auto_increment_increment = 3;设置步长
    ```
    
15. TCL(Transaction Control Language 事务控制语言)语言

    15.1 事务

    ```
    一个或一组sql语言组成一个执行单元，这个执行单元要么全部执行，要么全部不执行。
    
    查看存储引擎：show engines;
    
    事务的ACID属性：
    	1、原子性(Atomicity)：事务是一个不可分割的工作单元，事务中的操作要么都发生，要么都不发生
    	2、一致性(Consistency)：事务必须使数据库从一致性形态变化到另外一个一致性形态
    	3、隔离型(Isolation)：指一个事务执行不能被其他事务干扰，即一个事务内部的操作以及使用的数据对并发的其他事务是隔离的，并发执行的各个事务之间不能互相干扰。
    	4、持久性(Durability)：持久性是指一个事务一旦被提交，它对数据库中数据对改变就是永久性的，接下来的其他操作和数据库故障不应该对其有任何影响。
    	
    事务的创建：
    	隐式事务：事务没有明显的开启和结束的标志(insert、update、deltet)
    	显示事务：事务具有明显的开启和结束的标志
    		前提：必须先设置自动提交功能为禁用 set autocommit = 0;
    
    显示事务的步骤：
    	1、开启事务
    		set autocommit = 0;
    		start transaction; 可选
    	2、编写事务中的sql语句(insert、update、select、delete)
    	3、结束事务
    		commit; 提交事务
    		rollback;回滚
    ```

    15.2 数据库的隔离级别

    ```
    并发导致的问题：
    	脏读：对于两个事务T1、T2，T1读取了已经被T2更新但还没有被提交的字段，之后若T2回滚，T1读取的内容就是暂时且无效的。
    	不可重复读：对于两个事务T1、T2，T1读取一个字段，然后T2更新了该字段，之后，T1再次读取同一个字段，值就不同了。
    	幻读：对于两个事务T1、T2，T1从一个表中读取了一个字段，然后T2在该表中插入了一些新的行，之后，如果T1再次读取同一个表，就会多出几行。
    	
    隔离级别：
    	read uncommited(读未提交数据)：脏读、不可重复读、幻读都可能出现
    	read commited(读已提交数据)：可以避免脏读
    	repeatable read(可重复读) mysql默认：可以避免脏读、不可重复读
    	serializable(串行化)：都可以避免但是性能非常低
    	
    查看隔离级别：select @@transcation_isolation;
    设置当前事务隔离级别：set session transaction isolated level 隔离级别；
    设置全局事务隔离级别：set global transaction isolated level 隔离级别；
    ```

    