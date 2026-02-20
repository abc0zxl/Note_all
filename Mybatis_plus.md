# 错误

1.数据库某些字段不能当名字：**toString**，他会被mybatis-plus 解析错误

# 注解

1.**@TableName（value="AAA", autoResultMap=true）**：

**作用**：这个是mybatis-plus的一个注解，用于连接表，AAA，后面的参数是关于映射值。

**位置**：entity的类上面

2.**@TableId（type= IdType.AUTO）**：

**作用**：在实体类中说明好了表中各个属性后，表中的主键需要在上面写上这个注解。

**位置**：在主键属性上面

3.**@AllArgsConstructor**

**作用**：帮我们写有参构造器

**位置**：在实体类的类名上面

4.**@NoArgsConstructor**

**作用**：帮我们写无参构造器

**位置**：在实体类的类名上面

5.**@EnumValue**

**作用**：Mybatis-plus专门给枚举类型准备的注解，解决枚举类型和数据库转换之间的问题

![image.png](/assets/dcd45deb-8371-4361-b496-e3f438c28119.png)

* 通过查看枚举类型的结构就知道，他是一对一对的
* 当调用他的LOCK值时，不知道调用哪个，所以要用注解**标记好对应顺序位置的值**

**位置**：在用于声明枚举值属性的**变量上面**

6.**@TableField（fill=FieldFill.INSERT_UPDATA）**

**作用**：为了插入的时候自动填充，同时也可以更新，但这个需要配合填充配置一起用。**这样mybatis-plus才知道要填充什么东西**

**位置**：在实体类属性上面

7.**@TableLogic(value="0",delval="2")**

**作用**：调用这个逻辑的时候这个属性会变为2，主要用于**逻辑删除**

**位置**：在逻辑删除属性的上面

8.**@DS("AAA")**

**作用**：配合全局配置中的多数据源配置，某个controller方法，选择用AAA作为这个方法中要用的数据库

**位置**：如果想让整个类默认用某个数据库的话是放在类上面，如果是某个controller方法或者service方法的话就是方法上面

![image.png](/assets/5e7ff2a8-1ad4-4e1f-9939-fb30b8ae2b96.png)


9.**@Version**

**作用**：乐观锁版本号标识注解，因为乐观锁需要一个变量来记录这个版本号

**位置**：在变量上面

# Mybatis_plus

1.**Mybatis**：是半自动的ORM框架

* 需要自己手写大量的SQL代码

2.**Mybatis-plus**：是MyBatis的增强工具

* 不用写重复的CRUD SQL，大大提升开发效率

3.**条件查询**：

* **mybatis**：要哦用where标签，拼接容易出错
* **mybatis-plus**：提供了多种方法，用链式调用拼接条件，**避免了SQL注入**
* **mp**：自带**内置分页插件**，调用方法自动分页，**而mb需要自己写分页逻辑**
* **mp**：内置多种主键策略

4.**不用手写sql**：

* 它内置了很多基本的java方法，实现原来的sql
* 如：selectById(id)
* **动态条件查询**：也有等价替换原来的**where标签**

![image.png](/assets/2bcc2d86-65a2-43a2-892b-14d90ac85ece.png)

## 分页实现

1.**创建分页对象**：

2.**写条件**：

3.**调用分页方法**：

4.**返回分页结果**：总条数，总页数，当前页数据

# MyBatis-Plus

为了简化开发，提高效率而生，

1.**无侵入**：

2.**损耗小**：

3.**内置代码生成器**：

4.**内置分页插件**：

5.**支持Lambda**

## 实现步骤

1.**创建项目**

* 创建那个spring initializr
* 选择maven
* 选择依赖：Lombok（用于给实体添加get，set），springweb，mybatis framework（在sql中），mysql driver

1.**添加依赖**：

* mybatis-plus包（**最关键**）

![image.png](/assets/3070736a-3c71-47c9-8e32-39f4dc086b07.png)

* **排除包（排除掉原来的mybatis）**
* ![image.png](/assets/dcaca007-472a-47ea-9abc-ed2fa21bb33d.png)
* 分页插件包（后面的4.9去掉就不报错了）

![image.png](/assets/783243bd-b5e0-4d8a-a8d8-6a65ff235d62.png)

* 辅助工具包

![image.png](/assets/bd79f367-c828-4e47-b2f4-abf0883fa008.png)

* 其他包

![image.png](/assets/11d17b40-73fd-49c5-8d2a-0ea23f82198e.png)

## 一个字母都不能错（固定搭配）

mybatis-plus和Springboot之间的版本要求非常高，及其难配置

```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <!-- Spring Boot 父依赖（3.2.5 稳定版，适配 JDK 17） -->
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>3.2.5</version>
        <relativePath/>
    </parent>

    <groupId>org.example</groupId>
    <artifactId>Mybatis-plus1</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>Mybatis-plus1</name>
    <description>Mybatis-plus1</description>

    <properties>
        <java.version>17</java.version>
    </properties>

    <dependencies>
        <!-- WebMVC 核心依赖（继承 parent 版本，无需手动指定） -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>

        <!-- MyBatis-Plus 核心依赖（3.5.5 适配 Spring Boot 3.2.5） -->
        <!-- 无需引入原生 MyBatis 启动器，MyBatis-Plus 已内置兼容版本 -->
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
            <version>3.0.3</version>
        </dependency>

        <!-- MySQL 驱动（运行时依赖，继承 parent 版本） -->
        <dependency>
            <groupId>com.mysql</groupId>
            <artifactId>mysql-connector-j</artifactId>
            <scope>runtime</scope>
        </dependency>

        <!-- Lombok（简化实体类，可选） -->
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>

        <!-- 测试核心依赖（替换错误的 webmvc-test，包含所有测试所需包） -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>

        <!-- MyBatis 测试支持（可选，如需 MyBatis 专属测试功能） -->
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter-test</artifactId>
            <version>3.0.3</version> <!-- 适配 Spring Boot 3.2.5 -->
            <scope>test</scope>
        </dependency>


        <dependency>
            <groupId>com.baomidou</groupId>
            <artifactId>mybatis-plus-boot-starter</artifactId>
            <version>3.5.5</version>
            <exclusions>
                <exclusion>
                    <groupId>org.mybatis</groupId>
                    <artifactId>mybatis-spring</artifactId>
                </exclusion>
            </exclusions>
        </dependency>

    </dependencies>

    <build>
        <plugins>
            <!-- 编译插件（Lombok 注解处理器配置） -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                    <source>17</source>
                    <target>17</target>
                    <annotationProcessorPaths>
                        <path>
                            <groupId>org.projectlombok</groupId>
                            <artifactId>lombok</artifactId>
                            <version>${lombok.version}</version> <!-- 继承 parent 版本 -->
                        </path>
                    </annotationProcessorPaths>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>

```

2.**配置mysql数据源**

配置模板

```
  datasource:
    url: jdbc:mysql://localhost:3306/up_door?useSSL=false&serverTimezone=UTC
    username: root
    password: 123456
    driver-class-name: com.mysql.cj.jdbc.Driver
  mybatis-plus:
    configuration:
      log-impl: org.apache.ibatis.logging.stdout.StdOutImpl

```

3.**创建mapper包**：

* 接口mapperAAA要继承BaseMapper<user

4.**配置springboot**：

* 在启动文件中加入注解@MapperScan("AAA")
* 其中AAA是到mapper包的绝对地址

5.**运行mybatis-plus的例子**：

* 直接不用写mapper的内容，继承baseMapper即可
* 创建mapper对象
* 调用mybatis-plus的方法
* 如：UserMapper.selectById(1001)

# MyBatis-Plus常用方法表

## BaseMapper的常用方法

他包含基本的sql方法，比较适合在controller层使用


|  |  |  |
| - | - | - |

1.**selectById**：

**作用**：根据ID查这个mapper对象下的表

**位置**：mapper对象的方法

2.**selectList**

**作用**：查询mapper对象表中所有

**位置**：他是mapper对象的方法，需要用list来承载

3.**setAAA**

**作用**：根据这个主键，更新对象里AAA这个值，setAAA就相当于get，set里的set方法

**位置**：单个行对象

# IService使用的方法

他比BaseMapper有更多的方法，比较适合在service层使用

**基本servic框架**：这个只用搭框架不用往里面写东西

* **Service接口**：service接口继承IService<T
* **Service实现类**：需要继承**ServiceImpl《UserMapper,User》**,再**实现**他对应的接口

![image.png](/assets/6a2a7e2f-342b-4fea-acbd-b038a68b197e.png)

## IService常用方法

1.**save**

**作用**：保存对象到service中对应的数据表中

**位置**：他是service对象的方法

![image.png](/assets/da79fcf9-251c-4565-a426-8ab3b05d4d31.png)

2.**saveBatch**

**作用**：批量保存，返回boolean值

**位置**：也是Service的方法

![image.png](/assets/770006c6-8bad-4aee-bf67-7d2bb1ebe5c7.png)

3.**saveOrUpdate（user）**

**作用**：会先查看这个存入对象user的ID，如果存在就更新，不存在就插入

**位置**：service的方法

4.**saveOrUpdateBatch（users）**

**作用**：和上面差不多，只不过他是批量保存

**位置**：service的方法

5.**removeById（id）**

**作用**：根据id删除

**位置**：service的方法

6.**removeByMap(map)**

**作用**：根据条件删除

**位置**：也是service的方法

7.**remove（wrapper）**

**作用**：根据条件构造器删除

**位置**：service的方法

8.**removeByIds（ids）**

**作用**：多个ID同时删除

**位置**：service的方法

9.**getById（id）**

**作用**：通过id获对象

**位置**：service的方法

10.**list()**

**作用**：批量获取数据

11.**listMap()**

**作用**：在条件下查询列表

12.**getOne（wrapper）**

**作用**：在构造器中获取一条数据

## 条件构造器

1.**QueryWrapper**：通过查询条件构造器

2.**UpdateWrapper**：更新操作条件构造器

3.**LambdaQueryWrapper**：Lambda语法查询构造器

4.**LambdaUpdateWrapper**：Lambda语法更新构造器

### LambdaQueryWrapper

1.**.eq**(User::getName,AAA)

* 这个表示**相等条件**

2.**.gt(User::getAge,70)**

* 这个表示**大于条件**

3.**.last("limit 1")**

* 表示限制1条,当查找到多条数据但是有只想要通过getOne获取其中一条的时候，就要加上这个条件

4.**.like(User::getName,"A")**

* 表示查找相似的数据

5.**.ne(User::getAge,10)**

* 表示不等值查询

6.**.ge(User::getAge,20)**

* 大于等于

7.**.lt      .le(User::getAge,30)**

* 小于和小于等于

8.**.between（User::getAge,20,80）**

* 区间查询

9.**模糊查询**

![image.png](/assets/09551e12-ac90-4bde-a88a-12f94641fa5a.png)

10.**复杂条件组合查询**

![image.png](/assets/3f569010-e473-4fc4-8c08-c5adf2632b21.png)

![image.png](/assets/968669d9-5aa9-4370-90ff-48ed509df78b.png)

* 括号内部的w和x都是**lambda的语法**，是一个临时参数，在外部就不用管理了，调用创建的lambdawrapper对象即可

11.**嵌套条件**

![image.png](/assets/d5d0c791-3f98-48b9-962a-7d8e358ebafe.png)

12.**orderByAsc（"AA","BB"）**

* 先按照AA升序排序，再按照BB升序排序

13.**orderByDest("CC")**

* 按照CC降序排序

## 分页查询方法步骤

1.**创建页面对象**

![image.png](/assets/a6fe0ab8-9248-44a2-891e-9a010997bf08.png)

2.**编写查询条件**

![image.png](/assets/09403041-ef81-4ce4-8cfd-9b52fe6dc03b.png)

3.**调用分页查询插件**

* 将页面对象和查询条件录入

![image.png](/assets/c30603fe-e519-47a8-99ad-8a86f6c014fa.png)

14.**select("A","B","C")chax**

**作用**：只查询A,B,C三个字段的值，不全部查

**位置**：他是构造器方法，因为他在设置查询规则

分页

## UpdateWrapper更新构造器

1.**.set**

**作用**：录入数据，一个set，修改一个属性

**位置**：是updatewrapper对象的方法

![image.png](/assets/c968d3ba-8daa-47d9-baef-961bc8f97cc9.png)

# 动态条件构建

1.**原来采用if标签的方式判断改部分判断语句是否要拼接上去**

2.**构造器方式**：再每个条件中，第一个参数就是可以用来判断这个条件是否加入这个构造器。

![image.png](/assets/c32b8873-2d15-4623-b663-337014d581f1.png)

# 嵌入sql语句

有时候必须要用到sql的时候就需要用到**子查询**

**实现方法**

1.**创建构造器对象**

2.**调用方法inSql**

* 第一个id是等待接收的容器，第二个sql里的id是条件查询出来后的id，最后会将查询出来的id放到第一个容器id中

# 原生mapper基础流式查询两种方式

1.**为了解决大数据量的时候内存不够用的难题**

2.**处理百万级，千万级的数据量的时候**

* **防止内存溢出OOM**：例如，当查询list的时候，数据库会将符合条件的都放入内存，这时如果数据过多就会导致内存溢出
* **保证程序稳定运行**：内存中只持有一条数据

# 流式查询

1.**接口定义**

在要使用流式查询的mapper中写入下面的定义

![image.png](/assets/0e29a280-173c-4d89-b729-50bef28c73fa.png)

* @Options：他限制了读取方式，一条一条读
* **去掉画红线部分**

2.**调用resultHandler方法**

* 在controller中调用UserMapper中的方法
* ![image.png](/assets/2b3450bc-9f29-432f-8f6b-cf9668719696.png)
* **getResultCount()**:这个是stream的方法，用于计数的作用，表示**读到哪条数据了**
* **getResultObject()**:这个也是stream的方法，用于获取数据的方法，将其存储到数据对象中

# 游标查询

1.**导入定义**

![image.png](/assets/0dbf63ba-b9da-4c52-b075-881d651905bc.png)

2.**注意**：Cursor这个单词不会给提示，要自己引入依赖

```
import org.apache.ibatis.cursor.Cursor;

```

3.**调用游标**：

![image.png](/assets/1a529902-917f-44ea-a6d8-f06087662fc0.png)

4.**添加注解**：因为spring每次用完数据连接都会断掉，所以这个会报错

* 这时就需要加上**事务注解@Transactional**
* ![image.png](/assets/70dcc69c-c1f3-40c7-9c42-0347cd86a1c5.png)

# Mybatis-plus流式查询两种方式

1.**替代上面的第一种流式查询方法**：

![image.png](/assets/473a1d2c-202e-47a9-a15e-ab6f764c54ab.png)

2.**带条件的分页流式查询**

![image.png](/assets/baa9733f-d60c-42c5-999e-6948a4e7ba68.png)

## 四种流式查询的应用场景

1.**第一种**：就是平常的方式

2.**第二种**：java8的流式处理

3.**第三种**：大批量的分页查询

4.**第四种**：复杂事务场景，保证数据的一致性

# 自动映射枚举

优雅的处理数据库字段和java枚举类型之间的转换

**实现步骤**

1.**创建枚举类文件**

![image.png](/assets/d89d85e7-766f-4fb0-baf7-bfd6064fd2ad.png)

* 如果没有声明@EnumValue，他就会直接将枚举方法名字直接存入，就是setGender.MALE，数据库就存的是MALE
* 或者可以通过**实现加存储枚举接口的方式**

![image.png](/assets/1817f13d-bd26-45d2-8dce-a9104472eb4a.png)

* 测试通过了

![image.png](/assets/3390eeab-8580-434f-9687-140e2df956c6.png)

# 自动填充字段

公告字段，如时间，日期等，在原来的springboot中要通过额外的代码插入，

**作用**：可以在实体类的位置声明好这个是需要自动填充的即可

1.**标记要自动填充位置**

![image.png](/assets/49735a00-0686-4175-962a-775b974f42e4.png)

2，**编写填充逻辑**

注解只是用来标记的，还要在注解上声明要填充的内容方法。

![image.png](/assets/b2349606-6de2-4101-93b6-4b9967fd6e62.png)

3.**解决上面的当前修改用户的问题**

每当更新数据的时候都会有一个updateuser需要存储。

![image.png](/assets/76684813-f0c4-4edf-bac8-101b17677849.png)

4.**设置当前用户ID**

上面讲了如何从threadlocal中获取userid，肯定时要设置了才能获取到。

所以要在登陆后**拦截器中设置好当前用户的id**

![image.png](/assets/1aad0b4e-dca3-46ee-b2b7-2a6781a69c28.png)

5.**注意**：

* 配置类要记得写注入到spring管理的注解
* 自动填充的实现配置，它里面的**第一个参数的是属性名称**
* 数据库中的时间还是datetime类型的属性

# 主键生成策略

mybatis-plus中可以设置五种策略来设置主键字段里的值

* AUTO：数据库自增ID
* NONE：根据全局配置的算法来，默认是ASSIGN_ID
* INPUT：手动设置主键值，

![image.png](/assets/906af9ec-5192-429f-ae4f-497c83ff0136.png)

* ASSIGN_ID：自动分配ID（默认雪花算法，支持Long/String）
* ASSIGN_UUID：自动分配UUID类型的值

**ID**：大多数是int类型的id

**UUID**：String类型的ID

**实际应用**

**![image.png](/assets/2ca90934-638b-47ce-abdb-cb00e5468a4f.png)**

# 逻辑删除

**原sql语句**：用来添加用来测试的标识，不用管

![image.png](/assets/e55c9349-aac1-4f43-8387-772f87caa230.png)

**逻辑删除逻辑优先级**：注解配置>全局配置>默认配置

**作用**：他这个删除不是直接删除让它消失，而是逻辑删除，修改**删除标识**

1.**标记注解**：**@TableLogic**

* 默认情况下会去使用全局配置中的配置

2.**配置全局配置**：

* 默认不配置的情况下，1表示删除，0表示未删除
* **可以自定义删除逻辑**：在mybatis-plus下的配置消息
* ![image.png](/assets/b878a529-322c-482b-8696-0908e454f609.png)

3.**注解声明删除逻辑**

![image.png](/assets/c1125751-b4db-4931-a77e-31144ba80433.png)

### 逻辑删除的查询

**只查找已删除的**：用**条件构造器的last**，.last(" OR deleted = 1 ")

# 多数据源支持

可以方便的在一个数据库中方便的操作多个不同的库，不用手动切换

1.**编写全局配置**：

![image.png](/assets/a07df8c6-34a9-4d2d-a9b1-774df4452a08.png)

2.**使用多数据源操作**

* 编写注解：@DS("AAA")
* **这个AAA**表示配置中的数据库名字，表示要调用这个数据库

![image.png](/assets/caea1681-c4e1-4e2e-b92a-39a9036796eb.png)

3.**局部使用@DS("AAA")**

**作用**：配合全局配置中的多数据源配置，某个controller方法，选择用AAA作为这个方法中要用的数据库

**位置**：如果想让整个类默认用某个数据库的话是放在类上面，如果是某个controller方法或者service方法的话就是方法上面

![image.png](/assets/5e7ff2a8-1ad4-4e1f-9939-fb30b8ae2b96.png)

4.**任意位置使用**

使用编程代码方式调整要使用的数据库

![image.png](/assets/5ea5e546-b895-4662-8c63-7b157631a746.png)

# 自定义类型处理器

mybatis-plus提供了强大的字段类型处理器，java类型和数据库类型之间的转换

**解决数据库字段类型和 Java 代码里的类型「说不到一块儿」的问题，帮你自动把两边的类型互相转换，不用手动写转换代码**。

1.**有效提高效率**：不用在原来每个插入代码的地方实现类型转换操作，

2.**可以避免出错**

3.**节省代码量**

## 自定义类型处理例子

#### 以map类型的转换为例子——JSON处理器

1.**利用内置的json处理器**：

@TableField(typeHandler=JacksonTypeHandler.class)

2.**编写这个处理器的依赖**：

![image.png](/assets/02c236b1-7bab-43a1-9456-46b3c55c270c.png)

3.**效果展示**

在java提取参数时，

**![image.png](/assets/a9ddace2-05cc-4468-b456-230198328418.png)**

在数据库中：他存储的时varchar

![image.png](/assets/ceec42eb-88c4-41ad-bc4e-27832da799a1.png)

4.**还有list等都是可以转换的**

![image.png](/assets/b77419c0-fcac-450e-85a0-14015c080679.png)

![image.png](/assets/0f1b3582-8424-4e63-9358-f1384f261f61.png)

## 自定义类型转换逻辑——Map

1.**编写转换逻辑**

![image.png](/assets/dab0b88e-4a74-4f7e-91f2-3053b45e9293.png)

* 可以看到它将List类型，转换为String类型

2.**调用自定义转换逻辑**

![image.png](/assets/19f62335-9094-4026-946c-740722923f3c.png)

## 自定义转换逻辑——List

1.**转换逻辑实现**：下面的是针对于List的固定写法，不用深究为什么这样写，是必选实现的几个方法

![image.png](/assets/195a96c9-3fda-4556-a774-62af010f7078.png)

2.**实现方法和上面一样**

## 自定义转换——实现AES加密

上传到数据库通过自定义类型转换实现**加密**，获取的时候进行解密

![image.png](/assets/35141a8a-0f2c-455d-8298-4e51a801bac6.png)


# MyBatis-Plus插件

1.**插件执行顺序**：这个是建议

![image.png](/assets/44d239fc-316b-4e12-abaa-3e19cf5b18dd.png)

# 分页插件

1.**第一步**：安装插件

![image.png](/assets/838c51a4-f43b-4b62-86a5-8a0e53db2cd1.png)

2.**编写分页插件配置类**

![image.png](/assets/b8eeef30-35b9-4407-a4fe-5d633da4083f.png)

* 记得在配置类上加 **@Configuration**
* **@MapperScan**
* 如果报错空指针,要处理一下报错位置的空指针，if返回空

3.**调用分页查询**

![image.png](/assets/84ccb140-8892-44be-bf22-687bb4f2ec1e.png)

# 处理并发修改冲突

**锁**：比如两个地方同时向同一个表插入数据，锁的作用

**作用**：让这些操作变得有顺序，避免乱套

**所得范围**：

* **行锁**：只锁一行数据
* **表锁**：把整个表都锁了，所有商品都不能改

## 悲观锁

1.**提前性**：提前预知到了，一定会有锁冲突，所以要把东西锁起来，用完再解锁。

2.**事务性**：这个只有事务才能实现，知道操作完才会解锁。

3.**流畅性**：绝对不会出现堵住的情况

#### 应用场景

* 扣库存
* 转账
* 秒杀


## 乐观锁

1.**提前性**：认定没人跟我抢，所以不会上锁直接改，最后再检查，有没有人插队。

2.**贴标签**：每次修改数据就会给标签添加一次版本数。

3.**修改策略**：版本号记录策略，

* 要修改的时候，会先读取改条数据的版本号A
* 然后提交sql语句，一个带着**版本识别的语句**，
* **语句中包含**：如果**还是上回那个版本号**，**他就会修改数据**
* **如果不是了，就说明有人提前修改了数据，他就放弃这次修改**
* 等下一次重新修改

#### 应用场景

* 修改信息
* 简单业务，追求高效场景




# 乐观锁插件

## 原始插件代码

1.**主要调用部分**：

![image.png](/assets/670d56fe-81c5-42c5-a036-78a128e3eda1.png)

2.**插件辅助部分**：用注解标记出用于记录版本号的变量

![image.png](/assets/63ea38c0-0640-49ca-b51f-ccee847ab6f4.png)

## 实用场景（只用于更新操作）

在实际应用中的触发场景

1.**首先**：已经在实体类中声明一个实体属性（表中存在）并用@Version标识出来

2.**其次**：**触发场景**

* 调用**更新数据**的方法的时候

3.**他只管更新的时候的锁情况**：以下场景**不会触发**

* 删除
* 查询
* 插入

# 防全表操作插件

如果删除表的时候忘了加条件，就会导致整个表清空。


1.**插件主要逻辑代码**

![image.png](/assets/a208918c-3fc8-4ddc-8737-f4fa78da5120.png)2.只要是全表操作都会报错

* 全表更新
* 全表删除


# 动态表名
