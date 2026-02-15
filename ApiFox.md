# API文档示例

1.**apifox文件夹示例**

![image.png](/assets/8a1be9c6-cad3-483a-ab11-d261256dc6e4.png)




## 返回响应

在设计接口时需要返回响应，而响应的数据结构需要自己定义。

1.**定义返回响应的数据结构**：在apifox左边的**组件库中**，里面有一个**默认响应模板**，在这里就可以设置全局的返回响应的数据结构

2.**为什么要自己设定**：因为有的公司的响应结构不一样

## 引用模型

在界面的左侧数据模型，他就是可以存放各种

**公共**数据对象，用于日常引用

1.**使用方法**：在编写参数类型时，在选类型的时候就会出现**引用模型**，就会将这个数据对象嵌入到这个Object对象中去

## 响应示例

因为完整的API文档需要**响应示例**，在编写接口的时候滑到最下面就会有**添加示例**这个按钮

![image.png](/assets/8f3ce722-c655-4825-9197-dc8f156cb827.png)

## 自动生成响应数据结构

#### 通过json自动生成

如果没定义好**引用模型**，在**返回响应下面**，有一个**通过JSON等生成**，

![image.png](/assets/c4f1d972-a296-4d02-bc61-3cf8e85263ec.png)

比如如果有实际要返回的json数据了，就可以直接将这个json数据粘贴到里面，就会自动生成类型

![image.png](/assets/fd092925-fa8f-497e-abfb-ad1bba9fd19e.png)

#### 通过连接数据库表，sql语句生成

连接数据库后可以导入数据库中的数据类型结构

1.**连接数据库**

![image.png](/assets/536d05eb-dfa6-4b3f-88b1-6d05708a94ca.png)

2.**从数据库导入数据**

![image.png](/assets/6a420d0e-57a7-4ad9-9fd1-ea6a7f8feb7b.png)

3.**也可以通过sql语句DDL（Data Definition Language）**

在上图的右边按钮就是

## 响应组件

这个就是返回响应的时候的**返回码**

![image.png](http://asset.localhost/C%3A%5CUsers%5CZhuanZ1%5CAppData%5CRoaming%5Ccom.codexu.NoteGen%2Farticle%2F%2Fassets%2F0b187281-b859-4c2f-bd2d-586a908720e4.png)

1.**设置响应码**

在apifox左边的**组件库**->**响应组件**里面

![image.png](/assets/8f7d6c42-a95b-4dda-832d-4a7fcf4b59ce.png)

## 自动生成API文档

1.**swwager辅助**

swwager可以自动生成API文档，apifox可以在**数据管理的导入数据中**，写入swwager的url，设置导入间隔时间，自动导入

2.**Idea的ApiFox插件**

这个直接就能自动导入代码中的存在接口，自动在界面中生成api文档

## 生成java后端代码

在**接口**文件夹位置，左边有**三个点**，点击就会有生成业务代码的功能

![image.png](/assets/aacc6357-cb1d-40c9-ad18-8d8068cf1ee8.png)

## 自动生成测试数据

在测试接口的时候，postman需要给参数提供具体的值，而apifox可以直接根据设置的参数来生成对应的值，

1.这个设定的值的方法和种类非常多

## 可以自动报错

如果后端的返回结果和**设定的响应**有差别，就会报错，同时还会返回，**响应时间**

![image.png](/assets/e5387e7b-8b26-4c4b-9ef0-e6edeb9b1bf4.png)


## 可以操作数据库

![image.png](/assets/a18ffef7-7116-4261-98bd-5ee1e27cad8e.png)
