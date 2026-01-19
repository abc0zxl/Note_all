# Thymeleaf模板引擎

这个是java目前比较流行的**模板引擎**

**主流模板引擎**：Thymeleaf，Freemarker，JSP

**页面数据**：存储到templates这个文件中

### 准备项目

1.**编写配置**：在application.yml中写入

* 接口号
  server：
  port:8001
* thymeleaf信息
  spring:
  thymeleaf:
  cache:false

2.**编写运行配置**：

3.**编写快捷模板**：这个可以运用到任何场景

在setting中找到**文件和代码模板**，编写一个便于查找的名字，类型，内容

下次调用模板时直接鼠标右键，获取这个名字就能快速生成模板

## 功能

1.**动态渲染**：th:text="${title}"这个可以请求控制层**@Controller**的代码。**可以动态修改**

* **@GetMapping（）**：可以在括号中写入请求的文件路径，表示获取达到该路径的请求时就执行注释下的方法。
* **model_name.addAttribute**：通过这个方法去修改html中的标签内容

2.**打开页面**：端口号+@GetMapping路径

3.**外部css导入**：

* css正常写
* **导入html中**：在head标签中用<link rel="stylesheet" th:href="@{css_name}"

4.**动态渲染的javascript**：

* **写标签**：<script th:inline="javascript"
* **获取数据到json**：要用特定的方法，两个中括号，一个刀乐一个大括号，放到user中const user=/\*[[\${user}]]\*/{};

5.**循环迭代输出**：关键词th:each=”AAA“

* **AAA**：这个是自定义的内容结构为AAA:${BBB.CCCC},其中AAA是自定义的获取迭代数据的一个变量，BBB是对象，CCC是兑现的列表类属性。
* **th:text="${AAA}"**：这个表示正式要显示的内容。
* **th:classappend**：这个表示可以单独处理某个列表值AAA，DDD:${BBB.CCCC},这个DDD是索引，在th:classappend中用￥{DDD.last}?FFF,可以将最后一个列表值，添加FFF的样式。

![image.png](/assets/dcf29094-c0c5-44d7-865f-363ed64e2c0e.png)

## 组件化

将这些内容碎片化。不揉成一堆。

**步骤：**

1.**新建文件**：用div包裹，用th:fragment="AAA"标签标识这个是用来**被调用**的碎片。

2.**调用碎片**：用标签th:insert=“~{BBB::CCC}”或者th:replace=“~~{BBB::CCC}”。表示调用文件名为BBB的文件中用fragment标记名为BBB的方法，**替换**进来，或者**插入**进来。

## 上下文对象（交互数据）

就是说可以调用后端的参数。

1.**工具函数**：例如在th:text="${#dates.format(user.createTime,"yyyy-mm-dd hh")"这个是格式化了后端的user.createTime,变成yyyy-mm-dd hh的格式输出。

其中#dates.fromat是一个关键字工具类。

## 组件调用参数

组件一般是被调用的，有时需要知道调用者的信息。

1.**错误修正法**：通过写注释的方式告诉idea要干啥，他就能提示如何获取别人的参数。

![image.png](/assets/d8d8b244-99e9-46d9-8dd2-ac45e865bf0f.png)

## 组件传递参数

在原来碎片化的代码基础上给调用的名称背后都加上括号。

1.**传递者**：

![image.png](/assets/bb5b325f-25d8-4181-abac-13a16aa5437e.png)

2.**接收者![image.png](/assets/c130f10e-29f2-4c13-ae12-1a031cc27bcc.png)**

## 局部替换组件

这个是一个更灵活的传递数据方式，在原有的基础上可以选择替换的位置。

1.**替换到<p中**：

* **在被替换方**：th:insert="~{component::CCC( ~{::#AAA})
* 《p id="AAA"》替换的位置</p

  ![image.png](/assets/f670ae52-9898-4611-98eb-9d117b47b8f0.png)
* **替换位置**：这个就是局部替换的碎片html，在原来的基础上把message提取出来然后用th:replace包裹返回过去。返回到上面的<p

  ![image.png](/assets/ec1754e7-bdd7-4067-b8db-2656fe7dfe95.png)
