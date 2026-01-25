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

* 很方便的实现**响应式**
* 但可读性很差
* 这在实际开发中比较常用

![image.png](/assets/c4fdc0ef-7a58-4f34-9e96-8220a132d251.png)

2.**选项式API**

* 这种方式太死板

![image.png](/assets/9511a9dc-ea26-43a9-890d-e5b492005015.png)

## 组合式API

**实现步骤**：

1.**标签格式**：用的也是script标签，但是旁边要加一个setup告知vue

2.**代码结构**：分三部分**导入方法**，**变量区域**，**方法实现区域**

* **API导入**
* **声明响应式**
* **声明函数**

**注意**：这里用的生命周期函数（钩子函数），和别的地方不一样，这里是onMounted

![image.png](/assets/dd4fd98d-6e63-46b9-ba94-266305bb9ef7.png)

3.**编写组件**：上面这个图片就相当于一个组件工具，它可以在

* 点击了这个count按钮后
* 触发这个函数increment（）
* 然后实现**响应式变量**的自加
* 然后就会立即响应到下面按钮的count中去

4.**调用该工具**：其他地方使用上面这个按钮时，使用步骤是

* **导入工具API**：import ApiVue from './Api.vue'
  这个ApiVue是别名
* **再次声明这个标签**：<ApiVue/》

![image.png](/assets/cc288cad-3db9-4516-8040-513d5d0e9dc9.png)

5.**里面容易出错的地方**

* 函数的名词边上要加（）
* 导入的原生Api要用{}，且名词左右两边要**加空格**

# 实际应用

## 列表显示

### 获取异步数据

这里还是用的axios

* **下载axios依赖**：需要在这个项目文件夹下安装axios
* **运行指令**：npm install axios,(需要**管理员**)

### 编写axios

* **导入axios**：import axios from ”axios“因为在项目的node_moduls下下好了一个叫axios的文件夹了
* **编写axios代码**：和一起的一样，但要注意这里的变量不再是date，它不用写多余的参数对象（像原始数据）
* ![image.png](/assets/66f62ce7-8bd6-45bd-8463-f00a583426d5.png)
* **定义一个响应式变量**：import { ref } from ‘vue’；
  const products=ref([]);
* **保存数据**：products.value=result.data
* **编写列表**：table.tbody.tr.td
  其中tr，td是用来编写循环绑定的
*

## 条件列表查询

**实现步骤**：

1.**设置响应式**：用于存储触发条件后传递的数据，位置和axios同级

2.**设置条件**：输入文本，按钮，点击事件，双向绑定

3.**设置触发函数**：

* 由于是条件查询，所以函数内部要设置一个查询axios，实现参数传递，参数存储异常报错，

![image.png](/assets/b7983972-8e8f-4ff8-884c-ef6add8ae35d.png)

## vue中重复代码的处理

### 请求头的处理

因为很多地方都要用http……可以将这些请求的相同字段

* 放到一个变量中
* 声明给axios，让她知道，会返回一个实例
* 之后就可以通过这个实列来替代axios.get

![image.png](/assets/7f481758-c03f-4cfb-a300-5c844a832a43.png)

* 注意这里的变量名必须是baseURL

### axios中请求成功和失败部分的处理

因为这里有很多相同的.then 和.catch，因为这里是关于请求响应的回调，在这两种情况下都会触发拦截器

#### 拦截器的辅助

所以直接用一个拦截器就能是实现所有axios的.then和.catch

1.**请求工具**：

* 放到项目的新文件夹util中

2.**编写拦截器**：

* 这个固定代码，固定模板

![image.png](/assets/f6e91734-b3d1-4120-8a3b-ab48d3b2d49d.png)

3.**暴露接口方法**：export default AAAA;同上

![image.png](/assets/1a3be369-4b31-4ab7-b76b-f39fb5db8581.png)

4.**调用这个接口**：

* 由于又const AAA=axios.create(baseURL)
* 所以需要将原来的axios.get替换成AAA.get

5.**同步等待**：可以直接将调用这个拦截器接口位置的wait和async**删除掉**

## 封装接口

之前自己编写的接口文件都放到一个.js的文件中，然后放到vue项目的api文件下

**例如**：获取所有列表函数，获取条件列表函数

**代码结构**：以axios代码为例子

* **导入axios**：import axios……
* **设置函数**：export function AAAAAA(){
* **返回参数**：原来全写到一个Vue的时候，是将数据传递给一个对象的（循环数组，响应式变量），**但是现在文件中没有这些变量了**。所以都用return返回出去。
* **传入参数**：原来实在axios中用param{}传递，现在直接用上面的参数来传递

![image.png](/assets/efc982ed-ca10-47dc-99d1-4c13fc70f9af.png)

#### 调用接口

1.它支持批量导入特定的函数

![image.png](/assets/ae1ab5b4-1524-46c4-b668-9c3c8ff15345.png)

2.**调用函数**

![image.png](/assets/3939f2b8-55c2-4fc2-a8fc-4ef889c9b205.png)

# 同步异步错误

表示，在调用这个api时，它时同步的，但是函数内部时异步获取数据的

* 存在数据获取失败的情况
* 因为不知道什么时候会获取到

这时可以用两个方法 来告知这个部分用**同步还是异步**

## async和await

这个十分麻烦，因为将内部获取列表的部分axios声明为**同步后**，整个函数又成为异步的了，所以在调用这个函数的位置也要说明为同步，同时外层函数又要声明为异步

![image.png](/assets/e2af675a-c43b-4675-b7c1-24f278cb6614.png)

![image.png](/assets/2715a4c1-e8e7-4eb2-b53d-bd153fdb9aa5.png)

# **跨域请求**：

1.**浏览器的限制**：向不同源（协议，域名，端口）发送ajax请求会失败

![image.png](/assets/67137a42-00d8-4519-a7d1-4e6f6042e6f5.png)

2.**例子**：浏览器用的是vue的端口1234，后端端口是8080。

* 浏览器可以随意向Vue发送请求，因为他俩同域
* 但是向8080发送时就会失败，因为这个时**浏览器的限制**。

### 解决方法

1.**临时解决方法**：在后端控制器加一个@CrossOrigin

#### 配置代理

因为这个时浏览器的限制，可以直接避免跨域，采用发往同域的Vue服务器的方法。**让代理服务器发送请求给后端**

![image.png](/assets/687553f9-b64d-4807-b7ae-9509bcbb118e.png)

##### **实现步骤**：

1.**替换请求路径**：去请求配置文件，

* 修改baseURL='',修改为‘/api’

2.**设置邀请配置文件**：vite.config.js

* **配置代理**：server:{proxy:{将上面的/api进行处理
* target：替换这个/api之前的部分
* changOrigin:true
* rewrite(重写):(path)=>path.replace()替换掉url中原来的/api
* **注意这部分代码要写在export defult defineConfig之中![image.png](/assets/8f753004-9e6e-46e9-90cc-a537dc6e4633.png)
