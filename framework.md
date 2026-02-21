# FrameWork

### 三层架构

1.**子模块1**：common

* constant
* context
* enumeration
* exception
* json
* properties
* result
* utils

2.**子模块2**：server（启动类）

* config
* controller
* handler
* interceptor
* mapper
* service

3.**子模块3**：pojo

* dto
* entity
* vo

### 五层架构

1.**子模块1**：common

* constant
* enums
* exception
* result
* utils

2.**子模块2**：pojo

* entity
* dto
* vo

3.**子模块3**：mapper

* mapper

4.**子模块4**：service

* manager
* service

5.**子模块5**：web（启动类）

* controller
* interceptor
* config
* aspect



### common和service层

1.**common适应放**：

* 纯静态
* 全局都要调用

2.**service适应放**：

* 需要用到配置类的
* 需要用到spring的
* 需要交给spring管理的
* 需要和外界交互数据的

### 注入问题

1.**模块有多个，启动类只有一个模块有，如何扫描到别的模块**：添加扫描范围，直接整个项目都扫

![image.png](/assets/5c0082f7-8b02-4247-a08e-35b784474800.png)

### 跨模块路径问题

配置类中需要知道某个文件的位置，分两种情况：其中一种路径写法不一样

* ![image.png](/assets/f8c69b69-a23e-4031-a76d-759705c4462e.png)
