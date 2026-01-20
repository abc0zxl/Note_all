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
