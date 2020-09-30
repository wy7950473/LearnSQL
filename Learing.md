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
5.MySQL的优点
	5.1 成本低:开放源代码，一般可以免费试用
	5.2 性能高:执行很快
	5.3 简单:很容易安装和使用
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