# Vue3

**优势**：

1.**更容易维护**：

* 组合式api
* 支持全面的ts编写

2.**更快的速度**：

* 重写了代码和算法

3.**更小的体积**

* 有更好的treeshaking

4.**更优的数据响应式**

* Proxy**底层代理**

# 迭代原因

1.**选项式到组合式**：

原来的选项式中某个选项编写的多了以后，可读性非常差，因为每个选项都和方法长得很像，

# 创建vue3

1.**原来创建vue2**：这个用的式vue cli

2.**现在创建vue3**：新一代构建工具**create-vue**

* **构建工具**：vite

![image.png](/assets/b91141ff-0dcf-43ef-aedc-59c5b4132cc7.png)

### 创建流程

1.**16.0以上的node.js环境**：

* **node -v**

2.**创建一个Vue应用**

* **npm init vue@latest**他会执行create-vue

# Vue3目录和Vue2的异同

1.**vite.config.js**：之前是vue.config.js基于**webpack**，现在是基于**vite**的

* **作用**：用于修改和设置配置信息

2.**package.json**：内部已经变成了vue3和vite了

3.**main.js**：修改了实例的创建方式

* 他将创建实例的行为封装成了一个方法。**用createApp函数创建应用实例**

![image.png](/assets/491cfb8f-1cda-48b2-9a92-8a93c5bb2d3f.png)

![image.png](/assets/21b77b49-aff0-4354-9f32-590dda725a01.png)

# 组合式API（setup）

![image.png](/assets/aea5f6e2-3573-4d98-b7eb-1b99fbcfbe9e.png)

**setup**是组合式API的入口

* 执行时间比beforeCreate要早
* **所以**：setup用不了this
* vue3不用纠结this指向谁

### 如何使用setup中的参数

在setup中不能直接调用属性，

* 例如，const AAA。在模板中就不能用{{ AAA }}调用它。

**调用方法**：必须要通过**return**将属性名**暴露出去才能被调用**

* return可以是setup的方法

# 语法糖-setup

**写法**：《script setup》

**作用**：帮助自动return

# reactive函数

**作用**：接收对象类型数据的参数传入，**并返回一个响应式对象**

**简单的来说**：处理复杂类型的数据响应

因为响应式的参数名字可以实现数据的**双向绑定**。

所以要将方法转换成响应式

**如果是简单的类型（没有响应式）**：就不能获取到这个数据，也不能实现双向绑定

**例子**：

![image.png](/assets/a01d75b4-207b-4747-8f88-3e9c8296cde2.png)

# ref（）

**作用**：接收**简单类型或者对象类型数据**，并返回一个响应式对象

**原理**：在原来简单的类型基础上，包裹成立复杂对象，实现响应式

**调用**：

* **在script标签中**：所以要通过默认的.value调用
* **在template标签中**：可以不用加.value就能访问

# 统一用ref了，不用reactive

# computed计算属性属性的使用

1.**实现步骤**：

* **导入computed**：
* **在computed方法中编写方法逻辑**：然后封装好传递给自己设定好的方法名中

![image.png](/assets/d45a8c81-3ceb-4c2c-ab42-6d581e504e4a.png)

2.**修改属性**：

![image.png](/assets/1456a59f-6c29-48db-bb4e-f4d300cf9ffe.png)

3.**上面获取数组用computed而下面修改数组不用的区别**：计算属性他是立即执行的，会动态更新，会自动缓存。因为这些功能才用的computed


# watch

**作用**：监听一个或者多个数据的变化，数据变化时执行回调函数

**标准**：分为**浅层监视**和**深度监视**，默认情况下是监视某些确定的**属性**，而对于某些模糊的区域，无法知道对哪个属性进行监听

**附加功能**：

* **实现立刻响应执行**:在第三个参数位置上,声明immediate:true

### 浅层监视

1.**监听单个数据**：

![image.png](/assets/f8b571a8-7692-42e1-bb54-897b61326899.png)

2.**监听多个数据**：

将多个监听对象放到一个数组中

![image.png](/assets/6670c365-6674-4c71-8d1b-89e2b31c58c5.png)

### 深度监视

对一整个对象进行监听

**作用**：不仅仅监视单个属性，也可以监视整个对象中，某个属性变化的功能

**用法**：在watch的第三个参数位置上，声明deep:true

![image.png](/assets/536092c8-77a9-4ef3-8e5e-17b8a8373426.png)

# 对象中的特定属性监视

**作用**：只监听对象中某个特定的属性的变化，

![image.png](/assets/aacf3615-a739-489b-91ba-f71f71bef5b2.png)



# 生命周期函数

![image.png](/assets/0e8847f6-6b51-4640-a6bd-73401a49e530.png)  

**使用方法**:直接用他的方法,在内部编写逻辑即可

**特点:**

* 按照代码编写顺序,按照顺序执行

![image.png](/assets/f6e4532b-958a-4504-98b8-2c9edb245993.png)




# 父子通信

**现状**:现在无法通过设置props来
