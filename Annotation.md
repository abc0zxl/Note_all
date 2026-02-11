1.**@RequestBody**：

**作用**：用于将前端发过来的json数据转换为java对象

位置：参数前面

2.**@NotNULL**

参数不能为空

3.**@NotEmpty**

表示参数不能为空外，字符串类型也不能为null

**@URL**

**作用**：用于识别这个传过来的参数是不是一个合法的url地址

4.**@Validated**

如果不在实体类参数前面加这个注解的话，原来在实体中定义的校验方法,如@NotNull，@NotEmpty就不生效。

5.**@RequestParam(requed=flase)**

**作用**：告知这个参数不是必须的

**位置**：放在参数左边

6.**@RequestBody**

讲前端传过来的json字符串转换成java对象

7.**@Documented**

**作用**：讲标注了这个注解的**自定义注解类**，这个自定义注解会被java文档生成工具收录到API文档中。

**位置**：自定义注解的类上面，专用**元注解**

8.**@Target**

**作用**：表示i这个自定义注解将来可以放到说明上面生效，**类上**，**属性**

9.**@Retention**

**作用**：表示这个自定义注解将来运行时，在那些阶段会被保留。（运行时，）

10.**@Constraint（validatedBy={AAA.class}）**

**作用**：表示谁来提供这个注解的校验规则

11.**@SpringBootTest**

**作用**：表示这个单元测试类在执行之前会先**初始化Spring容器**

**位置**：放在测试类上，一个项目可以有很多个这样的注解

12.**@CrossOrigin**

**作用**：支持跨域请求注解

**位置**：controller的类上

13.**@DateTimeFormat(pattern="yyyy-mm-dd")**

**作用**：用于表明时间的格式，这个要配合LocalDate一起用

![image.png](/assets/4abc8ba0-6786-44f6-8a5a-d9044a87e745.png)

**位置**：放在LocalDate参数前面

14.**@Value**

**作用**：获取配置文件中的数据

**位置**：在方法的参数中

15.**@ConfigurationProperties(prefix="AAA")**

**作用**：

**位置**：

16，**@Bean**

**作用**：在非四大注解中的类，手动创建并注册Bean到Spring容器中，

**位置**：主要放在@Configuration的配置类中的**方法上**

17.**@Import**

**作用**：可以导入**配置类**和**接口实现类**，突破默认的包扫描范围限制，

**位置**：在类上

18.**@Conditional**

**作用**：将一个用于判断的java文件，变得能调用

**位置**：类上

19.**@EnableAutoConfiguration**：

**作用**：告诉springboot根据项目引入依赖，自动配置对应的功能组件，**比如**：使用了Redis，就会自动引入RedisTemplate的配置

**位置**：在类上

20.**@Data**

**作用**：自动生成setter，getter，tostring

**位置**：类上面

21.**@NotNull**:表示参数非空

22.**@NotEmpty**：表示这个参数，以及string类不可以为null

23.**@Email**：表示这个参数为邮箱专属类型，也包含非空

24.**@Pattern（regexp="XXX"）**

**作用**：用于验证字符串是否匹配指定的**正则表达式**

**位置**：在参数左边

![image.png](/assets/8a7ba8a8-df8d-4195-ade7-ce7ae19ec4c4.png)

25.**@Inherited**

**作用**：能让子类自动继承父类上**标注在类上**的注解

**位置**：在**自定义**类上

26.**@RequestBody**

**作用**：解析Http请求体的json，xml数据为java对象

**位置**：方法的参数左边

27.**@RetentionPolicy**

**作用**：表示这个自定义注解类在java程序生命周期中能**存活**多久（source，class，runtime）三个阶段，大部分要用到runtime阶段
