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

1.**底部安全区域小程序已经帮我们处理好了**

2.**我们处理一下顶部的安全区域即可**


### 获取顶部安全区域数值

![image.png](/assets/b7cfe821-3d1d-41c9-9e19-a7ee45804f38.png)

![image.png](/assets/24359b63-bcd2-4037-8576-cf3b1b2f19b5.png)

### 将原来的导航栏样式的顶部间隔设置为动态值
