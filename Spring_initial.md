# Spring

目前最好的一个生态框架

1.他是一个轻量级的开发框架

2.解决了业务逻辑层的开发和各个层的耦合问题

3.他提供了两大核心**依赖注入（DI，IOC）**和**面向切面编程（AOP）**

## Spring 的Web方向

#### 创建项目步骤

1.**下载插件**：idea下载spring initial插件

2.**勾选依赖**： Spring web

## Spring Framework

也叫做Spring5

1.**版本需求**：在Framework5后要用JDK8

# IOC控制反转

**目的**：解决耦合问题

也可以说是**依赖注入**（DI）

**理解**：原来的对象创建控制权在**程序员**手中，实现控制反转后，对象的创建工作交给了Spring来处理。

**问题**：

* **变更数据库**：多了一个数据库访问接口，名称不同，要到后续代码中**全改过**来。变更的越多发生**异常**的概率越大。——**高耦合度**
* **依赖关系**：service层必须依赖dao层，如果dom层出错，会导致所有都运行不了
* **修改数据操作接口**：这个也就是修改service中的对象的实现方法，如果有上百个的话，就要改上百次，所以如果用ioc的话就只用改一次。将原来service中的对象方法换成




#### 新增IOC解说

1.原来没有ioc时，需要将对象的实现方法写死。

2.如果需求有新的大规模变动，必须得换对象的实现方法，就需要修改很多地方。

就比如说，对象是通过接口得到的，这个接口的具体实现可能有很多种，很多种就相当于改了很多版需求。但是没有IOC的时候对象的具体方法实现都是写死的，要改的话就要改很多地方。

现在有了IOC，我们就写一个接口对象，对象的具体方法实现不用管，不由我们自己来定了，是由spring来管理。而不是固定的。

##### 在代码方面

* 早期的IOC是由XML来实现的，实现了只用修改一处代码，就能实现方法的变换，
* 现在通过注解，实现了完全的自动化操作，由ioc容器来实现方法的注入。

##### 在性能方面

* 原来没有IOC时，每个用到对象方法的地方都得重新new一次对象，会有性能的浪费
* 有了IOC就解决了这个问题





















**面向对象五大原则**：

* **ISP**：接口分离原则
* **DIP**：依赖倒置原则。他也是IOC的前身，将原来的service依赖dom，转换为dom依赖service，就好比电脑没有鼠标照样运行。

IOC遵循的原则是DIP，DI是IOC的具体实现

**功能特点**

1.**对象**：由Spring来管理，创建，装配

### IOC实现

控制反转的三种实现方法

1.**导入jar包**+配置xml：现在不建议用这种方法，但是这是最原始的方法。这个包在spring仓库官网repo.spring.io中。现在不可用了，找不到。

* 导入jar包
* 编写xml，分离dao和service。用<bean声明这两个

2.**maven+注解+xml**：在spring2.5后，就用的**注解+xml**的方式开发。

* spring的xml导入Spring-Context，它包含了很多jar包
* 将数据库操作接口导入ioc容器中
* 创建service的bean，用于注入依赖
* 在service中的创建对象要声明一下set和get，因为这种模式下不能使用new，要用set实现注入。
* 注意在调用bean时，要注意声明的类范围，如果范围大的话会识别到多个bean，此时会因为不知到注入那个而报错。
* 通过修改bean中的类信息就能完成快速换依赖

3.**springBoot_javaconfig**：在spring4.0后，就完全用的**javaconfig**来配置。

**配置bean的别名**：用alias标签，在获取数据库操作类bean时，可以用这个名字精准获取bean

### DI依赖注入

1.**基于setter方法的依赖注入**

这个在spring的xml中的<baen，标签下用<property 写入对应对象，然后调用对应属性的set，实现依赖注入

2.**基于构造函数的依赖注入**

在这个spring的xml中的<bean.标签下用<constructor-arg注入对象的具体参数，但这个需要写所有的参数，还可以省略属性名的书写，会自动直接按照顺序写入属性值。

3.**复杂数据类型的依赖注入**

这种是因为这个实体中的某个属性的类型为其他的实体类时，它有两种注入方式。

* **外部bean**：先将这个外部的实体注入，再将内部的bean的值赋值为这个外部bean的id。
* **内部bean**：先用property，然后再里面创建一个无id的bean。就完成注入

这两种方式第一种适合**公共引用**的方式，第二种适合**隐私的方式**。

4.**P名命空间法**：这个是用于简化setter方法的，直接在bean的标签中写入属性值，但是list，和外部实体类，还是需要用复杂数据类型注入的方式。

* p命名空间在顶部的<beans中写入，xmlns:"http://www.springframework.org/schema/p"
* 在<bean中直接写入p:age、p:name等。

#### bean的高级使用

1.**depends-on**：用于控制bean的属性加载顺序。编写在bean中的。

2.**懒加载lazy-init**：通常情况下，bean会被提前全部加载好，如果在bean中利用了这个，就会在不利用这个bean时，不加载他。

3**作用域**：通常情况下bean的方法，同一个id只会加载一次，但是在bean中声明了scope="prototype"。就可以创建任意多个实例对象。

* **共享冲突**：这个应用场景时，当一个共享的**对象**，**变量**，会出现线程安全问题。这时，将这个对象的bean标记为**scope=prototype**就可以解决线程安全问题。
* 它可以在某些场景下才会加载多个实例，这就叫作用域。

## 自动注入

原来的注入别的实体、bean，要用ref或者**外部**。

1.**byType**：通过类型自动匹配

现在利用**autowire="butype"**,它会识别容器，识别到后自动注入到bean中，不用手动写额外的代码来声明。

2.**byName**：通过set方法名字匹配

遇到多个同类型的情况，这时就不要用类型匹配，用set名字匹配。他就会根据id区匹配。

例如给属性赋值，使用set时发现是setWife2它就会去匹配那个，bean的id为wife2的bean，并注入到当前的bean中。

**注意**：

* 当bean中要匹配bean时没有匹配到，它不会报错
* 当匹配到多个时，可以这只一个主要的”primery=true“就会优先用这个，或者设置autowife-condidate=false就会取消自动注入。

## IOC生命周期

这里讨论的是如何控制他的生命周期，这里有三种方式

1.**接口方式实现**：初始化，销毁。

* **初始化回调**：在实体类中继承InitializingBean，这个可以重写afterPropertiesSet,编写这个阶段的任务
* **销毁回调**：继承DisposableBean，重写destroy
* 但是这个销毁阶段，不是说这个bean执行完，用完了就会销毁，而是要整个ioc容器关闭，他才会执行销毁。

2.**基于配置的方式实现**：

* **定义bean**：在这个bean中声明好，初始化和销毁的方法名字
* **方法创建**：在实体中创建这两个方法，编写各个阶段的任务
* 上面两个方式中，接口方式的优先级比配置方式的优先级高。

## 第三方Bean对象创建

因为要使用一些外部的对象，例如数据库连接池。

**步骤**：

* 导入pom文件
* 在对应ioc.xml中写入这个库，编写bean
* 也可以通过这个项目的配置文件db.properties，编写信息，然后再去bean中导入

  **导入**：<contest:property-placeholder location="db.peroperties"
* f

![image.png](/assets/bcbc8a2d-3986-4fea-8747-1a22b5a3005a.png)

## SpEL表达式语言

它支持运行时查询操作对象

**功能**：

* 支持任何运算符
* 可以引用bean的某个值
* 可以引用其他bean
* 调用静态方法

![image.png](/assets/85531a66-fe64-4760-9e5c-5f1874b6a110.png)

# IOC基于@注解开发方式

它提供了4中注解将这个类注册为bean（Repository

,Controller,Service,Component),这些按照字面意思标记在各个层中。有**增强可读性**和**spring管理**

这个基于注解的方式**主要应用**于SSM框架开发中。

1.**@Controller**：用于标记bean或者entity 中的实体类

2。**@Repository**：用于标记

3.**@Service**：用于标记

4.**@Component**：

**注意**：

* 注解要标记在类上面，不要标记在接口上面
* **bean名字**：当告知xml扫描注解后，这些类会变成bean，这个bean的名字就是他的类名的**首字母小写**。
* 使用ioc容器的方法，必须保证这个类必须在这个ioc容器种
* 项目的结构层次必须在一个java文件夹下的同一个文件夹中不然无法编写xml中的范围。
*
* **修改Bean的名称对应的属性的名字**：匹配到多个bean时，可以去尝试改变service中的@Service("AAA")调用名称改成对象的名字，
* **告知上级要寻找bean的名称**：在遇到匹配不到或者匹配到多个时，可以用@Qualifier("AAAAA")直接对应的service包名AAAAA，**覆盖**原来要找的名称，开头要小写。
* **设置注入的主要bean**：如果遇到多个个注入的bean，可以设置一个首要注入的注释在要注入的bean的类名上面用@Premery
* **接口上不能用注解**：因为注解开发，是一个实例化一个对象的过程，接口不可以实例化。

**用法**：

* **标记类**：将各个类用注解标记上
* **告知xml**：让xml扫描某个包，用<context:AAAA-scan base-package="BBB"识别这些注解类
* **注入属性值**：在对应的注解类种调用**注解@Value**就可以写入（硬编码值，${},#{}），在@Value中用"刀乐"符号可以访问db.properties中的值。

  ![image.png](/assets/34156b3c-41b3-4014-9bf5-0c7cb70b8767.png)

  这个在spirng2.5中不能直接获取值，还是需要到xml中声明这个db.properties![image.png](/assets/bb6d743f-3f5f-430d-8443-c2289c4ef30f.png)

#### **排除扫描**

这个是告知xml不要扫描某个、某类的注解。编写在<context:AAA-scan之中也用<context：exclude-filter包裹

它的类型有5种，

1.**annotation**：根据注解完整限定名设置排除

2.**assignable**：根据类的完整限定名设置排除

## 自动匹配

原来用的是xml种bean的autowire=”byXXX“现在可以直接用注解，**@Autowired**，

1.**匹配方式**：

* 优先用bytype，然后用byname
* 没有匹配到会报错

2.**修改名字**：有三种方式，

* 一种是直接修改修改这个属性名字
* 修改bean中的属性名字
* 用qualifier覆盖原来的名字

3.**公共接口场景**：这种情况就要讨论匹配到多个bean的问题。这种例如在service中，有相同的操作方式，对对象不同，利用**泛型**来共用一个接口，这时业务端匹配到的bean就有多个，这时也需要将对象也加入**泛型**，明确操作**实例**

![image.png](/assets/5e1c945f-3551-4223-9add-3f18738cfda8.png)

4.**注解的位置**：可以不固定在对象创建上面，可以房子啊方法上面，但限于在方法要导入对象的**参数**形式。

![image.png](/assets/eb600787-1d6e-4e6d-8993-a9e27b7576df.png)

5.**替代方法**：除了Autowired还可以用**@Resource**

* **这两个区别**：Resource需要**JDK**，autowired依赖spring
* **优先匹配方式**：Autowired优先匹配类型，resource优先匹配名字

## 杂项功能

1.**加载顺序**：这个时替代了原来在xml中的depend-on，用注解**@dependsOn（”aaa“）**,这样就可以修改原来按照文件夹顺序加载。

2.**懒加载**：用注解@Lazy

3.**什么周期**：初始化用@PostConstruct,销毁用@PreDestory

4.**第三方bean**：在spring2.5的时代，无法丢弃xml的开发

### 加载Spring容器工具

1.**spring的顶层核心接口**：ApplicationContext

2.**根据路径的xml配置实例化spring容器**：ClassPathXmlApplicationContext

3.**根据磁盘路径的xml配置实例化spring容器**：FileSystemXmlApplicationContext

4.**根据javaconfig来配置实例化spring容器**：

AnnotationConfigApplicationContext

## 基于JavaConfig的配置

这个是Spring3.0开始，可以使用java配置**代替XML配置定义的外部Bean**，这时还不是很成熟。

**在Spring4.0后，支持springboot1.0后就可以完全靠javaConfig方式进行开发**

1.javaconfig是在springboot后出现的，但是它的用法也是springframerwork中的一部分。

### @Bean

他是一个**方法**级别的注解（要编写在类上  ），支持原来在xml中<bean中的大部分方法。也允许在@Configuration中

1.**配置第三方bean**：用注解@Bean，类内部编写属性值

* 以数据库为例子，
* **创建对象**：DruidDataSource da=new DruidDataSource();
* **设置属性值**：

  ![image.png](/assets/460d5ade-1300-431d-9064-8795489a3bbd.png)
* **调用**：也是用DruidDataSource创建一个获取它的bean对象，
* 在@Bean(中)也可以编写initMethod，destroyMethod，用来表示什么周期的代码
* @Bean中也能写，别名， 这个别名的设置有两个参数，name={”AAA“，”BBB“}

### @Configuration

原来要在xml中**启动spring上下文**，现在用一个注解可以代替原来的spring-config.xml

1.**加载Spring上下文**：用AnnotationConfigApplicationContext

### @PropertySource

这个作用是导入外部属性，例如db.properties,

但是不能立即通过它的名字获取值，要先用@Value获取到变量中，再插入到第三方bean中

### @Import

这个作用是引入别的配置文件。主要有**四大利用领域**

1.**导入其他配置类**：@import(secondJavaConfig.class)

2.**导入注册类**：@import(Role.class)

3.**导入多个bean**：@import(myimportSelector.class)

#### 导入配置类

因为再创建引入上下文时，只能用一个配置文件，所以就要用到了这个import

**注意事项**：

* 在第三方bean方法中，想要用别的bean，可以直接在这个方法括号中写入要导入的bean即可
* 引入外部bean（同一个config文件中的bean），不用额外声明，在别的bean中就能调用
* 当被import声明的bean没有被@component包裹时，运行的时候会自动给它加上这个注解

#### 导入注册类

#### 导入多个bean

@Import(MyInportSelector.class)

这个可以批量注入bean，这些要导入到ioc的bean文件可以不用加@Component,在MyInportSelector中实现importselector接口，将多个路径写入字符串中就可以注册bean到ioc中

**注意**：

1.**bean的无参构造函数**：只有当bean被实例化时才会触发这个构造函数

2.**批量注入的bean名字**：由于没有设置批量注入的各个bean名字，此时必须用类名来获取这个bean

3.**实现接口的类参数名称**：这个要用importingClassMetadata

#### 导入这个bean处于的BeanDefinition转台的实现来，可以注册多个bean定义

可以跳过@Component，直接去注册它,可以定义一个bean名字

**Bean的状态**：

* **概念态**：指被@Component标记的代码，此时还没有被注册，这个还处于概念状态
* **定义态**：BeanDefinition，指被扫描过后的状态，这个类似于画了个图纸，即将投入生产，但是还没有投入生产
* **实现态**：将图纸实现出来了

所以此阶段导入注册bean，要做的工作就是BeanDefinition，

**步骤**：

1,**继承接口**：importbeandefinitionregistrer

2.**创建BeanDefinition**：

GenericBeanDefinition b=new GenericBeanDefinition();

3.**导入要注册的类**：b.setBeanClass(Person.class)

4.**注册这个BeanDefinition,定义bean的名字**：registry.registerBeanDefinition(“bean_name”);

# AOP面向切面编程

他是基于**OOP**基础上的新的编程思想。

可以在不修改原有代码的情况下，可以增强主要业务**没有关系的公共代码**，日志，事务等，通过**切面**增添到指定位置

![image.png](/assets/807ebe8e-023c-4961-9091-eb79cbdc571f.png)

**切面**：这个就是和业务代码没什么关联的公共代码（代理）

**通知**：就是切入到不同业务逻辑中的部分，它包含多个方法。如**切入前**，**切入后**，代表实现业务逻辑前，实现业务逻辑后，常见于**日志**

**切点**：就是切面所能调用的业务逻辑结点。

**增强**：就是被切面调用了的方法。这些方法就是被AOP增强了的方法

**链接点**：切面和增强方法的链接点。

**切入点**：AOP可以控制需要被增强的点，被增强的结点就是**切入点**。

被代理类：

**前置通知**：

**后置通知**：

**前置异常通知**：

**后置返回通知**：

**环绕通知**：就是在这个类中任意一个通知。

## 代理设计模式

实现多个功能时场景时，会出现相同的代理逻辑（日志，显示数据等功能）（这里说的是代理，并非取代所有交互逻辑实现），所以出现了一部分相同的代码。

但是每个功能有不同的业务逻辑（用户数据处理，商品数据处理）

这种情况有两种处理方式**静态代理**，**动态代理**

**设计思想**：

* **后期任务增加**：任务增加，耦合度变大，要分离开来，例如后期要实现（日志，逻辑）等，此时修改代码困难，复用性低
* **分离实现**：就应该和纯业务类（纯计算）代码分离开，这样增强了业务类的复用性，也可以很任意的编写多个**代理逻辑**。

---

### 静态代理

手动创建一个代理类服务于特定的被代理对象，可以登录，然后执行一系列任务，然后再回来。

1.**代理对象**：

2.**被代理对象**：

**缺陷**：

* **代理类编写**：这个是实现代理逻辑的部分，通过实现业务代码接口，然后实现代理部分。一旦出现不同的业务代码，就要编写另外的代理类。**重复了**

### 动态代理

动态代理它讨论的点是，有不同的业务代码时，如果要实现相同的代理逻辑，静态代理就需要编写新的代理类，而动态代理，因为它不用特定的接口，所以共用一个代理逻辑，**省去了编写相同代理逻辑的代理类**，只用在测试的时候导入对应的业务逻辑接口即可。

#### JDK动态代理

动态的创建代理类，服务于被代理对象。这种有两种方式jdk，cglib。

1.**类加载器**：ClassLoader，指定被加载的类获得

2.**指定接口类型**：Class<?>[]  interfaces=new Class[]{ICalculator.class};

3.**委托执行的处理类**：一个处理类，InvocationHandler，最好用一个类实现其接口的方式。然后调用方法。这里面都放的是**代理类的执行方法 **

4.**动态创建代理类**：agent_name o=(agent_name)Proxy.newProxyInstance(classLoader,interfaces,handler);

**使用时**：要用Proxy。他是基于反射的。

**注意**：

* **被代理类调用方法**：它调用的方法都会经过处理类invactionhanderler中。
* **被代理类正真的执行**：实在代理类的执行方法中（inovacationhanderler），调用执行被代理的方法
* **弱点**：必须要传递一个接口。这个调用动态代理时必须要传递一个接口进去，这个接口就是实现所有被代理方法的接口

  ```
          ICalculator proxy= (ICalculator) Proxy.newProxyInstance(classLoader, interfaces, hand);
  ```

#### CGLIB动态代理

这个不是非要被代理类业务方法的接口

**AOP作用**：

* **动态选择代理方式**：识别代理类的功能是否是通过接口实现的，就是service中的impl代码是否实现了接口，可以就用jdk，不可以就用cglib，
* **帮忙放到IOC**：创建完jdk，cglib后会放到ioc容器中
* **更强大**：相较于原来的代码实现代理，这个只用几个注解就可以实现。而且更灵活

#### Spring AOP的简单配置

这个是一个**切面类**，不是上面的**代理类**，

**案例**：service是属于被代理类调用的业务逻辑，代理类会自动生成，而切面类是规则制定者，让AOP自己管理这些切点

**切面类**：给谁增强的信息，是规则的定义者

**代理类**：是规则的执行者

##### 原来的问题

如果给业务类增加代码，如增加日志功能，就会需要手动一个个一个加，现在可以通过AOP切面，切入这些业务类的每一个方法中，不用一个一个加。

1.**添加依赖**：在pom.xml导入aspectj和aspects，

2.**添加注解**：在需要增强的方法（切面）上，标记好@Aspect，将切面交给Spring管理。

这个添加注释后就代表这个是一个**切面**，接下来要编写切入到方法中的前后“新增功能”。

3.**编写切面控制注解**：有5种情况就是上面的前置通知，后置通知，前置异……等。

* **@Before（）**：这个是前置通知，在（）写入execution的路径，可以精确到某个方法，然后在其方法前执行被这个@Before标记的类。
  *：表示所有返回值，或者所有参数类型。

  ![image.png](/assets/b8033297-3fd1-4359-99f8-c7cb16a462fd.png)

  ![image.png](/assets/b845f800-1b03-4f0a-bd72-ee17982cb484.png)
* **@After（）**：这个是后置通知，和上面类似
* **@**

![image.png](/assets/1e5f13ec-4530-4e06-9e11-35d37f9170a6.png)

4.**开启AOP功能**：这个在XML中用下图的字段开启AOP功能

![image.png](/assets/8d5fe6ab-e5b2-4883-b9b0-436a87896bfb.png)

**注意**：

* 要想springaop帮忙管理，就需要将代理类和业务类都在ioc容器中

#### AOP切入点表达式

1.**execution**：这个可以匹配到方法级别

![image.png](http://asset.localhost/C%3A%5CUsers%5CZhuanZ1%5CAppData%5CRoaming%5Ccom.codexu.NoteGen%2Farticle%2F%2Fassets%2Fb845f800-1b03-4f0a-bd72-ee17982cb484.png)

2.**within**：这个只能匹配到类级，只能指定类，类下面的某个方法无法指定

3.**this**：匹配实现了接口的类

4.**target**：

5.**@annotation**：这个匹配到某个类的**注解**，在切面中的@annotation（）写入**完整限定名**，可以精确到某个类想的注解，一般是用的**自定义注解来匹配**。因为有些注解在编译后会消失。

#### 日志记录（after，before，afterthrow，afterreturn）

在上面的切面中编写的代码都只返回了一段话，后期需要从当前切入到的这个方法的方法中获取信息。

1.**获取方法名，参数**：

* 切面方法的参数

  public void before(JoinPoint joinPoint)
* 获取方法名

  StringmethodName=joinPoint.getSignature().getName();
* 获取所有参数

  Object[] args=joinPoint.getArgs();
* 获取一个返回值

  在注释中要加入一个第二个参数，returning="returnValue“。。。。。。在类方法的参数写入Object returnValue，这个returnValue就是返回值。必须是下面的字母，不能错。

  ![image.png](/assets/0a1874bb-fe1f-41d5-8f21-6c8629d28295.png)
* 获取异常数据

  将注释的第二个参数设置为throwing="ex",方法参数设置为Exception ex，

  也可以通过字符流输出异常信息，用于存储异常信息。

  ![image.png](/assets/ee4d9082-c3e0-4137-bfbd-6a554db9e784.png)

2.**在切面中的复用方法**：因为在切面方法中的注释的括号中很多都是一样的，所以可以用一个@Pointcut来做一个方法，通过这个方法名代替这些重用的方法。

3.**可以在5个阶段的注释中**：编写多个条件用&&连接

#### 环绕通知（around）

这个是区别于上面四种通知的一个。它像是一个功能强大的综合同时方法，可以实现上面四个。但是还是上面的四种好操作一些

1.**写注解**：@Around()括号内写切点

2.**编写方法**：public void around(ProceedingJoinPoint joinPoint)这个括号里的东西不能变

3.……

## 用XML的方式实现AOP

这个也叫做基于Schema的方式

可以使用注解方法和xml混合的方式，java中写方法内容，然后用注解来编写aop结构

1.**写父节点标签**：用<aop:config    包裹aop的内容。

2.**aop包裹标签**：

<aop:aspect

3.编写复用切点

<aop:pointcut id="cutAllService" expression="execution(切点位置）>

4.**编写四种通知**：

* <aop:before method="before"  pointcut="切点",这个切点也可以编写多个条件，用&amp&amp连接（因为要转译）
* <aop:after method="after" pointcut_ref="这里就可以用上面的服用切点id代替冗长的切点信息"
* <aop:after-throwing method="……
* <aop:after-returning
* <aop;around

**注意**：

* java的aop方法中有返回值时（异常值返回，结果返回），在xml中要编写returning=”xxx“

# Spring JDBC Template

他是JDBC的一个操作工具

1.**连接方法**

![image.png](/assets/29a41f11-8aa6-47fd-8207-94e3801c9624.png)

2.**获取处理对象**：JdbcTemplate jdbcTemplation=ioc.getBean(JdbcTemplate.class);

3.**查询方法**：直接查询官网https://docs.spring.io/spring-framework/docs/5.2.6.RELEASE/spring-framework-reference/data-access.html#jdbc

4.**具名JDBC Template**：需要改xml的class，改为NameParameterJdbcTemplate，用constructor-arg type="AAA"的方式注入，调用时用map传入参数。

# Spring声明式事务

**事务**：将一组业务当成一个业务来做，要么成功，要么失败，保证业务的完整性操作。

**事务四大特性**：ACID

* 原子性：要么都超过要么都失败。
* 一致性：事务前后的数据要保证数据的完整性，相互守恒。
* 隔离性：并发情况下事物之间要相互隔离。
* 持久性：数据一旦保存就是持久性的，

**编程式事务**：在代码中直接加入事务的逻辑，**开始传输**，**提交事务**，**回滚事务**。

**声明式事务**：直接在方法外部添加注解，或者直接在配置文件中定义，将事务管理代码从业务从业务代码中分离出来。这个就是用到了AOP的功能

**步骤**：

1.**配置事务管理器**：在xml中编写

![image.png](/assets/0e601946-0935-4058-ae7e-6b0b0936095e.png)

2.**开启事务注解方式**：一个字母都不能错，提示的代码注意要选择tx结尾的，别的不行。

![image.png](/assets/467a07f0-086b-45f8-8009-42c8f7a4bc92.png)

1.**标记业务代码**：在业务代码类上面添加一个**注释@Translational，就能实现事务的四个特性。

* 注解有两个位置，类上，方法上，一个局部一个是整个类，建议写在逻辑层上。

2.**设置隔离级别**：isolation，可以解决并发的问题

* **脏读**：在transactional注释中添加isolation=isolation.READ_COMMITTED,
* **不可重复性**：就是执行这个数据期间发生了数据变化，添加REPEATABLE_READ可以上锁不让别人操作这**行**数据
* **幻影读**：这个针对的是**多行**数据，在统计信息期间出现，行的增删改，通过增加SERIALIZABLE,防止别人操作这个**表**。性能比较差。

## 事务传播行为

1.**required**：这个表示的是service中一个嵌套的方法，内部被标记为事务的话，外部若有事务存在，就会合并到外部中，等同于外部有标记，内部没标记

2.**supports**：外部不存在事务就不开启事务，存在事务就融入到外部事务中，表示这个方法他可以单独执行，例如中途查询是否对错的查询功能。

![image.png](/assets/ad3447b2-01f7-4dd9-9bd0-6fc0d0c4d8de.png)

3.**required_new**：挂起外部事物，创建新的事务。

这种是用在日志事务中的一个方法，因为原来的事务中途出错会回滚到原来的状态，导致记录日志的事务也发生回滚而记录失败，标记上这个后，执行到这个required_new事务就会挂起原来的事务，这个new的事务完完全全执行完后，再恢复原来挂起的事务，若中途出错不会影响日志。

5.**超时属性**：设置一个时间，time=2，超过这个运行时间就报错。

## 基于XML的事务

也是通过切点的方式精准添加**事务**，这个方法更方便

1.**编写公共切点标签**：

<aop:pointcut id="transaction" expression="execution(* cn.t……)">

2.**编写事务标签**：

* **声明标签**：<tx:advice
* **声明事务权限**：哪些方法要用事务，

  ![image.png](/assets/64f172cc-0d8d-4495-af63-e86735225344.png)

# 源码讲解
