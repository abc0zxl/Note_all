# 注意

1.函数没有return会返回undefine

2.**遍历方法**：for in语法

![image.png](/assets/cc2cbe32-10d1-4d55-a1d4-c4590aa10db0.png)

3.**null**：他是**空对象**

4.**变量声明**：尽量用const，对象插入const不报错，但是将一个新的对象赋值给const变量，**会导致地址改变**，报错。

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

使用js操作html和浏览器


# DOM

文档对象模型



# BOM

浏览器对象模型
