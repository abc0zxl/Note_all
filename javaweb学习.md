## 环境配置

**JRE**:java runtime environment
是运行 Java 程序的 “运行环境”，包含 Java 虚拟机（JVM）、Java 类库等，**仅能运行已编译的 Java 程序**，不能用于开发。
**JDK**Java Development Kit
是 Java 开发的 “工具包”，**包含了 JRE**，同时还提供了编译器（`javac`）、调试工具、文档生成工具等**开发必需的组件**。
## idea
**bootstrap项目启动，引导**
Spring Boot 项目：必须有 Bootstrap 启动类（比如 `TakeawayApplication`），你点击 IDE 的 “运行” 按钮，本质就是执行这个类的 `main` 方法，引导项目启动（加载配置、启动 Tomcat）。
**Facets**
给项目贴的 “类型标签”，决定 IDE 提供什么开发工具支持：IDE 就会自动适配相关功能（比如显示 Tomcat 部署选项、识别 Servlet 类）。

**Artifacts**
项目的 “成品包”****IDE 或构建工具（Maven/Gradle）打包后生成的 “最终可运行文件”****
**Deployment**
把 Artifacts（成品包）放到服务器 / 容器中，让项目可运行的过程。
**以上四个是专属于idea中的操作，该项目放在eclipse中也可以运行**
## 组件
都是java生态的打包，分发，部署
**JAR**：java archive
JAR 面向通用 Java 程序 / 组件
用于把各种结构类打包成一个压缩文件
**WAR**：Web Application Archive
WAR 专门面向 Java Web 应用
把所有web应用的所有资源打包，专门部署到web服务器中

## 目录结构
**resource:**存放java文件的地方
****
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1MDA4NzA1MTAsMTk2NDM2ODQ3MCw0ND
A5MDU2MTldfQ==
-->