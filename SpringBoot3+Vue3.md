# 手动搭建SpringBoot项目

**技术**：

1.后端

* Validation
* Mybatis
* Redis
* Junit
* 项目部署

2.前端

* Vue
* Router
* Pinia
* Element-plus

#### 从Maven开始搭建

1.选择Maven创建项目，

2.选择导入的库，quicksts

3.创建工程

4.**在pom.xml**中写一个父工程，这是固定的

根据笔记内容，**在 `pom.xml` 中写一个父工程**是 SpringBoot 项目搭建的固定步骤，具体做法如下：

### 1. **父工程配置**

在 `pom.xml` 中声明 SpringBoot 的父工程依赖，这可以统一管理项目的依赖版本，避免版本冲突。配置示例如下：

根据实际需求选择版本 -->
<relativePath/>  从仓库查找，不继承本地父工程 -->
</parent>

```

### 2. **作用说明**
- **版本管理**：父工程定义了 SpringBoot 及相关依赖的默认版本，无需在子依赖中重复指定。
- **插件配置**：内置了 Maven 编译、打包等插件配置（如 `spring-boot-maven-plugin`）。
- **简化配置**：提供了默认的资源配置和依赖管理，减少冗余配置。

### 3. **注意事项**
- 版本选择应与项目技术栈兼容（如笔记中使用了 MyBatis、Redis 等）。
- 如果已有父工程（如公司内部项目），可能需要调整或继承其他父工程。

### 4. **后续步骤**
配置父工程后，继续在 `pom.xml` 中添加项目所需依赖（如 `spring-boot-starter-web`、`mybatis-spring-boot-starter` 等），并编写全局配置文件（如 `application.properties` 或 `application.yml`）。

如果需要更详细的代码示例或问题排查，请进一步提问！
```

```xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.7.0</version> 
```

![image.png](/assets/5fcf3c31-0fb4-4983-9ef6-c7c2acb4c94e.png)

5.导入依赖,自动类型依赖不用写版本号

* starter-web
* mybatis-spring-boot-starter
* mysql-connector-j

6.编写全局配置

* mysql的配置信息
* ![image.png](/assets/1df8180c-c605-41ce-a2be-c06f2539ea7e.png)

7.搭建文件夹框架

8.编写启动类

* 注解SpringBootApplication
* SpringApplication.run(AAA.class.args)

#### properties代码

1.设置端口号：sever.port:

2.设置虚拟目录：server.servlet.context-path:

3.第三方非约定配置信息：

* AAA.user:
* AAA.code:
* AAA.host:

3.第三方配置（数据库）：spring:datasource:

* driver-class-name:
* url:
* username:
* password:

#### 发送邮件

1.**导入依赖**：org.eclipse.angus《》jakarta.mail

2.**编写工具类**：需要新建一个文件夹utils，创建一个MailUtil.java的文件

![image.png](/assets/9757d302-b17d-4795-a7d7-49416eedd1aa.png)

3.**编写service**：由于不涉及数据库操作，所以看起来像bean，注意记得把他们的方法都弄出来。get,set

![image.png](/assets/44bd6fcb-cab4-47ba-9535-2d0fdf80eb7a.png)

4.**编写controller**：

![image.png](/assets/15b55450-356f-4a79-904c-bfa4641538dc.png)

5.**改进配置信息**：

* 将数值类信息放到配置文件中
* **获取信息**：通过@Value("${AAA.user}")获取
* **改进绑定信息方式**：用@ConfigurationProperties（prefix="AAA"）写入相同层级的名字，这个方式需要将变量名和配置类名字匹配相同

# SpringBoot整合MyBatis

1.正常搭建mybatis框架

2.mapper接口注入到ioc也可以用注解@Mapper

3.**编写第三方配置**：

![image.png](/assets/d2cbef56-eb56-4a7d-90c2-e5efcb79e419.png)

### Bean扫描

1.**标签扫描**

2.**注解开启扫描**

### Bean注册

* Component
* Service
* Controller
* Resiponse
* 第三方非自定义bean的注册，

  **第一种方法**：@Bean

  **第二种方法**：@Import

#### @Bean注解

这个可以将自定义的bean注册到ioc种，方法是

1.这个bean方法的文件必须是一个配置文件（有@ConfigurationProperties）

2.在方法上声明@Bean,即可完成注入

3.**测试方法**：直接调用这个bean创建对象，看有没有放到ioc种

![image.png](/assets/51c7d3f0-1f5b-4e47-b7b3-265b4877e5fb.png)

#### @Import注解

它可以导入**配置类**和**接口实现类**

原来的@Bean扫描的位置和启动类同级

如果不同级了，就会导致扫描不到，这时就需要用到@Import了

直接在启动类上写下@Import+文件名字就能识别内部的@Bean完成注入

##### 组合注解

1.定义一个注解类，

2.然后将常用注解导入，

3.然后就可以用一个注解完成原来的多个注解。

#### 条件注释@Conditional

1.当配置文件种存在对应的属性

![image.png](/assets/025db269-7b5c-4d6f-81f8-33bcf9942427.png)

2.当不存在当前类型的bean时

3.当环境存在指定的这个类时

### 手动注入Bean

上面讲到的@Bean和@Import都不是自动装配

### 自动装入配置

最重要的注解@EnableAutoConfiguration

# 开发模式

1.接口文档

前后端配合的东西

**步骤**：

* 明确需求
* 阅读接口文档
* 思路分析
* 开发
* 测试

**接口文档示例**：

![image.png](/assets/b071da1f-0a73-46c8-b245-44ba6d0e183f.png)

# 宠物补给站-系统

**应用场景**：当今世界孤独经济开始盛行，宠物店越来越多，除了卖宠物一方面，还有宠物的食物也是很重要的一方面，这个宠物补给站，是专为宠物粮食定制的一个分类和推荐系统，便于快速寻找到想要的宠物粮食，或者宠物用品。

**功能**：目前专注于猫咪的食品分类。

**分类标准**：两级分类，猫咪种类，食品分类

## 数据库设计

用户：

* 用户id
* 用户名
* 用户邮箱
* 用户手机号
* 用户密码
* 用户头像
* 创建时间
* 更新时间

商品：

* 商品id
* 商品名字
* 商品描述
* 商品价格
* 商品图片
* 商品功效String
* 商品分类
* 商品库存
* 商品状态
* 创建时间
* 更新时间

类别管理：

* 分类id
* 分类名称，用于类别描述
* 分类类别，用于外部选择
* 创建时间
* 更新时间

## 用户

##### 创建Bean目录文件

1.**Bean文件**：

lombok它可以在编译阶段，为实体类自动生成setter,getter,tostring方法

* **添加依赖**：org.projectlombok
* **实体类上添加注解**：@Data

然后就不用自己编写setter，getter，tostring都不用自己写了

2.**Result文件**

它用于输出操作后的结果信息，将所有接口的返回值都设为result

* **业务状态**：
* **提示信息**：
* **响应数据**：泛型
* ![image.png](/assets/78909258-0e3d-4489-83c1-d0c05a25b3e9.png)

### 注册功能

**输入**：用户名，密码，邮箱，手机号，再次输入密码

##### 注意register插入用户的操作

在service种需要加密密码，再去存储

**加密**：

* **用专用的工具类**：Md5Util

##### Mapper实现

1.**直接传入参数方式**：

* sql语句要注意声明一下要插入哪些参数，因为有些参数是后期添加的
* ![image.png](/assets/54449db4-700d-4870-ab89-e05059e43937.png)
* 这种方式比较生硬

2.**传入对象方式**：

## 测试功能

用postman

**步骤**

1.**创建工作空间**：左上角workspace

2.**创建名字**：一般就是这个项目名字

3.**导入测试用例**：这个项目是跟着别人做的，左上角import

# 以上用到的技术

自动生成setget：Lombok依赖

接口测试结果：Result.java

密码加密：Md5

测试：postman

## 登录

## 注册

## token生成

## 拦截器验证

## 获取用户信息

由于每次请求都带有jwt，里面包含加密的用户名，解析后通过用户名查找就可以了。

1.**获取token**：通过request获取

2.**解析token**：获取里面的用户名

3.**调整敏感信息**：像密码有时候不应该获取过来，又因为前端获取到的是一个json，所以可以在实体类的密码属性上面添加一个注解

@JsonIgnore：表示改属性被转换为json时被忽略。

4.**获取用户详细信息**：

**问题**，mapper中的查找用户方法虽然成功运行了，但是有些字段还是没有获取出来，这是因为属性名称和实际名称不同导致的。因为没有编写获取这些参数的操作，知识告知要返回一个对象。

5.**配置名命转化配置**：在全局配置中，打开这个名命转换，但是仅仅限于部分转化

* 驼峰名命
* 下划线名命
* ……
* ![image.png](/assets/af062f9a-3a5c-4e9a-8f0c-e1c56cabba49.png)

6.**升级版利用token获取用户名**：在后续代码中只要想获取用户都需要编写解码逻辑。太繁琐了，

* 利用拦截器在内部拦截器执行解码后的数据，然后获取用户名字
* 这里用到了线程的知识，因为线程是由工具类触发的，所以在内部已经实现了一套线程的识别逻辑，不会混乱。
* 这里会用到一个工具类ThreadLocalUtile.java
* 创建他的对象，调用set方法把数据存入线程
* 拦截器pre通过后，在controller就可以利用这个线程get到这个参数实现参数的传递。

## 更新信息

更新信息传递的是一个对象的时候。

#### 实体参数的校验

当传递的参数是一个对象时，就不能用原来在参数旁边的validation方法了，可以利用尸体参数校验的方法。

@NotNUull：表示这个参数不能为空

@NotEmpty：表示这个参数，以及string类不能为null

@Email：这个是邮箱的专属注解，也有非空的意思。

@Pattern:(regexp=""):这个是validation的方

#### postman

由于来回传递对象用的是json，而且是修改信息

**参数位置**：

1.所以参数信息应该放在json中，而不是header

![image.png](/assets/88fb67b2-a8e8-4227-bf56-41c9821133c4.png)

## 设置更新时间

有两种方式

1.**mysql提供的**：在sql语句上编写

![image.png](/assets/d293cc2b-cf3d-4205-9139-59961699f0aa.png)

2.**在controller生成时间**：

![image.png](/assets/f62c6042-f66f-4fdf-b912-cd7de2f37ce4.png)

3.**注意**

* 像这种能导入LocalDateTime.new()的属性，他们再实体类中都是LocalDateTime类型。不然会报错

# 接口已经编写完毕

# 实现接口和前端的交互

这个Vue要放到项目里面和springboot放一起

1.**实现跨域请求**：由于vue访问的是controller中的接口

2.**加人跨域注解**：@CrossOrigin
