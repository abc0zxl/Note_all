# 错误

1.**参数数量不匹配**：mapper中录入的参数数量和数据库中的列名称数量不匹配需要在insert中声明好那个列名对应哪个实例。

2.**数组**：是int[] id;

3.**mapper中的数组**：MyBatis 对于**无注解的数组类型参数**，不会自动关联自定义名称 `dels`，只会给它默认的参数名：`array`，要用@Param 声明一下

4.**外键约束**：已经被购物车收取的商品id，现在处于外键约束状态，不可以删除该商品

5.**页面分页**：这个用的是sql语句实现的。定义开始和数量，实现显示特定页面的功能

6.**service和servlet**的方法名不能一样

7.**条件查询**：如果要分页的话也要带入分页的内容进入service，还有**动态sql**

8.**sql传入的参数**：如果是只传入了一个对象没有@Param的话，sql里面可以直接用他的方法，不用加brand.

9.**模糊查询**：%和like相辅相成，缺一不可，在查询字段两边加上%才能实现模糊查询，左右两边的%分别表示从两边扩展字符

10.**获取json**：用请求获取字节流，获取json字符串

11.**携带数据的请求**：需要将get修改为post

12.**关键字大小写**：Null不等于null

13.**this**：在axios的函数体中用不了this去标识**vue对象**，要在外卖呢声明一个变量回调到函数体中

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

## 学习路径

![image.png](/assets/c327b70b-82f1-4a1c-b7d5-5abe6ebc7e3a.png)

### Servlet

使用它需要继承**HttpServlet**

1.运行在web服务器上的java程序，他就是一个java类，一个用于和服务器交互的java类

2.他是一个中间层，**连接浏览器和服务器的中间层**

3.负责链接来自web浏览器和其他http客户程序和http服务器上的程序

4.读取客户端发送的显示数据

5.读取浏览器的隐式请求数据，http请求头等

6.servlet和jsp讲结果包装在html中，浏览器向服务器传送信息

7.将包装好的html，用http发出。

#### 使用方法

1.**导入Servlet**

![image.png](/assets/625fc638-83b1-4f16-b914-126f0a91c1d8.png)

2.**实现Servlet的接口**

public class sevlettest1 implements Servlet{}

3.**编写@WebServlet注解**

配置Servlet的访问路径

4.**启动**

启动Tomcat，输入URL，访问该Servlet

**核心方法：**

**init**：实例化

**destroy**:servlet对象被销毁前的调用

**service**：没收到一个http请求调用一次

**doGet，doPost**:收到get,post请求时，有service的方法来调用 ,在没有重写他俩的时候，他俩都差不都

## Get和Post

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

### 设计，使用

1.**获取该对象是post还是get**：

* 获取请求对象
  HttpServletRequest reqest=(HttpServletReques) req;
* **获取方法字段**
  String method=request.getMethoed();
* 判断字段
  "GET".equals(method)

## **Tomcat**

tomcat会把收到的http请求按照http协议格式解析成一个httprequest对象。（也就是上面的servlet发出的http）

### 状态码

![image.png](/assets/cc761b36-13d4-4c9d-87ee-2ca388173c3b.png)

![image.png](/assets/de39551d-f941-41d5-be53-2592ed11c1f8.png)

### tomcat使用

1.**使用本地的tomcat**

* add configuration
* 选择Tomcat->Local
* 选择Tomcat的安装路径
* 部署项目，Deployment
* Artifact
* 选择自己的项目

可以在tomcat的设置页面设置**默认浏览器**和**端口号**

2.**在XML中配置Tomcat**

他用的不是本地的tomcat，而是在库中现成下载

* ![image.png](/assets/d368a6dd-313b-465e-87a5-4da4458c68aa.png)
* 运行这个XML，就完成了配置

## HTTP

1.给予TCP协议，面向连接，安全

2.一次请求对应一次响应

**缺点**

1.多次请求不能共享

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

**urlPatters** ：是客户端的拦截标识，在这里设置的地址，**表示这些地址都可以访问到这个java文件的方法**

* 他含有四中匹配方式
* **精确匹配**
* **目录匹配**
* **扩展名匹配**：
* **任意匹配**：
* ![image.png](/assets/35d80541-e05c-4f37-85cc-ae4eff400d43.png)

**@WebInitParam**：也可以用他来初始化xml的内容

例如下图

![image.png](/assets/5daae266-bbb8-4a0f-b008-f569d8c88edf.png)

他代替了

![image.png](/assets/cb46093a-5191-4a0d-a243-f7d1ea71039d.png)

### HttpServletRequest

是java提供的对HTTP协议封装的请求对象接口

如果要使用request对象的功能，就去查阅api文档的httpservletrequest接口。

1.**获取请求行**：就有点像各种路径

2.**请求头**：

3.**请求体**：下面是**字符流**和**字节流**获取

* **BufferedReader br=req.getReader()** 用这个就能获取post或者get中传递的信息
* **ServletInputStream getInputStream()**:也是获取信息

#### 快捷Servlet方法中的框架

用这个方法可以直接生成@WebServlet，throws，doget，dopost等框架

1.点击包名，右键

2.选择**Servlet**

#### get，post乱码解决

1.**Post乱码解决**

* 因post有默认的字符输入流的解析方式，所以会乱码
* request.setCharacterEncoding("UTF-8")

2.**Get乱码解决**

* 因为get不是用的流方式读取，而是用的字节流getStream(),
  1.因为get的乱码是双方的编码方式不匹配的问题
  2.且tomcat方的解码方式不能修改
  3.但底层的二进制是不变的
  4.在tomcat8后就修复了get的乱码，不用再主动处理
* **字节转换方法：**
  1.**转换为字节**byte[] bytes=decode.getBytes(charsetName:"IOS-8859-1")
  ![image.png](/assets/f6a5e12c-5233-4771-bffb-701653f6820d.png)
  2.**转换为字符串**：String s=new String(bytes,chasetName:"utf-8")

#### 请求参数的获取

在方法中重写两个doget和dopost方法，利用之前学的请求方式判断方法，然后就能调用对应的参数获取方法

**获取方法**

1.**get请求**：用getQueryString()

2.**post请求**：用getReader()和readLine()

3.**公共获取方法**：

* 前端请求参数传递过来时，会形成一个Map键值，内部包含一个名字和若干个参数合成的数组
  Map<String,String[]>
* **获取键值对**：可以直接获取整个Map，或者他的参数组，或者单个值
  1.Map getParameterMap();
  2.String [] getParameterValues(String name);
  3.getParameter(String name);这个最常用

### HttpServletResponse

这个也是servlet的，用于服务器传回到浏览器，

1.**void setHeader();** 用于覆盖原数据的方法，例如三秒刷新一次数据。**还能覆盖当前的访问地址，达到跳转的效果**

2.**void setContentType(String type)**:用于设置发给客户端的**数据的格式**

3.**void setCharacterEncoding(String charset)**：设置被发送客户端的**响应字符编码**

4.**void sendRedirect(String location)**：制定重定向位置URL，通过httpsServletresponse来重写url，例如，登录成功和失败时会跳转不同的页面，这时就需要他了。

![image.png](/assets/9affcb6f-dce0-47d9-bda7-a57f756f21f9.png)

* 关于路径的设置问题，什么时候用虚拟目录什么时候用不需要虚拟目录
* **需要**：如果请求是从浏览器发出，后端服务器要接受处理的情况就需要

  ![image.png](/assets/fb80a1c5-b5e0-4fdf-bac3-7254f34408d4.png)
* **不需要**：如果从浏览器发出只在前端间做跳转就不需要
* **动态获取目录**:这个可能会遇到代码目录有变动的情况，就会全部修改路径，可以用**getContextPath（)+跳转的地方**,

5.**PrintWriter getWriter()**：用于body写入文本格式数据

* **setHeader**：正常情况只返回子字符串格式，**
  1.获取字符流对象**：用getwriter获取
  2.respongse.setHeader("content-type","text/html");配合write将返回http格式的文本
  3.![image.png](/assets/4cbff214-cd82-4837-b773-f377488e1e07.png)
* **乱码解决**：同时设置字符格式和字符集
  respongse.setContentType("type/html;charset=utf-8");

6.**getOutputStream()**: 用于文件的输出，而设置的字节输出流.将字节输出到别的地方。例如下图输出一个文件

![image.png](/assets/9122f8d2-68a2-4e16-8d83-9002c26c3687.png)

* **字符输出方式**：如上图，比较繁琐
* **工具输出**：IOUtils.copy(fis.os);这一行代码就能完成上面的**3**.

  **注意前提**：这个需要一个**工具类**，在XML中导入坐标**commons-io**,2.6

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

1.**开始**：servlet第一次被访问时开始，由容器创建servlet对象

3.**初始化对象**：在创建对象后，容器将调用servlet的init（）方法来初始化这个对象。完成一些配置工作，**只调用一次**；

2.中途无论怎么使用，只要没有终止运行（关闭tomcat），就不会再次初始化

3.**销毁**：关闭服务时，servlet销毁，用的时destory（）这时就是真的结束了。随后会被java的垃圾收集器回收

### Session

他从申请session生命周期开始，中途不会结束

**结束条件**：

1.30分钟自动超时，或者通过Web.xml来设定超时时间

2.重启Session。

3.利用session.invaildate关闭会话。

### **ServletConfig**

servletconfig就代表servlet中xml的配置信息，它可以获得这些信息。

1.**获取配置参数**：ServletConfig

2.**返回配置参数**：getServletConfig

### ServletContext

1.每个web工程都只有一个ServletContext，

2.就是说项目的每个位置都时同一个对象

## Servlet请求转发（forward）

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

3.数据（生命周期）问题，为什么AServlet第二次转发时，数据已经消失。

#### **关键机制：`forward()` 的“控制权移交”**

1. **`forward()` 是终点操作**：
   当 `AServlet` 调用 `dispatcher1.forward()` 时，它已将请求的**控制权完全移交给 `BServlet`**。`AServlet` 中 `forward()` 之后的代码不会执行（除非抛出异常）。
2. **请求响应周期结束**：
   `BServlet` 处理完成后，直接向客户端发送响应，整个请求结束。`request` 对象被容器回收，所有请求属性丢失。
3. **无法“接力”转发**：
   同一个请求不能多次调用 `forward()`，因为第一次 `forward()` 后响应已提交或关闭，再次操作会抛出 `IllegalStateException`。

4.重定向需要完整路径

5.**重定向（`sendRedirect`）默认会用 GET 方法请求目标 URL**

**getContextPath()**获取当前路径

![image.png](/assets/822c4b55-ac04-41d6-b53e-7d11af6bfa18.png)

#### 转发链

使 A → B → C 形成**转发链**，只要数据存储在 `request` 中，它就能在链中传递（因为 `forward()` 传递同一个 `request` 对象

#### 解决方法

可以利用Session来保持数据。

```
		HttpSession session = req.getSession(false); // false：不创建新Session，避免空数据
```

## 完成CRUD操作

### 步骤

1.编写Mapper接口，以及内部的方法List<Brand

2.利用插件辅助，完成sql映射文件的创建，编写id

3.完成对实例的书写，内部编写，方法和返回

3.执行，测试

#### 注意

1.当实体类的名字和数据库的名字不一样时，可以给sql映射文件中设置别名，这个别名和实体类中的名字一样

![image.png](/assets/d6de2393-0be5-481d-ba40-2203bac7e2b0.png)

也可以用<sql  标签来写一个公共的，因为数据库中大部分都是一样的名字，然后就可以编写一个公共的sql片段来使用

但是这种方法还是不灵活，因为sql片段，只能返回片段中的名字，别的不返回。

2.可以额外定义一个映射标签，用于书写单个实体类中的别名

**<resultMap id="" type=""**

<result  column="" property=""

这个type为实体类，

column为表的列名字，

property为实体类中的属性名字，**完成映射**

这样sql的返回类似type就写为**resultMap中的id**

### 条件查询

比如利用id来查询对应信息

例如一个信息表种，一行后方有一个按钮，对应的时这一列信息的其他信息，这是就需要获取他的id，更具id来查询信息

![image.png](/assets/96c5ea3b-2897-4dd9-8a0d-f9212af6b940.png)

sql的id占位符

1.#{id}：会自动换成？，这个能防止sql注入，可以用在参数传递的时候

2.${id}：这个时直接拼接，可以用在表名，列名不固定的地方

```
    <select id="selectTyPe" resultType="goods">
        select *from
        goods where id=#{};
    </select>
```

#### 多条件查询

mapper如何传入多个参数，有三种方法

散装参数，对象参数，集合参数

#### **散装方法**：

1.sql正常写，多少个条件，就多少个#{}；

2.在Mapper接口上有变动，需要用一个**注解@Param**

##### @Param

**语法**：@Parameter("AAA")int BBB

这个可以在参数括号中**随意排放**，表示sql语句中的AAA就用BBB替代，这个就是传参

#### 对象参数

在调用sql的java文件的地方

1.创建一个实例对象

2.调用对象的方法（列名），传入参数

3.传入对象

#### 集合参数

1.用Map的HashMap（）方法创建一个对象

2.创建对应的**键值对**

3.在原来的位置传入对象就可以

#### 缺参数查询（灵活查询）

**问题**：原来，条件查询需要所有参数都写入才能查出来，因为传入时，把参数修改成null

**解决**：

1.编写**动态SQL**，当传入**非空**和**非'' **时，才修改sql的条件。这样就解决了缺少参数时的查询。

2.动态sql，中存在字段矛盾的问题，可以用

A:**恒等式，补充上这个位置**，或者用

B:<where 标签，他会自动去除**and**

![image.png](/assets/2f4c00f1-6798-44df-8a0d-71d3098546cd.png)

C.**单条件查询**：就不用where和and了用 **<choose** 和 **<when test =** 分别代表了c语言的switch和case

D:**模糊查询**：%和like相辅相成，缺一不可，在查询字段两边加上%才能实现模糊查询，左右两边的%分别表示从两边扩展字符

在test中写入参数写入条件

在<when中写入条件

当一个条件参数没有传入时，sql语句会错误，可以利用otherwise写入一个恒等式

### 数据插入

和上面的差不多，但是录入到数据库时，需要输入到数据库

1.**手动提交**：手动编写sqlsession.commit();来提交数据。

2.**自动提交**：可以在sqlsession的方法括号中写入，autoCommit：false，

#### 注意

1.主键不能主动输入

2.idea插入成功但是commit失败的数据，当有一个成功时，之前的都会接着录入

#### 插入后获取id

插入后有时需要获取这个插入的id，进行其他操作，但在录入到数据库之前时没有分配主键id的，所以无法获取

**insert标签**

使用下面的语句，把insert的sql语句插就去，就可以获取id

<insert id="aaaa" useGeneratedKeys="true" keyPropert="id"

1.这个id是实体中的名字

2.在java文件中需要用   **对象.getId()** 获取id

### 修改数据

用的是**<update**  标签

#### 注意

1.他有返回值，影响的行数

2.他的sql语句可以不用像插入一样声明变动的列表名字

3.他在特殊的场景下需要通过**动态sql**让修改数据变得灵活

### 删除数据

1.**单个删除**：按照常规方法写就行，使用<delete 标签

2.**批量删除**：例如例表中，通过复选框批量操作列表

本质上是一次性提交多个id，让程序操作

#### 批量删除

需要在**接口的输入值**和**sql的编写**做一些变动

1.**接口输入**：输入一个复选数量(@Param ids int[] ids)

用于sql中的   ？   的变化

2.**sql编写**：MyBatis会将收到的数组参数，封装为一个Map集合，可以要用@Param改变原来的**array**这个名称为ids，所以collection要么用**ids**，或者**array**

where id in （？？？？？）

**改写为**

where id in

<foreach collection="array" item="id" separator="," open="(" close=")"

#{id}

</foreach

### 注解完成CRUD

如果使用注解的方式的话，就不需要写xml文件了

1.在方法上面写一个包含sql的注解就好了

![image.png](/assets/74750d30-803e-4e13-a6f9-16abecdb794f.png)

2.仅适用于一些简单的功能，复杂的功能还是要在xml中写

**注意**：返回要使用实例对象来接住返回。

### MyBatis的接收参数

mybatis对各种各样的参数有不同的封装方式

#### 单个参数

POJO，Map，Colletion，List，Array，其他

**POJO**：可以直接使用

**Map**：也可以直接使用，注意名字即可

**Collection**：mybatis会识别这个参数的数量，然后看是不是Collection，

是的话，用map的创建一个键名为collection，

{collection，num集合}

{arg0，num}

如果是List的话创建一个键名为list

{list，num集合}

1.如果声明的是Collection的话，mybatis创建的map至少有2个键

2.如果是List类型的话，至少有三个键

**Array**：就只有两个键

{arg0,num集合}

{array,num集合}

#### 多个参数

他会将多个参数封装为map集合，他的键，是自己设定的键名字，

通过@Param注解，来辨别是不是多个参数

1.他每个参数都会写两个键值，argX，paramX，可以通过键名的预测直接在sql中写入这个名字，也可以正常运行

![image.png](/assets/77c0de56-767c-4e97-87da-7836872c8363.png)

2.当使用了@Param后，用@Param设置的名AAA，Mybatis会将原来的键名改成AAA

#### 综mybatis参数所述

尽量利用@Param注解，创建名字，修改map中的默认名字，让读写更加方便

# 功能实现

## 登陆注册模块

**步骤**

1.填写提交到LoginServlet

2.在LoginServlet中使用MyBatis查数据库验证是否正确

3.如果正确则登录成功

**注意**：

1.注意复制粘贴过来的代码，他的**名称空间地址**

![image.png](/assets/8c2af2c7-4133-4462-a62b-f14f0ab373d7.png)

2.还有配置文件中的地址，**都是从java文件夹开始的地址**

告诉他实体类在那个地址

![image.png](/assets/5a41af86-4cf6-4622-b38f-6f4e93856434.png)

告诉他Mapper文件在哪个地址

![image.png](/assets/fe830fbb-1c3d-4725-858f-abab68678762.png)

## 注册模块

1.**填写信息**：用户填写用户名，密码，点击注册，提交到registerServlet

2.**用Mybatis**：保存数据

3.**判断用户是否已存在**

**注意**

1.**返回类型**：Int和Integer不一样，Integer可以返回null，而Int不行

2.**检测插入成功**：最好的方法还是获取他的id。

![image.png](/assets/39a95fae-35f6-4f7a-8ef1-710e465baf7e.png)

在编写sql时，改成（count *）也可以解决返回类型不匹配的问题

## 工具类

用于解决代码重复编写的问题，

1.这种属于初始化Unit

2.因为重建sqlsessionFacotory是要被创建多次，所以可以用一个方法类，其他的用静态表示即可。

![image.png](/assets/2d60d162-b9ff-4bc9-8ef9-7783300688c7.png)

**注意**：

1.**导入类**：jsp中也可以像java一样写代码包括导入类，用<%括起来就好了

# javaweb四大域对象

1.**page**：当前页面有效

2.**request**：当前请求有效

3.**session**：当前会话有效

4.**application**：当前应用有效

# EL表达式

用于简化jsp页面内的java代码，用于**获取数据**，

**语法**：${expression}，如果想通过EL表达式获取数据，就要把数据存到四个域对象中。

在jsp中就能显示{中表示的java代码}，**注意**，要用<%@ page isELIgnored="false" %>才能显示数据

![image.png](/assets/ea3e211f-57cb-4592-b84a-06d2c8edc3ef.png)

**原理**：EL表达式他会去四大区域中找，从1~4逐渐扩大，直到找到目标为止

## JSTL标签

这也是一种替代jsp中的java代码的一种方案

**用法：**

1.**在XML导入坐标两个**：

![image.png](/assets/88df5c54-04e8-4066-98cf-04bd27e74622.png)

2.**在jsp中导入标签库**：

![image.png](/assets/d81245ea-ff23-4946-b7e9-e76db2a49d12.png)

3.**就可以使用jstl的功能了**

4.**嵌入java**：用${java……}嵌入即可

5.**排序号**:在foreach中写入**varStatus=”status“**

**注意**：

1.**自动解析**：jstl有自动解析功能，必须要用pojo中的实体类的类方法的名字。

2.**不显示数据**：因为没加解析数据的声明

**<%@ page isELIgnored="false" %>**

# 案例实现

## 准备环境

1.创建模块（就是新建项目），引入坐标xml

* 注意xml中一定要改为war包格式，**因为war是web项目的核心标识，默认情况是jar包，jar包表示的是java项目**
* XML:Mybatis,mysql,servlet,jsp,jstl,taglibs,tomcat(插件用<build),

2.创建三层架构的包

* web:放
* util：放工具类
* pojo：放实体类
* service
* mapper：放接口
* Dao层:放接口

3.创建数据库

4.实体类创建Brand

5.创建Mybatis

* **核心配置包**：mybatis-config.xml（必须是这个名字，中间斜杠不能变）mybatis配置文件要放在sql映射文件同目录下。
* **mybatis中的mappers标签**：resource 属性要使用 / 分隔（类路径），而不是 . 包名形式
* **sql映射文件**：需要和mapper同文件夹
* **写mapper**：写接口

## 注意

1.**路径问题**：

* 前端请求路径：![image.png](/assets/ba2a1632-b850-4daa-a32d-614e9f0f3994.png)
* 实例对象的书写：正常情况是都把列名写上，如果是写了部分，就会报错500，
  1.因为用的sql语句是全部查询select*from product
  2.mybatis会按照顺序去调用构造器，结果数据类型和结果不匹配，强制转换后报错。
* **解决方法**：在实例中加一个**无参构造方法**
* 一旦有无参构造 + setter，MyBatis 会选这种方式：他会先更具列名对应的setxx，它就不会再用“构造器按顺序硬塞值”的方式，类型就不会对不上。
* 注意 XML 里要用 **&amp &**

## 获取数据库表数据

1.**创建util，mapper**：创建工具类减少代码的重复性，sql的调用类

2.**创建service**：写一个方法类，类中实现了获取一个输入流，factory，在获取一个sqlsession对象用于执行sql。

3.**创建Servlet**：处理请求，以及去调用Servlet中的方法，封装数据到列表，在转发到jsp中

![image.png](/assets/06b1004f-becf-4861-8a07-376e08191056.png)

4.**链接**：检查各个链接点是否正确，

5.**编写前端**：编写jsp+jstl+EL，让数据显示到页面上

* **编码方式**：注意前后端编码方式
* **注意加导入EL类**：不然显示会有问题<%@ page isELIgnored="false" %>
* **属性名称和数据库名称不匹配**：这种情况会导致空列，这时需要在sql映射文件中修改，将名字替换成正在使用的名字，然后将这一标准用注解@resultMap传回mapper中。

![image.png](/assets/61011af4-62b4-4a5c-ba5a-d32c28c62565.png)

通过`column="brand_name"`（数据库列名）和`property="brandName"`（Java 属性名）的映射，能解决列名不匹配的问题

## 插入数据

1.**定义sql**：

* 在mapper中注意要用@Param(AAA) String BBB,这个AAA表示sql映射文件中的调用的名字，BBB只是局部变量。
* **参数不全**：sql需要显式声明写入的参数

2.**编写service**：创建工厂类，编写执行sql的语句，写回数据库。

3.**编写页面跳转逻辑**：在按钮页面用，写入跳转逻辑

script

![image.png](/assets/8a7a28e9-cf32-4c8e-8c90-508e2aea85fe.png)

4.**编写html写入页面**：注意跳转到对应的sevlet

5.**编写Servlet**：调用service，写入数据，再用

```
request.getRequestDispatcher("/viewALL2").forward(request,response);
```

跳转到用于显示所有数据的servlet，执行这个java代码，他是间接显示到界面，因为，此处的跳转是java文件，在这个servletjava文件中有跳转到jsp的代码所以实现了页面显示。

**注意**：这个/viewALL2是webservlet地址

6.**检查路径**：这个表达式会自动读取你部署在 Tomcat 上的 Web 项目的**根路径**<form action="${pageContext.request.contextPath}/addServlet" method="post"

7.**注意jsp**：的导入类，有EL表达式必须要有ELIgnoral=false

8.**特殊sql列**：报错**Field 'category\_id' doesn't have a default value**，表示mysql要求这个列必须有值

9.**数据类型**：像decimal，bigint，tinyint在java中直接写不了

![image.png](/assets/2e66fbf6-1711-483a-b180-4e2bc5022f55.png)

10**getParamer**：它返回的都是String，不能立马转，要用String获取后，再单独转BigDecimal

## 修改数据

**步骤**：

1.**获取该数据**：会写到界面上在修改

2.**执行修改**：

* 获取修改的行id，通过href传入id，到达servlet，这个可以直接用Parameter查到

  ![image.png](/assets/ebf05bab-b999-433f-b0ff-47a49556ec61.png)
* 递交id调用service的方法查询该id，这个要提前编写好
* Servlet获取id查询好后，封装该数据返回给前端request
* 前端用EL表达式显示这些数据
* 再编写mapper，sql通过ID存入该数据，update，**注意**：要用实例对象
* **编写前端**：主要是id的问题，原来提交过去的id再页面左下角可以看见，不希望客户看见的话就要用隐藏域,hidden

  <input type="hidden" name="id" value="${product.id}"
* 再编写servlet，连接上SelectallServlet

![image.png](/assets/eb1c6b64-522a-4fdf-b1d9-c559424453b7.png)

### **注意**

为什么mapper中的sales_count=#{count}又是会报找不到字段，字段不匹配的错误，为null的情况

### ！！！！！！！！！

#### 原因

在config中没有声明mapUnderscoreToCamelCase之前

mybatis在处理mapper中上面的操作时，他不是用的#{count}和等号左边的数据库字段进行匹配，而是去实体类中找getXXX,他去掉get用XXX，再变成小写，再自动补驼峰（这些是强制执行的）。和等号左边匹配，就会导致不匹配，所以会报错null。

#### 解决

加入**模糊化参数匹配规则**之后，他会将等号左右两边的名字全部转化成**全小写**，**无下划线**的格式，所以就匹配了。

# 会话

当用户打开浏览器，会话**已建立**，某一方断开连接**会话结束**，会话期间会有**多次请求和响应**

![image.png](/assets/3aa85ccd-0fd6-46c6-a537-f6fad4997c95.png)

1.**数量**：一个用户浏览器就代表一个对话，多个请求响应也共用一个对话

## 会话跟踪

他是一种维护浏览器状态的方法，分辨这些请求是来自哪个浏览器

**目的**：一边在同一次会话的多次请求间**共享数据**。

**问题**：

1.**识别问题**：每次的请求HTTP是**无状态**的，服务求并不能识别这个请求是来自哪个浏览器。

2.**速度问题**：如果用post或者get传输浏览器标识和数据的化，会导致后续的请求体积越来越大，会导致速度变慢。

**解决**：

1.**Cookei**：客户端会话跟踪技术，将数据放在Cookei里面

2.**Session**：服务求会话跟踪技术，将数据放在Session里面

### Cookie使用

利用Cookie携带数据，进行交互，他的实现是基于HTTP协议的。set-cookie和cookie作为响应头和请求头

![image.png](/assets/8552392d-35e3-4ac9-97f3-de29ef50dd07.png)

#### **服务器任务**：

**创建Cookie**和**发送 Cookie**，

1.**创建Cookie**：Cookie cookie=new Cookie("key","value");

2.**发送Cookie到客户端**：response.addCookie(cookie);

3.**获取所有Cookie**：通过request对象的getCookies()获取对象

4.**for遍历所有数据**：for(Cookie cook:cookies),单独获取每个标签，配合if，获取想要的值。

5.**前端获取Cookie**：
![image.png](/assets/85e7a0c7-337e-409d-be4a-836038b96da8.png)

#### cookie生命周期

**默认情况**：cookie数据存在电脑的内存中，内存释放就会被销毁

**自定义setMaxAge(int seconds)**：可以设置Cookie存活时间，

* **正数**：会作为存活时间（秒）。
* **负数**：表示默认，浏览器关了就会销毁
* **0**：表示立马销毁Cookie

**浏览器查看cookie方式**：控制台->application->cookie

#### cookie存储中文默认情况不能存储中文，不支持中文

**解决**：需要转码存储再浏览器中，获取数据时，再通过解码获取中文

**编码**：value=URLEncode.encode(value,"UTF-8")

**解码**：value=URLDecode.decode(value,"UTF-8")

#### 服务端会话跟踪Session

**需求**：**共享数据**

* 需要将数据放在服务端，便于**处理数据**和**保护数据**
* 实现一次会话多次请求之间的数据共享
* 实现服务器端的，特定客户的数据共享

**功能**：

* **创建**：HTTPSession session=request.getSession（）
* **存储键值对**：void setAttribute(String name,Object 0)
* **获取键值对**：Object getAttribute(String name**

**原理**：

1.**基于Cookie实现**：多次请求使用的Session用的时同一个Session，不同浏览器访问他的Session就不一样

2.**唯一性**：session是在后端创建的，他响应的时候会**传递一个唯一标识id**给前端浏览器Cookie，在后续的请求时，Cookie都会带上这个id，完成不同浏览器之间会话的**隔离**

* 如果Cookie携带了sessionid就找对应的Session
* 如果没有携带sessionid，就会新建一个Session对象

3.**存放位置**：是放在内存中的

**问题**：

1.**服务器重启Session是否还存在**：

* 不正常重启：会丢失
* **正常重启(钝化)**：不会丢失，Tomcat会将Session写入硬盘(tomcat中的一个文件)中帮我保存，**（活化**再次启动，文件中的数据还会加载到Session中

2.**Session生命周期**:

* **浏览器关闭**：关闭浏览器后session就会销毁
* **时间**：误操作的情况下，30mini后自动销毁（代码在config->xml627）
* **主动销毁**：退出登录时就会用到销毁。session对象.invalidate();

#### **注意**

1.**数量**：一个浏览器可以有多个cookie，并发送

2.**存储位置**：Cookie在客户端，session在服务端

3.**安全性**：Cookie来回传不安全

4.**大小**：Cookie有大小限制

5.**生命周期**：Cookie可以长期存储，session不行

6.**性能**：Cookie不占用服务器

7.**使用场景**：Cookie用于存储用户**未登录前**需要长期存储的数据，session用于存储**登陆后**的敏感数据

* **购物车**：可以不安全，需要长期存储，
* **用户名**：需要安全用session存储，记住密码（只能用cookie）
* **验证码**：需要安全用session存储，

# 验证码功能

1.**展示验证码**：实现切换验证码图片，这个是一个**工具**，不用深究原理，会调用即可

* **验证码工具类**：这个在帮助文档里面
* **切换验证码**：绑定一个单击事件,通过图像的id找到对应的src，然后在调用src的值（跳转servlet），返回新的code，达到刷新的目的。
* **验证码路径**：因为生成的验证码图片，本地浏览器会缓存在一个特定的地方，如果还是用原来的路径生成图片，则图片切换不了。要在路径后面加一个用于不会重复的字段。

  ![image.png](/assets/e7a164a4-767a-4f80-945d-c97e054b4a6e.png)
* **点击事件**：图片文字都可以通过id来设置点击事件，换个id就可以了

2.**验证验证码**：

* **存储位置**：一定要存储在session中，不能存在客户端。
* **比对**：程序默认忽略**大小写**。不能用equals，要用**enqualsIgnorCase**

# Filter过滤器

javaweb三大组件**Servlet，Filter，Listener**

**作用**：把请求的数据拦截下来，先经过过滤器，在去后端的各个功能中，从而实现一些特殊的功能（敏感信息，权限，敏感字符处理）

![image.png](/assets/c6de66ef-8fe7-4b3c-afb2-861342051e77.png)

1.他是一个接口，使用需要重写他的三个方法（初始化，使用，销毁）

2.@WebFilter（”“）声明拦截范围

3.**放行**：当请求被拦截后，会停滞在这里，需要放行后才能继续下面的操作。

4.**过程**：拦截->执行放行前逻辑->放行->访问资源->执行放行后的逻辑

5.放行前要对request进行处理

**注意**：因为javaScript时后端动态页面技术，他的执行流程是，**先后端解析**，再返回前端渲染

**拦截Filter（/*）**：

* 意味着访问jsp的请求会拦截，
* 所以不会先执行jsp，而是先执行拦截器中的代码
* 释放后获取到了jsp代码，执行jsp中的代码，然后再回到filter，再执行filter中剩余的代码
* 放行前后端没收到request数据，放行后执行了前端，所以request有了数据，接下来的过滤器剩余的代码就对request的内容进行处理。

**拦截种类**：

* **全体拦截**：/*
* **具体拦截资源**：/AAA.jsp
* **目录拦截**：/AAA/*回访我目录user下的所有请求
* **后缀拦截**：会访问后缀名为jsp的资源

## 过滤器链

多个嵌套，

![image.png](/assets/4ef77151-eb58-45e2-a35c-9a1a90b9406c.png)

**注意**：

1.**如果都是全局的拦截器**：这两个没有必然的联系，则会按照目录的顺序被依次拦截，拦截器拦截拦截器

* **过滤器类名排序**：对比类名，小的先执行，A>B,null>2。

### 登录验证

现在没有权限限制的话，知道了jsp名，会导致不用登陆也能过去，所以要拦截下来，查看是否已经登录

1.**必须要放行**：如果全部拦截，会把登录界面也给拦截

2.**路径验证**：将必须要放行的页面，用urls记录好，再获取当前请求的路径，然后进行比对。

String url=req.getRequestURL().toString();

# 监听器Listener

他是javaweb的三大组件之一，他可以监听**Application**，**Session**，**Request**的**创建，销毁**动作，然后做出反应，

![image.png](/assets/40408d89-f9a9-4387-86af-67445e274e59.png)

1.**Session**：比别的多两个

* **绑定，解除**
* **活化，钝化**

2.**ServletContext**：他的第一个方法，里面包含**创建和销毁**的监听，调用这个接口后，重写两个方法，然后就可以在里面编写监听到行为后的操作。

* 注意要在这个类上添加@WebListener注解

# JSON实现列表查询

html+servlet

实现，前端html，请求后端的列表，**转换**，然后返回到前端，显示列表。

### **步骤**

1.**添加事件**：等待页面加载完成后发送请求

window.onload=function(){axios({method:"get",url:""}).then(function (resp){})}

# 实现分页查询

主要要关注**分多少页**，**从哪开始分页**，**总共多少页**，**对象是什么**

1.**需要两个sql**：一个查询条目数，一个返回该页的行对象。

2.**查的什么对象**：这个用一个**实体类**封装好，在查询到数据后用于封装用的代码，它里面有**总页数**，**list对象**，由于这个list对象未知，固定对象又不太好，所以要引入要给参数给它，告知它返回什么对象

3.**嵌套**：这个是因为，在点击页码时自动换页，所以把原来在默认的位置的查询method，放一个事件到点击页码的方法中。
