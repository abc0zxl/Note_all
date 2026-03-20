# 重建项目

1.**基于VueCli**搭建项目架子

2.**自定义创建项目**：

* 基本配置同时选择上下面的配置
* Router
* Babel
* Vuex
* Css
* Linter

3.**配置**：

* ESLint+standart
* 单独存放配置文件

4.**清理项目解构**：删除不要的，新建需要的

# vant组件库

**作用**：可以找到第三方组件库，找到现成的组件，然后调用

**注意**：vue2适用于vant2，

* vue3适用于vant3，4

**官网地址**：https://vant-ui.github.io/vant/v2/#/zh-CN/button

![image.png](/assets/563b22d6-60ae-46f8-853a-65b4646b34f7.png)

![image.png](/assets/3341eb98-ed05-4b6c-8ad4-c1cef7c84f17.png)

### vant的使用

#### 整体导入

1.**下载vant**：注意版本

2.**在main.js中注册**：

3.**测试是否导入成功**：

![image.png](/assets/6858ac69-bd92-4d92-bda2-a55b1b35f87f.png)

#### 按需引用（插件辅助）

**原因**：整体导入会导致空间问题（直接导入vant）

* 按需导入会导致**引用的导入代码难写**（导入部分Button）

**解决方法**：安装一个专门辅助导入的插件**babel-plugin-import**

* **下载插件**yarn add babel-plugin-import -D
* **读取官方文档**：编写配置文件
* ![image.png](/assets/c4953b47-4eea-435c-8480-15092cb7a85f.png)
* 就可以开始按需导入了
* **按需导入**：

![image.png](/assets/56050a24-73ab-4d6d-91fb-887ab69040a9.png)

* **重启项目即可生效**

#### 优化vant

将依赖文件单独放到一个文件夹中

* 在utils中新建一个**vant-ui.js**
* 在mian.js中导入这个文件即可



# 移动端页面单位

**作用**：全部采用vw为页面的大小单位去开发，十分便捷

**实际用的单位**：实际用的是px

**解决**：px如何转换为vw，通过**postcss插件**，实现项目的vw适配

* **下载插件**：
* **写入配置**：这个vant官网有
* ![image.png](/assets/48280fb0-8e29-46aa-8b9f-6d50762c2f52.png)

**适配屏幕**：上图是iphonex，别的手机尺寸的话需要单独来这里调整
