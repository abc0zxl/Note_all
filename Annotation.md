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

**位置**：主要放在@Configuration的配置类上

17.**@Import**

**作用**：可以导入**配置类**和**接口实现类**，突破默认的包扫描范围限制，

**位置**：
