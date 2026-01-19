#### 依赖管理

Maven通过依赖声明自动下载和管理jar包，避免手动导入。依赖可配置作用域（如compile、test）、排除传递依赖，并支持分类器区分不同构建版本。文件

### .properties文件

**这个是通用的键值对格式的配置文件**

1.一个项目中不只有一个properties文件，每个不同名字的properties的文件作用不一样

2.可以

**数据库连接数据**

**各种中间件的连接数据**

**连接池大小等**

**减少修改配置带来的损失，可以不用重新编译修改**

## jar包

#### 日志log4j

log4j1是老版本，不在维护，log4j2是log4j1的升级版

1.log4j2支持动态修改

2.log4j2支持多线程

#### 日志Logback

目前最常用的一个日志

## Maven

原因：原有的java项目，使用外部的包时需要下载好，再放入到lib文件夹中，才能正常使用。这样十分麻烦

作用：maven就是未来解决这个问题而产生的，它可以不用导入具体的jar包，在他的代码中写入包名，版本即可，运行时会下载。排除了各种麻烦

1.提供了一套标准的项目结构

2.标砖的构建流程（编一，测试，打包，发布……）

3.提供了一套依赖管理机制

### 痛点

**项目的结构问题**：eclipse，myeclipse，idea等他们创建的项目结构都不一样

**解决**：Maven提供了一个标准的项目结构，所有编程软件创建的maven项目结构就一摸一样了

![image.png](/assets/4e033de2-5034-48ce-addc-9947c28432c9.png)

### 常用命令

1.**compile**：编译

2.**clean**：清理

3.**test**：测试

4.**package**：打包

5.**install**：安装

#### 辅助插件Maven helper

### 生命周期

主要有5个阶段

1.clean：执行后会自动执行

2.compile：编译项目源代码

3.test：使用合适的单元测试框架运行测试

4.package：将编译后的文件打包。

5.install：安装项目到本地仓库

……

## XML（extensible,markup,language）

可扩展标记语言

**作用**

1.**保存数据**：解决数据在载体中数据太大的问题

2.**传输数据**：数据包的传输

3.**配置文件**：

**特点：**

1.平台无关

2.他90%的语言都支持xml（c,java，xml发布之后出现的语言）

3.具有自我描述性，所有**标签**都可以自定义，但是会产生协作冲突（看不懂）的问题。

![image.png](/assets/0e528f50-c6d0-4a18-a4f7-9b684ca01294.png)

4.**但是也有他们官方固定好的标签，作用于特殊的功能**

这个都是MyBatis-e-mapper.dtd文件中的方法，也可以说是**接口功能**

**语法**

1.必须有根元素，像html中标记对。

2.他的标签**有开必有合**

3.对大小写敏感

4.正确的嵌套

5.属性必须加引号（单引号，双引号）

![image.png](/assets/ebf39315-517d-46fc-a2b3-82e024a0dab4.png)

### 应用

#### CDATA

在xml中书写字符时，可能会和标签符号冲突，可以用cdata来框住这个部分

![image.png](/assets/9167045e-81be-4a89-b1b0-1f8f8efc6eb5.png)

### 语法统一(DTD)

由于xml可以自定义标签名，导致协作的问题

#### 官方统一

但是也有他们官方固定好的标签，作用于特殊的功能

这个都是MyBatis-e-mapper.dtd文件中的方法，也可以说是**接口功能**

#### 自定义的统一标签

后缀也是**.dtd**

#### XSD

是dtd的替代品

### 解析XML

方法DOM，SAX，JDOM，DOM4J，前两种属于官方的方法，后两种属于扩展方法。

**1.DOM解析**

在解析xml时，会将所有元素按照层次顺序，在内存中构造出树形结构。

**优点**：可以便利修改结点

**缺点**：内存压力较大，解析较慢

**2.SAX解析**

**优点**：比xml解析更快

**缺点**：不可以修改结点

### 可以遍历xml中的元素

关键字：root，Element

![image.png](/assets/de0bdef4-6cf0-4b70-8057-826cff08aee9.png)

getName是获取标签名字，getData是获取标签里的内容，他俩都是用来显示的。

输出：

id:1

name:kobe

age:38

![image.png](/assets/9b09cddc-9e8d-43a2-9d89-bf0c0f8ffc28.png)

### POM.xml

是一个用于解析xml的一个依赖**jsoup**，有很多不同的版本。这次的pom.xml就是专门用于同一各个平台的项目结构（maven）中的一个依赖，参数管理文件。

**结构**：

1.项目对象模型（再pom中），在pom中有一个字段说明了这个项目，是唯一的。

2.依赖管理模型（在pom中），仓库中自动调取依赖。

（先在**本地仓库**找，没有再去**中央仓库**找）

![image.png](/assets/37a5d8f4-966a-47bd-bf1b-531da24d2bfc.png)

#### 依赖的结构

![image.png](/assets/da85b60f-9f03-417e-b4fe-7dd618904deb.png)

## 依赖声明

![image.png](/assets/8ad56e72-2ea0-4017-b89e-34563f8a2f57.png)

```
<dependency>
    <!-- 必填：依赖的“组ID”（通常是公司/组织的域名反转，如com.alibaba） -->
    <groupId>依赖的组ID</groupId>
    <!-- 必填：依赖的“ artifactID”（通常是项目/模块名，如fastjson） -->
    <artifactId>依赖的模块名</artifactId>
    <!-- 必填：依赖的版本号（如2.0.3） -->
    <version>依赖的版本号</version>
  
    <!-- 可选：依赖的作用域（控制依赖在哪些阶段生效） -->
    <scope>作用域（如compile/provided/test）</scope>
    <!-- 可选：排除传递依赖（解决冲突时用） -->
    <exclusions>
        <exclusion>
            <groupId>要排除的依赖组ID</groupId>
            <artifactId>要排除的依赖模块名</artifactId>
        </exclusion>
    </exclusions>
    <!-- 可选：依赖的类型（默认是jar，也可以是war/pom等） -->
    <type>依赖类型（默认jar）</type>
    <!-- 可选：依赖的分类器（区分同一版本的不同构建，如jdk17版本的jar） -->
    <classifier>分类器（如jdk17）</classifier>
</dependency>
```

# JSON

它是一种javascript的对象表示法

**优点**

* 层次简单
* 作为数据载体：用于数据传输

**语法**：

* **双引号**：他的键必须要有双引号
* **数据据类型**：
  1.数字
  2.字符串
  3.bool值
  4.数组
  5.对象
  6.null
* **变量结构**：有一个一个键值对组成

  ![image.png](/assets/401bb05c-88de-414c-aca8-55df552ffa31.png)
* **调用**：变量名.键名
* **数据转换**

  1.**步骤**：xml导入坐标com.alibaba->fastjson

  2.**java->json**：String json1=JSON.toJSONString(obj);

  3.**json->java对象**：User user=JSON.parseObject(jsonStr,User.class);
* **java中写json对象**：要注意双引号，非边界的双引号**必须要用转义**

# 框架和架构

这个是两个不同的东西，**架构**是设计思想，**框架**是落地的工具。

1.**架构**：他是一种抽象的思想，比如**分层架构**，**业务流程**。

* MVC
* 微服务架构
* 分层架构

2.**框架**：是一种可以落地的软件代码集合，开发工具，有具体的代码。

* Spring，
* MyBatis
* Hibernate，
* SpringBoot

# Hibernate框架

他是一个Java持久层ORM框架，明确位于分层架构中的**持久层**（DAO），简化了原来的JDBC的操作

# ORM思想

Object-Relational-Mapping,对象关系映射。

他是对JDBC的封装和简化。

他是一种设计思想，解决**面向对象模型**和**关系型数据模型**之间的问题

1.**java对象**与**数据库表**之间的**映射关系**

2.屏蔽对象与数据库之间的细节

3.ORM是一个思想内核

**Hibernate,Batis,Spring Data JPA**等是基于**ORM思想**的**具体框架**

## 全自动ORM

这个指的是Hibernate框架，适用于小型项目，各种管理系统，追求快速开发，对性能无要求，数据库关联比较复杂的情况

1.他会**自动生成**常见的CRUD的sql语句

2.无需关注sql的细节直接传递对象和数据库交互

3.但灵活度低

4.**弱绑定**：各种数据库可以相互切换

5.学习成别高，要掌握缓存机制，联级操作等

## 半自动ORM

这个如MyBatis框架，适用于大型项目，各种金融，商城，平台，对性能有机制要求，要精准优化，要编写复杂的sql

1.他不会自动生成sql，需要手动编写sql语句。

2.灵活度高

3.**强绑定**：编写的sql只能适应一种数据库

# JPA标准

Java Persistence API

他是一种**规范，标准**，规范了java对象和数据库表之间的映射关系。仅提供了一套规范，不提供实现方法。

**解决**：早期 ORM 框架（如 Hibernate、TopLink）各自为战，API 不统一，开发者切换框架成本高，因此 Java 官方制定了 JPA 规范，统一 ORM 框架的使用标准。

1.为后来的ORM框架开发提供标准。

## Spring Data JPA框架

他是对JPA规范的进一步封装，**简化和增强**。

他基于JPA规范，但不提供底层的ORM实现方法。他的运行要依赖于Hibernate。


| JDBC      | 底层 API 标准（工具集） | Java 官方提供的操作关系型数据库的**基础接口 / 规范**，是 Java 与数据库交互的最低层标准 | 是（但开发效率极低）         |
| --------- | ----------------------- | -------------------------------------------------------------------------------------- | ---------------------------- |
| ORM       | 软件设计思想（模式）    | 「对象关系映射」的抽象理念，无具体代码，核心是建立 Java 对象与数据库表的一一映射       | 否（仅指导开发，无实际实现） |
| JPA       | ORM 规范标准（接口集）  | Java 官方基于 ORM 思想制定的**ORM 统一规范 / 接口**，定义了 ORM 的核心标准和 API       | 否（仅提供规范，无底层实现） |
| Hibernate | ORM 具体框架（实现类）  | 完全遵循 JPA 规范，同时也是 ORM 思想的**落地实现框架**，是 JPA 规范的主流实现          | 是（可直接引入项目使用）     |

# Vue项目-目录结构

![image.png](/assets/0cbab111-b07e-4bb3-b307-81f12989e077.png)

# Spring的框架目录

### SpringFramework

1.**dao**：存放对数据库操作的代码，全称Data Access Object,这个运用于传统的JDBC原生操作，不同于mapper的接口+xml注解，这个完全是实现类。

2.**entity**：是存放实体类的地方

3.**impl**：这个是dao，service等文件夹中用于定义接口内容的文件夹

4.**controller**：它会调用service层的接口实现功能

### SpringMVC

1.**POJO**：有点像entity，bean，是一个实体类，要用的时候创建其对象，然后获取参数。他是个普通的java类，也是javaBean，需要用@Data注解，声明一下
