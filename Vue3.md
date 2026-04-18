# 注意

1.在 Vue 3 中，`computed` 会自动**追踪**其内部使用的所有响应式数据，当这些数据变化时，计算属性会重新求值。

Vue3

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

**注意**：uniapp的生命周期和vue3的生命周期是分开的，但是编写uniapp的时候也能一起用

**特点:**

* 按照代码编写顺序,按照顺序执行

![image.png](/assets/f6e4532b-958a-4504-98b8-2c9edb245993.png)

# 父传子通信

**现状**:现在无法通过设置props来接收父组件传递过来的参数

**实现方法:**

1.**子组件**:通过**编译器宏defineProps**,实现props的功能,并设置好参数名字

![image.png](/assets/6891f5c8-6014-4c96-9727-464540d57f1a.png)

2.**父组件**:通过子组件的标签设置参数,这回是直接调用这个参数名字传递参数即可

![image.png](/assets/21f4d932-adeb-4aa7-bd8d-4030dee809dd.png)

# 子传父通信

1.**子组件发消息**:也是用emit,但是形式不一样,是通过调用函数的形式来发送的

* **首先**:通过**编译器宏**获取emits这个响应式
* **然后**:调用这个设置好的emits发送消息

![image.png](/assets/c21fafff-6a86-43e7-8ad5-280063c3f95b.png)

2.**父组件收消息**:通过子组件设置的参数名称来接收

![image.png](/assets/200eb422-828a-462f-81ae-8896990d4033.png)

# 模板引用

**作用**:通过ref表示获取整个是dom对象或者组件实例对象

**使用方法**

* **获取ref对象**
* **绑定ref对象**

![image.png](/assets/dd393788-2cdd-40ea-bbc7-c05e6bcbaa01.png)

**使用场景**

* 定位输入框位置,结合钩子函数,实现焦点自动聚焦

# defineExpose

**问题**:在vue3中script setup的语法糖中,**内部属性和方法是不对外开放给父组件访问的**

**解决问题**:可以通过**编译宏**defineExpose指定哪些属性和方法允许访问

**作用场景**:顶层组件向任意底层组件床底数据和方法,实现跨层组件同行

**测试**:运行函数时,在控制台中可以通过proxy看到子组件开放的属性和方法

![image.png](/assets/0eb19777-9ce6-4e6e-9724-6ee9d689e38a.png)

# 跨层传递参数

例如一个页面中,有商品信息,商品信息的某个区域有一个评论信息.

* **顶层**:整个框
* **中间**:商品信息
* **底层**:评论区域

1.**顶层传递到底层**:通过**provide(AAA,BBB)**:来传递

![image.png](/assets/59e91147-f44a-40af-b9e9-038f6eb04f03.png)

2.**接收数据**:通过**inject(AAA)**接收

![image.png](/assets/5aa42612-9170-400f-8358-cfea56c92551.png)

3.**还可以传递方法**:

![image.png](/assets/f32ccc0f-0bbc-40d6-9e2a-b15ca0401b60.png)

![image.png](/assets/b43d8b6b-36c3-46ac-b6ad-9c1df50f9152.png)

# defineOpitons

**原因**:像props,emits等都有**编译器宏**来设置,而像设置组件名字等**options**属性
**等一些vue2的功能则没有办法实现

**实现方法**:通过**defineOptions**来实现,在内部定义这些属性

![image.png](/assets/31f20a7d-303c-4674-ae6c-8933b3a279d7.png)

# defineModel

vue3的v-model和vue2的v-model底层中是不一样的

他用的是:modelvalue

![image.png](/assets/eec9e0c2-9102-48a8-a819-1a1d22e4e396.png)

**优点**

不在通过props来接收了,通过defineModel()来接收

![image.png](/assets/0dc9e201-c394-4611-b4db-190a26bbfa98.png)

**作用**:可以便捷的实现传递v-model的值

### 实际应用

**简单的说**:就是实现**组件级别的双线绑定**

value="modelvalue"是接收父组件传递的值，modelValue=e.target.value是给父组件传递值

1.**父组件**

![image.png](/assets/bb3af768-b9d7-4af2-96a9-c4c5fbe13435.png)

2.**子组件**![image.png](/assets/84de6ec3-b49d-4f7f-9632-f6fc36b58670.png)

3.**让它生效方法**:不启用无法起作用

在vite.config.js中编写

![image.png](/assets/c8790bb4-39df-4abc-8c76-c321dfef219e.png)

# Pinia

最新的状态管理工具

**特点**

* 没有mutation
* 符合组合式风格api
* 去掉了modules的功能
* 适配ts更佳

**使用特点**

* **actions**:可以直接修改state,不要mutations了

# 配置有Pinia的vue3项目

**Pinia官网**:

**安装pinia**:yarn add pinia

**引入pinia**👍![image.png](/assets/b0d7ae62-7894-4085-b4c7-76f79ea429df.png)

**特点**

和vuex很像,就是他的各个参数和方法的设置方式都按照**组合式方式来**

![image.png](/assets/5ef70fa6-af45-4b5f-a09f-8a0469d0443b.png)

**注意**

* 设置方和调用方都得设置ref
* 要通过手动刷新才会更新数据

![image.png](/assets/1726dc6d-a02b-477e-b71d-2a895495a142.png)

**设置方法**

就在文件中设置就好了,普通方法就用箭头函数即可

# Pinia获取数据

这里获取数据是获取**频道列表数据**.并把数据渲染到App组件中去

**原理**:创建一个叫channel的空间来存储获取的数据

1.**获取数据,给channel写入数据**

![image.png](/assets/d9a7c94e-63e3-45f2-b255-79850bb6b938.png)

**创建仓库**:图中创建了一个叫channel的仓库,文件名字也叫channel,这个**箭头函数**中可以设置

* 异步请求

**仓库名字作用**:作为store的唯一id

* 用于区分不同的Store

2.**获取channel数据到前端**

![image.png](/assets/a689aba9-7e16-4d9c-b5f9-d5140e1b7692.png)

3.**注意**:

* 如果将获取过来的getList**解构了的话**:会导致解构出来的属性,**失去响应式的功能**
* store应该分成不同的模块和文件处理,就是说store中应该有多个文件
* store是一个用reactive包装的对象,获取的数据是一个响应式的,所以说解构的时候相当于重写赋值了两个属性.**就丢失了响应式的作用**
* **解构方法**的话可以直接解构

### 解决解构数据问题

利用**storeToRefs(AAA)**

![image.png](/assets/74a013fb-e821-4fb5-b808-a38d7143f06a.png)

# 调试Pinia

这个就相当于调试vuex

**位置**:浏览器控制台的vue插件中的**Pinia**

# Pinia持久化

通过插件来实现

**作用**:页面刷新数据不丢失

**配置信息**

* 使用localStorage进行存储
* store.$id作为sotrege的key
* 通过**JSON.stringify/JSON.parse**序列化和反序列化

1.**配置步骤**

![image.png](/assets/888a2dd2-aa9d-4ee3-8458-2b99977d4fe7.png)

2.**将插件添加到Pinia**

不是在main.js中

![image.png](/assets/5f5a99a2-9b99-490b-b030-de52d1922184.png)

3.**使用Pinia持久化**:在第三个参数的位置,开启当前模块的持久化,**persist:true**

![image.png](/assets/39874a06-b051-44e2-b5b1-2c8794e6b80b.png)

# 持久化范围

**自定义范围**:在第三个个参数中通过paths:['AAA','BBB']声明**需要持久化的项**

![image.png](/assets/0071e384-6bf4-4898-8539-742138acf75b.png)

**默认范围**:不设置paths就表示整个state都会持久化1

# Vuex和Pinia持久化相关知识

### Vuex

#### 直接讲他的各个字段是干啥用的

1.**state**：存放参数的，只存放参数

2.**mutations**：存放方法的，里面的方法可以传入参数，并支持修改state

3.**actions**：存放有异步要求的方法，

4.**getters**：存放计算属性的，他可以调用state，他是属性不是方法

5.**mudels**：用来导入子state文件

#### 关于调用(直接调用)

1.**this.$store.commit**：调用state的属性

2.**this.$store.mutations**：调用mutations中的属性

3.**this.$store.dispatch**：调用actions中的属性

4.**this.$store.getters**：调用getter中的属性

#### 快捷导入

1.**mapMutations**：

2.**mapGetters**：

3.**mapActions**：

4.**mapState**：

### **注意事项**

1.computed：这个的作用是用来存放需要响应式的属性。需要用computed来监听他们，他是一个依赖响应式数据能自动更新的地方。

2.mapState和mapGetters：都是导入的属性，所以只能放在computed中

3.mapActions和mapMutations：导入的是方法，可以放在methods，watch中等地方。

4.在代码中可以用{{AAAA}}来调用放在computed中的属性。

5.vuex没有明确的分区，参数都放在一个地方。

![70417e23c8ed919664cfc277252af658.jpg](/assets/3195c4c2-aafa-4460-9afd-7876066e3df3.jpg)


### Pinia持久化

他直接省去了mutations，mudels，让仓库有了名字，可以是实现分区。

1.**存储参数位置**：**state**：（）=>({  ……

2.**存储方法位置**：

* **getters**
* **actions**


3.**调用参数**：

* **mapStores**：这个是导入多个库
* **mapState**：这个是导入一个库中的某些参数
* **mapActions**：导入某个库的方法

4.**可以自动补全**：

* **修改state参数的时候**：自动补全为action的一个方法
* ![image.png](/assets/55f1e5b8-9e7e-44c4-9c80-90788218b819.png)




#### 利用函数方法定义Store

1.原来的外部框架不变

2.**定义属性**：直接用const响应式来声明

3.**定义方法**：直接用function AAAA(){来定义

4.**额外的必要操作**：将他们一一返回


![image.png](/assets/f4044948-9b68-442f-848b-a6c44d621b7c.png)

### Pinia定义综合案例

![image.png](/assets/5463b60a-866e-4d84-9d4b-ff28533123b6.png)
