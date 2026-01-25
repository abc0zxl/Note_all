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

# 实际应用

**在项目中下载依赖**：element-plus，原来采用**导包，连接，**，现在直接在这个项目中下一个。

npm install element-plus --save

1.**导入依赖**：在main.js中

![image.png](/assets/ae55157c-48c1-418d-9a3a-b441f20b305d.png)

2.**编写界面**：这个需要在src下创建这个页面

然后参考element官网编写即可

3.**语言问题**：有时候会显示英语，就要在main.js中导入element的中文包，并启用，两个步骤

![image.png](/assets/1054f7a6-e1fd-4a0d-8459-f323da684ef4.png)



# 登录注册代码

1.**表单验证**：

* 用rules来编写规则，
* 用prop来指定校验项

2.****
