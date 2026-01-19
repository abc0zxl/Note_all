### DAO（Data Access Object）

它是一种**设计模式**，用抽象，封装对数据源进行访问

1.使**业务逻辑**和**数据访问逻辑**分层

### Maven

原因：原有的java项目，使用外部的包时需要下载好，再放入到lib文件夹中，才能正常使用。这样十分麻烦

作用：maven就是未来解决这个问题而产生的，它可以不用导入具体的jar包，在他的代码中写入包名，版本即可，运行时会下载。排除了各种麻烦

# SSM

SSM 是 **Spring + Spring MVC + MyBatis** 三个 Java 开源框架的组合，也俗称**三大框架**

**Spring**：是一个框架，项目的容器，让各个工具整合在一起协同作业。管理对象。

它的核心是 **IOC（控制反转）** 和 **AOP（面向切面编程）**

**Spring MVC**：接收前端请求，处理请求，返回响应

**MyBatis**：负责数据库的交互，简化sql

![image.png](/assets/53ba1a10-c1a3-467c-8ebc-efd071764dd5.png)

# B/S

browser和Server，浏览器客户端架构

# JavaEE

指java企业版，指java企业级开发的技术规范总和

![image.png](/assets/3a478070-c7ac-4cef-8335-8773dae59825.png)

# MVC

**起因**：

* jsp+java的代码不利于解读
* 原始代码**耦合性强**

**优点**：

* 任务分功明确

### Controller

**载体**：Servlet

**作用**：处理请求，调用模型和试图

Controller 层的核心职责是 “接收请求、分发业务、返回响应”，而 Servlet 正是实现这个职责的**底层技术组件** —— 没有 Servlet，Controller 层就失去了和前端通信的 “入口”。

**例子**：

* **封装**：组合Model层的功能，实现复杂的数据处理，然后封装为一个功能
* 例如实现：**注册**（selectbyname，insert）

### Model

**载体**：JavaBean

**作用**：业务模型，业务处理，CRUD基本操作

**例子**：

* 调用访问数据：selectByName，selectAll，insert，update，delete

### View

**载体**：JSP，Servlet

**作用**：接受请求，封装数据，调用controller，响应数据

**例子**：

* **调用**：首先调用Servlet实现的controller层
* **接着调用**：接着controller层发挥作用获取到数据后，将数据返回给view层显示。

## 流程

浏览器请求会先访问cotroller层，

controller调用model获取数据

controller将数据交给view显示数据

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

# Maven Web项目创建

他是一个用于管理和构建java项目的工具，有了它就统一了一个开发目录。

## 步骤

1.项目骨架创建

* 选择Maven
* 勾选使用骨架创建
* ![image.png](/assets/9cf4e38f-f5ff-48f9-ad18-cd33ed9b9099.png)

2.删除pom.xml中的多余坐标

![image.png](/assets/bc635ccf-4875-4fb9-b939-f82944558752.png)

3.补齐缺失的目录结构（我创建的缺少一个java文件）

![image.png](/assets/16709c04-97ce-4ad0-b119-e70bae8d2b2c.png)

# AJAX

就是一种异步的JavaScript

## 前端数据交互发展

1.Servlet阶段：只能再java中写入复杂的html

2.jsp阶段：可以用<%写入java代码，实现和后端的数据交互，但是可读性比较差，java，html相互嵌套

3.Servlet+jsp阶段:相互配合，用Servlet处理逻辑封装数据，JSP获取数据，展示数据

4.Servlet+html+ajax:后续大部分的开发方式

# Vue

1.是一个前端框架，用于简化javascript中的DOM操作，简化书写

2.基于**MVVM**实现双向绑定，model-view-viewmodel

* **动态的展示**：视图变了模型变，模型变了视图变
  这个就省去了编写dom操作的代码，模型（json……），中的数据自动变，不用（byid获取，模型写入）操作。
* f

## DOM操作

1.**数据录入**：前端中一个一个数据用id导入到对象中

# Struts框架

他是一套严格基于MVC设计javaweb应用框架，

1. 依赖于ServletAPI
2.

现在已经被SpringMVC等框架替代

## Struts1

他是基于ServletAPI构建的，他的action类非线程安全，数据封装繁琐

## Struts2

基于WebWork框架构建的，他的action类是线程安全的，支持**注解**和**XML**，扩展性强，

# WebWork框架

他是一个开源的jave Web MVC框架，

1.解决早期mvc框架的高耦合，等问题

2.它**不依赖**Servlet API的特则，独立于Web容器，

3.也是严格遵循**MVC**设计模式

4.它取代了传统框架中的Filter的部分功能

5.支持**注解**，**XML**简化配置流程

# 前后端分离

它可以将一个系统开发分为两个项目，一个前端，一个后端。

**接口文档**：通过**需求分析**，**接口定义**，得到一个API接口文档。两个项目通过一个统一的**接口文档**，阅读**接口文档**显现开发。

#### YApi

他是一个高效，易用，功能强大的api管理平台。

**使用步骤**：

* 添加项目
* 添加分类
* 添加接口

## 前端工程化

**前端开发特点**：模块化、规范化、组件化、自动化

**环境准备**：

1.**脚手架**：Vue-cli用于快速生成一个vue模板，使统一目录结构

2.**安装运行环境**：安装node.js

3.**联网创建项目**：

* 新建文件夹
* 本文件夹运行cmd，输入vue ui加入图形化界面
* 预设模板：手动。
* 功能：主要要Router
* 版本：vue2
* 检测规范：ESLint with error prevention only
