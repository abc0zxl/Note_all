# 首页修改

修改头部

![image.png](/assets/fe0ee2ea-8ce1-49d9-8748-074b2cd0e583.png)

# 导航

**图标库**：https://www.iconfont.cn/

![image.png](/assets/b212651c-99a9-4a13-9086-a1a1f2d228a8.png)

# 轮播图实现

1.**导入图片**：

![image.png](/assets/118dfa81-776b-402e-8842-0d56ab9c2c80.png)

2.**编写轮播逻辑**：这个是在index.vue编写的

* 有专用轮播标签：**<swiper-item》**
* 这个标签还要编写数据绑定用于换图片
* 这个轮播图相关功能可以查找官方文档

![image.png](/assets/4d7126e3-b37b-49a6-b738-859425589a80.png)

![image.png](/assets/28449ed7-cc96-4d58-8057-ffa4752e112d.png)

3.**编写轮播图的显示效果**：

* 首先在标签里加个类名，用于编写css时所用的名字
* 注意这里的.banner,.banner要严格这样编写
* ![image.png](/assets/58fbc3b4-ddd1-4a20-ad37-e9ad9a64aad9.png)

# 返回提示信息

![image.png](/assets/629a8e6b-8e8d-46b8-b4c9-69f8eca75aa4.png)1.**uni.showToast()**：这个是uni-app提供的跨端API，作用是再页面上弹出一个轻量级的提示框

2.**icon：’none‘**：指定提示框的图标样式为”无图标“，可以是**success**,**loading**

![image.png](/assets/978b037a-677e-4c66-89b9-515c6df0aeaf.png)

![image.png](/assets/332fac6d-ec78-4931-8a64-4ba8a2ad2941.png)

# 自定义导航栏

**原因**：不同的机型，顶部的显示效果不一样，有的好有的坏，所以要用到自定义导航栏

**实现步骤**

1.**导入别人的导航栏**：这个放到首页的文件夹下，用一个新的文件来存储这个导航栏组件

2.**在首页中导入这个组件**：

![image.png](/assets/a2a82a19-54c8-4c46-b89d-16753a7e0c3c.png)

3.**将原来的导航栏隐藏**：

* 在pages.json中
* 添加一个导航栏的风格声明

![image.png](/assets/21fc35cf-9a34-4155-b970-1388f26d9771.png)

## 安全区域

不同的机型他的安全区域不同，这个安全区域是表示不被顶部刘海，或右上角的推出按钮所阻挡的区域。

**![image.png](/assets/afadff41-85b8-450c-bdcc-771b4b61b561.png)**

1.**底部安全区域小程序已经帮我们处理好了**

2.**我们处理一下顶部的安全区域即可**，微信提供的数值单位是**px**

3.**然后根据导航栏的样式，再设置一下最顶部信息条的颜色，防止撞色**

### 获取顶部安全区域数值

![image.png](/assets/b7cfe821-3d1d-41c9-9e19-a7ee45804f38.png)

![image.png](/assets/24359b63-bcd2-4037-8576-cf3b1b2f19b5.png)

### 将原来的导航栏样式的顶部间隔设置为动态值

![image.png](/assets/95d5eaf3-754e-40d6-8757-7ef4c6a6c5a3.png)

在最外层的标签上

![image.png](/assets/11f8db5b-be12-4d9a-8fc8-966342b4f3d5.png)

### 修改顶部信息条字体颜色

![image.png](/assets/57dfb7c8-d788-4162-9669-93f12c9fac2e.png)

![image.png](/assets/cf47f8cc-601e-49e7-a8f2-a9c5303d9de8.png)

### 配置底色，用于和别的区域区别开

![image.png](/assets/5a74f95c-1012-4950-815c-a0fe5d4855b4.png)

### 配置每个分类的图标和标题

![image.png](/assets/505fd4b5-232c-44ad-a6a9-36727be51fa6.png)

### 推荐页面

![image.png](/assets/1820bbe4-702e-4757-a688-33566a266c49.png)

### 猜你喜欢模块

**通用组件都要放在src下的component中**：

### 页面滚动让上面的导航栏不动

上面的情况下滚动页面，上面的导航栏会跟着滚动走，而不是停留在上面

**关键字**：<scroll-view scroll-y》，css

**作用**：被他框住的部分会滚动，在外面的就不会跟着滚动

**方法**：

这个直接用模板

1.**先让page占满整页**

2.**显示模式调整为flex**

3.**告诉flex元素按照纵向排列**

4.**让要滚动的部分占满他标签内的所有页面**

![image.png](/assets/5f3a8bc2-ff47-4197-b6e5-a00aa75b313b.png)
