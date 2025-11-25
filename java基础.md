## 注意事项

 1. stirng的s要大写
 2. 公共类里面修改属性值的构造方法的方法名字必须和包名字
 3. 外部类的写法和重新写一个java结构差不多，除了主方法有异同，别的都一样。
 4. 每个java文件编译时都会生成至少一个class文件，

package com.example.demo;
import java.util.Date;
import java.util.*;
public class hello{
private string name;
private int age;
static string text;
public func1()
{
this.text="record student information";
}

public func2(string name,int age)
{
this.name=name;
this.age=age;
}
public void func3()
{
System.out.println("name is:"+name+",age is:"+age);
}
public static void main(string[] args)
{
hello.func1();
func2 A=new func2("小白"，21);
A.fun3();
}
}
class out_func{
public void printfunc(){
System.out.println("这是辅助类");
}

**1.文件注释**用于说明该文件的作用

**2.包声明**（可以不写）：防止类名冲突

**3.调用外部包**：用于调用外部的包，或者调用功能包
**4.公共类**：用于定义外部可以访问的类，这个类名必须与该**java文件**的名字相同
**5.类注释**：用于说明该公共类的内容
**6.类成员**：用于存储类的数据，公共类被调用时可以修改公共类的成员
**7.构造方法**：定义，创造功能（在没有修改类成员时，要标注出来void，还有void的种类）他们的名字必须和公共类名字一样
**8.主方法**：程序运行的入口
|**无参数构造方法**|**含参数构造方法**|
|-主方法可以直接调用-|-主方法要new对象来调用-|
**9.非公共类**：不在公共类中，外部不能调用，仅仅该文件内可以调用


## getter和setter

**功能**:修改私有属性
**意义**：**遵循java封装的规范**编程软件能快速生成这两个类，不用手打
**vscode**中右键**源代码操作**，选择操作，就可以立马生成出来

## java结构名词
**构造方法**：他的名称必须和公共类名（java文件名）必须一样，用于修改属性
**普通方法**：和公共类名字不一样，是一种定义的方法，他的作用是使用属性值，而不会修改

## 继承
**extends**构造方法、private、final、静态成员、父类的包资源，不可以继承
可以直接使用父类中的方法。
但增强了类之间的耦合性。
提高代码的维护性，复用性。
继承所用的属性，最深可以用到父类的属性（非私有的），也可以重复定义同名属性，会使用最近的一个属性
**this**:引用本文件中公共类空间中的属性的一个标识
**super**：调用父公共类空间中的属性的标识

 1. **super.xxx**:调用父类公共类中的属性
 2. **super(xxx)**:调用父类中带参的构造方法
 3. **super.xxxx(xxxx)**:调用父类中的普通

**注意**：因为子类的构造方法的**第一条语句默认是super()**，所以父类中的属性最好要先完成初始化。
 1. 每当主类中new好一个对象时，如果对象中没有数据，则默认调用子类的无参构造方法，并且逐级调用下去。如果父类中没有无参的构造方法，则不会调用。
 2. 如果是有数据的则调用含参的构造方法，也会调用父类中的带参构造方法。

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwNDgwMDA4MDddfQ==
-->