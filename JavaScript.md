# 注意

1.函数没有return会返回undefine

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


2，**事件冒泡**，就是在上面的事件对象中的第二个参数设施事件响应内容function

* 这几个事件必须是同一种类型的事件

# BOM

浏览器对象模型

![image.png](/assets/451be1de-8995-46bc-9fe3-76d8a4cde596.png)
