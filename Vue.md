# 错误

1.**普通变量**：例如int类型，在vue中就用let类型

# Vue3

他是一款偶关键用户界面的渐进式javascript框架

# Vue3——html

## 代码基本框架

![image.png](/assets/dbd7b6f3-c194-4481-9bf5-67288d3c3623.png)

# HTML+Vue

vue它有专属的.vue文件可以编写，也可以在HTML中编写Vue

## 步骤

1.**引入Vue.js**：这个文件有**生产版**和**开发版**两个版本，这里用的是生产版

2.**创建Vue核心对象，绑定数据**：

* el:表示element，指明要控制的id名字，这个是实现双向绑定的**前提**。
* **data(){**：可以定义操作。例如return返回一个AAA模型
* **范围**：这个部分要重写用一个script标签括起来

3.**编写视图**：

* 绑定模型：用关键字**v-model**=“AAA”，要和vue核心对象里面的返回模型名字一样
* **插值表达式**：{{XXXXX}}可以在浏览器页面上直接显示这个模型，**前提是这个input必须在div中**

## 常用指令

![image.png](/assets/249212b2-22b8-45be-97fd-c3ff8cae1086.png)

1.**<v-bind**：为html标签绑定属性值，如href，css样式等，调用所属性为这些标签赋值。

* 简单的说：原来是用<a href=""》XXX</a》
* 现在不用在旁边写href了，就用<a标签括起来一个XXX就好了简洁明了
* 在该绑定的实例内，编写url，AAA="https://xxxx"
* 然后回到<a v-bind:href=”AAA“即可完成绑定
* 或者简写为:href="AAA"

![image.png](/assets/938c1569-0376-49d1-87b3-7276565b5f59.png)

2.**<v-model**：为了创建双向绑定的，可以修改属性值。

* **作用**：下方数据发生变化，视图也发生变化，这就是双向绑定
* 这个和双括号显示数据有区别，但内部不能实现实时传输数据，这个可以实现数据实时传输，但没有实现数据的显示。所以**双括号**和**双向绑定**
* 调用的参数也是data中的一个对象
* ![屏幕截图 2026-01-24 115037.png](/assets/ff5ebf85-46d8-4635-a388-5776451f9a81.png)

3.**<v-on**：为html标签绑定**事件**，这个要用methods:括起来

* 在绑定的vue实例中，在method方法里，声明这个函数
* ![image.png](/assets/8ee17a40-34e5-4dc4-9b60-aa9481a0d74a.png)
* 在要用到这个函数的地方用

  v-on:click="AAA",

  @click="AAA",完成绑定事件
* f
*

4.**<v-else-if**：用于存在或者不存在<div

![image.png](/assets/8b8fe574-cb08-452c-80ce-b6d3f0b0af81.png)

* 其中customer是return下的一个对象
* ![image.png](/assets/6b92188a-d6e6-4788-890d-2d5b01f40020.png)

5.**<v-show**：用于隐藏<div，用于高响应，

6.**<v-for**：也是使用data中的数据，循环操作数组addrs，addr是变量

![image.png](http://asset.localhost/C%3A%5CUsers%5CZhuanZ1%5CAppData%5CRoaming%5Ccom.codexu.NoteGen%2Farticle%2F%2Fassets%2Fd442b0fb-7935-4d75-9f9b-1556a59f1d71.png)

![image.png](http://asset.localhost/C%3A%5CUsers%5CZhuanZ1%5CAppData%5CRoaming%5Ccom.codexu.NoteGen%2Farticle%2F%2Fassets%2F7e605911-0473-404d-88d4-4c4bc8be96e0.png)

* 这个数据的位置也是在data下的return中的一个数组。

  ![image.png](/assets/efbd06dc-356b-452c-841e-2a3e1b92b71c.png)
* 之所以能调取到这个数据 ，是因为div和下面的spcript标签中的某个应用实例的.mount("#xxx")，**完成了数据绑定**，所以在这个div下直接用这个数组名字就能调取到数据
* ![image.png](/assets/10701965-3ae8-4331-b574-fc36d7e089af.png)

## Vue生命周期

她又八个阶段，每触发一个生命周期，就会触发一个生命周期的事件（**钩子**）

![image.png](/assets/1a7cf697-6ecc-4246-a820-993f3b07b231.png)

### 语法规则

1.**书写位置**：

* 和data(),method()同级

2.**书写规则**：

* mounted:function(){XXXXXXXXXXXX}
* 这里的mounted就是上面的状态，不能是别的
* {}里面就是用来书写该周期要执行的代码

#### 注意

1.**mounted**：这个是最主要的状态，表示页面已经渲染成功，Vue初始化完成

2.**设置生命周期事件**：直接在data(){}中写入对应的名字mounted（）{}然后写入jsp代码，到时间就会执行

## 使用案例

### 遍历列表

在这里简化了DOM操作，但依旧要用axios实现异步，利用vue的生命周期。

1.**在模型中使用axios**：因为axios代码在Vue模型中，在axios中要调用他的外围的数据要把this放外面。

![image.png](/assets/793ab292-36de-4907-91f9-39fe6ffba22c.png)

2.**属性名字**：这里要用实例中的名字，不行换成小写也许，他会自己转换

3.**不用再写json模型**：直接用v-model就能绑定模型变量

### 添加商品

这里重点是添加点击事件，

#### 步骤

1.编写依赖

2.<div id="确定好要控制的范围

3.编写**vue核心对象**实现绑定和模型声明

4.对按钮做一些变动，将原来调用的id，改为@click="AAA"

5.加入异步请求的操作，传输数据

6.绑定所有输出的数据

7.**触发提交**：因为这里是用的vue的生命周期事件来提交，所以按钮要把submit类型改为button，因为submit默认提交事件,也可以用下面这个阻止。

8.**去除默认**：e.preventDefalt();

# Elementf

他是饿了么公司开发的一套基于Vue的网站组件库，用于快速构建网页。

可以查看有哪些样式，代码可以直接去网站调用

https://element.eleme.cn/#/zh-CN

1.**超链接**

2.**按钮**

![image.png](/assets/7c63fabd-cfbb-4367-b509-d945f735f792.png)

3.**图片**

4.**表格**

## 布局

element有两种布局方式

1.**Layout布局**：以行和列来布局的，行有若干，列有24个分栏

2.**Container布局容器**：顶部栏，侧边栏，中部列表，这些网站都有代码，懂vue就能看懂，网站中均有例子展示

## 使用

不用主动背诵这些按钮样式，直接看官网挑选自己需要的样式即可

1.**引入element的三个依赖**：导入vue.js,element_ui,

![image.png](/assets/355f6a09-1f58-40ed-aa54-25f8ffb41423.png)

2.**创建vue核心对象**：

3.上Element查组件，

4.**修改事件**：例如点击按钮@click="AAA=true"就能弹出对话框，这个AAA就是控制对话框显示与否的代码。

5.**发送数据到控制台**：console用this.product

## 复选操作

在裂变边上有选择框，![image.png](/assets/fbbeed77-5f4b-444c-87b8-ed2dd565970d.png)

### 批量删除

**步骤**：

* **动态sql**：创建sql映射，
* **json转数组**：连接上mapper，service，servlet，
* **Vue核心创建链接的数组**：用于双向绑定，动态记录
* **原方法获取已选ID**：在element的复选框中，有一个multipleSelection[i]获取，因为它就存的**实体**
* **提交id**：用axios提交

# Vue3项目


## 创建Vue项目

**步骤**：

1.**创建位置**：象在哪里创建就直接去那个文件夹下

2.**打开命令行**：注意要以管理员身份打开

3.**运行创建程序**：npm init vue@latest

* 记得开启github网络访问

4.**项目参数设置**：一直回车就好

5.**根据他的提示**：提示进入一个文件夹下，

6.**安装项目**：这个也是和他给的提示放一起的。

## Vue项目框架

通过在线床架目录框架后，可以用来编写前端代码。

![image.png](http://asset.localhost/C%3A%5CUsers%5CZhuanZ1%5CAppData%5CRoaming%5Ccom.codexu.NoteGen%2Farticle%2F%2Fassets%2F0cbab111-b07e-4bb3-b307-81f12989e077.png)


### 项目开发流程

1.**默认首页**：index.html,这个是开始访问Vue时，最初进入的页面，这个内部有一个代码，表示去执行main.js

2.**入口文件**：这个时index后下一个要执行的文件，他导入了App.vue文件

3.**根项目**：这个就是App.vue,他就是页面显示的核心



2.**VsCode运行**：在界面左下角有一个npm脚步，点击serve，就可以运行。

**.Vue文件**：他是Vue的**组件文件**



* script：控制模板中的**数据来源**和**行为**
* template:他是模板，用于生成HTML
* style：编写CSS的样式代码

  ![image.png](/assets/fe422988-a3f2-46ac-9611-fb01d289b742.png)

3.**Element环境配置**：

* **下载ElementUI组件库**：在项目的文件夹下运行(要管理 员权限)

  ![image.png](/assets/c1ac4590-575a-4e53-a05e-09f8f18f4bf6.png)
* 配置main.js，**导入Element，使用Element**
* **创建Element组件**：在views文件夹下创建element文件夹
* **去官网找代码**：

  1.**快速整理文件**：shift+alt+f，让代码看着更加整洁
* **修改默认显示路径**：在App.vue中导入element-vue

4.**Element容器**

这个作用是让页面各个部分分区，**菜单**，**列表**，……

* **新建文件夹**：在view文件夹下创建**tlias**文件夹，再创建element组件
* **创建结构**：在template中的<AAA-view的这个AAA可以自己定义

## **Vue Router**

他是一个官方标准

有三个部分组成：

* **VueRouter**：他是一个中转中心，是一个路由表
* <router-link：请求组件，用于发起连接的请求
* <router-view：动态视图组件`，用于渲染展示这个路由请求

![image.png](/assets/8c577129-a719-4bdd-9cde-5493a05c2d70.png)

### VueRouter路由表

它里面是一个**js**文件，

**步骤**：

* 导入vue，vue-router
* **编写转发路径**：path是请求，component是目标路径

  ![image.png](/assets/aaccaa3a-5848-4c39-8e2c-b772717a823f.png)
* **编写转发标签**：

  ![image.png](/assets/e590dd07-910e-4b3e-a3dc-4d915b71d40b.png)
* **默认的入口**：当第一次加载时，会默认的路径是\,所以要配置个\的路由
* f
* f



## 实际应用


### **修改配置参数**：

1.修改端口号

![image.png](/assets/a9207660-dea4-4bae-9d6b-8f0b90d0d7a8.png)

### 列表数据的加载

这里要用到axios完成数据的异步加载

**步骤**：

* **安装Axios**：npm install axios
* **导入**：再script中写入import axios from 'axios';

**扩展**：集体修改一列，男->1

![image.png](/assets/6bbc2b16-db40-4edb-aedd-e8ea068ec958.png)

* f
* f
* f

## 打包Vue项目

就是那个Build按钮，打包好后的文件会在项目的list文件夹下

**部署打包文件**：下载一个nginx，用来查看打包的前端文件

![image.png](/assets/fdf8b999-0086-4df0-8549-41b6765f8757.png)

**步骤**：

* 将打包好的文件夹放到html静态资源文件目录下
* 如果没有反应的话，先查看**error.log**查看是否有错误，可以再nginx.conf中修改默认端口号
* 没有的话默认再**80端口**下

### Nginx实地部署软件

他用于实际应用中部署前端的软件，有高并发，稳定，负载均衡，安全防护，支持https等。是一个实地部署工具。

他可以运行**打包好的前端Vue**。


# Vue——API变成风格

1.**组合式API**

![image.png](/assets/c4fdc0ef-7a58-4f34-9e96-8220a132d251.png)

2.**选项式API**

![image.png](/assets/9511a9dc-ea26-43a9-890d-e5b492005015.png)




# Vue
