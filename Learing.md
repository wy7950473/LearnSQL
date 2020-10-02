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
	# 设置mysql客户端默认字符集
	default-character-set=utf8 
	[mysqld]
	#设置3306端口
	port = 3306 
	# 设置mysql的安装目录
	basedir=D:\\softnew\\MYSQL\\mysql-5.7.20-winx64
	# 允许最大连接数
	max_connections=200
	# 服务端使用的字符集默认为8比特编码的latin1字符集
	character-set-server=utf8
	# 创建新表时将使用的默认存储引擎
	default-storage-engine=INNODB
8.MySQL服务的停止与启动
	8.1 停止（Windows）: net stop "MySQL服务名"
	8.2 启动（Windows）： net start "MySQL服务名"
9.MySQL服务的登录和退出(Windows)
	9.1 登录:mysql -h (主机) -P (端口号) -u (用户名) -p(密码)
	9.2 退出：exit
10.MySQL的常见命令
	10.1 显示存在的数据库: show databases;
	10.2 打开指定数据库: use "数据库名";
	10.3 显示当前数据库中存在的表: show tables;
	10.4 显示指定库的表: show tables from "数据库名"；
	10.5 查看当前所在的库:select database();
	10.6 创建表 create table “表名”(字段名 字段类型，字段名 字段类型(字段长度));
	10.7 查看表的结构:desc "表名"；
	10.8 查看数据：select * from “表名”；
	10.9 插入数据:insert into “表名" (字段名，字段名) values（字段值，字段值）；
	10.10 修改数据: update “表名” set 字段名=字段值 where 条件；
	10.11 删除数据: delete from “表名” where 条件； 
	10.12 查看数据库的版本：在客户端(select version())、不在客户端(mysql --version/mysql -V);
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
escape '符号'(把指定符号定义为转移符)
		12.2.4 between and:可以提高语句的简洁度、包含边界值、两个值的顺序不能颠倒
		12.2.5 in:可以提高语句的简洁度、值类型必须统一(兼容)、不支持通配符
		12.2.6 is null/is not null:=和<>不能判断null值
		12.2.7 安全等于( <=> ): 可以用于判断null值和普通类型的值