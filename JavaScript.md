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

## 箭头函数

const getData=()=>{    }

1.**const getData**：表示声明一个名字叫做getData的常量，用来存储后面的函数

2.**（）=>**：这个是放参数的地方

3.**{}**：这个是放函数体的地方

## 扩展运算符

**作用**：展开所有属性

1.**保证options完整性**：如果{}只放一个属性的话，原来的属性都会消失

* 展开原来options.header中所有属性，
* 再加上这个新加的
* 就保证了完整性

![image.png](/assets/65d4d630-df76-4e61-8a89-8c0579b0ff28.png)
