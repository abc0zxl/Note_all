# 框架标签

## 列表标签

1.**有序列表**：

2.**无序列表**：

## 表格标签<table

1.**行标签**：<tr

2.**列标签**：<th,<td

## 布局标签

1.**块级标签**：<div

2.**行级标签**：<span

## 表单标签<form

主要用于数据采集功能，例如登录注册，信息设置，都是表单。

每种不同的数据，他的提交方式都有差别

1.**表单属性**：<form

* action=:指定表单提交位置url
* method=：有post和get两个，两个请求参数的传输方式不一样

2..**提交标签**：<input

* name=：表示传输数据的**键**
* type=：数据的存储类型,

3.**下拉列表标签**：<select

4.**文本域**：<textarea

![image.png](/assets/578e772d-6ea9-4985-b515-5efd5d9c8950.png)

# 内容标签

1.**图片**：<img

### 数组

**数组方法**：

* foreach：只会遍历有值的元素
  扩展： ES6: **箭头函数**，可以将function(e)替换为（e）=>
* **push**：添加元素到数组尾部
* **Splice**：删除元素
*

# CSS

在html中用<style包裹

1.**元素选择器**：例如div

2.**id选择器**：用#开头

3.**类选择器**：用.开头

### 内部的属性

直接上网找

https://www.w3school.com.cn/cssref/index.asp

# JavaScript

1.**注释**：//

2.**结尾**：；

3.**输出语句**

* window.alert()写入警告框
* document.write()写入html输出
* console.log()写入控制台

4.**变量**

* **var**：用var当变量类型，可以接受各种类型，因为js是一个弱类型语言
* **let**：let关键字作用域只有在当前的代码块，比var小
* **const**：表示这个变量不能被改变

5.**类型**

* number
* string
* boolean
* null
* undefined：当变量未被初始化，也不是null时，会被定义为undefined类型

6.**功能函数**

function add（a,b){return a+b;}

* 不需要写返回参数的类型
* 传递参数的数量没有限制

## BOM对象

浏览器对象模型

### 属性

1.window

2.navigator

3.screen

4.**history**：

* history历史记录：他有back(),forward()两个方法，就是浏览器左上角的两个箭头

5.**location**：地址栏对象

* **href**：可以设置一个url地址

### 方法

* confirm（）一个带有一段消息，一个**确认**和一个**取消**的对话框
* setTimeout（function，time  ）:在一定时间后执行一个function
* setinterval（function,time）：在一定时间后循环执行function

## DOM

文档标记模型

**作用**：对HTML文档进行操作

1.**Document**：获取对象

* getElementById：通过Id来获取对象，例如imaElement
* getElementsByTagName：根据div获取
* getElementsByName：根据name属性获取
* getElementsByClassName：根据class获取

**练习**：换取页面中的图片

1. 获取原来放置图片链接的标签对象
2. 用这个对象调用其功能换掉这个图片的地址
3. 换文本内容，这个内容可以在其中注入标签，一达到改变文本样式的目的
4. ![image.png](/assets/b3e3b68b-c7d2-4307-a731-b43c009e6b56.png)

具体内部有哪些方法可以查看网站

https://www.w3school.com.cn/jsref/coll_doc_images.asp

2.**Element**：他的方法如下

* innerHTML：返回元素内容，达到修改元素的效果

3.**Attribute**

4.**Text**

## 事件监听

就是指html上发生的事情（鼠标点击，键盘，鼠标活动）

### 点击事件

如何让事件发生后执行代码

**onclick**：事件发生后执行的方法

1.**耦合方法**：直接在标签中写入onclick=“function_name()”

然后在script中用function ”xxxx“{xxx}写入事件

2.**DOM方 法**：在标签中的id写入对象，给这个对象利用DOM方法，将对象的onclick写上函数

### 焦点事件

例：移动光标到输入框，会给提示信息

1.弹窗信息

2.换色

3.置换输入框内容

4.输入是否满足要求，在事件的方法定义判断方法，满足就true修改表单，不满足就不修改

……

#### 常用功能

1.**onblur**:失去焦点时执行

2.**onsubmit**:点击按钮时发生事件

3.onfocus：获取焦点

# jsp（Java Server Pages）

Java服务端页面

可以写html，js，css，还可以写java代码

他是JSP=HTML+JAVA

**痛点**：在java逻辑端运行后，想要返回到浏览器html上，要写非常多的代码

![image.png](/assets/56b7e473-917d-4676-8ca0-793c63b9b20b.png)

### 解决

直接在jsp中写登陆注册的逻辑代码，避免在Srvlet中直接输出HTML标签

### 使用步骤

1.**打包**：在xml中导入jar包

2.**创建jsp文件**：然后写代码

3.**位置**：放在webapp的文件夹下面

4.**编写java代码**：在body中写<%…………%>,用于写入java代码

**注意**：

1.jsp本质上就是个servlet

2.浏览器访问jsp文件时，会走动转换成java代码（Servlet）

3.jsp底层代码还是像原来一样，在java中编写一堆html的转换语言

![image.png](/assets/c2a650af-d67e-4878-bea6-90a074a740f5.png)

## html编码格式声明

### 在jsp中

他又两个位置有编码格式声明

![image.png](/assets/96d68d8b-9448-4c21-9da7-f6ae271d0b24.png)

1.**在<%@中的**：

* 用于把jsp的代码解析到服务端时用的编码方式，防止乱码。
* 同时指定服务返回的html响应要用utf-8方式编码

2.**在<head中的**：

* 告诉浏览器渲染这个html页面时用utf-8来解析页面的内容

## jsp脚本

1.<%……%>放在jspServlet()中

2.<%=……%>放在out.print（）中，作为print的参数

3.<%!……%>放在jspServlet（）之外

### 技巧

#### 在jsp中的java代码中写html

1.阅读麻烦

2.需要依赖各种环境

3.书写麻烦

4.占内存和磁盘

5.调试麻烦

用<%……%>截断java代码的上下两部分

![image.png](/assets/99e70497-5210-4714-b2b7-54cd618f222f.png)

```
    <%
        for(int i=0;i<brands.size();i++)
        {
            Goods2 brand=brands.get(i);
    %>
    <tr align="center">

        <td><%=brand.getId()%></td>
        <td><%=brand.getName()%></td>
        <td><%=brand.getPrice()%></td>
        <td><%=brand.getUnit()%></td>
        <td><a href="#">修改</a> <a href="#">删除</a></td>
    </tr>
    <%
        }
    %>
```

#### 升级的jsp嵌入Java方法

用HTML展现页面，用AJAX来动态处理数据,

**AJAX**：的作用是给静态的HTML页面增加动态的效果，它通过javascript去服务端抓取数据，然后呈现再上面。

# AJAX异步jsp和XML

最主要的功能就是替换原来的jsp

**痛点**：

1.**耦合严重**：原来的jsp需要依赖于后端的代码一起运行，不能做到前后端分离，

2.**难分功**：编写jsp还是需要后端工程师来干****

**作用**：

1.**数据交换**：通过AJAX向服务器发送请求，获取服务器响应的数据

2.**替换操作**：原来要用jsp来实现动态显示，现在可以用HTML+AJAX来体换

![image.png](/assets/36ae3996-826f-4e7c-ba27-62ad97f52aa7.png)

3.**异步交互**：不重新加载整个页面和服务器交换数据

* 例如，输入时自动显示相关内容

## 实现步骤

1.**编写服务端servlet**：正常编写就好

2.**前端创建核心对象**：下面这三个代码去浏览器网站找代码https://www.w3school.com.cn/js/js_ajax_http_response.asp

3.**发送请求**：因为前后端开始分离了，所以要用全路径发送请求
4.**获取响应**：它包含各种状态，特定的状态才获取响应

![image.png](/assets/b6b3ff19-2c16-47ff-8d8f-7d58360e59c1.png)

## 登录提示案例

当用户输入用户名时，自动查找该用户是否存在，然后在不刷新的情况下响应到页面上，实现动态。

**步骤**：

1.**绑定事件**：当失去焦点时，就发送

2.**返回标记**：是否存在的标记，然后再前端显示是否存在该用户

**注意**：

1.**html编码**：现在用的是html，他和jsp不一样

2.**乱码**：html的解决方式和jsp不一样，查看帮助文件

3.**ajav发送请求**：不用绝对网址，要用相对的网址，和encodeURICommpnone的编码防止中文乱码。

4.没弄懂

## AXIOS异步框架

他是对原生的进行封装，具体功能访问api文档

https://www.axios-http.cn/docs/api_intro

### 代码框架

![image.png](/assets/ebd6e30a-110e-4b65-8553-0be4b61d340a.png)

### **请求发送使用步骤**

1.**导入接口文件**：引入js文件，推荐用导入连接的方式引入：

![image.png](/assets/b6a1e7f4-4c8b-4a6b-868b-ad8d79173984.png)


2.**获取数据**：

![image.png](/assets/920ed5b6-4d3b-4952-ac13-6be2819dbea8.png)

3.**发送数据**：

![image.png](/assets/3585d6b8-b581-4d34-9ee8-0beb10b8d0af.png)



### 请求发送升级版

在请求数据的配置上，不用在用属性来名命

1.**请求方式声明**：不用单独用一个method来说明

* 集成到axios.post或者axios.get

2.**data的传递**：也不用data：来特殊声明

* 在第二个参数位置声明'id=1'即可。


![image.png](/assets/f5ee21b9-3eff-4f1d-bb5f-89557eb74f02.png)





### 登录案例

**步骤**：

1**声明依赖**

2.**请求响应**

3.**例子**：登录验证用户是否存在

![image.png](/assets/4967b845-61ae-4f16-9017-6fba805c8f6c.png)

4.**Idea的html乱码**：给web.xml设置

![image.png](/assets/c65a8d25-e2a0-4410-8de2-2cfc9b393347.png)

5.**简化Axios**：直接axios.get/post(url,paramater)

![image.png](/assets/2b541ade-ee88-4c83-8d51-b8bee5dea4e8.png)
