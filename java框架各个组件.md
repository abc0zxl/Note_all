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

有三种生命周期

1.clean：执行后会自动执行

2.install：执行后会自动执行编译测试打包的步骤

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
