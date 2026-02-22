****# SpringBoot的注解

1.**@Builder**：

**作用**：表示这个pojo类可以用构造器方式赋值

**位置**：类前面

2.**@NotNULL**

参数不能为空

3.**@NotEmpty**

表示参数不能为空外，字符串类型也不能为null

**@URL**

**作用**：用于识别这个传过来的参数是不是一个合法的url地址

4.**@Validated**

如果不在实体类参数前面加这个注解的话，原来在实体中定义的校验方法,如@NotNull，@NotEmpty就不生效。

**作用**：是增强工具，只有需要**分组校验的时候才用**

**位置**：放在controller上，或者service上

5.**@RequestParam(requed=flase)**

**作用**：告知这个参数不是必须的

**位置**：放在参数左边

6.**@ResponseBody**

**作用**：像前端返回数据j，直接用json字符串

**位置**：放在类上面

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

28.**@SpringBootConfiguration**

**作用**：声明他是标注的类是一个配置类，他的效果和@Configuration大致一样，更推荐用这个，可以适配springboot上下文

29.**@ComponentScan**：

**作用**：可以放很多排除方法在里面

30.**@GetMapping**

**作用**：他是在@RequestMapping增加条件后的一个注解，将指定的Url路径，映射到controller方法上，仅接收get类型的http请求

**位置**：只能放在Controller/RestController的类中

31.**@Controller**

32.**@Service**

33.**@Repository**

**作用**：在Spring框架中，标记**数据访问层DAO/Mapper组件**的注解，让Spring容器管理这个类，比@component的异常处理更好，**如果是Mybatis项目，也推荐@Mapper+@Repository**

**位置**：数据访问层的类上

![image.png](/assets/e6410458-38eb-496e-9fab-20df7464f366.png)

34.**@Transactioanl**

**作用**：为方法添加事务控制，确保一组数据的原子性。具有**回滚的功能**

**位置**：**优先**放在**业务代码上**（service）方法上

![image.png](/assets/fddd83aa-b319-4ecb-a552-cf4b1b11bc2d.png)

35.**@Component**：将这个类交给spring管理

36.**@Autowired**：将这个对象交给spring的ioc容器管理

37.**@Slf4j**：

38.**@Overried**：表示这个是一个重写方法

39.**@Aspect**：声明AOP位置

40.**@Valid**：

**作用**：校验注解的**激活开关**，告诉这个参数对应的DTO的所有校验规则，让这个DTO类型文件中的校验注解生效。

**位置**：参数左边

41.**@NoArgsConstructor**

**作用**：自动生成**无参构造方法**

**位置**：在关于实体属类的上面

42.**@AllArgsConstructor**

**作用**：自动生成**全参数构造方法**

**位置**：在关于实体属性类的上面

43.**@NotBlank（message="XXXXX"）**

**作用**：在标记的属性上面，该属性为空的时候就会发出异常，返回错误信息。

**位置**：在实体属性上面

44.**@RestControllerAdvice**

**作用**：标记这个类是一个全局异常处理器

**位置**：在异常处理类文件上面

45.**@RestController**

**作用**：@Controller+@ResponseBody结合体

**位置**：类方法上面

46.**@RequestMapping**

**作用**：给这个controller补一段url

**位置**：controller上面

# MyBatis-Plus的注解

1.**@TableName(value="AAA")**

**作用**：将这个**实体类**和**数据库表AAA**绑定

**位置**：实体类的类名上面

2.**@TableId**

**作用**：标记这个属性中**主键的情况**

**位置**：实体类主键的上方

* IdType.AUTO:表示这个属性是自增的

3.**@MapperScan（“”）**

**作用**：告诉spring，mapper的位置

**位置**：在启动类上面

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
