# MyBatis

mybatis是一款优秀的**持久化层**框架

1.他支持自定义的SQL

2.存储过程

3.自定义SQL

4.可以**免除**所有的数据库代码、参数设置、数据封装

## 痛点

1.**硬连接**:原JDBC连接方法，  需要在CRUD的文件中配置繁琐的连接配置，也叫**硬链接**

虽然他也有.propertise编写集中的账号密码，但是每次修改还是要重启项目，

2.**手动录入参数**：原JDBC给sql设置参数需要手动一个一个写

3.**封装结果集**：还需要一个一个部分的封装到数组对象容器中

4.**重复性操作**：每个功能的CRUD操作的sql语句，虽然一样但是都要编写

### **注意**：

1.mybatis的xml中的config配置代码，他的标签是有顺序的

### 用法

```
1.引入依赖：放入到pom.xml中（非config）
```

mybatis的依赖

mysql的依赖

junit测试依赖

……这些可以放在一个文件中，要用的时候一起粘贴

```
2.将mybatis的对象引入代码中，从xml中获取配置，
```

![image.png](/assets/7437cbf7-cd76-44d7-bba8-efcb676ae6ee.png)

```
3.创建会话，SqlSession sqlse=sqlSessionFactory.openSession();
```

```
4.连接接口，这个接口usermapper是连接的数据库的一个表
```

User Mapper map=sqlSession

```
5.连接数据库的配置，写到mybatis-config.xml的文件中,这个也可以写到自己的文件中，要用的时候直接拿
```

![image.png](/assets/8b6cd730-879c-45dd-96a2-78ae1e098c1d.png)

### 数据库访问接口编写

1.**编写方法**：一个接口，里面定义方法名字

2.**编写sql语句**：在GoodsMapper.xml中设置这个名字的数据库语句

**是 “接口类名” 和 XML 文件名一致，且有更严格的约束**

3.**连接**：告知mybatis-config.xml，我的数据库语句的xml，**这一步，只用设置一次**，这样就实现了数据库的连接。

![image.png](/assets/1f98c280-4d51-48f9-adfd-1aa178153e0c.png)

![image.png](/assets/64da7a5a-4117-4406-990b-bb5ea56bb158.png)

4.**映射**：将mybatis的配置xml，**加载上**数据库操作的xml文件**映射**

5.**编写POJO类，也叫实体类**：将操作功能，例如对User表的操作，就写一个User.java，包含对应的操作属性。

### 调用执行

接下来可以按照上面的方法，实现各种sql操作，且不用重写多个sql代码，调用一个mapper中的sql方法就可以实现数据库操作。

1.**获取SqlSessionFactory对象**：

他的实例可以通过SqlSessionFactoryBuilder获取，

先获取一个字节流，再获取……factory对象

固定输入

![image.png](/assets/43088218-68a2-47fc-bd6c-70ce6b598a03.png)

2.**获取sqlsession对象**

用openSession()获取

3.用带有sql语句的xml中的唯一**id**，给这个对象，然后执行sql语句

4.关闭sqlsession对象。

## Mapper代理开发

**痛点**：

1.在获取sqlsession对象后执行sql的xml时，用的还是**硬编码**，要来回看id是啥

**解决**：

1.通过获取好的sqlSession对象，利用他的方法getMapper

2.通过idea的提示，就能获取代理对象

3.再利用这个对象，配合上**代码补全功能**就能得到这个sql语句xml的id，然后自动执行sql

### 步骤

1.sql映射文件要有一个同名的Mapper接口

2.这个sql映射文件和mapper接口放在同一个目录下.目的是方便mapper扫描sql映射文件。

```
并不是非要直观上的同一个文件，也可以在别的地方建立一个文件链接，如图所示。
```

				**A**.这种有两种方法，一种是直接引入明确的xml路径，进行加载，这种要写好多个
**B**.用**包扫描**的方式只用写一个，简化mapper对sql映射文件的扫描

```
<package name="com.itheima.mapper >
```
![image.png](/assets/bf908add-4fe7-4af7-a346-33030571cb86.png)

3.Mapper的方法就是sql映射文件中的sql语句的id，还要保持返回值的类型一致。

### 注意

1.sql映射文件中的namespace不再是原来的随随便便的名字了

由于原来不用mapper的时候是通过sql映射文件的唯一id来调用的sql，现在用的mapper接口的方法，要给对应的mapper代理文件和sql映射文件放在同一目录下，mapper代理文件好直接调用这个sql映射文件，所以他的**id**必须等于**对应mapper代理接口的文件相对路径**

这个路径是直观的说法，它实际上叫做**全限定类名**

2.**SQL 标签的 id 必须等于 Mapper 接口的方法名**

## Mybatis配置

1.**多个数据库**：可以写多个environment，也就是说可以链接多个数据库，通过不同的defult属性（辨识数据库的唯一id）来切换environment

2.**简化sql映射文件**：sql中的resultType原来要写一长串（返回实例文件的相对路径），可以用一个自定义别名来简化，之后不用区分大小写，直接写返回类型。

**自定义别名**

目的是解决resultType书写麻烦的问题，

用TypeAliases起一个别名（这个必须写在environment上面，configuration下面）

![image.png](/assets/2e2e672c-dae8-45b3-9ee4-239efe3afdc0.png)
