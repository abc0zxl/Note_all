## 注意事项

 1. stirng的s要大写
 2. 公共类里面修改属性值的构造方法的方法名字必须和包名字
 3. 外部类的写法和重新写一个java结构差不多，除了主方法有异同，别的都一样。
 4. 每个java文件编译时都会生成至少一个class文件，
 5. java文件，一个文件中只能有一个public类
 6. 文件名必须和public名字相同
 7. 类中，方法内调用属性值，需要用this.

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

## 封装
#### getter和setter

**功能**:修改私有属性
**意义**：**遵循java封装的规范**编程软件能快速生成这两个类，不用手打
**vscode**中右键**源代码操作**，选择操作，就可以立马生成出来

#### java结构名词
**构造方法**：他的名称必须和公共类名（java文件名）必须一样，用于修改属性
**普通方法**：和公共类名字不一样，是一种定义的方法，他的作用是使用属性值，而不会修改
**final**:限制变量，方法，类的。

 1. 变量：不可变
 2. 类：不可被继承
 3. 方法：不可重写
**static**：影响调用范围，可以用类名直接调用，主类中也可以。
 4. 属性：这个属性所有对象可以共享
 5. 方法：不用new就可以访问
 6. 代码：类加载时就执行

## 继承
**extends**构造方法、private、final、静态成员、父类的包资源，不可以继承

 1. 可以直接使用父类中的方法。 
 2. 但增强了类之间的耦合性。 
 3. 提高代码的维护性，复用性。
 4. 继承所用的属性，最深可以用到父类的属性（非私有的），也可以重复定义同名属性，会使用最近的一个属性
 5. 可以纵向多继承（嵌套继承）
 6. 不可以支持横向的继承（比如 class C extends A, B 是错误）

**this**:引用本文件中公共类空间中的属性的一个标识
**super**：调用父公共类空间中的属性的标识

 1. **super.xxx**:调用父类公共类中的属性
 2. **super(xxx)**:调用父类中带参的构造方法
 3. **super.xxxx(xxxx)**:调用父类中的普通

**注意**：因为子类的构造方法的**第一条语句默认是super()**（这是因为子类时父类的继承），所以父类中的构造方法最先完成初始化。
 1. **子类继承了父类的属性和方法，必须先让父类完成自身的初始化，子类才能正常使用继承来的资源**
 2.  无论主类中的对象是带参的还是不带参的都会先让父类的构造方法先运行
 3. 如果子类中没有定义构造方法则会，自动给子类造一个，但是这个构造方法只有一个默认的super，向父类调用，以此类推。
**显式调用：**有实际手打的代码运行（有定义构造方法）
**隐式调用：**没有实际代码，但是会通过默认的操作，加上这个代码去运行（没有定义子类构造方法，会自动加上，以及super父类构造方法）
 4. **注意上述说的是构造方法，非普通方法**

对象.xxx:他会先在子类中找，然后再去父类中找这个方法，如果没有就报错。
如果子类中有和父类同名的普通方法，则需要干预（也就是重写），如果不干预的话就会只调用子类中的，父类的就不会调用，可以用super显示调用父类中的同名方法。
![输入图片说明](/imgs/2025-11-25/gb5wcNTPpQfRcjtR.png)
这种操作相当于**方法重写**，主要看super的位置在哪
## 多态
#### 重载
指同一个类中的，两个名子相同的方法，但是参数不一样。
#### 重写
若子类中的方法与父类中的某一方法具有相同的方法名、返回类型和参数表，则新方法将覆盖原有的方法
**@override**:是一个标注，表示这个是子类重写父类的方法。
**vs快捷键**：alt+windows+n选择父类的方法，自动生成。

 1. 重写的方法，方法名，括号中的参数必须和父类中的某个方法一样，否则为子类的新方法。
 2. 子类的报错标准不能比父类还宽泛，只能一样或者说更少。
 3. 子类的返回类型必须相同，名字可以是继承父类的返回类型的新名字（**协变返回类型**），但不可以是别的返回类型。
 4. 子类的重写，他的访问级别只能相同或者更低。
## 抽象
**抽象类**也就是**模版类**
 1. 抽象类，按照如下定义
 public abstract class Animal
 {
 public abstract void eat();
 }
 2. 抽象类中的**抽象方法**，只有方法名和一个分号，没有方法体；（注意抽象方法和普通方法，后者可以有方法体）
 3. 如果这个类的方法里有抽象方法，则该类一定是一个抽象类
 4. 抽象类中可以有非抽象方法。
 5. 抽象方法的具体内容，由非抽象子类定义，具体实现被延迟到子类中实现。
 6. 如果非抽象类继承了抽象类，则必须重写所有**抽象方法**（非普通方法），或者作为抽象子类。
 7. 抽象类中的abstract方法，不可被实例化。


## 接口

 1. 弥补了抽象类不可以继承多个类的缺陷
      ```
```java
public class UnionPay implements Payable, Pointable {
    private String bankCardNo; // 银行卡号
```
 3. 继承的多个类可以没有任何关系
 4. 接口不能有普通变量，只能有静态变量，不用写类型的权限，自动补为public static final xxxx，只能是这个，且必须初始化。
 5. 接口里面的抽象方法可以不用谢abstract，编译器会自动补齐。
 6. 默认方法：子类可以直接继承或者重写，可以调用接口中的静态方法，或者抽象方法。
 7. 静态方法：只能通过接口名加方法名，不可被重写。
 8. 私有方法：作为类中的公共方法的复用逻辑，只能在这个接口中调用
 9. 静态私有方法：用与静态方法的复用逻辑。
 10. 所有方法都是抽象的
 11. 接口中default的方法，子类可以直接调用其方法，不用加前缀名字
 12. static方法，子类调用时需要用到接口名字加方法名，调用其方法。
  
 ```
```java
public interface Payable {
    // 1. 接口的属性：只能是 public static final 静态常量（关键字可省略，编译器自动补全）
    // 必须初始化，属于接口本身，通过“接口名.属性名”访问
    String PAY_VERSION = "V2.0"; // 支付接口版本（等价于 public static final String PAY_VERSION = "V2.0"）
    BigDecimal MAX_PAY_AMOUNT = new BigDecimal("100000"); // 最大支付金额（10万元）

    // 2. 抽象方法：无方法体，默认 public abstract（关键字可省略）
    // 作用：强制实现类必须提供具体实现（核心规范）
    boolean pay(BigDecimal amount, String password); // 支付（金额+支付密码）
    void refund(String orderId); // 退款（订单号）

    // 3. 默认方法（Java 8+）：default 修饰，有方法体
    // 作用：提供默认实现，子类可直接继承或重写（解决接口扩展不破坏原有实现类的问题）
    default String getPayDesc() {
        // 可调用接口的静态方法或抽象方法（抽象方法由实现类提供具体逻辑）
        return "使用" + PAY_VERSION + "版本支付，最大支持" + MAX_PAY_AMOUNT + "元";
    }

    // 4. 静态方法（Java 8+）：static 修饰，有方法体
    // 作用：属于接口的工具方法，只能通过“接口名.方法名”调用，不能被子类重写
    static boolean validateAmount(BigDecimal amount) {
        // 校验支付金额合法性（大于0，小于等于最大支付金额）
        return amount.compareTo(BigDecimal.ZERO) > 0 
                && amount.compareTo(MAX_PAY_AMOUNT) <= 0;
    }

    // 5. 私有方法（Java 9+）：private 修饰，有方法体
    // 作用：抽取接口内部复用逻辑（默认方法/静态方法可调用，外部不可见）
    private String encryptPassword(String password) {
        // 模拟密码加密（实际开发中用MD5/SHA等算法）
        return password + "_encrypted";
    }

    // 6. 私有静态方法（Java 9+）：private static 修饰，有方法体
    // 作用：接口静态方法的内部复用逻辑
    private static String generateOrderNo() {
        // 模拟生成唯一订单号（实际开发中用UUID+时间戳）
        return "ORDER_" + System.currentTimeMillis();
    }
}
```
```

## java内置类和库
**内置类：**不用各种导入的，约有150-200个。
**核心库**：java只有java.lang 对应的基础库，可以免import，别的都得用import导入，内置有150多个可直接用的类，接口等。

 1. **String**
 2. **Math**
 3. 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwNjQ4NzExOTUsNjA4ODQwNDYyLDE1Mj
UxNTQ1MTQsLTE2MzA1OTYwMjUsLTg3OTY0MjAwMF19
-->