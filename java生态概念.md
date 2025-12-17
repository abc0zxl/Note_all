### DAO（Data Access Object）

它是一种**设计模式**，用抽象，封装对数据源进行访问

1.使**业务逻辑**和**数据访问逻辑**分层

### Maven

原因：原有的java项目，使用外部的包时需要下载好，再放入到lib文件夹中，才能正常使用。这样十分麻烦

作用：maven就是未来解决这个问题而产生的，它可以不用导入具体的jar包，在他的代码中写入包名，版本即可，运行时会下载。排除了各种麻烦

# SSM

SSM 是 **Spring + Spring MVC + MyBatis** 三个 Java 开源框架的组合

**Spring**：是一个框架，项目的容器，让各个工具整合在一起协同作业。管理对象。


它的核心是 **IOC（控制反转）** 和 **AOP（面向切面编程）**

**Spring MVC**：接收前端请求，处理请求，返回响应

**MyBatis**：负责数据库的交互，简化sql

# MVC

### Controller

Controller 层的核心职责是 “接收请求、分发业务、返回响应”，而 Servlet 正是实现这个职责的**底层技术组件** —— 没有 Servlet，Controller 层就失去了和前端通信的 “入口”。

### Model

### View

# XML

在eclipse中创建的javaweb项目，默认是无xml的，在现在的eclipse中默认启动的是servlet3.0模式，用的是**注解模式**

如果想写xml有两个方法

1.添加Maven

创建maven时，选择javaweb项目，自动就有xml。

2.手动填充xml的核心内容

<?xml version="1.0" encoding="UTF-8"?>

<projectxmlns="http://maven.apache.org/POM/4.0.0"

xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"

xsi:schemaLocation="http://maven.apache.org/POM/4.0.0

http://maven.apache.org/xsd/maven-4.0.0.xsd">

<!-- 基础配置 -->

<modelVersion>4.0.0</modelVersion>

<groupId>com.xxx</groupId><!-- 你刚才填的Group Id -->

<artifactId>javaweb-demo</artifactId><!-- 你刚才填的Artifact Id -->

<version>0.0.1-SNAPSHOT</version>

<packaging>war</packaging><!-- JavaWeb项目必须是war包 -->

<name>JavaWeb-Demo</name>

</project>

**上面这个是代码**

## **Eclipse启动**

要从index.jsp主页开始启动tomcat才行

JavaWeb 项目依赖 Servlet 容器（Tomcat）提供的运行环境，**直接运行 Java 文件**（如右键→Run As→Java Application）会缺失容器环境，必然报错。

### CRUD

是计算机领域的一个**最基本的程序操作**的简称

create

read

update

delete

## java生态发展路线

### java原生


| 基础层     | Java SE            | 所有 Java 开发的语言基础     |
| ---------- | ------------------ | ---------------------------- |
| Web 基础层 | JavaWeb（Servlet） | Web 开发的底层规范           |
| 核心框架层 | Spring Framework   | Spring 生态的 IoC/AOP 核心   |
| Web 框架层 | SpringMVC          | 基于 Spring 的 Web 请求处理  |
| 简化开发层 | SpringBoot         | 简化 Spring 配置，开箱即用   |
| 分布式层   | SpringCloud        | 基于 SpringBoot 的微服务套件 |

### spring

而 Spring Framework 是这个生态里**最基础、最核心的底层框架**（是 “根”），所有 Spring 相关技术都基于它的 IoC/AOP 核心能力构建，没有它就没有后续的 SpringMVC、SpringBoot、SpringCloud。

## JDBC

是java语言操作关系型数据库的一套API，

1.可以操作多种数据库mysql，oracle，db2

2.变更数据库不用变代码，更改相应的驱动**jar包**就好

![image.png](/assets/4e9c3659-fb4a-4aa0-89cf-e8c49164e914.png)

**1.注册查询：**

Class.forName("com.mysql.jdbc.Driver");

**2.设置连接对象**

String url="jdbc:mysql://**127.0.0.1:3306**/db1?useSSL=false";

默认情况下是3306，也就是说可以简化上面加粗的数字

**参数设置**：是放在url字段？后面的部分，用&隔开

安全连接SSL：需要复杂配置，不用可以false掉

String username="root";

String password ="1234";

Connection conn=DriverManager.getConnection(url,username,password);

**3.定义sql执行语句**

String sql="update account set money=2000 where id=1";

**获取一个执行sql的对象**

Statement stmt=conn.createStatement();

**执行sql**

int count =stmt.executeUpdate(sql);

**释放资源**

stmt.close();

conn.close();

### 注意

1.如果你用 MySQL 8.0+，驱动类是`com.mysql.cj.jdbc.Driver`（旧版`com.mysql.jdbc.Driver`已过时，可能报错）；

### 配置运行步骤

在有项目文件夹的情况下

1.建立一个放jar包的文件夹（或者lib）

2.导入jar包

### Connection执行事务

他可以执行sql事务

重要性：当这个sql语句执行到中途发现执行错误（因为事务是好多个sql一起执行），就要利用**connection事务**的回滚，返回原来的状态

![image.png](/assets/f30f8a7f-a568-4114-842f-ce5b5510712c.png)

### Statement数据库操作接口

1.executeUpdate：增删改操作

2.executeQuery：查询操作

**修改数据时**：这个语句的执行完后会返回一个bool值，可以判断是否执行成功（用于返回给用户提示）

**删除数据时：**删除成功不一定返回”1“

![image.png](/assets/356360ab-03f6-4b6b-9c3d-d0885f5a3449.png)

### ResultSet结果集对象

他执行DQL（Data query language）语句

1.**next（）**：将数据库光标向前移动一行，返回bool

2.**getxxx（）**：获得数据

![image.png](/assets/e8b78b27-5dba-491d-baf6-9f321622cc94.png)

#### 容器思想ArrayList

例子：系统中各种列表的显示

1.定义列表对象（一行一个）Account:

2.查询数据，存入这个对象

3.将这些Account存入ArrayList中就可以集中显示了

### PreparedStatement

预编译SQL语句

1.预防sql注入

2.加速了sql的执行速度，因为预编译了

开启：useServerPrepStmts=true;

#### SQL注入

指通过操作输入来**修改操作好的sql语句**，达到执行代码对服务器攻击的方法，

**原因**：输入密码和原sql语句拼凑成了其他sql语句

![image.png](/assets/51c48280-3f95-4047-933f-109376c4379a.png)

![image.png](/assets/f27e2808-c3ff-4fd1-ade1-dde98afaa550.png)

#### 解决SQL注入

提前把sql放到特殊对象并执行，原理就是把里面的单引号，各种符号转义为文本格式，

1.用**问号**替代原来的**字符串替代**

2.创建preparedstatement对象执行这个sql

3.设置这个对象的sql中**问号**的值

4.用executexxx()执行这个语句

### 数据库连接池

类似于线程池

1.资源复用

2.提升数据库响应速度都

3.避免数据库的连接遗漏（当连接池连接对象用完了后，会查看对象，强制停止异常的连接对象，并把对象资源分配给新的连接）

#### 使用方法

**接口**：DataSource

方法：getConnection()

常见连接池：Druid(德鲁伊，最好)，C3P0,DBCP

1.导入jar包

2.定义加载配置文件

3.获取连接池对象

```
        Properties prop=new Properties();
        prop.load(new FileInputStream("src/druid.properties"));
        DataSource data=DruidDataSourceFactory.createDataSource(prop);
        Connection conn=data.getConnection();
        System.out.println(conn);
```

**找文件路径**：System.out.println(System.getProperty("user.dir")):

### JDBC实践

1.编写数据库

2.创建实体类

3.编写操作功能

#### 编写数据库操作

##### 查询

1.获取连接

2.定义sql执行语句

3.获取properStatement对象

4.执行sql

5.处理结果

6.释放资源
