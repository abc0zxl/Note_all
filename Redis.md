# 散碎操作

1.**修改密码**：在redis.windows.conf下查找requirepass代码

* 去掉注释
* 设置密码

2.**通过密码连接Redis**：

![image.png](/assets/17e7b4f4-062d-4232-a80f-fc70311d3053.png)

# 应用场景

1.缓存对象：最常用

2.实现分布式锁：setnx

3.共享session：就是JWT存储操作

4.实现计数器

5.限流操作，拒绝请求

6.实现哈希结构

* 购物车
* 动态配置管理

7.多维度数据统计

8.双端队列 list的：简单的消息队列

9.轻量级消息队列：

10.消息流：实时消息流，发群消息

11.set结构：抽奖系统，（重复奖品，无重复奖品，数据去重），点赞，共同好友，兴趣爱好

12.zset：有序无重复，需要排序的场景，各种排行榜，滑动窗口限流，消息的保护，在线用户列表。

13. 存取数据非常快，

15.软件里的动态推送快速显示

16.点赞列表

17.数据持久化，定期把内存的数据放到硬盘中

18.可以实现分布式架构

## 应用场景

1.缓存

* 朋友圈
* 电商商品详情页
* 视频网站的首页推荐

2.计数器：实时更新，数据准确

* 公众号阅读量
* 商品销量
* 视频播放量

3.分布式锁：

* 秒杀活动
* 防止超卖

4.**总的来说就是**：

* 实现锁
* 公共数据操作

# redis（Remotion Dectionary server）

* 一个轻量级的工具，一种存储数据的数据库
* 将数据存到内存中，key-value数据结构
* 他解决了高访问量场景下的问题，大量数据存储在MySql，对于高访问量的数据存储在Redis（内存），两两相互配合
* 高性能，支持多种数据类型
* 目的是为了实现高速访问的作用
* 一个处理缓存的中间件，
* 几乎在每个项目中都会用到，
* 在小企业的项目中完全够用

# 处理的问题

* 数据库的访问量有限，但超限可以用Redis来解决
* 秒杀，抢车票
*


# 目录结构

介绍redis文件的几个重要的文件

1.**Redis配置文件**：redis.windows.conf

2.**Redis客户端**：redis-cli.pdb

3.**Redis服务端**：redis-server.exe


# Redis数据类型

1.**字符串string**：

2.**哈希hash**：

3.**列表list**：可以有重复元素

4.集合set：无序集合，没有重复元素

5.**有序集合**：这个集合中每个元素关联一个**分数**，根据分数的高低来升序排序，没有重复元素（**排行榜**）

* sorted set
* zset


# 下面全都是在Redis的命令行中执行的命令，代码中的命令和这个完全不一样

# 字符串常用命令

1.**设置指定key的值**：SET key value

2.**获取指定key值**：GET key

3.**设置指定的值，并设置过期时间**：SETEX key seconds value

4.**只有在key不存在时设置key的值**：SETNX key value



# 哈希操作命令

Redis hash 是一个String类型的field和value的映射表，特别适合用于存储对象

**结构**：像一个二级存储目录

key ->(field1,field2)=(value1,value2)

下面图片没有插入命令


![image.png](/assets/a30b4d15-84a6-4385-ab8e-b53bf6da51d8.png)


# 列表操作命令

按照**插入顺序**排序，操作类似一个队列，左侧按顺序插入，右侧按顺序删除

![image.png](/assets/4543586c-fd5a-4643-941b-011e6ee7066e.png)


# 集合操作命令

无序集合，没有重复元素

![image.png](/assets/12021c80-702a-484e-aba6-237c0903ef38.png)

# 有序集合操作命令

这个集合中每个元素关联一个**分数**，根据分数的高低来升序排序，没有重复元素

**实用**：排行榜

![image.png](/assets/6a77e4a1-7dd9-4bb4-9d98-bab0e842de68.png)

# 通用命令

他跟具体数据类型无关，所有数据类型都能用的命令

![image.png](/assets/4949c1d1-1c35-4b53-bf01-46d153782907.png)

1.**第一个命令pattern**：他表示某种命令如*，表示查找所有




# Redis的java客户端SpringDataRedis

他也是spring的一部分，可以用这个工具来简化Redis的操作

**使用步骤**：

1.**导入他的依赖到xml中**

![image.png](/assets/a2271c72-6abf-4418-9efa-ec64cb301b27.png)

2.**配置Redis数据源**

密码，端口号，数据库编号，ip地址

![image.png](/assets/206cd48b-3d14-4038-8727-5ade42602b9d.png)

3.**编写配置类，创建RedisTemplate对象**

在config包下创建类

![image.png](/assets/492c41aa-8013-4ef7-9ec2-18b01f436e6f.png)

4.**通过RedisTemplate对象来操作Redis**

* 这个模板可以创建多个数据类型的操作对象
* 在redis上看到value乱码没有关系，提取出来就不是乱的
* 在上面的图片中仅设置了key的序列化器，所以key在redis 的图形界面上不会乱码
* 然后就可以通过这些对应类型的模板来执行对应类型的指令。

5.**String类型的操作**：上半部分是模板对象

![image.png](/assets/a6ecd2fd-6a1f-48f1-aa30-55ad18503ac7.png)


6.**Hash类型的操作**：

* **插入**：对象AAA.put(key,hashkey,value)
* **获取**：对象AAA.get(key,hashkey,value)
* **删除**：对象AAA.delete(key,hashkey)
* **获取指定key值的hashkey的列表**：set hashkeys=AAA.keys(BBB)
* **获取指定key值的value列表**：List values=AAA.values(BBB)

![image.png](/assets/d3183abd-38d1-46f4-a7ff-e31027826bcf.png)

6.**列表类型的操作**：

* **在一个key中连续插入多个value**：AAA.leftPushAll(key,value1,value2……）
* **插入单个value**：AAA.leftPush(key,value)
* **提取出key中地址范围的value**：
  AAA.rightPop(key)
* **统计该key中的value数**：
  AAA.size(key)

![image.png](/assets/3a4529a1-fcff-42bb-b060-1b00cd743641.png)

7**集合类型的操作**：

* **两个集合的交集**：AAA.intersect(key1,key2),用set集合来封装
* **两个集合的并集**：AAA.union(key1,key2),用set来封装

![image.png](/assets/35123733-cf94-4097-a004-314665950b0d.png)


8.**有序集合的操作**：

* **获取排序的value**：AAA..range(key,start,end),用set来封装
* **给指定的key中的某个value添他的成绩**：AAA.incrementScore(key，value,delta)

![image.png](/assets/2bdb6258-a320-4df8-bc13-272e2bcd389b.png)


9.**通用命令**：

* **查询指定查询标准的key**：redisTemplate.keys（XXX）
* **查询指定的key是否存在**：redisTemplate.hasKey(BBB)结果用bool来接住
* **查询该key的类型**：redisTemplate.type(AAA),结果用DataType来封装。
* **删除指定的key**：redisTemplate.delete(AAA)
*

![image.png](/assets/da699ae5-eb61-4835-a618-b52449b889d9.png)
