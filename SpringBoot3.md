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

**单体架构**：整个项目所有功能最终打包成一个**可运行的应用包**，部署在一个进程中，和内部多少模块无关

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

10.**@GetMapping**：这个相当于@RequestMapping+method=……get

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

**springboot多模块**：

1.**有两种方式**：maven模块和spring initializr模块

* **maven**：轻量级，依赖继承清晰，符合模块职责，项目结构清晰
* **spring initializr**：**过度设计**，**依赖冗余**，**容易产生混淆（因为都有web模块）**，**项目结构**。

2. **要用maven创建多模块项目**

**创建步骤**

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
* 注意上面的optional>true：表示这个**依赖**不会传播
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

3.遇到符号识别错误如%的情况，记得用单引号括起来

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

5.**没有GetImportSelector的时候**：他会直接调用该方法下的selectImport完成注入bean

6.**有GetImportSelector**：会调用该方法下的selectImport注入bean

#### 到这里完成了bean的注入

![image.png](/assets/a4007c69-11c2-4dce-86fb-cfce76b6e80b.png)

#### 接下来开始自动配置依赖

1.也是DeferredImportSelector下的一个类，叫**process**

2.**调用自动配置类的方法**：getSutoConfigurationEnty

3.**进入上面这个类**：实现getCandidateConfigurations，实现将所有自动配置方法全部导入，用于整合所有第三方库的作用。

#### 接下来开始是了解自动配置是如何实现的

1.**进入getCandidateConfigurations方法**：发现她调用了一个loadFactoryNames ,他的参数中有一个是getSpringFactoriesLoaderFactoryClass().它获取了所有已经存在的配置类

2.上面这个get……FacotryClass()**,返回了EnableAutoConfiguration.class**

3.loadFactoryNames接收了这个上面返回的这个EnableAutoConfiguration.class.

4.**获取到了一个完整的关于自动配置的类名**

#### 讲解LoadFactoryNames如何实现返回自动配置类名字

1.在LoadFactoryName中，调用**loadSpringFactories（）**，就返回了这个自动配置类的类名

2.**LoadSpringFactories()**：读取一个专门存放配置类的文件，

**下面是获取所有自动配置类**：

* 它通过getResources（）读取一个常量FACTORIES_RESOURCE_LOCATION,这个常量存放的是一个路径，为了去读取spring.factories文件

  ![image.png](/assets/1cb72255-c354-4dbc-b112-6a3293ff029a.png)
* 这个getResources，回去每个jar包（打包好了的）的类路径下去找，BOOT-INF，里面有个lib，进去后在所有的jar包中找
* 因为它很消耗新能，所以这个getResources已经在启动时就已经读取了，并放到了缓存中
* 它返回的是一个Map结构，里面的值都是自动配置类，都已经读 取到
* 由于这些获取到的类不全是自动配置，所以要过
* **通过LodFactoryyName返回的自动配置类**，有一个类是专门来做过滤所有的自动配置类
* 它过滤完获取到的是一个Map集合，这样就拿到了所偶有的自动配置类

#### 目前还是导入，接下来讨论在某些场景下自动配置的场景

1.**最终过滤**：getConfigurationClassFilter().filter(configuration)根据pom中的starter过滤出**有效的的配置类**

这个原理就是查看每个自动配置类中的@Conditional开头的注解，查看哪些自动配置类符合，就保留这些配置类。

在propertie配置文件输入debug=true运行项目也可以看到保留了哪些自动配置类。

## 自动配置发展

在springboot3后，第三方的自动配置类不再从springboot.factories获取。

#### 新的springboot3获取所有自动配置类

1.**AutoConfigurationImportSelector.java**：原来是Def……，

2.**getAutoConfigurationEntry方法**：里面有个用于获取所有自动配置类的方法，getCandidateConfigurations.

3.去往新的地方获取自动配置类,不再是原来的.factories。而是。import文件

4.通过一系列**条件注解**，判断这个项目是否需要某些类，然后就筛选出要的配置类。

用getConfigurationClassFilter().fileter()

上面讲的是如何获取自动配置类，下面讲配置类如何运作

## 自动配置类原理

1.**自动配置类标志性注解**：@Configuration每个自动配置类上面都会有这个注解。

2.会给标记了这个注解的类，创建cglib动态代理，当调用方法时会先去ioc容器找。不用每次都创建对象。

3.如果这个注解声明了proxyBeanMethods=false,则不采用动态代理。

4.**启用一个配置类的属性**：@EnableConfigurationProperties，表示当前自动配置类用到了哪些属性，这个注解会声明出来一个专门放属性的类

5.**条件注解**：用于规定当前的自动配置类注解能不能起作用的注解。

* @Conditional10nWebApplication(type=Condition10nWebApplication.Type.SERVLET)web环境必须是servlet才可以起作用
* @Conditional10nClass(CharacterEncodingFilter.class)
* @Conditional10nProperty(prefix="server.servlet.encoding",value="enabled",matchIfMessing=true),
* ![image.png](/assets/9fdf45da-c17a-4707-929f-a731f0ab9b69.png)

6.**注入@bean**：

* 在下面还有一个注解@Conditional0nMissingBean,表示如果这个bean不存在才注入这个bean到IOC中
* **读懂这个bean**：可以知道在properties中专门配置参数，以及会有什么用，
  l例子
* ![image.png](/assets/574dd7e5-5cda-4cde-83d9-7cd7c11bec7e.png)

## 自动配置类总结

**区分依赖和自动配置的区别**：

1.**封装简化**：用少量starter依赖就能代替原来零散繁杂的jar包依赖。在springboot中通过一两个依赖就能代替（包含）掉原来一堆依赖，

2.**配置层面**：而自动配置类，是指不用像原来那样ssm手动配置字符过滤器，各种过滤器，前端控制器，	扫描路径依赖注入规则等等配置，通过识别当前的项目环境，通过借助条件注解导入了要用到的配置，并设置了默认的值，不用自己编写一大堆配置了，专注于开发业务

# 热部署和日志

**热部署**：写代码时不用每次都重启，**提升开发效率**

**日志**：用于记录错误信息，

## 热部署

**步骤**：

1.**引入依赖**：org.springframework.boot

spring-boot-devtools

2.**配置idea**：

* setting：compiler,勾选build project automatically
* ctrl+shift+alt+/：选择registry，勾选……when.app.running

## 日志

**作用**：

* 记录错误信息到文本中。
* 输出一些关键变量

**常见日志**：

* SLF4J
* Log4j
* Logback
* Log4j2
* JCL：
* jul：这个jul框架是jdk开发的。

1.Log4j被apatch基金会收购了

2.log4j2是apatch的性能比log4j高好几倍

3.logback也比log4j高好几倍

4.目前最好的组合是logback+slf4j

**背景**：在编写项目时，想要获取一些关键信息，或者捕捉错误信息显示出来，只能用system.out.println，这种情况，在idea的控制台输出一大堆，很难查找，且每次运行都会清空记录。

1.难以查找

2.日志记录庞大（单个文件大）

3.如果项目上线，怎么能立马知晓并修改

4.关键变量记录，能否加入等级制度

5.记录日志时，如何不阻塞线程

6.突然更换日志框架的工作量

**问题**：

* 需求多
* 日志框架太多比较混乱

### 解决框架混乱

1.**JCL的诞生**：他是用来整合日志的，不是先日志功能，它可以修改项目所用的日志框架，通过设置class来指定所用的日志框架，是主动去找日志框架

2.**SLF4J**：它也是一个日志门面，是JCL的升级版，

**上面两个区别**：

* 一个是它主动去找，另一个需要用桥接器来适配它，两个相反
* slf4j因为有桥接器，性能比jcl好
* slf4j不好配比较复杂，jcl比较实用简单

#### JCL使用

1.**引入依赖**：commons-logging

2.**指定日志框架**：通过设置一个properties配置文件

![image.png](/assets/1b8e20b5-4af5-414c-b2fe-c2555a7752d0.png)

```
        Log log= LogFactory.getLog(JulMain.class);
```

#### Log4j使用

1.要导入依赖，注意调用时别用错了，这个是apach的不是util的

2.导入log4j的配置

log4j.rootLogger=trace, stdout log4j.appender.stdout=org.apache.log4j.ConsoleAppender log4j.appender.stdout.layout=org.apache.log4j.PatternLayout log4j.appender.stdout.layout.ConversionPattern=%d %p [%c] - %m%n

#### SLF4J

它有两个重要的东西，**适配器，桥接器**

1.**桥接器**：slf4j要实现某个日志框架，这个日志框架就需要用**桥接器**实现和slf4j的连接

2.**适配器**：一个项目的多个模块间可能用到日志门面不一样，日志框架也不一样，当**项目合并时**，slf4j为了统一，就设计了适配器，实现了转化作用，转换为slf4j.

**使用**

1.**引入依赖**：org.slf4j

2.**引入类**：注意要slf4j的

3.**添加桥接器**：不同的日志框架有不同的桥接器，通过引入桥接器依赖，自动通过依赖来确定用那个日志框架

4.**注意**：一个slf4j只能有一个桥接器

![image.png](/assets/a9205ddf-2dd7-406c-882f-a28aaae5df8f.png)

* **添加依赖**：log4j12

```
        Logger logger= LoggerFactory.getLogger(Log4jMain.class);

```

##### **遇到两个不同日志框架的场景解决方法**

不同的框架所记录日志的格式不相同

**开发标准**：日志的使用不能直接使用日志框架，要通过门面来实现，这样好统一框架。

**转换**：通过添加专用的适配器完成转换

![image.png](/assets/615f7aae-a209-4e87-9a7d-bcd3d4891656.png)

**步骤**：这里演示JCL的转换，可以看到上面要用jcl-over-slf4j.jar，

1.**添加适配器**：jcl-over-slf4j.jar

2.运行这个文件，就会发现变成了slf4j

## SpringBoot的日志

1.它也是采用的slf4j+logback的方式进行日志的记录

2.Spring默认的框架是JCl，所以starter的时候会引入两个转换到slf4j的依赖，logback,log4j,jcl三个**适配器**

![image.png](/assets/c536575f-6d76-4330-8ac0-a4778a9d5815.png)

### 使用

#### 日志级别

可以通过不同的级别来控制日志记录方式

* TRACE
* DEBUG
* INFO:到这是默认的日志级别，以下才会被日志记录
* WARN
* ERROR
* FATAL
* OFF

![image.png](/assets/7a2ee256-eb2b-4ed7-89e8-3d625a656954.png)

**修改默认日志级别**：在properties中写入，logging:level:root：trace它可以精确到某个文件

logging:level:com:AAA:trace

#### 日志格式

默认的格式如下

![image.png](/assets/f4041913-53ed-45a0-a423-fa1da1ddecdb.png)

1.日期，毫秒级

2.日志级别

3.进程ID

4.空格，分割正真主要的日志信息

5.线程名称

6.记录，日志的类

7.日志消息

##### 修改默认日志格式

1.**去网站找**https://docs.spring.io/spring-boot/docs/current/reference/html/appendix-application-properties.html#logging.logback.rollingpolicy.max-file-size

2.**编写修改信息**：在properties文件中用logging:pattern:console:XXXXXXXXXX导入修改的信息。一次性导入

* 在日志格式中，大写的英文都是变量，它调用的是系统环境变量中的值
* 可以在properties中编写对应的配置，然后就能设置到环境变量中，例如这个关于时间的变量，这个可以用到Logging：pattern下的**deteformat**，自己配置时间格式
* ![image.png](/assets/0b2a4be0-2f3d-4ebb-b4d1-8c0f97c61596.png)
* 更多的对应关系可以去官网查看

3.**Logback的日志格式修改**：

她不用变量，直接声明格式

![image.png](/assets/5745c530-5b95-4172-8ecd-edc6a2a3701f.png)

* **%d**：表示这个日志格式是logback的
* **中括号里的**：这个是真的日志格式

4.**设置日志显示的细节**：颜色，缩进，间隔等等

上官网找：https://docs.spring.io/spring-boot/docs/current/reference/html/appendix-application-properties.html#logging.logback.rollingpolicy.max-file-size

![image.png](/assets/6e89dab2-da47-497a-ae68-b5ce563b42c8.png)

## 输出日志

1.Spring仅仅记录到控制台，不写日志文件，

2.**设置一个属性**：logging.file.name或者logging.file.path的属性在properties文件中，在后面接上要存储文件的文件名字

* **loggin.file.name**：
* 没有路径会放在项目的相对路径下
* 可以指定存储路径和存储文件的名称
* **loggin.file.path:**
* 不可以指定名称，
* 必须要指定一个物理路径
* 名字默认用spring.log

## 日志迭代

**归档**：他是一种生命周期管理机制，当该文件满足某种条件（大小，时间），就会讲这个**满文件**，就会将该文件通过各种方式转存为历史归档文件。同时建立一个新的文件来继续记录新的日志。

**设置归档的配置**：这个写在properties中

![image.png](/assets/f20543e7-b35c-407d-a8dd-9725b805f59d.png)

### 自定义日志配置文件

原来是在全局配置文件properties中编写它的配置

1.如果想实现日志通过邮件传输，

2.BBBBBB

****日志还可以实现项目的功能，但是实现上面的功能**的话还需要通过日志专用的配置文件来配置，因为**全局配置（springboot）**不能实现这些功能。

#### logback.xml**基础框架**

具体细节可以查看文档：https://docs.spring.io/spring-boot/docs/current/reference/html/spring-boot-features.html#boot-features-logging

![image.png](/assets/1f61419f-3228-4d42-bc30-d763be3fd9a4.png)

1.不同的输出方式，可以通过修改class的参数的方式来修改，上面就是i输出到控制台

2.也可以控制全局的日志级别，和精确到文件的日志级别控制，**也会导致全局的日志配置文件失效**

3.也可以更具全局配置文件的参数，在某些参数条件下设置特定的日志格式，

4.还有在某些情况下需要将日志配置文件的名字 改为"logback-spring.xml"，因为，logback.xml会在springboot容器加载前先被logback给加载到，但是logback又需要springProfile的信息，所以会报错，但  是logback-spring.xml可以解决这个问题。

5.它还可以**引用**到全局配置文件中的参数。  其中scope是使用范围，name是这个获取到参数的参数名，source表示获取位置，defaultValue是表示没有获取到的情况下设置的默认参数。

![image.png](/assets/bcb23d3d-1caa-412a-b32c-8bbfcafb249b.png)

#### 切换日志框架

1.**Spring Boot 默认日志框架是 Logback**

2.目前logback和log4j2是市面上两个最好的框架，这两个如何转换呢？

**场景启动器**：例如starter这种依赖，会根据你的项目环境配置依赖。

3.因为springboot默认添加了logback的桥接器，但是slf4j只能有一个桥接器，想换成别的日志框架的话，得排除这个桥接器。（这个要去场景启动器内部设置）

**实现步骤**

1.**打开依赖图表**：选择到自动的日志依赖spring-boot-starter-logging

2.**排除桥接器**：右键它选择Exclude，这个方法失效了，没有了，只有通过在pom中手写排除方法才行。

* <exclusions》
* 《exclusion>

3.**添加log4j2**：在配置文件中添加上log4j2的桥接器即可。

![image.png](/assets/576b98cb-5447-4cfa-b758-65b37de6eacb.png)

4.**注意原来的日志配置**：不同的配置格式不一样，查官网转换过来

![image.png](/assets/46439264-2f16-4c84-a960-06780d56024e.png)

5.**注意**：日志配置的文件名字也要改过来，原来logback-spring,改成log4j2-spring

# 全局指令

server.port=8081修改端口号

server.servlet.context-path=/order给所有接口加一个前缀

# SpringBoot与Web开发

## RestTemplate的使用

**作用**：让访问后端，和后端传输数据更加便捷，他是一个模板类

**问题**：原来需要通过前端来访问数据，传递数据，转换格式（两边都要），还要编写前端来测试，非常繁琐。

**原理**：他是基于HttpMessageConverters,他的作用是自动完成json转换，省去了json转换代码的实现。

一个项目多个子模块，直接按照spring initial正常创建就好

**适用**：

* 它适用于微服务的架构下，服务之间的远程调用
* 他的闭端是，如果有很多子模块来访问的话有很多地址，没办法实现**负载均衡**，目前微服务有了更好的方法，所以也不太适用于微服务，而且好多方法已经停用了，在打代码的时候也知道

### 平替的方法WebClient

它也可以调用远程

* 依赖于webflux
* 他的访问时无阻塞的。而resttemplate是无阻塞的，响应的。
* 它只有特定的项目才会用到。

### 多模块分工

**步骤：**

1.多创建一个模块，专门用于用户操作。

2.在controller添加连接控制模板

```
package org.example.demo2.controller;

import org.example.demo2.entity.Result;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.client.RestTemplate;

@RestController
public class OrderController{
    //下单 访问远程rest服务
    private final RestTemplate restTemplate;

    // 直接创建RestTemplate实例，而不使用RestTemplateBuilder
    public OrderController() {
        this.restTemplate = new RestTemplate();
    }

    @RequestMapping("/order")
    public String order() {
        // 将Result改为String类型，并提供一个实际的id值
        Result result = restTemplate.getForObject("http://localhost:8080/user/{id}", Result.class, 1);
        System.out.println(result);
        return result.toString();
    }
}

```

调用RestTemplate的方法，

![image.png](/assets/4c5f2e2e-f30a-4620-82ed-aebfbabc70bd.png)

3.**解耦操作**：在这个模块中添加上实体类，如存储结构的实体类，用户实体类

4.**访问接口调整**：因为时子模块来访问主模块，所以两个端口不能一样。

**修改结果类**：在主模块controller中，如果向存入不止一个User实体的data的话，就不要将泛型定为User，放置为空就好，或者设为list<user》因为springboot会自动识别传入的参数类型，自己设置。然后调用Service的getAllUser放到data参数的位置就好。用于记录每次修改数据后的数据状态。

5.**注意后台请求注解**：增删改查的注解都不同

* 这里重点说一下修改数据时传入的对象，主模块要接受id同时要接受对象，这个对象参数前要用注解@RequestBody提示以下

#### RestTemplate方法的使用

1.**getForObject**：这个可以获取一个对象，可用于传递参数，他的参数具体看提示

2.**getForEnity**：这个可以获取对象以及包含响应中的一些重要信息（响应头，响应状态码，响应体等）一起返回

3.**postForEnity**：这个就是说是post的请求，用于存储敏感信息，注意，**传统编写它的返回类型和变量时，可能会报错，这时在后方加一个.var就会自动生成变量。

4.**put**：用于修改数据。它没有返回值。

5.**exchange**：用于修改数据用的，它可以用返回值,它也有删除功能，修改参数为httpmethod.delete就可以他是一个万用方法

#### 以上是模拟前端

也可以不用子模块，直接在主模块的测试类中测试这些方法，但注意这里用的RestTemplate和子模块用的不一样，这里有专用的方法TestRestTemplate

#### Postman的使用

他也是一个测试接口的工具，

* 不用编写爱出错的前端来请求响应数据

**使用方法**：

1.**添加对象**：在post模式下，点击body，编写json即可

#### MockMvc的调用

1.不用启动web项目就能测试

2.当项目所需的环境复杂时，为了速度可以用它

3.它可以不依赖tomcat，模拟一个http请求的环境

4.他自己调用controller来完成模拟。

5.不依赖于网络环境，也提供了一套验证工具

**使用**：

##### 这个是查询的场景

1.编写配置信息

* **写注解**：要两个SpringBootTest,AutoConfigureMockMvc
* **从ioc获取mockmvc对象**：@Autowireed
* **编写单元测试方法**：

2..可以直接请求controller

**发起一个模拟请求**：mockMvc.perform(

//编写发送get请求的语句

MockMvcRequestBuilders.get("/user/{id}",1),

//设置响应的文本类型

accept(MediaType.APPLICATION_JSON_UTF)

)

//添加响应断言.表示运行后的数据是否和我想要的数据匹配，

.andExpect(MockMvcResultMatchers.status().isOk())

.andExpect(MockMvcResultMatchers.jsonPath("$.data.username").value(expectedValue:"zhangsan");

.andDo(MockMvcResultHandlers.print());

![image.png](/assets/7bc6ffbe-a90a-4c02-a701-177d3ca970c8.png)

##### 添加数据场景

1.和上面相比，配置信息多了个响应文本类型。和文本类型

2.然后把get改成post

3.**编写添加的对象**：用json的形式编写

![image.png](/assets/25e28cab-8b8a-486f-8c1d-091a6d454921.png)

4.**关于断言部分**：

有的用于测试是否是期望值，有的是用于将信息返回到控制台。

**andDo(print())**：将参数输出的![image.png](/assets/8afb61ec-1e05-43aa-88a9-8df5ad61e4a8.png)

### swagger的使用

**问题**：在前后端分离项目中

* **前端调用**：他需要知道这个接口的功能，参数，返回参数等。前期需要用一个文档来说明这个接口的信息，会反反复复修改。十分麻烦。

**作用**：

* 他是一个描述呈现接口文档的工具
* 通过添加注解的方式来标即功能。swagger通过读取注解了解到这个接口的各个信息，就会形成一个接口文档。
* 减少了前后端接口配合的工作量。

**实现步骤**：

* **加入依赖**：springfox-swagger2和springfox-swagger-ui。这里看到了spring，因为它用到了springmvc的规则，因为他要识别注解，以及json规范。
* **编写配置文档**：直接用模板即可

![image.png](/assets/16331713-4904-4e41-b501-55344b1326ae.png)

* **配置内容**：
  1.声明这个java文件的作用
  2.哪些加口会映射到文档中
  3.可以设置接口选择器
  4.哪些接口生成接口文档
  5.设置文档的描述信息
* **加入注解**：

  ![image.png](/assets/d604dfa9-19db-4511-9b22-f3460ea8f7ad.png)

  在各个位置描述
* **获取中文描述文档**：

  y有固定的访问地址http://localhost:8080/swagger-ui.html
* f

**注意**：swagger适用于早期的springboot版本，新版的springboot大部分有了更新的方法SpringDoc OpenAPI

# SpringBoot自动配置原理

### 关于controller到视图输出的方面

#### 主要功能：ContentNegotiatingViewResolver

* 它不会解析视图，他是委派给其他视图解析器进行解析。（jsp，themeleaf）
* ![image.png](/assets/5ed4da9a-3fee-4c45-b20a-b091db7f2fff.png)
* 这个类中会执行一个方法resolveViewName，它会传入一个viewName,可能是jsp，或者themeleaf，然后获取，匹配他们

1.**视图解析器初始化**：也是再上面的主要功能类中的一个方法iniServletContext

#### 主要功能：BeanNameViewResolver

他会更具hander方法返回视图名称，然后再IOC中查找，找到和它名字一摸一样的bean

这个对应的bean（视图）是一个和controller中一个方法return的名称，它会实现View接口，

### 关于静态资源的识别与调用

**约定大于配置**

原来需要再xml中编写这个静态资源的信息，现在再springboot就不用了，他有一个指定的位置存放，只要放在约定好的文件夹中就可以了。这就是**约定大于配置**

**这个实现原理**：

再springmvc的自动配置类中。会有一个专门处理静态资源的方法**addResourceHandlers**

1.**addResourceHandlers**：

* 他会判断当前的访问路径是不是一个WebJars。
* 这个WebJars作用就是将静态资源放在jar中进行访问。
* 当访问路径有webjars时他就会映射到项目的resource中的webjars进行寻找
* 接着在这个寻找过后他有一个静态地址的访问，
* ![image.png](/assets/bc67ff6b-c486-471b-8022-e4a56a020e11.png)
* 这个静态资源地址映射到的是一个地址集，用于声明静态资源存放的地址，当不想再约定的位置放静态资源时，可以去立马加上
* SpringBoot它主要写的是后端，关于前端的东西都视为静态资源，所以html直接放到啊静态资源中即可

2.**自定义静态资源地址**：

如果不想用默认的路径，可以再配置文件中指定一个特定的静态资源地址，但是要注意，原来默认的多个地址都会失效。

![image.png](/assets/87ec087e-f033-4ccd-8053-700412f680ab.png)

#### 日期转换

原来需要编写专门的注解来设置日期格式，现在有现成的**默认格式**方法来实现，也能支持日期的**转换**。

![image.png](/assets/8a69bf0f-dd49-46b7-85ff-c325a885a3ef.png)

#### 关于http的报物转换处理

这里用的时HttpMessageConverters,他能自动实现转换

**使用**：

1.**在配置文件中**：

#### 视图解析器配置

原来是去xml中配置前端控制器中的标签实现前后缀的设置，比较繁琐

，现在在springboot中可以直接通过主配置文件的方式来设置前后缀，比较方便。

![image.png](/assets/45805878-70b4-4ecb-bfad-4348b2756e05.png)

设置了这个后，控制器return的名字就拼接上这个前后缀，找到这个html。这个要放到项目结构中的templates文件中。这个是约定好的。

**原理**：草泥马晃晃晃，你tm谁啊你

* 在WebMvcAutoConfiguration中有一个方法用来找到和这个静态资源的html
* ![image.png](/assets/83a33ff1-f843-49ae-8fe4-6370e80e11fe.png)
* 当然也可以不在全局配置文件中设置这个前后缀，因为有默认的。

#### 数据转化为javabean的原理

原来在上面说的是HttpMessage,现在 又出现了个ConfigurableWebBindingInitializer。

**因为每个请求的方式不同，用的转换也不同**：如form请求，ajax的json提交，

## 拦截器的设置

**步骤**：

* 创建一个文件interceptor，
* **创建拦截器java文件**
* **实现HandlerInterceptor接口**：有三个方法

#### 实现一个拦截器记录时间的方法

##### 编写拦截器

* 创建一个时间对象在三个方法外面，
* LocalDateTime.now()获取当前时间
* Duration between=Duration.between(AAA,end)获取时间差
* 然后可以用日志记录下来
* ![image.png](/assets/4b97db9b-05f0-4e23-a0a7-88f375176069.png)

##### 编写配置，让拦截器生效

要设定拦截范围，排除拦截等

* **在Config文件中创建MyWebMvcConfiguration.java文件**：
* 实现接口WebMvcConfigurer
* 添加拦截器addInterceptors
* 参数为InterceptorRegistry registry
* 编写拦截器，拦截器规则

![image.png](/assets/d089fb18-a33c-43dc-bf39-f5fca73d1204.png)

#### 配置跨域请求的代码CORS

就是说不是一个模块或者项目，端口号不同。没有权限互相访问。这时就要在MyWebMvcConfigurer中配置跨域请求了。

1.在配置文件中加入addCorsMappings

2.参数是CoreRegistry registry

3.**设置跨域接口**：

4.**配置跨域请求方式**：

**![image.png](/assets/258bf107-aea3-4e77-a486-fef9a7adebc2.png)**

5.这样在前后端分离的场景就可以跨域访问了

6.还可以设置特定的端口来允许访问端口：

* .allowedOrigins("http://localhost:8081")

#### WebMvcConfigurer原理

这个有些需要自己配置，但是大部分都已经配置好了，在自动配置类**WebMvcAutoConfigurationAdapter**中他们实现了这个接口，已经完成了很多不常用的配置。

1.我们只用定制我们需要的即可

* 视图控制器
* 拦截器

2.**放到IOc中**：它会将所有实现了webmvcconfigure的配置类全部注入容器中，放到一个变量中configuras

##### 委派器

在收集完webmvcconfigurer到config（List）变量后，它会将这个config放到委派器中去。

![image.png](/assets/71521cd8-0115-4250-9d5e-c2dfe8cbbc24.png)

1.**调用配置方法**：调用的时候就是去循环委派器

##### 注意

在webMvcConfigurer中有个注解不能用，@EnableWebMvc，用了之后，这个在别的地方的默认配置就失效了

# JSON国际化

在springboot中jackson就是默认配置的库，他目前是最好的。

1.例如不让user对象进行json转换，把@JsonIgnore放到User类上，可以用于排除json序列化

2.**可以设置日期格式**：@JsonFormat（pattern="yyyy-mm-dd",locale="zh"）

* **本地化**：locale=“zh”，表示以中国的地区的显示方法显示日期

3.**设置Json注解执行条件**：@JsonInclude(JsonInclude.include.NON_NULL)表示只有这个属性非null时才启用这个json序列化

**序列化**：表示启用json

**格式化**：表示修改他的格式

4.**设置别名**：@JsonProperty("aaa")

![image.png](/assets/9b842aa4-e782-4d19-80d6-0c6b6b573da1.png)

# SpringBoot嵌入式Servlet容器

spring默认的servlet容器是tomcat，

**传统容器方式**：容器就是像tomcat，jetty，项目打包好了后，放到这个容器立马运行，容器和应用分离

**嵌入式容器**：tomcat和项目是一体的不需额外安装容器

### 嵌入式Servlet容器的配置修改

由于嵌入式容器的配置都是默认的，有的配置不满足需要，所以出现了自定义配置（定制servlet容器）

**配置值修改位置**：有两个方式

* yml和properties
* java实现WebServerFactoryCustomer的方式
* **第一种方式更简单**
* ![image.png](/assets/526c3baa-8d42-4b29-b77a-7389006979fa.png)

**网络设置**：server.port设置请求端口，绑定端口地址

* **请求端口**:server.port设置端口号
* **绑定端口**：server.address表示只有该地址可以访问

**错误页面路径配置**：server.error.path

**会话超时时间**：server.servlet.sesson.timeout

1.在全局配置的书写内容中

* 不带具体的服务器名称，比较简短的，则是全局通用配置
* 如果带有具体的服务器名称则是单独对该服务器的配置。

## Servlet的三大组件

1.servlet

2.listener

3.filter

### Servlet的使用

#### Service3.0的使用

1.基于service3.0,原生javaweb开发，通过注解来开发

![image.png](/assets/4a1ec21d-b1a2-4c14-bb5e-a2002047e52c.png)

**然后**：在启动类上加上@ServletComponnetScan

#### Springboot中提供了bean

通过提供的三个bean来动态注册，不通过注解方式

![image.png](/assets/e6f3cf50-831f-4749-92d2-c245d00c4807.png)

1.**ServletRegistrationBean**：实现servlet，

* ![image.png](/assets/cfae3da9-1657-4ced-8713-898fd9aee98b.png)
* 声明一个servlet注册bean，然后给她设置响应的Servlet，设置名字，添加映射，映射到原来要加注解的@WebServlet中去，return这个注册器bean
* 注意加@Configuration

### 服务器的切换

主流三种Tomcat,Undertow,Jetty

![image.png](/assets/601e2abc-dc93-4419-8942-c52aa686faff.png)

#### 实现步骤

1.**排除原来的依赖**：starter-Tomcat

2.**写入jetty依赖**：spring-boot-starter-jetty

## 嵌入式自动配置原理

### Servlet容器的自动装配

它最根源的原因是@import

1.**imort中有三个关于服务器类**，他们内部就有一个条件注解，下面展示的是jetty，通过Servlet容器中的start依赖（Tomcat场景启动器）判断classpath是否存在对应的类。。

![image.png](/assets/1b082eba-8c41-413f-a31a-b08ce92f38ac.png)

![image.png](/assets/5abbaea2-e8d5-41fb-a2f2-f826b5f3a315.png)

## 外部Servlet容器

#### 内部Servlet

原来的内部servlet容器，会将项目打包成jar包，运行它需要环境变量，导入场景启动器就好了 ，但是内部的servlet参数不好配。还是采用原来的方式比较好一点，这种情况要导成war包，给运维。

#### 外部Servlet

外部Sevlet会打包成war包，也需要安装tomcat环境变量，本地的开发工具也需要绑定tomcat

1.**修改打包方式**：在pom。xml中修改

#### 步骤

1.下载tomcat容器

2.将pom.xml设置为war包

3.修改依赖，因为单独下载了个tomcat，有很多包重了，所以要将原来在pom.xml的tomcat依赖设置为provided，让她不参数打包。

* tomcat在starter-web中，所以在下方新增一个tomcat依赖，告知为provided就好了

4.**运行方式的修改**：原来是在run方法中运行开始，现在用原来的方式

* 增添运行配置，
* 采用本地tomcat部署
* 如果是原来的Service3.0的方式的话可以运行了 ，如果是SPrinboot的话还不行，
* Springboot项目，tomcat不知道启动类是哪个，所以要加一个启动类
* 该启动类和springboot启动类平级，然后就可以运行了
* ![image.png](/assets/a5a26f1f-9faa-43c1-abe7-6f660c3d6241.png)

# SpringBoot与AOP

**实现步骤**

1.**添加AOP场景启动器**：spring-boot-starter-aop

2.**创建AOP实现文件**：单独文件夹aspect，创建LogAspect.java

3.**添加标记**：@Aspect,@Componet

4.**补充内容**：

模板

![image.png](/assets/3a214ea7-d9d6-4a82-a6df-416a3eeac800.png)

# SpringBoot+MyBatis

##### 添加依赖

1.Spring web

2.JDBC API
3.MyBatis Framework

4.MySQL Driver

##### 查看依赖是否齐全

1，gdbc

2.mybatis

3.数据库驱动

4.数据库连接池

##### 编写全集配置

1.如果东西比较多的话，推荐用yml。

2.复制粘贴固定模板

![image.png](/assets/5c58a2a4-d731-44e1-aced-a5075df9b3b2.png)

##### 注意引入的依赖

如果不是场景启动器类的依赖，还是需要自己设定一些配置参数。例如这里的druid

1.**新建文件**：config文件下的DruidConfiguration.java

2.**添加注解**：配置文件注解，条件注解（）

3.**编写方法**：public DataSource dataSource()这个摸底为了导入数据库的配置参数，因为要自己配置一些配置参数，

* 一个一个导入比较麻烦
* 可以利用导入属性的注解@ConfigurationProperties(),这个注解作用是批量导入配置文件中的属性，然后绑定到java的字段上。
* 这样省去了一个一个写的步骤，
* 将注解写到方法上，配合上@Bean一起用
* ![image.png](/assets/3cf9812f-c2dc-44ac-8eca-236739472283.png)
* 上面是**第一种方式**
* 第二种方式是这个DataSource独有的方法
* ![image.png](/assets/7acd6387-4a0b-4eda-8efb-8b2803eecdd8.png)

##### 配置连接池

![image.png](/assets/5007f6ef-2b15-4fb9-884c-e68de68ae0cb.png)

##### 配置监控过滤器

![image.png](/assets/78fd71eb-5e43-4732-b59b-e81ce075687b.png)
