# 注意

2.**遍历方法**：for in语法

![image.png](/assets/cc2cbe32-10d1-4d55-a1d4-c4590aa10db0.png)

3.**null**：他是**空对象**

4.**变量声明**：尽量用const，对象插入const不报错，但是将一个新的对象赋值给const变量，**会导致地址改变**，报错。

5.**DOM对象**：在html中div叫做标签，在js张叫做dom对象

6.**Dom对象数组**：他是一个**伪数组**，

7.**模板字符串${AAA}**：他的作用是**在字符串中嵌入变量，表达式，并自动拼接**

8.**清空字符串的空格**：DOM对象.value.trim()

9.**空的时候也是假**

10.**模板字符串的使用**：标签的话需要改成斜杠好才能用

![image.png](/assets/3506e330-0641-45fb-a04d-b01b0834d2e4.png)

11.**不给body设置高度没有滚动条**：

12.**css中选择不同的input**：通常是.和#指定某个盒子，
![image.png](/assets/c55f3baf-9f99-46ea-a7c9-408e6a66d7a3.png)

13.**精确的找盒子**：直接去浏览器看这个盒子的名字，都是下划线连接的

14.**通过拼接url跳转**：href='#/friend"

15.正则表达式是字符组合匹配的一种模式

16.类的索引必须要加.标签不用

![image.png](/assets/d497dcc6-307f-487b-835a-ddc498084573.png)

# JavaScript

现在用的是最新版的ECMAScript,也叫ES6(2015年)

javascript的var类型他的特点是

根据原文内容，JavaScript 中 `var` 类型的特点包括：

## 变量

存储数据的一个容器,存储数据的标识符,通过该表示符获取内存中存储的数据

### var

表示一个变量,但具体类型还没有定下来,按照存储不同的内容来判断他是什么类型

* 支持科学计数法
* 支持二进制,16进制
* 支持不同种类的变量类型

## 数据类型

1.Number:整数,浮点数,未赋值为

2.String:存储为字符串就为string类型

3.Boolean:存储关键字false,true时为Boolean类型

4.Undefind:var声明了变量但是未赋值的变量类型.

* var abc;

5.Null:这个给时主动给赋值为null的时候才是null

* var abc=null;
* 明确未来这个变量是一个对象类型,
* 但是现在没有赋值对象的一个类型.

6.Symbol

**作用**:undefind和null:是表示变量未赋值的时候,明确给它声明的一个类型.

## 数组操作

1.**尾部新增**：AAA.push()

* 一次可以在数组**后面**加**一个** 或者**好几个**

2.**头部新增**：AAA.unshift()

* 一次可以在数组**前面**加**一个** 或者**好几个

3.**尾部删除**：AAA.pop()

4.**头部删除**：AAA.shift()

5.**中途删除**：AAA.splice(start,deleteCount)

6.**对象数组**：这种含有**无对象名字**的方式和**有对象名字**的方式。

* 数组中的对象，不管有名字还是无名字，**元素都可以不一样**

7.**map遍历数组**:他有返回值,可以返回一个处理后的新数组

* map有映射的作用.
* ![image.png](/assets/e6e43332-d37c-4c9d-a779-d3f5f4e58e21.png)

8.**join方法**:

作用是把数组装换为**字符串**

* 可以设置各个元素的分割字符

## 基础显示

1.**输入框**：prompt("AAA");

2.**页面上显示**：document.write('BBB')

* **双引号**：这个BBB可以是文本
* **单引号**：这个给BBB可以是容器
* **它可以组合成容器**：如条形图的每个条单元![image.png](/assets/c22fd151-adee-4722-8fd5-0b8db7b54613.png)
*

## 函数

他的基本规则是

* **默认值**：有参的时候，传递无参，需要让参数有默认值，
* **类型**：可以传入**数组**，**常量**
* **返回值**：可以在for内加一个**return**，返回数值
* **自带参数容器**：在函数中可以用arguments作为参数容器的操作工具

**![image.png](/assets/01428a70-fe31-42b1-ab5d-8ccaf68f8a73.png)**

## 匿名函数

也叫**立即执行函数**

* 他没有函数名字
* 代码运行立即执行
* 它有两种写法

![image.png](/assets/17fed08f-2feb-4d8b-8b5a-6138b011c54d.png)

![image.png](/assets/131b435e-c8b7-4edf-8bf6-8bc374f93bb1.png)

1.**应用场景**：

* 对象中的函数元素
* ![image.png](/assets/a0560d39-ccca-4755-85dc-6d6f6455fcdd.png)
* 含参数的函数元素
* ![image.png](/assets/66d19798-da04-499e-8fef-8dd7d6ea2394.png)

## 对象的定义

1.**对象的增删改**

* 可以用let，const，var定义
* const的对象不可以修改值
* 增加元素的时候直接.AAA即可
* 删除元素的时候要用关键字 **delete AAA.BBB**

![image.png](/assets/6432401d-d3e6-4167-a092-f46388594914.png)

2.**访问对象的方式**

* 点形式
* []形式：AAA['BBB']

## 箭头函数

const getData=()=>{    }

1.**const getData**：表示声明一个名字叫做getData的常量，用来存储后面的函数

2.**（）=>**：这个是放参数的地方

3.**{}**：这个是放函数体的地方

## 内置函数

1.访问mdn，可以查看各种内置函数，

* 如math.pi，可以直接在搜索框搜索math

## 扩展运算符

**作用**：展开所有属性

1.**保证options完整性**：如果{}只放一个属性的话，原来的属性都会消失

* 展开原来options.header中所有属性，
* 再加上这个新加的
* 就保证了完整性

![image.png](/assets/65d4d630-df76-4e61-8a89-8c0579b0ff28.png)

## 短路求值

**关键字**：**||**或者**|**

**A  ||  B**

1.如果A为空或不存在，就会调用B

![image.png](/assets/54dd46a9-a17e-48cc-8979-5af3310def41.png)

## 数组查找.find（）

![image.png](/assets/a4d793a9-5010-4b6a-9677-5b39487cdaa7.png)

这个能查找数组对象中符合要求的数组，返回第一个满足条件的元素

**v**：他表示数组中的每一个元素

**v.type**：他表示当前元素的type属性

# Web API

使用js操作html和浏览器，控制网页元素交互等各种网页交互效果

# DOM

文档对象模型

1.**DOM树**：将HTML文档以树状结构直观表现出来，直观的表现标签与标签之间的关系

![image.png](/assets/a1606ed7-9954-4c67-8505-4b0c64dcbd2c.png)

2.**DOM对象**：如何一个标签都是一个对象，看上图每个结点都可以作为一个对象

![image.png](/assets/51cb2647-bd72-451a-893e-cb0aeeb5a8f5.png)

3.**document对象**：这个是dom提供一个对象，他是最大的一个对象

* 可以操作页面内容：document.write()
* 获取标签：document.queryment()

4.**获取DOM对象**：获取某个对象（标签），可以操作，修改这个标签的内容

* **获取dom对象**：document.querySelector("AAA")**只会选择第一个AAA标签**
* ![image.png](/assets/10205e9f-2663-479e-b8ca-a2cd07d6368e.png)
* **获取嵌套标签里的某个dom对象**：嵌套用空格隔开，
* ![image.png](/assets/d9a83bf8-304b-4d2a-875a-e560019323b0.png)
* **获取dom数组**：获取只当某个层级的多个对象
* ![image.png](/assets/a44d59a5-2abf-49b0-99d5-69085768b3bb.png)
* **其他获取方式**：
* getElementById()
* getElementsByTagName()
* getElementsByClassName()

5.**修改dom内容**：

dom对象.innerText

dom对象.innerHTML

* innerText不解析标签
* innerHTML解析标签

6.**全局body**：这个也是一个盒子，就是整个页面容器，可以在样式中操作这个里面的各种样式

![image.png](/assets/1503ce0b-5541-4c9e-9756-b05540cd159e.png)

7.**类名变更**：可以通过dom对象和**classList**给目标对象修改类名

* **添加类名**：AAA.classList.add('active')这个active是续接在原类名后面的名字。
* **删除类名字**：AAA.classList.remove()
* **有就删除，没有就加上**：AAA.classList.toggle()

8.**获取input和button**：

* 可以操作input的内容
* 可以操作button是否启用

### 自定义属性

规定用data-AAA的方式命名自定义属性

1.**获取这个属性**：首先获取他的标签。在通过这个dom对象.**dataset**.AAA获取到这个属性值

### 间歇函数

1.**setInterval(AAA,BBB)**：函数AAA，每隔BBB毫秒执行一次

* 鼠标悬浮到轮播图，轮播图自动切换

2.**closeInterval（n)**：关闭定时器，关闭方法是

* 获取到对应的setInterval的唯一标识n
* 用closeInterval（n）关闭即可

![image.png](/assets/3aa9f78b-96ab-4747-bd2c-c68dd922c855.png)

3.**应用场景**：

* 60秒倒计时关闭按钮

### 焦点事件

这个也是需要获得这个DOM对象，通过操作dom对象类设置焦点。
![image.png](/assets/2146dcfe-c2c4-40ee-b35a-a3e97ceb0fea.png)

### 事件对象

1.**type**：获取当前事件的类型

2.**click**：**鼠标**点击事件，可以获取点击这个操作的各种信息

![image.png](/assets/277e21bf-89fe-4e16-8780-19777a099a91.png)

3.**keyup**：**键盘**点击事件，可以获取点击的是键盘某个键的各种信息

![image.png](/assets/c8e4b825-6c8b-426f-98c7-ee21fbeab66d.png)

### 事件流

1.**事件流捕获**：这个捕获是页面组件层叠时候的说法，例如div叠了好多层

* 显示的时候，顶层肯定是子组件，最底层是document。
* 点击的时候从顶层捕获到三层，依次是子div，……,到底部document。
* 然后需要在添加事件对象的时候，将第三个参数设置为true，标识**捕获状态**，![image.png](/assets/0eff4c74-cb17-4c5b-be90-a1ccf61dad52.png)
*

2.**事件冒泡**，就是在上面的事件对象中的第二个参数设施事件响应内容function

* 这几个事件必须是同一种类型的事件

3.**事件委托**：就是获取父元素，给父元素加事件，点击子元素后，响应的是父元素。

* ul中有多个li，点击li后就可以操作这个li

![image.png](/assets/e0968fb2-dff2-41e1-8185-1cf75b55a7d6.png)

![image.png](/assets/452835da-6a1d-4399-913e-f18f0701ec64.png)

4.**页面加载事件**：load

* 当这个函数中有别的参数和动作，需要让函数中的资源都加载好后才能执行。
* 这个时候就需要用到**加载事件**

![image.png](/assets/ea519a43-ee30-4d60-92db-53cb7398b926.png)

5.**页面滚动事件**：scroll

* **scrollTop**：被卷去的头部的距离
* **可以设置起始页面位置**：开始的时候就是显示设定的滚动位置
* **可以设置滚动事件**：滚动到某个位置就显示某些组件

6.**像素事件**：

* 可以直接获取页面宽度，高度**clientWidth，clientHeight**
* 可以获取元素自身宽度，高度**offsetWidth，offsetHeight**

7.**获取到大盒子的顶部距离**：用**offsetTop**

8.**设定跳转的顶部距离位置**：先获取想要的top距离

* 用offsetTop获取这个盒子的距离
* 用scrollTop设定跳转距离

![image.png](/assets/8d1334ec-7cca-4caf-9d2b-1d6a3640c1bf.png)

### 将日期写道div中

* 自己添间隔函数，触发事件更新

![image.png](/assets/eaeceda2-f160-4fcf-baf8-72158f841a20.png)

### dom节点查找

在div中，一般获取这个div类的对象后，获取的是当前这个等级的div对象，

* 获取**父级**（高一级外围div）:**parentNode**
* **可以实现点击X，关闭这个盒子的操作**：子div影响父级div

![image.png](/assets/cc9802bc-1dbe-4918-90aa-3e951a61862f.png)

* **也可以获取子级节点**：**children**
* **也可以获取兄弟结点**：previousElementSibling，nextElementSibling

### 创造节点

不用手写出<div

* **创建ul等标签**：createElement
* **插入元素到某个位置**：insertBefore

### 克隆，删除节点

1.**克隆节点**

关键字：**cloneNode（true）**

* 克隆修改不会影响原来的节点

2.**删除节点**

关键字：**AAA.removeChild（BBB）**

* 需要通过父组件AAA，来删除BBB

### M端事件

就是移动端事件，例如触屏事件

* **touchstart**：开始触摸
* **touchmove**：正在触摸
* **touchend**：触摸结束

### 表单验证

![image.png](/assets/6511dd64-d2eb-420d-baf2-3902ade06622.png)

# BOM

浏览器对象模型，它属于window对象，

* window是最大的，其次是document

下面展开window对象的**常见属性**，BOM对象的**基本功能**讲解

1.**window对象**：

* BOM
* 定时器
* js执行机制
* location对象
* navigator对象
* histroy对象

2.**BOM**：

BOM包含DOM

![image.png](/assets/d94e3b30-c6b1-4a8e-a25e-2e80077e58c3.png)

3.**所有var定义的全局变量都会变成window对象的属性和方法**

### 定时器

他就是一个延时函数,只会执行一次

1.**设置延时**：setTimeout

2.**清除延时**：clearTime

### js执行机制

1.js是为了处理页面交互，操作DOM而生的。

2.js是单线程的，同一个时间只能做一件事情。

3.**执行栈**是主执行路线

**同步**：

* 前一个任务结束后，再执行后一个任务
* 执行顺序和任务排列顺序是一致的

**异步**：

* **异步任务**是耗时的
* 处理完这个任务后，这个任务执行
* 异步任务是放到**任务队列**中的

**异步任务的执行时机**：

* 含有异步任务的代码会有，一个栈，一个队列
* **执行栈**：存放非异步任务
* **任务队列**：存放异步任务
* 上面是按照顺序次序将，同步任务，异步任务放到栈和队列
* **当执行栈中的同步任务执行完后**，开始**将任务队列的任务放到栈中**
* **执行异步任务**

4.**js执行实际情况**

* js会将异步任务推给**浏览器**，浏览器可以执行异步任务（定时任务的耗时操作，到时间放到异步队列）
* 执行后放到**异步队列**，
* **执行栈执行完后，再一个一个取异步队列的任务执行**

![image.png](/assets/b8d6625c-75a2-47c4-9d49-edaa9cc7af97.png)

### location对象

1.**可以实现url直接跳转**：location.hrl("")

2.**可以实现页面刷新**：location.reload(true)强 制刷新

3.**可以获取url的内容**：location.AAA

* href：完整的
* search:获取？后的参数
* hash:获取地址中#后的部分

### navigation对象

1.**可以获取浏览器的版本及平台**:这个直接用现成的代码即可

### history对象

2.**查找历史。回到上一个页面，前进一个页面**

![image.png](/assets/964d795c-4570-4f0f-bd69-b69fcef701a0.png)

### localStorage本地存储和sessionStorage

**语法**:

1.**localStorage存储**:localStorage.setItem(key,value)

2.**sessionStorage存储**:

**存储规则**

1.sessionStorage生命周期为关闭浏览器窗口

1.localStorage可以永久存储在本地,除非手动删除,否则关闭页面也会存在

2.在同一个窗口下数据可以共享

3.以键值对的形式存储使用

4.sessionStorage用法和localStorage相同

5.本地存储只能存字符串数据类型json

#### 操作

1.**localStorage增删查**

* setItem
* removeItem
* getItem

#### 复杂数据结构的存储

例如用json存储的数据.

![image.png](/assets/2bcfe32f-fb56-4a44-9293-53a1f1989b76.png)

获取字符串类型的数据,转换为对象

![image.png](/assets/cda91073-e105-4cbd-8df2-d123ab5ddb56.png)

### 正则表达式

1.**测试时候匹配**:console.log(reg.test(str))




## 作用域链

1.**底层的变量查找机制**

* 优先查找当前作用域的变量
* 查找不到就去**父级作用域**，一个一个找，直到全局作用域
* **作用域链**：从子作用域**串联到**全局作用域
* 父级作用域无法查找到**子作用域**

## 垃圾回收机制

内存在不适用的时候会被**垃圾回收器**自动回收，也就是**内存的生命周期**

* 内存分配
* 内存使用
* 内存回收：这个由**垃圾回收器**自动回收

一般来说**全局变量的值**不会被回收，

**局部变量**不用了，就会被**自动回收**掉

1.**内存泄漏**：程序中分配的内存由于某种原因，程序**未被释放 **，或者**无法释放**

2.**栈**：这个由系统自动分配和释放，存放参数值，局部变量等

3.**堆**：一般由程序员分配，程序员不释放，就由**垃圾回收机制回收**，**复杂数据类型**放到堆里面


#### 引用计数法

这个是IE浏览器用的回收机制算法

1.**扫描记录的引用数量**：

* 被引用一次就++
* 减少一次就--
* 到0就释放

2.**嵌套引用（循环引用）**：这个是**引用计数法**的一个缺陷

如果互相引用的话，对导致两个对象都没办法回收

3.**释放方法**：他会从某个点开始查找，向被引用的点移动。如果查找不到就要回收

#### 闭包
