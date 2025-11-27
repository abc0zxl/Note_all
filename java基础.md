## 注意事项

1. stirng的s要大写
2. 公共类里面修改属性值的构造方法的方法名字必须和包名字
3. 外部类的写法和重新写一个java结构差不多，除了主方法有异同，别的都一样。
4. 每个java文件编译时都会生成至少一个class文件，
5. java文件，一个文件中只能有一个public类
6. 文件名必须和public名字相同
7. 类中，方法内调用属性值，需要用this.
8. java设置日期时要用完整的位数比如01,02,03
9. java文件的命名也不能用关键字，而且要注意大小写
10. 找不到包的时候直接*
11. 以后用英文代替中文，因为java要报错
12. 调用接口interface需要用implements
13. jvm是java的核心运行载体，没有jvm，java字节码就是一个纯文本文件，无法执行。
14. java默认导入lang包，不用手动导入
15. 对象的括号，叫做**构造方法调用符**，也叫**实例化括号**
16. 一个类既可以使用多个接口又可以使用一个继class ChildClass extends ParentClass implements InterfaceA, InterfaceB
17. f


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
2. 无论主类中的对象是带参的还是不带参的都会先让父类的构造方法先运行
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

## java内置类和库

**内置类：**不用各种导入的，约有150-200个。
**核心库**：java只有java.lang 对应的基础库，可以免import，别的都得用import导入，内置有150多个可直接用的类，接口等。

1. **String**
2. **Math**

**集合框架：**

1. **List**：存储顺序就是存入的顺序，可重复，需要ArrayList和List包，
   初始化：List<Integer> list_name=new ArrayList<Integer>();
   插入：list.add(xx);
   修改：list_name.set(int place,int num);
   查找：int_name.indexOf(xx);返回位置
2. **Set**：不允许重复元素
   初始化：Set<Integer> list_name=new HashSet<>();
   长度：list_name.size();
3. **Map**

### **List 子类**

#### ArrayList

存储的是Object数组、

1. **优点**:查找快，遍历数据快
2. **缺点**：移动元素，修改效率慢

#### LinkedList

3. **优点**：便于添加，删除和定点修改删除
4. **缺点**：查找慢，因为底层用的**二分法**

### **Set子类**

#### HashSet

不允许重复元素，元素没有顺序

#### TreeSet

不允许重复元素，元素有顺序，基于**红黑树**实现

### Map子类

#### HashMap

按照输入的键值对的顺序存储没有顺序
例如：Map<String,Integer> map_name=new HashMap<>();

#### TreeMap

按顺序存储，存到红黑树中，两种情况
**默认顺序**:数字，字符，日期（从小到大）
**自定义顺序**:（在初始化对象时，在后面的括号中输入标准，例如：((k1,k2)->k2-k1）
例如：TreeMap<Integer,Integer> Tress_name=new TreeMap<>((k1,k2)->k2-k1);

### java时间

#### 获取时间

1. **输出现在时间**
   LocalDateTime A=LocalDateTime()；
   当前以毫秒为单位的时间
   System.currentTimeMillis();
2. **给变量设置指定时间** LocalDate B=LocalDate.of(XXXX,XX,XX);
3. **时间变量修改添加时间** LocalDate C=B.plusDays(1);在原来的时间基础上加一天，加什么可以有plus设置。例如plusDays,plusHours……
4. **取一个月的最后一天** LocalDate last_of_month=today.with(TemporalAdjusters.lastDayOfMonth());
5. **取一年的 第一个星期的星期一** LocalDate first_week=LocalDate.parse("2025-2-1").with(TemporalAdjusters.firstInMonth(DayOfWeek.Monday))

#### **设置时间，时间对象**

1. 通过时间戳创建
   用于将不同单位的时间转化为别的规格（ofErop……）
2. 通过Date对象创建
3. 通过解析字符串创建
4. 设置时区，时区转换
5. 规格化时间（DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");）
   自定义一个时间规格，然后，手动输入，让电脑识别，录入对象中

#### 时间的计算

**时差计算（Period）**
创建：Period p=Period.between(A,B);

## IO流

### 字节流

**创建文件流程**

1. 设置路径
2. 创建文件对象
3. 判断创建文件的父目录是否存在，不存在则创建
4. 创建
   输入对象：Scanner
   输出对象：OutputStream
   键盘写入对象：InputStream
5. 可以向文件中写入数据
6. 指定一个编码方式
7. 吧键盘写入对象的数据写入到文件中·
8. 输出文件内容
   10.判断是否有错误
   catch(IOException e){
   System.err.println("err information is:"+e.getMessage());
   这段告诉了“为什么错”
   e.printStackTrace();
   这段告诉了“错在哪里”

**注意**：

1. 创建文件的文件名字是和路径一同给出的。
2. file.createNewFile();和OutputStream outputStream = new FileOutputStream(file);都可以创建出来一个文件，前者是专门创建文件，后者是为了写入数据而创建。
3. while ((content = fis.read()) != -1) { fos.write(content); }是读一个字节写一个字节。而不是字符。
4. 用字节流写入完后，要强制刷入数据write_name.flush();

### 字符流

**字符设置**
字符流是由java的虚拟机将**字节**转换得到的
因为有很多不同的字符标准，很容易乱码，所以直接提供了个操作字符的接口（Standard Charsets）
**Reader**
**Write**

### 节点流

就是从一个特定的数据源，使用不同的节点流读取数据，写入，但不支持修改和删除数据源。

1. FileInputStream
   他读取的文件应该是FIle nameF=new File（“XXX”）
   赋给Stream
   FileInputStream name=new FIleInputStream(nameF)
   写入完后要关闭write_name.close();
2. FileOutputStream
3. ByteArrayInputStream
4. ByteArrayOutputStream

### 处理流

连接在已存在的流之上，为程序提供强大的读写能力。

### 缓冲流

通过将数据缓存到一个区域，然后一次性读取或者写入多个字节，避免频繁的IO操作，从而提高流的传输效率。
**装饰器**：例如BufferedInputStream
可以用来增强普通的io功能
BufferedInputStream buf=new BufferedInputStream(new FileInputStream("input.txt"))

**Input**：是指从**外存**读取到**内存**
**output**：是从**内存**写入到**外存**
利用缓冲流会大大节省时间。
100页pdf
[图片上传中...(image-fOoV6CZupv7kM2Mi)][图片上传中...(image-MDQ4wUcTkcleL4hR)]![](https://p11-flow-imagex-download-sign.byteimg.com/tos-cn-i-a9rns2rl98/5d24850d07d44e4b977cda22f2d8b080.png~tplv-a9rns2rl98-24-95-exif:960:960.png?rcl=20251126201235FE3E9102B92FFDC1EE9E&rk3s=8e244e95&rrcfp=8a172a1a&x-expires=1764763955&x-signature=rPZXVTF8RFxpve0Awyapjer3N0k%3D)

**字符缓冲流**
BufferedReader
BufferedWriter
相比于之前的这个主要用来操作字符，之前的bufferedStream是字节

### 对象处理流

**序列化**:将数据的值和数据的数据类型同时存入到文件中（Output）
**反序列化**：读取文件中的数据和数据类型，恢复到原来的样子。
**关键字**：OjectOutputStream和OjectOutputStream

### 转换流

可以将字节流转换成字符流
可以指定读取文件时按照什么样的编码
**关键字**：InputStreamReader和OutputStreamWriter

例子：创建一个缓冲流的读取对象
他有两个内容，文件，读取格式。
InputStreamReader inputStreamReader = new InputStreamReader(new FileInputStream("D:\\JAVA\\IDEA\\file\\3.txt"), UTF_8);

他的缓冲读取关键字是
BufferedReader
写入的时候不需要这个
**buffer关键字区别**
BufferedInputStream:字节缓冲流，读取单位为字节

1. 可以处理所有类型文件
2. 但是处理中文容易乱码
   Bufferedread:字符缓冲流，读取单位为字符
3. 专门处理文本文件
4. 因为可以设置读取编码类型
5. 但是无法处理二进制文件

## 异常处理

try{}
catch(ExceptionType name){}
finally{}
**try-catch**:
**finally**无论是否发生异常都会处理
**自定义异常**:用java文件继承Exception，然后就可以把这个文件当作异常标准。**要用if**

## 多线程

1.一个java程序中至少有两个线程（垃圾回收，main方法）
2.线程之间的堆内存是共享的，但是栈不共享

**主线程**：main
**锁池**：可以理解为一种阻塞

### 线程的实现

#### **第一种方法**

1.重写java.lang.Thread中的run方法，
2.new（创建）一个线程用start()启动
3.创建的线程可以直接调用他的方法，让他运行，但这种还是单线程顺序执行，还是在主线程中
4.用**start()**创建线程，不用调用他的方法名字就能运行，这个是因为**JVM的机制**。
5.多线程能很大程度上节省时间。

#### 第二种

1.重写java.long.Runnable的**接口**，实现run，

2.也是用start（）启动

3.这种方法创建线，需要在对象创建时写入实例化的线程接口

Tread t=new Tread(new runable_name());

4.他是一个接口所以使用他的类还可以继承别的类

5.是一种常用的方法

#### 获取线程姓名

1.获取当前线程对象

2，获取线程名字

3。修改线程对象名字

#### 线程的阻塞

可以让这个线程暂停，让出cpu

1。唤醒进程

void interrupt()

2。阻塞->唤醒：实现了线程的暂停，资源的转让，定时唤醒


#### 线程的终止

##### 方法一

直接终止。

t.stop();

##### 方法二

合理终止

t.run=flase;

if(run)

在重写接口的地方写一个循环，用于检测标记是否标记为退出，然后用return终止这个进程

### 线程的调度

1。抢占式

2。非抢占式
