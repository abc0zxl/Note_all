# 移动端技术



# URL Scheme

**作用**：在移动端可以根据各个应用在手机上注册的URL_scheme跳转过来

**来源**：

![image.png](/assets/6921989b-a041-40ef-88a0-fa08cf76346d.png)

这个技术适用于移动端Android，IOS。

* **不适用于小程序，因为他们是封闭管理的微信小程序不可能打开支付宝app**


**什么是urlscheme**：

![image.png](/assets/d269e381-c02b-4c9c-8bb4-b2a6e624e4b3.png)

* 当App安装到手机上是，会将自己的身份注册到系统中。
* **Android**![image.png](/assets/715e2c84-58c4-4ae2-a862-24b434493839.png)
*
* **IOS**![image.png](/assets/2d33dc93-a83a-4460-8d0b-c79eda1b117b.png)
*

**查看注册协议**：可以在ADB查找到

1.**uniapp中实现方法**

plus.runtime.openURL('alipays://platformapi/startapp?appId=2019051064522000'，function111)
