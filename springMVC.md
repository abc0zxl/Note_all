# 注意

1.Servlet规范是由Oracle公司制定的

2.web框架的运行需要tomcat服务器

3.当pom配错时，要留意缓存好的配置文件，极其可能导致运行失败

# SpringMVC

技术栈：javaSE，HTML，CSS，JavaScript，AJAX，axios，Thymeleaf，Servlet，Maven，Spring

**什么是MVC**：

* Model：处理核心业务的代码
* View：负责展示数据
* Controller：负责控制，协调各个功能，业务

**优点**：

* 低耦合，扩展性强
* 代码复用性强
* 代码可维护性强
* 各个部分代码分功明确，可以专注某部分的开发

**三层模型**：他不是MVC

* 表示层：view
* 业务层：service
* 持久层：dao，mybatis

**什么是SpringMVC**：

* 他是一个实体框架，他已经把mvc的框架搭好了，我们只用往里面填写代码即可
* **入口控制**：所用请求都要经过DispatherServlet（前端控制器）
* **分发请求**：controller控制器将控制请求去往何处处理
* **自动封装到bean中**：无需手动获取请求参数再写入到对象中。
* **IOC容器**：通过注解就能自动创建对象
* **统一处理请求**：过滤器，拦截器，异常处理器
* **支持多种视图解析**：JSP，Freemarker，Thymeleaf等
* 她也叫spring6

**SpringMVC优点**：

* **轻量级**
* **模块化**：方便处理
* **依赖注入**：
* **易于扩展**
* **易于测试**：脱离web容器，Tomcat服务器页可以但与测
* **自动配置**
* **灵活性**：支持多种视图

## 搭建Springmvc

通过基础的java项目搭建springmvc框架

1.**创建java项目**：并且再项目框架中选择jdk版本

2.**创建maven模块**：这个只选择java模块中的maven

3.**配置xml文件**：

* 打包方式
* 编写依赖：springmvc框架，servlet依赖，logback日志，thymeleaf-spring6依赖。

4.**补充项目结构**：再main下创建webapp

* **告知idea这个目录**：
* 在项目结构中设置模型，在资源描述中定位其目录位置。
* 在部署描述中，增添完整的项目路径

5.**配置前端控制器**：因为这个是所有请求都要过的一个地方，在springmvc框架内配置一个类DispatcherServlet

```
    <servlet>
        <servlet-name>springmvc</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>springmvc</servlet-name>
<!--        除了xxx.jsp结尾 的请求路径之外的请求路径，不走springmvc的前端控制器-->
        <url-pattern>/</url-pattern>
    </servlet-mapping>
```

**web.xml模板**

```
<!DOCTYPE web-app PUBLIC
 "-//Sun Microsystems, Inc.//DTD Web Application 2.3//EN"
 "http://java.sun.com/dtd/web-app_2_3.dtd" >

<web-app>
  <display-name>Archetype Created Web Application</display-name>

    <servlet>
        <servlet-name>springmvc</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>

        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:springmvc-servlet.xml</param-value>
        </init-param>
        <load-on-startup>0</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>springmvc</servlet-name>
        <!--        除了xxx.jsp结尾 的请求路径之外的请求路径，不走springmvc的前端控制器-->
        <url-pattern>/</url-pattern>
    </servlet-mapping>
</web-app>

```

## 前端控制器DispatcherServlet

**作用**：他的地位是SpringMVC框架提供的最核心的类。他是整个SpringMVC框架的前端控制器，负责接受HTTP请求、

1.**转发路由到各个处理位置**：DispatcherServlet监听到HTTP的请求，将URL处理解析为Request对象。分发到对应的controller

2.**处理URL**：将这个URL解析后和**对应的处理器**进行匹配，确定用哪个**控制器**处理请求。

3.**调用相应控制器**：相应的控制器处理业务逻辑，然后返回一个**模型对象**

4.**返回到视图**：DispatcherServlet调用视图引擎，将**模型对象**呈现到HTML页面，支持**响应**：xml，html，json

**注意**：

* @controller知识@component的别名

## 配置spring的xml配置

**位置**：他有固定的位置，在WEB-INF中，

**名字**：名字要和web.xml中的名字要一致

**内容**：

* **扫描组件**
* **视图解析器**：这个有固定代码
  1.MVC支持多种视图控制器，替换下面的代码即可更换，**只用写一次**。

![image.png](/assets/160b1a00-a70a-492b-b4bc-bceb77b95dd4.png)

**提供视图**：

* **新建.thymeleaf文件**：在WEB-INF/templates下
* 在文件中提供符合thymeleaf语法格式的字符串。

**controller返回到视图逻辑**：

* return的是AAA是**逻辑视图名称**
* xml给组合成物理视图名称：prefix+名称+suffix
* 使用thymeleaf模板引擎将这个路径名称的文件，转换为html，最终响应给浏览器。

## Thymeleaf内容

**Thymeleaf跳转**：

* **传统方式**：通过url跳转，在url后面加上RequestMapping内容，可实现一个请求
* **thymeleaf方式**：首先在html标签中加入一个声明，xmlns:th="http://www.thymeleaf.org">
  可以直接用th:href="@{/test}"代替，这种方式更加灵活

**初始主页面**：可以利用一个万能路径，可以获取任意路径请求，然后就能跳转到这个主页面。

## 杂项

**springmvc的配置文件的位置和名字可以任意**：通过在标签<servlet中，写入<init-param,就能指定一个初始化参数来指定配置文件位置。

![image.png](/assets/a1d03971-bc41-47f6-8004-811beac326c1.png)

**刚开始启动页面时有延时**：因为没有立即加载前端控制器等资源。可以在<servlet标签中加入一个<load-on-startup》0《/……》可以提前加载好控制器，就能缩小延时。

**html后缀可能不是html文件**：浏览器解析不了thymeleaf，所以要看，如果包含xmlns：th的声明他就是一个thymeleaf模板。

# RequestMapping注解

**作用**：请求和方法之间的映射，这个注解写了一个唯一的路径，请求了这个路径，就会调用这个方法功能。return到明确的thymeleaf名字

**规则**：

* 同一个web，不可以用两个一样的RequestMapping
* 可以放在类上面，表示类中的方法都得经过这个路径，在方法上的路径会进一步的细分

## Value属性

1.**Value**：

* **数组性**：他是一个字符串数组
* **作用**：因为他是在RequestMapping中的，所以可以设置多个路径值，表示这些路径都可以访问到这个方法
* 可以用path替代这个value

2.**Ant风格的Value**：

* **Ant风格**：表示支持模糊匹配模式
* **通配符？**：表示任意一个字符
* 通配符*：表示N个任意字符
* 通配符**：表示N个任意字符，且可以出现/符号（只能作为后续任意/出现，中途不可以统配多个/符号）
* **例子**：value="/x?z/Products"

3.**有占位符的功能**：

* **新型URL**：通过/隔开参数名和参数，完成传参，这个方式，URL更简洁

  ![image.png](/assets/131337bc-7f70-4b23-b207-f1ddfb8b908b.png)
* **传参方式**：通过注解@PathVariable(占位符名字)，声明下方变量，完成映射。
* **位置**：这个获取参数的注解PathVariable是放在方法的括号中的。

## method属性

1.**405报错**：这个是http端的错误，表示method方式和后端不匹配。

2.**请求条件**：只有当请求路径和，method请求方式相同时才会执行下面的方法。

3.**默认方式**：前后端都是GET

4.**数组性**：表示post，get可以同时设置。都能接受

**替代方法**：衍生Mapping，他是包含了RequestMapping的功能+method的功能，内部也可以写路径。

* @PostMapping：替代POST
* @GetMapping:替代GET
* @DeleteMapping：表示删除指定资源
* @PatchMapping：部分更改请求

## params属性

用于设置**请求参数**，来**映射请求**

```
    @RequestMapping(value="/User6",params = {"username=abc","password"})

```

* **数组性**：可以设置多个参数
* **一致性**：请求的参数必须和设置的参数完全一致后，才能映射成功
* **携带参数方式：**

![image.png](/assets/dacf594a-6f52-4c17-ba26-77d28bf3fbf3.png)

/springmvc/login?username=admin&password=456

## web请求方式

1.GET

2.POST

3.PUT：更新资源请求，用于更新指定路径上的所有可编辑内容。

4.HEAD：请求服务器返回资源的头部，

**CRUD常用**：在RESTFul风格的编程中常用下面的方式

* 增：POST请求
* 删：DELETE请求
* 改：PUT请求
* 查：GET请求

**注意**：

* 原始的表单只能提交get,post，即使设置别的请求，发送的依旧是get请求。
* 用ajax可以实现put， delet， head

**get和post特点**

* get时安全的，只会会获取数据，不会修改数据
* post时不安全的，可能会修改服务器资源
* get支持缓存，如果没有变化，他还是用的上一次的数据，而post时真的请求数据。

## **header属性**：

![image.png](/assets/e161b12e-07d5-40e1-a444-7e754d9bfbe5.png)

* 请求头是由一个个键值对组成。
* 可以设置固定值，必须符合才可以映射成功
* 不设值：表示存在即可

**注意**：

* 设置Referer属性时，他的url表示，得从这个url访问过去才行，不能立即访问设置的url+repostmapping地址。

# 获取请求数据

## 前期准备

1.**设置依赖**：通常的mvc配置就可以

2.**设置配置**：也是和平时一样就可以

3.**获取request，response，session的配置**：

* 注意PathVariable只适用于get，不适用于post
* **首先**：设置方法参数为HttpServletRequest aaa，用于接收request对象
* **同样**：可以设置HttpServletResponse，HttpSession等。

4.**获取数据方式1**：

* **原生方式**：用对象.getparameter的方式
* **注解方式**：这个时SpringMVC提供的方式@PostMapping，具体方式看下一行

5.**注解方式获取数据2**：

* **设置方法参数**：这个依据要获取的数据类型来设置
* **原理**：注解将获取的对象和**设置的形参**产生映射
* **在每个形参上设置映射注解**：@RequestParam（前端id），映射到下面的参数上就可以直接使用了
* **转换类型**：按钮类型等可以自动转换为int或者string

### @RequestParam的属性

* **value**：他和name可以互相代替
* **required**：设置该参数是否为必须的，**因为默认情况下必须要传过来**，required=false就表示这个参数就不是必须的。
* **defaultValue**：可以给参数设置默认值。

6.**数据获取方式3**：依靠控制器中的形参名字获取名字，这样就可以直接省略**注解**

* **配置**：如果时spirng6以上，需要配置
* ![image.png](/assets/1574b135-c294-4c3c-9cf4-e408edbeb1e9.png)
* **如果没对应上**：就会返回为null

7.**数据接收方式4**：通过**POJO**类获取

* **一致性**：**POJO的属性名**必须和**请求参数的参数名**保持一致。
* **反射机制**：在前端调用其参数时不用用对象来获取属性，可以直接用他的属性名字就可以。
* **反射**：他不是按照原来的先创建对象，在写入参数到对象中，传递对象，而是直接写入到精确的**参数名**，当提交到服务器时，他再用对象接住这些参数，写入到对象中去。就完成了传递。
* 这个时最常用的
* **注意**：这个pojo类中的SetAAA方法，这个AAA非常重要，必须要和前端的id一致，也要和数据库属性名字一致。

## RequestHeader注解

1.**基本属性**：

* value：这个是用来映射参数名称的，必须和要映射的参数名称一致。
* required
* defaultValue

2.**特点**：

* 可以获取请求信息，**请求行**，**请求头**，**请求体**。可以直接将请求头写入到返回的参数中。

![image.png](/assets/c11de4b1-21fc-4fdb-97f4-d4b7a2c00b2c.png)

## CookieValue注解

* **作用**：将提交过来的Cookie数据**映射**到**方法形参**上
* **属性**：基本的value，required，defaultValue都有
* **前端编写**：用script编写要发送的cookie。
* ![image.png](/assets/1efba28a-ea73-47e2-92e1-93c48b22bcd8.png)
* script中cookie书写要求：
* 逗号后面要有一个空格
* 里面的时间是cookie过期时间，过了就不会显示了
* **下面为模板**：一个字母都不能差
* ![image.png](/assets/737f4866-22f4-4058-91b7-94a14f5e9c06.png)

## 中文乱码问题

**必配即可，无需多言**：

1.原来的tomcat8，需要管这些，如果用的是tomcat9或者tomcat10就不用管那么多因为默认**UTF-8**

### 关于Get方式乱码解决

1.**对URL进行编码**：再tomcat服务器的配置中，进入到CATALINA_HOME/conf/server.xml中，找到8080的位置，再标签中加入一段。

URIEncoding="UTF-8"

### 关于POST方式的乱码

1.**设置请求体的编码方式**：request.setCharacterEncoding("UTF-8")这个必须在执行getParamere之前执行，在tomcat10中不需要考虑乱码问题（因为默认是utf-8）.

2.**设置过滤器**：在请求通过控制器之前执行即可完成集体转码。

* 创建filter文件
* 实现Filter接口，注意要用**Servlet下的接口哦**
* 设置字符集的代码
* ![image.png](/assets/b31a03ad-4bde-4e64-8534-8aed86b609f3.png)
* 将过滤器配置到web.xml中
* ![image.png](/assets/91eee66d-950a-41e5-916d-c93284f0a8dc.png)

3.**直接用SpringMVC的内置过滤器**：

* 在web.xml中设置
* 名字固定为**characterEncodingFilter**
* ![image.png](/assets/974c8fa9-a9d6-4052-8844-9888a3cd7961.png)

# 三个域对象

**请求域**：request

**会话域**：session

**应用域**：application

1.**都有的功能**：存储，读取，删除

* setAttribute
* getAttribute
* removeSttribute

2.**这三个域**：是作用区域逐渐扩大的

**一个会话**：一个浏览器的打开和关闭就是一次会话

## request域

接口名字：HttpServletRequest

作用：如果想在同一个请求中**共享数据**，就用**请求域**

例子：服务器返回时跳转的页面访问在服务器设置的request共享内容，通过id来访问

### 使用方法

1.**原生的Servlet方式**：参数就是HttpServletRequest req。设置参数req.setAttribute(id,"text")

2.**Model方式**：这个设置参数用的时addAttribute

3.**Map方式**：这个用的是put，注意参数设置的是Map<type_name,param_type_name> map

4.**ModelMap方式**：这个参数直接就是ModelMap m，设置参数用的是addAttribute

**上面三个的关系**： 表面上用的是不同的方法，实际上用的是同一个对象。org.springframeword.validation.support.BindingAwareModelMap

5.**ModelView方式**：及封装了业务处理的**数据**，页实现了跳转到哪个**视图**。这个方法的返回参数是ModelAndView。设置参数用（创建对象（ModelAndView），写入参数（addObject），返回视图(serViewName)）,直接返回这个对象，能实现原来的return到视图的作用。

**总结**：上面后四种方法，实际上都会返回一个ModelAndView对象，然后把这个对象给DispatcherServlet

* 当路径不是JSP的时候都会走前端控制器dispatcherServlet，然后会通过请求路径来肇东对应的处理器方法，返回一个视图名称（ModelAndView），

## session域

对象：JSESSIONID

接口名：HttpSessioon

作用：多次请求之间共用一个数据。通过jsessionid传递。

**使用场景**：登录的信息保存

### 使用方法

1.**原生Servlet**：

* 方法参数用的是HttpSession
* 设置参数用setAttribute

2.**SessionAttribute注解**：

* 在方法的上面用注解@RequestMapping（）
* 方法的参数用ModelMap设置
* 在这个java大类的上面设置注解@Session Attributes({"A","B"})
* 这个A，B就是写入到session域中的id
* 调用的时候直接用他的参数调用其id即可
* **注意效用时要加上session.**

## application

接口名：ServletContext

作用：整个web应用的整体信息，服务器启动和结束时销毁。

**使用场景**：记录整个网站的人数信息。

### 使用方法

这个就一个方法

1.**参数设置**：用HttpServletRequest

2.**设置参数的方法**：ServletContext ap=req.getServletContext();

3.**写入参数**：setAttribute

4.**调用参数**：要加上application.后面再接上id，这样才会起效

# View层

1.**常见视图**：

* InternalResourceView：springmvc内置的，一种转发视图
* RedirectView：springmvc内置的，一种重定向视图
* ThymeleafView：第三方的视图，专门解析thymeleaf模板的语法的

2.**设置视图方式**：再xml中的视图控制器第一行设置

3.**重要实现接口**：

* DispatcherServlet：上面已经讲过了
* ViewResolver：他的作用时，将逻辑视图名称转换为物理视图名称，
* View：他的作用是，将模板语法的字符串，转化为html代码，并将html响应给浏览器

![image.png](/assets/4d5b17f6-cfbb-4885-9406-0c1ede7fd710.png)

源码解析

![image.png](/assets/ef0b598c-1ee4-4b6b-a8a8-4d2c7dac4608.png)

## Thymelaef情况下的运行流程

1.**发送请求到服务器**

2.**dispatchServlet接收到请求**

3.**dis……发送到对应的controller**

4.**dis……调用其controller方法**

5.**controller返回一个逻辑视图给dis……**

6.**DispatcheSerlvet**：调用ThymeleaViewResoler的resultViewName的方法，将逻辑视图名称转换为物理视图名称，并创建thymeleafview视图对象，防护igeidispatcherServlet

7.**dis……调用**：ThymeleafView的render方法，将模板语言转换为html代码，发送到浏览器，完成最终的渲染。

## JSP作为视图

流程和Thymeleaf类似，将ThymeleafView换成**InternalResourceView**就差不多了

1.**实现**：他是InternalResourceView实现的。

2.**配置的视图解析器**：和原来的大差不差，重点是把里面的**前缀路径**，**后缀文件类型名**，**第一行的视图解析器依赖**。修改一下就好

**![image.png](/assets/67d44bdc-eec3-4e91-b5a4-8d76cc9b1584.png)**

**渲染数据步骤**：上面两个方法的这一步都在rander方法中执行。

## 转发重定向

### 转发

1.转发是一次请求，浏览器地址不会发生改变

2.**代码**：request.getRequestDiapatche("/index").fowrd(request,response);

3.**特点**：可以访问内部的资源，是服务器转发的

#### forward转发

1.**通过<a 连接方式的跳转**：这个默认情况是转发（forward）

2.**在服务器中的转发**：return（”forward：/b“）这个原理是创建了一个InternalResourceView（内部资源视图） 这个在内部转发，地址栏的地址是不会变的。

### 重定向

1.重定向是两次请求，浏览器上面的地址会发生变化。

2.**代码**：response.sendRedirect("/index")

3.**特点**：不可以访问内部的资源，因为这时一次全新的请求，因为 是浏览器转发的

#### redirect重定向

1.**这个跳转方式使用的比较多**：return（”redirect:"/b"“）

2.这个方式会发生地址栏的改变是从/a到/b

3.底层创建的是**redirectView**

#### 重定向跨域

关键词：<mvc:view-controller,**编写在spring.xml中**

特点：需要些全路径

使用场景：controller控制器中没有业务处理逻辑，只有跳转时，可以用这个替代。

**注意**：单独加这个标签会导致所有@controller注释失效，所以必须要结合**开启注释**一起用，在这个标签下方写入<mvc:annotation-driven/》

## 访问静态资源

### 解决方案一

例如：图片，图标，等

1.**无法直接访问**：因为springmvc请求都得经过DispatcherServlet，但是没有对应的控制代码

2.**编写标签**：<mvc:default-servlet-handler/》这个时tomcat***自带的一个访问方式DefaultServlet，但默认是关闭的，所以开启后就可以通过url直接访问静态资源了。

3.**原理**：在url访问静态资源时，回直接过DispatcherServlet，如果发送404就会自动走DefultServlet

### 解决方案二

1.**使用标签**：<mvc:resources mapping="/static/**",location="/static/"》就可以解决

## RESTFul编程风格

**全称**：Representational State Transfer(表述性状态转移)，简称REST

* **表述性**：是指URL+请求方式
* **状态**：是指服务器端的数据
* **转移**：变化
* 把上面合起来一起读

**介绍**：他是**web服务接口**的一种**设计风格**

通过采用：**不同的请求方式**+**Url来确定web服务中的资源**

**什么是web服务接口**：例如查看用户详细信息的跳转文字，一点击发送URL地址，这个地址就是web服务接口

1.**全新的规则**：针对原来难以读取，不整洁的web服务接口有了全新的设计

2.**特点**：更加简洁，易于理解，易于扩展，安全可靠。

3.**请求方式的规范**：

* 新增：必须用Post，正常添加就好,因为form标签可以用post
* 查询：必须用get：直接用<a href="@{/rest/1001}就可以传递id了
* 修改：必须用but，这个必须是在表单form为post的前提下，再进行下一步。
  添加一个隐藏域再表单第一行，
  **第二步**：<input type="hidden" name="_method" value="put"》这个**必须是这些字母**。

  **第三步**：添加一个过滤器，将post转换为put请求

  ![image.png](/assets/670d4842-27ae-41ca-956f-f23f584679fd.png)

  **注意**：关于字符编码格式的过滤器必须要在他之前
* 删除：必须用delete，

  **第一步**：编写一个连接提交标签录入数据<a

  **第二步**：编写隐藏域

  **第三步**：编写script函数用于提交，将隐藏域的数据写到let对象中

  **第四步**：将提交数据的<a 标签的href信息写入到let对象中

  **第五步**：发送对象，并将let对象的默认提交方式关闭

  **第六步**：编写控制器，注意参数上要加映射标签

4.**url的规范**：将原来的？= &都用/代替

5.**使用场景**：

![image.png](/assets/f4bca23d-1926-47db-91a5-fb7beec3c414.png)

# SpringMVC的CRUD

注意：

1.**扫描包**：可以用逗号可开，扫描多个包

2.**请求url旁有无关字符**：因为少写了th:

## 修改用户信息

1.**流程**：

2.**查询这个修改的用户信息**：查询到后返回到用户对象，查询匹配方法

* **循环匹配**：for(User user:users)if(user.getId()==id)
* **用filter方式**：users.stream().filter(user->user.getId().equals(id)).findFirst().get();

3.**双选按钮的值导到视图层**：在两个标签中分别加入 th:field="${user.sex}"

4.**获取数据**：在controller用的是get

5.**在url中写入id**：@{'/user/'+${user.id}}注意单引号，和EL表达式

6.**将数据显示到表单**：value之前要加th:

7.**覆盖用户数据**：users.set(i,user);

8.**修改信息为什么没有修改成功**：修改表单时，也需要获取到原来的id，不获取就不会成功

9.**删除要用script的原因**：因为要添加提示信息，是否要删除表单，注意要加隐藏域。

![image.png](/assets/e635c941-bf58-48d0-bfc8-b1f9b074c765.png)

10.**删除添加的script**：用onclick触发，这个del（必须时event）

## HttpMessageConverter

**HTTP消息转换器**

**作用**：HTTP协议和**java对象**之间的转换

**方法**：1，2都是针对响应体，请求体（体）的

1.**StringHttpMessageConverter**：默认的消息转换器，没有指定的时候就默认用的这个，**负责将java程序中的html程序写入到http响应体中**

2.**FormHttpMessageConverter**：例如springmvc的，将http中的属性信息直接写入到服务器方法参数的对象中去，用的就是这个

![image.png](/assets/af7123f6-4327-43b7-a1ba-5b8088efb7f0.png)

3.**MappingJackson2HttpMessageConveret**

**注意**：

1.HTTP消息就是HTTP协议

2.get请求体在**请求行中**，post请求体在**请求体中**

3.**响应体**：就是要返回到浏览器的html代码

## AJAX异步请求

### 原生AJAX

**请求+返回数据**：这个部分在vue框架的methods:{中

**前端代码固定**：

![image.png](/assets/f39affea-792a-4bda-8e86-5578f0b1e6d3.png)

**后端发送数据**：参数要声明响应类型HttpServletResponse，然后用PrintWriter就可以了

**缺点**：

* 不利于做测试，因为他要的是HttpServletRequest的参数，这个只能从前端发过来。

### 升级版AJAX+SpringMVC

用一个注解@ResponseBody方式代替controller中方法的**参数，PrinWriter**，直接用return就可以返回到浏览器一个字符串，而不再是**逻辑视图**。

**注意**：

* 异常还是要写一下的。
* return的json，中的双引号**需要转义**
* 直接返回在发送求的页面

1.**SpringMVC有内置json转换**

* 必须要有@ResponseBody注解，
* **需要jackson依赖**；一个专门用来转换数据格式的依赖
* 当方法返回的是一个实体对象时，会自动转换为json格式

**![image.png](/assets/c20a3687-f6a8-4496-bde3-d689779e030f.png)**

2.**采用的消息转换器是什么？**：是MappingJaksonHttpMessageConverter.

3.**非常好用的注解**：@RestController他是一个结合体，在大类上方和@controller同一个位置，实现类@Controller而且给每个方法加了个@ResponseBody

## @RequestBody

这个注解作用是将**请求体**交给java程序，**String类型**的变量接受这个**请求体**内容。

1.**位置**：这个注解的位置只能在**方法参数上**

2.**作用**：

* **对象转string**：原来发送过来的是一个对象，加了这个注解后，就变成了字符串类型的参数，而且是Json类型。
* **json转对象**：可以将前端发过来的json数据转换为java对象

3.**消息转换器**：用的是FormHttpMessageConverter，注意这里说的是**请求体**给java程序，转换为了**String字符串**，

## **注意**

1.**版本错误**：vue.createApp()这个是Vue3的东西

2.**Vue发送json数据请求模板**：一个字母都不能差

```
<div id="app">
    <button @click="transUser">提交用户数据（POST请求）</button>
    <h1>{{ message }}</h1>
</div>

<script th:inline="javascript">
    let jsonuser = {
        "id": 1,
        "username": "lll",
        "password": "123321",
        "email": "@@@@@"
    };

    // Vue 3 实例创建
    Vue.createApp({
        data() {
            return {
                message: ''
            }
        },
        methods: {
            async transUser() {
                    let response = await axios.post([[@{/}]]+ 'save', JSON.stringify(jsonuser), {
                        headers: {
                            "Content-Type": "application/json"
                        }
                    })
                    this.message = '请求成功！返回数据：' + response.data
            }
        }
    }).mount('#app');
```

## RequestEnity请求类

这个不是一个注解，而是一个可以用的类，

1.**封装**：他封装了整个请求协议，包括**请求行，请求头，请求体**

2.**声明请求体范式**：RequestEnity<User》 requestenity

3.**获取方式**：

* **getMethod()**：获取请求方法，需要用HttpMethod对象
* **getUrl()**：获取url，需要用URL对象
* **getHeaders（）**：获取请求头，需要用HttpHeaders对象
* **getContentType()**：获取请求头中的类型，需要用MediaType对象

  ![image.png](/assets/90da1adc-81d1-41f3-a861-7bb62631f8b0.png)
* **getBody()**：获取请求体，获取对象，可以是上面设置的User对象

## ResponseEnity响应体

他也是一个可以用的类

**作用**：在需要**定制响应体**，就可以用它

* 可以设置他的状态
* **状态=未发现**：httpstatus.not_found,就可以设置他的响应体为null。
* **状态=ok**：可以直接将对象写入他的.ok（user）方法中。

**定制步骤**：

* **控制端**：例如在一个查询数据的场景，他需要通过service获取一个用户对象，
* **service端**：编写一个调用dao后可以将数据写入对象中的功能，查找不到就返回**null**
* **控制端**：通过一个if判断是否为空，写入对应的数据，null或者对象
* **注意**：控制端返回类型为ResponseEntity<对象》

## 文件上传与下载

**注意**：

* 如果用的是spring5，则需要导入commons-fileupload这个包
* 如果是spring6，就不用导入commons-fileupload
* 原理上还是IO流

**前端规则**：

* 文件上传的标签中必须写入
  ```
   enctype="multipart/form-data"
  ```
* **文件组件**：<input type="file" name="fileNmae"》

**后端规则**：

* **spring配置文件**：servlet标签中写入<multipart-config》**关于上传文件规格的信息**

  ![image.png](/assets/c195ba1e-a76d-432d-87e0-702cca538ac4.png)
* **控制层**：这个用的还是post传输方法
* **参数**：有一个专用的参数MultipartFIle，上传的文件直接传到了这个参数中了，
* **参数注解**：这个multipartfile前要加注解，注解名字要和前端input名字一样

**调用方法**：

* **getName（）**：获取参数名字，就是input文件的名字
* **getOriginalFilename（）**： 获取的是文件的名字（带后缀）

**IO流操作**：

1.**获取输入流**：getInputStream(),负责读取客户端的文件(in)

2.**封装输入流**：创建一个缓冲区BufferedInputStream,方法中带入输入流名字，BufferedInputStream(in)

3.**输出流**：输出到哪里

* 路径存在的情况

  **第一步**：获取当前请求对象，getServletContext（）

  **第二步**：通过这个对象获取一个精确路径getRealPath("/upload")

  **第三步**：通过这个路径对象字符串创建一个**文件对象**
* 路径不存在的情况

  **第一步**：在上面的基础上加一个if判断，如果new的文件对象不存在

  **第二步**：调用文件对象的mkdirs()方法
* 存入文件 （输出流）

  **第一步**：创建一个文件名字为路径（非文件夹）的File对象。关键词：getAbsolutePath()+'/'+originalFilename

  **第三步**：将这个文件名字的文件对象写入到输出流中

  ![image.png](/assets/44d8293f-a689-4f2e-b229-f43c662fa3df.png)
* 编写读写方式

  **读写数量**：一次读写多少byte[] bytes=new byte[1024*10]读10kb

  **循环读**：边读边写，这个bis是上面的输入流

  ![image.png](/assets/85145243-15dd-4771-8d5b-ec7fac5d68e0.png)

### 注意

1.**文件存储路径**：我的电脑不适用用代码获取当前路径，每次都是存到了tomcat中，所以最好要用绝对路径存储文件，**只用修改一处**。

[image.png](/assets/abd17723-34d8-46f5-9fd3-f4fa9efd161e.png)

2.**文件覆盖问题**：因为BufferedOutputStrea会把同名文件清空，覆盖。可以在文件名字后面加一个id，就会让所有文件不一样，例如加**时间字符串**

**下面这个是通过重写文件名的方式**

* UUID.randomUUID().toString()：这个用来生成随机字符
* **截出文件的扩展名**：originalFilename.substring(originalFilename.lastIndexOf(".");
* **将上面两个相加就可以了****

![image.png](/assets/595bc62b-5a64-44de-81be-7cd37899112b.png)

### 文件下载

需要用到响应类ResponseEntity<>,编辑号**文件路径**，**响应头**，**状态**，写入到这个响应类对象中return

**步骤**：

* 编写方法类：
  public ResponseEntity<byte[]> downloadFile(HttpServletRequest request) throws IOException
* 获取目标下载路径的文件对象
  File file=new File(request.getServletContext().getRealPath("/upload")+"/file_name.jpg")
* 编写响应头：这个部分代码固定不变
  HttpHeaders headers = new HttpHeaders(）；获取头文件对象
  headers.setContextType(MediaType.APPLICATION_OCTET_STREAM);
  headers.setContentDispositionFormData("attachment",file.getName()）；
* 编写ResponseEntity对象封装这些信息。
  RResponseEntity<byte[]> AAA=new ResponseEntity<byte[]>(Files.readAllBytes(file.toPath()).headers.HttpStatus.OK);
* 返回这个ResponseEntity对象。

## 异常处理器

springmvc在执行过程中出现了异常，可以用**异常处理器**应对，这个是SpringMVC推出的

**作用**：当处理器方法执行过程中出现了异常，跳转到对应的视图，在视图上展示友好信息。

**关键词**：HandlerExceptionResolver，下面是他的两个实现类

* DefaultHandlerExceptionResolver：这个就是平时报错时，展示到浏览器上的页面，这个是默认的
* SimpleMappingExceptionResolver：这个是可以自己定义也买你的方法。

### 自定义异常处理器

DimpleMappingExceptionResolver配置文件

1.**XML配置文件**：

* **配置spring.xml**：加入异常处理器，这里加入的是发生的不同异常类型，然后跳转到不同的异常处理页面

  **框架**：<bean class="org.……。SimpleMappingExceptionResolver

  <property name="exceptionMapping

  <props》这个标签里面写入各个异常处理的键值对<prop》
* <prop key="AAA"这个是异常标准>CCC<

  这个CCC是发生异常后要跳转的页面html
* 在<property下还会配置一个<property

  <property name="exceptionAttribute value="BBB">

  这个name是固定的，底层是将错误信息写进request.setAttribute中，
* **前端调用**：打印这个错误信息，通过th:text="${BBB}"即可调用存储到request中的错误信息

2.**通过注解**：

@ExceptionHandler实现

**步骤**：

* 在contrller下创建一个专门用于异常处理的文件
* 写入注释@ControllerAdvice，这个注解包含了@controller的作用,所以不用单独再写一个controller
* 在类方法上方写入注解@ExceptionHandler
* 编写类方法，返回的是String，方法参数要一个Exception e，和一个公共模型Model，model
* 编写方法内容model.addAttribute("aaa",e);将错误信息写入模型域中，
* return到视图中

## 拦截器Interceptor

**作用**：在请求道道控制器**之前**或者**之后**进行拦截，可以对请求和响应做一些特定的处理。

**应用场景**：登录验证，权限校验，请求日志，更改响应

**拦截器和过滤器区别**：

* **过滤器**：侧重去请求和响应的流程中的处理，例如修改字符集，请求头，状态码等
* **拦截器**：侧重于对控制器的前置或者后置的处理，在到达控制器之前或者之后进行特定的操作。例如**打印日志、权限验证**。
* 过滤器的范围更大，拦截器的范围表较小

**特点**：

* 每个拦截器都有三个方法：前处理，后处理，渲染完成后的处理preHandle,postHandle,afterCompletion
* 只有prehandle返回的是bool值，true放行，false拦截
* 如果是false，后面两个都不会执行

### 拦截器使用

1.**配置拦截器**：在xml中写入一个配置，这个class是过滤器的路径

* **XML配置方式**：拦截所有请求的方式，这个是最基础的拦截![image.png](/assets/8493c940-52a1-4201-a752-a3d165d8ad16.png)

  **高级拦截器配置**：用于指定哪些路径拦截，那些路径不拦截，可以实现（哪些拦截），（哪些不拦截）

  ![image.png](/assets/21915342-6ffa-46d7-a82c-a2ce78987204.png)
* **注解配置方式**：

  **第一步**：给拦截器文件加一个@Component放到ioc中

  **第二步**：在xml的拦截器标签下导入

  <ref bean="interceptor_name"/》

2.**创建文件**：用一个单独的文件夹放这些拦截器

3.**编写类**：实现HandlerInterceptro接口，实现三个处理方式。

#### 拦截器的源码

1.**执行preHandle还有controller**：mv=ha.handle(processedRequest,response,mappedHandelr.gethandler());

2.**执行postHandle**：processDispatchResult(……）

3.**执行afterComplation**：mappedHeadler.triggerAfterCompletion(request,response,null)

4.**如果preHandle是false**：因为拦截器的三个步骤都是依托源码的toDispatch方法的，所以识别到false，就会有一个判断语句执行return。就导致controller不会执行

**注意**：

* 拦截器可以有多个，到会装到一个数组中ArrayList，源码的preHandle判断中，执行的是applyPreHandle可以返回每个拦截器是（true还是false）

### 拦截器的执行顺序

1.**在xml中**：在设置拦截器时可以设置多个，xml的拦截器顺序，就是执行顺序

2.**有递归思想**：因为最后一个执行的是C拦截器，所以postHandle第一个执行的就是C拦截器，afterComplation也是（ABC,CBA,CBA），可以看到执行postHandle时是从数组最大开始的，

![image.png](/assets/70bbdc85-7afc-4b58-8d6b-dddf5c7cc3b8.png)

3.**中途有false**：首先，所有proHandle都会按顺序执行，中途出现false后，后续的proHandle就不再执行了，postHandler都不会执行，但是afterCompletion会执行除了那个false的拦截器，

![image.png](/assets/16644922-eff4-4334-a48b-888bcaed6db1.png)

它选择了通过之前的记录方式声明for的循环初始位置，直接规避了原来的false

![image.png](/assets/efa2186f-607e-49a3-8e93-46eecc46ea3d.png)

4.**遇到false特点**：只要遇到拦截成功的情况，controller就不会执行，所有的posthandle都不会执行。

# 手工搭建SpringMVC

### 基本框架

1.**创建空项目**

2.**配置SDK，JDK**

3.**配置Maven**

4.**创建模块**：用的是Maven的框架

5.**dom.xml配置**：

* 采用war包方式

6.**搭建目录框架**：在main下创建一个webapp，要带蓝点（被idae识别），没有的话去项目结构的Modeules设置，注意从Facet和从Model去创建都能设置路径，但是只有从Facet进入创建这个路径，选择版本才能创建成功。

7.**配置tomcat**：在部署中部署的是项目模块的war exploded。

![image.png](/assets/b27d7fab-00b7-4e4f-a799-324ec72f2cf6.png)

8.**配置基本的web.xml**：在纯手动搭建工程中先不用写下面两个

* **编码前置处理过滤器**：CharacterEncodingFilter
* **前端控制器的配置**：dispatcherServlet

### 创建基本类和接口

以一种不用maven导入的方式手动创建这些接口和类，精准搭建框架。高仿一个springmvc项目

1.**DispatcherServlet（类）**：类

* Servle：接口，这个已经继承了HttpServlet，所以不用再引入HttpServlet接口

2.**HandlerExecutionChain(类)**：处理器执行链

3.**HanderMappping(接口)**：找到url对印的controller，下面两个实现类是它所需要的

* **RequestMappingHandlerMapping（类）**：这个是HandlerMapping接口的实现类
* **HandlerMethod（类）**：处理器方法

3.**HandlerInterceptor（接口）**：执行类，这个是执行拦截器每个阶段的接口

4.**HandlerAdapter（接口）**：处理器适配器接口

* **RequestMappingHandlerAdapter（类）**：是HandlerAdapter的实现类

5.**ModelAndView(类)**：返回视图的类

6.**ViewResolver(接口)**：

* **InternalResourceViewResolver（类）**：是VIewResolver的关于JSP的实现类

7.**View（接口）**：

* **InternalResourceView(类)**：上面的实现类

8.@Controller注解

9.@RequestMapping注解

## 注意

1.DispatcharServlet对象不需要我们去new这个对象，也不需要我们去调用，这个是由Tomcat服务器来调用的Servlet方法一次。

2.用户没发送一次发送请求时会调用DispatcharSerlvet的

3.**对获取到的字符串编码**：springMvcConfigPath=URLDecoder.decode(springMvcConfigPath,Charset.defaultCharset());

4.**重要的容器**：

* ApplicationContext
* WebApplicationContext：它继承了 AppliationContext，他是web项目专用的容器

  **概念1**：他们都属于IOC容器，初始化会将bean存入容器中，以Map集合的方式存储，Key就是bean的id名字，value就是bean的对象

## 注解

//这个Target 注解表示这个注解只能用在类上
1.**@Target(ElementType.TYPE)**
//这个Retention 注解表示这个注解在运行时才起作用
2.**@Retention(RetentionPolicy.RUNTIME)**

3.**@Nullable**：被标记的变量、方法参数或返回值**可以是 null，用于提示用的。

4.**@EnableWebMvc**：表示开启视图解析器注解

5.**@ComponentScan（AAA）**：表示扫描AAA中的注解

6.**@Configuration**：表示这个是一个配置类

# 全注解开发Servlet3.0

不再需要编web.xml,springmvc.xml

**专用接口**：ServletContainerInitializer，自动完成容器初始化

### 编写XML配置文件

这个使用java文件来编写的

**第一步**：在config文件夹下新建一个java文件

**第二步**：在类上加上注解@Configuration，表示专门用来做配置文件的

**第三步**：继承用于配置的java文件AbstractAnnotationConfigDispatcherServletInitializer

**第四步**：编写内容

#### 实现继承后的方法

1.getRootConfigClasses:：用来编写spring配置的

2.**getSevletConfigClasses**：这个专门用来编写SpringMVC配置的

* 这个在class[]后面用{}括起来的里面就是另一个java文件，用来存放springmvc的

3.**getServletMappings**：配置DispatcherServlet的<url-pattern

#### 如果想实现别的方法可以通过Ctrl+O获取

1.例如设置过滤器的方法，搜索Filter就能找到

![image.png](/assets/ad4362f5-dc26-460e-9254-081bdeccb5f7.png)

![image.png](/assets/571dc1fe-3219-4dbd-b503-8c5c0d3675a3.png)

#### 实现视图解析器

**首先**：@EnavleWebMvc开启注解驱动

这个有固定模板

@Bean public ThymeleafViewResolver getViewResolver(SpringTemplateEngine springTemplateEngine) {     ThymeleafViewResolver resolver = new ThymeleafViewResolver();     resolver.setTemplateEngine(springTemplateEngine);     resolver.setCharacterEncoding("UTF-8");     resolver.setOrder(1);     return resolver; }  @Bean public SpringTemplateEngine templateEngine(ITemplateResolver iTemplateResolver) {     SpringTemplateEngine templateEngine = new SpringTemplateEngine();     templateEngine.setTemplateResolver(iTemplateResolver);     return templateEngine; }  @Bean public ITemplateResolver templateResolver(ApplicationContext applicationContext) {     SpringResourceTemplateResolver resolver = new SpringResourceTemplateResolver();     resolver.setApplicationContext(applicationContext);     resolver.setPrefix("/WEB-INF/thymeleaf/");     resolver.setSuffix(".html");     resolver.setTemplateMode(TemplateMode.HTML);     resolver.setCharacterEncoding("UTF-8");     resolver.setCacheable(false);//开发时关闭缓存，改动即可生效     return resolver; }

#### 开启扫描

在类上写@ComponentScan

#### 开启静态资源处理

开启默认的servlet处理，ctrl+o打开

@Override
public void configureDefaultServletHandling(DefaultServletHandlerConfigurer configurer) {
configurer.enable();
}

#### 视图控制器

也是ctrl+o打开，addViewControll

#### 异常处理器

Ctrl+o打开，configureHandlerExceptionResolvers

![image.png](/assets/fee50799-4882-4411-98c0-4e1b269e9b82.png)

#### 拦截器配置

ctrl+o,打开addInterceptors

**第一步：**：写好拦截器java文件，记得加上注解component

**第二部**：配置好拦截器配置就是ctrl打开的那个

* 初始化一个拦截器对象MyInterceptor
* 拦截所有符号/**
* 排除拦截页面

![image.png](/assets/aac4cfa7-fbe8-4787-8536-54473cde2a00.png)

# SSM整合

现在基本上都采用全注解开发

#### ssm包结构

* bean
* config
* dao
* handler
* service.impl

#### pom依赖

```
    <packaging>war</packaging>
    <dependencies>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>6.0.0</version>
        </dependency>
        <dependency>
            <groupId>org.thymeleaf</groupId>
            <artifactId>thymeleaf-spring6</artifactId>
            <version>3.1.0.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-tx</artifactId>
            <version>6.1.3</version>
        </dependency>
        <dependency>
            <groupId>jakarta.servlet</groupId>
            <artifactId>jakarta.servlet-api</artifactId>
            <version>6.0.0</version>
        </dependency>

        <dependency>
            <groupId>ch.qos.logback</groupId>
            <artifactId>logback-classic</artifactId>
            <version>1.5.3</version>
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.13.2</version>
        </dependency>
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.16</version>
        </dependency>
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis-spring</artifactId>
            <version>3.0.3</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-jdbc</artifactId>
            <version>6.1.3</version> <!-- 与你的 Spring 版本保持一致 -->
        </dependency>
        <dependency>
            <groupId>com.mysql</groupId>
            <artifactId>mysql-connector-j</artifactId>
            <version>9.4.0</version>
        </dependency>
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid</artifactId>
            <version>1.2.8</version>
        </dependency>
        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-databind</artifactId>
            <version>2.19.2</version>
        </dependency>
        <dependency>
            <groupId>ch.qos.logback</groupId>
            <artifactId>logback-classic</artifactId>
            <version>1.5.22</version>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <version>1.18.42</version>
            <scope>provided</scope>
        </dependency>
    </dependencies>



```

### Spring 整合MyBatis

1.**编写jdbc.properties**：

* 数据库
* url
* username
* password

在resource包下创建文件

![image.png](/assets/20ffdb78-18fb-467d-9d10-7fbc33bb305b.png)

2.**编写DataSourceConfig**

![image.png](/assets/f278eb4b-86e2-49b9-b70c-693641190c48.png)

### MyBatisConfig编写

这个原来时xml文件，现在也可以用java文件

叫做MyBatisConfig，任务是声明实体类空间位置，还有数据库连接参数，还有数据库映射文件

![image.png](/assets/255caab8-b0b7-4ff6-9cf8-a7e78201b466.png)

### Spring整合SpringMVC

1.**编写SpringConfig**

用来声明spring配置

```
    1.组件扫描
    2.视图解析器
    3.静态资源处理
    4.开启注解驱动
    5.视图控制器
    6，拦截器
```

![image.png](/assets/464dbf4d-c20c-41c1-9b53-21cc239bb5c6.png)

2.**编写WebAppInitializer**

1.**第一步**：继承关于配置springmvc的类，实现它的三个配置分类，spring，springmvc，DispatcherServlet

都可以复制粘贴原来的项目

2.**第二步**：编写每个部分的配置

* **编写springmvcconfig配置**：
  ![image.png](/assets/157dcad6-6ba6-471c-88cf-e9b1a822ff25.png)

  这是视图解析器

  ![image.png](/assets/17bf20ac-58dc-4937-b8e5-9694d44f0a9e.png)

  ![image.png](/assets/e28599c6-cddc-459d-a917-d8eb1d51274c.png)

#### 添加事务控制

事务具有四大特性：最重要的是原子性，也有挂起事务的功能。

**第一步**：在SpringConfig中开启事务管理注解

@EnableTransactionManagement

**第二部**：在数据库资源配置的文件中编写事务管理机制

![image.png](/assets/7cbf28e4-f687-438e-b522-b44341f8a06f.png)



#### 编写RESult风格的html

**导入依赖**：vue,axios

![image.png](/assets/f5b4d614-b36e-4bd3-bced-63ba1dbc5e97.png)


# 注意

1.处理器的参数如果用的是get，记得加注解@PathVariable

2.处理器将数据给service要用return
