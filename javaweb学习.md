## 环境配置

**JRE**:java runtime environment
是运行 Java 程序的 “运行环境”，包含 Java 虚拟机（JVM）、Java 类库等，**仅能运行已编译的 Java 程序**，不能用于开发。
**JDK**Java Development Kit
是 Java 开发的 “工具包”，**包含了 JRE**，同时还提供了编译器（`javac`）、调试工具、文档生成工具等**开发必需的组件**。

## idea

**bootstrap项目启动，引导**
Spring Boot 项目：必须有 Bootstrap 启动类（比如 `TakeawayApplication`），你点击 IDE 的 “运行” 按钮，本质就是执行这个类的 `main` 方法，引导项目启动（加载配置、启动 Tomcat）。
**Facets**
给项目贴的 “类型标签”，决定 IDE 提供什么开发工具支持：IDE 就会自动适配相关功能（比如显示 Tomcat 部署选项、识别 Servlet 类）。

**Artifacts**
项目的 “成品包”****IDE 或构建工具（Maven/Gradle）打包后生成的 “最终可运行文件”****
**Deployment**
把 Artifacts（成品包）放到服务器 / 容器中，让项目可运行的过程。
**以上四个是专属于idea中的操作，该项目放在eclipse中也可以运行**

## 组件

都是java生态的打包，分发，部署
**JAR**：java archive
JAR 面向通用 Java 程序 / 组件
用于把各种结构类打包成一个压缩文件
**WAR**：Web Application Archive
WAR 专门面向 Java Web 应用
把所有web应用的所有资源打包，专门部署到web服务器中

## 目录结构

**resource:**存放java文件的地方
**xml**存放web的配置文件
**jar**依赖的包
**WebContent**存放web的项目文件

### 学习流程

前端：

1.**html**：头部，主题，文字与段落，列表，图片，

2.**web** ：，

3.**css**：

4.**div**：布局设置

**jsp**：

### Servlet

使用它需要继承**HttpServlet**

1.运行在web服务器上的java程序，他就是一个java类，一个用于和服务器交互的java类

2.他是一个中间层，**连接浏览器和服务器的中间层**

3.负责链接来自web浏览器和其他http客户程序和http服务器上的程序

4.读取客户端发送的显示数据

5.读取浏览器的隐式请求数据，http请求头等

6.servlet和jsp讲结果包装在html中，浏览器向服务器传送信息

7.将包装好的html，用http发出。

**核心方法：**

**init**：实例化

**destroy**:servlet对象被销毁前的调用

**service**：没收到一个http请求调用一次

**doGet，doPost**:收到get,post请求时，有service的方法来调用 ,在没有重写他俩的时候，他俩都差不都

#### doGet

用于响应浏览器发来的method="get"

1.参数在**URL**，参数直接挂在http的后面，可以直接看到

2.适用于没有隐私的数据，

3.适用于查找数据

#### doPost

用于响应浏览器发来的method="post"

1.参数在**请求体**，不能直接看到

2.适用于比较隐私的数据，比如修改数据时

3.适用于修改数据

Servlet中的doXXX方法会根据请求计算响应，并把响应数据设置到HttpResponse对象中，然后tomcat就会把这个httpresponse对象通过socket协会给浏览器。

**注意**

1.**他在运行时会被容器实例化为“对象”**

2.就是处理本次请求的那个“**Servlet**”对象，它**等同于**，识别@webservlet后用于交互的实例对象。如下图的**demoServlet1**

这个**对象**就是启动 Tomcat 后：

* 1.容器会： 扫描项目中带@WebServlet的类；
* 2.通过反射创建DemoServlet的实例对象（默认单例：整个项目中只有 1 个DemoServlet对象）；
* 3.把这个对象存到内存中，等待处理请求。Tomcat 启动后创建的 Servlet 对象，会一直存在于 JVM 内存中，直到 Tomcat 停止 / 项目被卸载；无论处理多少次请求（1 次或 1000 次），都是同一个对象在干活，不会销毁重建。

![image.png](/assets/cc460108-c89c-4b08-867b-48c24a2a7a78.png)

### **Tomcat**

tomcat会把收到的http请求按照http协议格式解析成一个httprequest对象。（也就是上面的servlet发出的http）

## 数据交互

案例1：xml+html+java

**这个是javaweb最主流的数据交互方式**

1.**html** :页面写入，输入了显式数据，用一个方法action获取**拦截**输入。

2.**xml**映射绑定 ：将html

获取到数据的关键字（要位置）的名字和

使用数据的位置的名字绑定（同名）

3.**调用**：然后java就可以利用xml调用html拦截的数


| 方式                   | 技术栈                      | 特点                                                           | 适用场景               |
| ---------------------- | --------------------------- | -------------------------------------------------------------- | ---------------------- |
| **Servlet + JSP/HTML** | 传统 Java Web（如你的描述） | 基于服务器端渲染，通过`request.getParameter()` 获取表单数据。  | 传统企业应用、遗留系统 |
| **Spring MVC**         | Spring 框架                 | 使用`@Controller` 和 `@RequestMapping`，简化配置和数据处理。   | 现代 Java Web 项目     |
| **前后端分离（API）**  | Spring Boot + Vue/React     | 前端通过 Ajax/Fetch 调用后端 REST API（JSON 传输），完全解耦。 | 现代 Web 应用、移动端  |

* **核心机制**：依赖 **Servlet API** 和 **HTTP 协议**，通过 `web.xml` 配置请求映射。
* **数据流**：
  `浏览器 → HTTP 请求 → Tomcat → web.xml 路由 → Servlet → 获取参数 → 业务处理`
* **局限性**：
  * 前后端耦合（HTML 和 Java 逻辑混合）。
  * 配置繁琐（需手动编写 `web.xml`）。
  * 不适合复杂交互（如实时更新）。

### WebServlet交互

传统的xml映射交互繁琐

在Servlet3.0后就可以用WebServlet来交互，直接一个注解就可以了。

@WebServlet(name="demoServlet1",urlPatterns= {"/getParameter","/getParameter2"})

**name**：Servlet 的 “逻辑名称”（等价于 xml 中`<servlet-name>`），是Servlet的唯一标识。

**urlPatters** ：是客户端的拦截标识

**@WebInitParam**：也可以用他来初始化xml的内容

例如下图

![image.png](/assets/5daae266-bbb8-4a0f-b008-f569d8c88edf.png)

他代替了

![image.png](/assets/cb46093a-5191-4a0d-a243-f7d1ea71039d.png)

### HttpServletResponse

这个也是servlet的，用于服务器传回到浏览器，

**void setHeader();** 用于覆盖原数据的方法，例如三秒刷新一次数据。

**void setContentType(String type)**:用于设置发给客户端的**数据的格式**

**void setCharacterEncoding(String charset)**：设置被发送客户端的**响应字符编码**

**void sendRedirect(String location)**：制定重定向位置URL，通过httpsServletresponse来重写url

![image.png](/assets/9affcb6f-dce0-47d9-bda7-a57f756f21f9.png)

**PrintWriter getWriter()**：用于body写入文本格式数据

### Servlet API

Servlet是MVC中controller的底层实现组件

他还是javaee中的一组接口和类，用于开发**服务端**的程序处理web请求，他提供了标准的方式来处理http协议，是java web开发的核心。

**核心组成部分**：

1. **接口和类**（如 `javax.servlet.*` 包中的内容）。
2. **生命周期方法**（如 `init()`、`service()`、`destroy()`）。
3. **HTTP 相关方法**（如 `doGet()`、`doPost()`）。
4. **请求/响应对象**（如 `HttpServletRequest`、`HttpServletResponse`）。

Servlet **不属于独立的 “层”**，而是**MVC 架构中 Controller 层的 “底层实现组件”**

## throws

![image.png](/assets/174e32a1-c933-4846-ab7f-b8842efbd9ee.png)

在重写方法中的throws，这个必须有，没有也会因为这个javaweb的重写方法没有throws而报错

表示声明该方法可能抛出的Servlet异常和IO异常

protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {     // 父类默认实现 }

## Servlet生命周期

tomcat启动到销毁

1.初始化servlet

2.中途无论怎么使用，只要没有终止运行（关闭tomcat），就不会再次初始化

3.知道销毁，关闭服务时，servlet销毁，这时就是真的结束了。

## **ServletConfig**

servletconfig就代表servlet中xml的配置信息，它可以或者这些信息。

### ServletContext

1.每个web工程都只有一个ServletContext，

2.就是说项目的每个位置都时同一个对象

### Servlet请求转发

#### setApplication（）会话响应

他是一个用于当前会话中的存储功能的组件

1.他存储的是一个对象，是一个特殊的对象

2.可以扩大范围的传递数据

3.他的生命周期可以自定义

4.他存储的地方是所有Servlet都可以访问到的”公共存储容器“

![image.png](/assets/b70d10f9-6d0f-4dbd-92d1-18b7cbcc71f4.png)

可以看到，setApplication的作用是存储数据的作用，这样就可以实现多个servlet对象的共享数据，以及数据的持续处理，同样是处理数据，getParameter的作用是访问前端数据。

1.因为getparameter到变量的数据别的servlet访问不到

**不同的Servlet**：最直观的就是不同的.java**业务代码**。

2.要想让别的servlet能访问到，需要提前设置一个全局变量用于穿甲你全局对象

**关于跨范围访问数据，为什么用到全局变量了，还需要用到这个关键字**

1.自己设置全局变量只是造了个**容器**

2.全局变量的访问秩序可直接由set application负责

3.他会记录当前servlet交流的id（自己识别的Session ID），不用自己设置名字

4.生命周期，数据类型由setapplication自动处理。

5.内部的线程，锁也由setapplication负责，省去了自己编写锁逻辑。

![image.png](/assets/5863a96d-a4b3-4930-a733-24a6ca377267.png)

### setAttribute()存储到对象中

实现了 **“一次处理，多处使用”** 的临时数据传送机制，优化了数据流，但前提是数据已通过 `getParameter()` 或其他方式获取。

![image.png](/assets/e0c10e5c-e5e1-4352-b64f-baa693e52980.png)

`attribute` 是 “绑定数据的通用方法”，参数统一，功能仅 “存 / 取对象”，无额外能力；

#### req.setAttribute()存储到请求范围

#### session.setAttribut

```

```

e()存储到会话范围

### RequestDispatcher.forward

把资源请求转发给另外一个servlet

1.他和setApplication的作用完全不同

2.他是**请求转发的作用**

**setApplication和setAttribute**可以把数据存储到公共区域

1.但是具体要看是哪个存储区，

2.如果是存储到当前的request对象中，则必须要用requestdisptcher转发才行。如果是别的就不用。

3.**接受方，使用getAttribute来获取转发**

**注意**

1.requestdispatcher（）的参数是转发的目的servlet路径

2.此处的forward（）的参数是

![image.png](/assets/47a4899e-644d-4332-8267-381b2d5157e9.png)

3.客户端调用`doPost`传递的数据，**不是必须用`req.setAttribute`** ——`req.setAttribute`的本质就是「后端临时存储数据的工具」，用不用全看你是否需要在**多个 Servlet / 组件间共享这份数据**。

4.**如果想把浏览器通过 doPost 传递来的数据，交给另一个 Servlet 处理，就必须用 RequestDispatcher 转发；如果只是在当前 Servlet 处理完直接响应浏览器，就完全不需要。**



### 请求重定向

如果A传给B处理这个请求，如果B处理不了，就会转发给C

1.会和请求转发不一样，转发是只发了一次，而重定向发了**两次**

2.他的url会改变

3.
