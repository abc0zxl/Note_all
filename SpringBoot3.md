# 约定大于配置

**注意**

1.**启动页面**：是那个调用run的文件

## 历史

公司：pivota

1.2008年收购了tomcat Apatch servlet，然后改进了原来的web.xml方式。

2.**收购Spring VMware**

3.**收购RabbitMq，redis**

##### 2014年发布SpringBoot

2018：SpringBoot2

##### 2015年发布Spring Cloud

##### 上市

**特点**：

1.基于Spring开发，继承了原来的优秀特性

2.目的是简化原来的初始搭建以及开发过程

* 提供了默认的配置等方式直接简化开发模式

3.集成了大量的常用第三方配置库，radis，mongoDB，Dubbo等。**开箱即用**，专注于业务开发

4.**自动配置**由于他大量集成了框架，使得**依赖包并不冲突，引用不稳定性**得到了很好的解决

5.**build anything**：

6.内嵌了Tomcat,Jetty Undertow等，不用再部署一个Tomcat服务器

7.**自动配置依赖**：提供了Startes POMs来简化Maven配置和减少版本冲突带来的问题,原来要配置POM.xml，要关心哪些要配置哪些不配置，版本问题等，现在它帮我们自动完成了配置，不用手写依赖了。

# SpringBoot为什么那么厉害

为何能替换掉原来的SSM等框架，而重新学习一套新的框架

**问题**：

* 原来的应用大多采用**单体架构（All in one）**：将所有的功能打包成一个独立应用程序，就是说一个项目就是一个大盒子，将suo'you的功能都装到这里面了。打包成一个独立运行的应用运行。做负载均衡时比较复杂。
  **缺点**：如果要负载均衡，多个模块就要搭建多次。版本控制，协作开发，单一模块等都在一个项目中。

  **优点**：部署简单，不用考虑多个服务之间的互调，把一个包上传到服务器就好了，水平扩展比较方便。
  所以**在高用户使用的场景**催生了SpringBoot的发展，在没有那么高的并发场景下单一架构更有优势。

  **解决**：Netflix，

1.直接简化了Spring的开发（初始框架配置搭建）

2.业务场景的需要，SpringCloud和SpringBoot相互促进

# 常用注解

1.**@Documented**：当你用 `javadoc` 命令生成项目文档时，被 `@Documented` 修饰的注解，会**被包含在它所修饰的类 / 方法的文档说明里**，让阅读文档的人知道这个类 / 方法使用了该注解。

2.**@Inherited**：让注解能被子类继承，如果用在父类上，那么它的**子类会自动继承这个注解**

3.**@Conditional**：条件注解***

* **第一步**：创建一个用于判断的java文件
* **第二部**：实现接口Condition，继承它的方法，通过返回值就能判断

4.**@Import**：导入类方法

5.**@RestBody**：用于表示将方法的返回值变成json等格式，不在当作html等的名字作为跳转了，直接将返回值放到页面上，而不用非要到一个特定页面上

6.**@RetentionPolicy**：用来声明该注解标注的类  ，编译后以什么方式保留

7.**@SpringBootConfiguration**：用来声明他标注的类是一个配置类

8.**@ComponentScan**：它里面可以放很多排除方法 excludeFilters

9.**@EnableAutoConfiguration**：开启自动配置类注解

# SpringBoot原理

前置知识：SSM框架的使用经验，熟练使用Maven，idea的使用

**环境需要**：

* **JDK17**：因为springboot3是基于jdk17来配置的
* **springFramework6**：原始spring6的依赖

1.**pom依赖**：

需要frameword，webmvc，context，aop，core，tomcat

![image.png](/assets/7923c255-e057-4843-b12d-e4beadd605a3.png)

#### 一个项目中如何写入多个模块

一个主模块，一个user模块继承主模块里面的依赖，注意要和父亲目录平级，

主目录的xml的model标签的地址要记得加../User表示和它平级

1.有三个项目

* 第一个父项目，用的是maven
* 第二个用java-maven项目
* 第三个用java-maven项目继承父类

  ![image.png](/assets/62c454d2-e858-4c35-94f8-da37def82e8b.png)

![image.png](/assets/6ef057a9-b7d6-49e3-8bf9-ba8a122fb555.png)

以上创建了两个模块Spring Boot1，User3

##### **在SpringBoot1下**：创建一个自定义注解

![image.png](/assets/6f6ee533-d874-4e68-b94f-95cc78ab514e.png)

##### **声明这个注释**：

![image.png](/assets/85b83206-5918-4b25-be07-6d0761622e05.png)

##### 在User3中org下写Spring启动的方法

这个启动就可以调用controller

然后能在浏览器上看到效果。

###### 步骤

**步骤一**：启动Tomcat在springboot1下的run方法中写入startTomcat()的方法，**用java代码的方式启动**，代码直接摘抄

* ```
  pr
  ivate static void startTomcat() {
         // 1. 创建 Tomcat 实例
         Tomcat tomcat = new Tomcat();

         // 2. 获取 Tomcat 服务器和服务
         Server server = tomcat.getServer();
         Service service = server.findService("Tomcat");

         // 3. 创建并配置连接器（端口 8081）
         Connector connector = new Connector();
         connector.setPort(8081);

         // 4. 创建并配置引擎
         Engine engine = new StandardEngine();
         engine.setDefaultHost("localhost");

         // 5. 创建并配置 Host
         Host host = new StandardHost();
         host.setName("localhost");

         // 6. 创建并配置 Context
         String contextPath = "";
         Context context = new StandardContext();
         context.setPath(contextPath);
         context.addLifecycleListener(new Tomcat.FixContextListener());

         // 7. 组装容器结构
         host.addChild(context);
         engine.addChild(host);
         service.setContainer(engine);
         service.addConnector(connector);

         // 8. 加载 SpringMVC 的 ApplicationContext
         XmlWebApplicationContext applicationContext = new XmlWebApplicationContext();
         applicationContext.setConfigLocation("classpath:springmvc.xml"); // 你的 SpringMVC 配置文件路径

         // 9. 注册 DispatcherServlet
         tomcat.addServlet(contextPath, "dispatcher", new DispatcherServlet(applicationContext));
         context.addServletMappingDecoded("/", "dispatcher");

         // 10. 启动 Tomcat
         try {
             tomcat.start();
             tomcat.getServer().await(); // 阻塞主线程，保持服务运行
         } catch (LifecycleException e) {
             e.printStackTrace();
         }
     }
  ```

**最后10的作用最关键**：负责向tomcat添加一个dispatcherserlvet（视图解析器）

* **添加参数**：目的为了寻找controller，在dispatcherservlet后有一个容器，用来放这些注解，所以在staticTomcat的参数写入一个Webappliationcontext的容器。
* **从run创建容器，并调用tomcat**：有两种容器，一个支持web端，一个没有web端
  AnnotationConfigWebApplicationContext和AnnotationConfigApplicationContext
* **给容器注册配置类**：将run传入的class当作配置类(register)，并启动(refresh)

#### 关于class导入的方面

在run调用的文件中这个class会解析当前这个类下的@bean或者打类上面的@自定义注解

1.**解析原理**：如果解析的是自定义的注解，他会找到注解的这个注解源头，如果上面有关于扫描的注解，它就会默认扫描spring当前解析的类，如果没有它就会去扫描他这个类下的包，然后就会扫描到@controller

#### 多态

如果不想用tomcat，可以用一个多态来获取，tomcatserver或者JettyWebServer

![image.png](/assets/f83b8f38-e757-4be6-bd5a-e28379a46513.png)

#### 创建一个用于自动转换启动器的我就

定义一个条件，在定义的条件下去启动不同的启动器

* 定义条件判断文件（继承Condition）
* 定义判断语句：通过依赖是否存在判断，是否有tomcat依赖，在Localclass中，写入判断文件中
* **导入这个自动导入类**：@Import导入这个类

### 自动配置类

## SpringBoot原理2

##### 搭建SpringBoot

1.**第一步**：创建Spring Initial，选择maven，jdk17

2.**第二步**：导入依赖，选额web下的springweb

3.**第三步**：编写controller，

4.**第四步**：找到run文件，直接启动运行

### 优点

1.搭建速度快

2.自动把所有jar包添加好了

3.内置tomcat无需配置tomcat

4.场景启动器stater,可以代替多种依赖场景自动导入依赖

![image.png](/assets/cc5d058e-75c5-4308-ab92-e3aed05da82a.png)

5.对Spring和第三方库提供了默认的配置，不需要编写任何的配置。

* 因为它有各种各样的自动配置类

##### 基本框架

![image.png](/assets/d5e6f2ef-eddb-4875-a2f2-b9f13b083f8a.png)

##### 启动流程

1.**将所有的依赖的jar，通通放到jar下**的BOOT-INF\lib,设置MANIFEST.MF，并设置了启动类放到jar包中

##### 自定义SpringApplication

###### 常用SpringApplication

这个可以查阅spring的文档，了解即可，不用过度深入

https://docs.spring.io/spring-boot/reference/features/spring-application.html#features.spring-application.lazy-initialization

1.**懒加载**：这个在properties中配置，当控制器未被使用时，就不会加载控制器

2.**注册监听器**：可以通过Spring Application下的addListeners来添加springboot提供的事件监听器

3.**如何使用这些方法**：需要实例化SpringApplication方法，才能调用，不然只有run方法

### 配置文件的使用

1.**全局配置文件**：或者叫做**核心配置文件**，application.properties,或者叫做application.yml,如果修改成了别的名字，就会自动采用默认配置

2.**两种语法对比**：

* properties：采用扁平的书写方式，一行一个
* yml：采用**树形结构**，这个可读性更强，若两个同时存在，则以yml的配置文件为主

  ![image.png](/assets/f745e44d-a72d-4565-92f0-dd914c68e609.png)

3.**打包后**：配置文件会放到class文件中

4.**配置文件优先级**：有多个配置文件的同时，高优先级的配置文件会覆盖掉低优先级的配置文件。

下面是识别顺序，第一个优先级最低

* classpath
* classpath.config
* 项目根目录
* 项目根目录/config

### Profile自动配置

**作用**：用于区分不同环境的不同配置，

**用法**：多个Profile文件方式，采用application-xxx.properties方式名命

#### 配置文件的注入

**作用**：将多个yaml文件的设置值映射到属性，这个过程叫做**配置绑定**，非**依赖注入DI**。起到一个临时写入数据的作用

**步骤**：

**第一步**：编写bean，并用@Value注解标注，编写的位置和参数名，例如@Value("{user.name}"),写在属性上方

**第二步**：在yml文件中用这个user:name:AAA就完成了注入，当然常见的名命方式他是支持的。

**第三步**：实现参数值的录入

#### **改进绑定方式**：

1.**注解方式**：省去了在每个属性上写@Value的时间，用@ConfigurationProperties(prefix="user")可以直接用实体类名字和属性名字代替

2.**注解方式使用**：在绑定数据时，很多名命方式都支持，（蛇形名命，烤肉串式名命，下划线，中划线）

#### **再次改进**：

上一个方式，虽然结局了大量@Value的情况，但是在编写绑定的数据时，依旧需要去实体类看，没有提示，所以出现了一个方法

**作用**：生成idea自动提示配置文件的，叫做META-INF元数据

**实现步骤**

* 导入依赖在当前模块中：

  ![image.png](/assets/8089c0eb-8a27-4adb-976f-ac35a3b8b686.png)
* 注意上面的optional>true：表示这个以来不会传播
* 去setting设置一下Annotation Processors,勾选上enable annotation processing，**注意要选中项目**
* ![image.png](/assets/5c40b96e-6ca5-4c65-baab-91546e7bb617.png)
* 实现了自动注释

  ### 实现注入的类型

1.**对象，map，键值对**：可以用yml文件的K:V方式

* **树形写法**：
* **行内写法**：
* ![image.png](/assets/4b2777f0-d549-4541-9f9c-5e8de08428b5.png)

2.**数组**：List，set这种的数据绑定书写方式和上面两个不太相同

**他不是键值对**：所以直接写值

![image.png](/assets/b6e96bbc-107a-4259-845d-fdf85a7655b2.png)

#### 绑定文件放置位置

1.遇到多个绑定需要分类的场景，则将绑定的文件单独放到一个文件夹中，

2.**声明绑定配置注解**：这个放到要作用的那个文件中去，在类上用@PropertySource("classpath:data/AAA.properties")但是这个只能用properties文件

##### 绑定文件的其他用法

他支持${AAA}去调用该文件的其他属性值，但AAA不可以是表达式

**特定功能**：还有其他功能可以用（随机值，），在网站上查看http://docs.spring.io/spring-boot/reference/features/external-config.html#features.external-config.random-values

### 数据校验

**作用**：spring设定了特定的规范来限制数据的范围，不用自己写逻辑

**使用步骤**：

1.**添加依赖**：Spirng-boot-starteer-validation

2.**写注释**：注意注释的来源有很多，要选上面这个以来里面的

* 类注释：@Validated
* 方法注释：@NotNull

![image.png](/assets/d8dff009-dd94-424a-b789-448ad6dc56f2.png)

### 关于数据绑定的总结

如果要批量绑定适合用@ConfigurationProperties

如果只有一两个：用@Value

如果需要用SpEL：用@Value

## SpringBoot自动配置原理

1.它提前设置了很多默认的配置

2.一方面将这些底层封装起来了，变得好用，另一方面也是因为不知道原理，导致越来越傻

**自动配置流程**：

1.@SpringBootApplication：这个是springboot启动入口

2.@EnableAutoConfiguration：开启自动配置，扫描所有配置类

3.@Import调入方法

4.**变种Import**：DeferredImportSelector

5.**没有GetImportSelector的时候**：他会直接调用该方法下的selectImport完成注入

6.**有GetImportSelector**：会调用该方法下的selectImport


![image.png](/assets/a4007c69-11c2-4dce-86fb-cfce76b6e80b.png)
