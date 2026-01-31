![image.png](/assets/d2b84aeb-fffb-48fa-bfa7-27d03e5c98ac.png)

* Eclipse 打开浏览器的 404：只显示 “请求的资源不可用”，信息很笼统；
* Postman 的 404：能看到完整的请求 URL（比如`/firtweb_test/BServ`）、请求方法（POST/GET）、响应头，方便你快速核对 “URL 是否写错、项目名是否正确”。

## Postman作用

1.用 Postman 可以**直接修改 URL / 参数重新测试**（比如改项目名、调整路径大小写），不用重启浏览器 / 项目；

2.浏览器访问需要手动输入 URL，修改后还要刷新，效率更低。

3.不用等前端写好再测试，可以直接用postman测试。

4.可以快速定位问题的位置，而直接打开的网页却不行。

### url书写

![image.png](/assets/848a0275-00a4-4c90-a752-00e07c5bfccf.png)

请求头：//端口名/项目名/Servlet名（非java文件名字）/参数


| 协议             | http://                                     | 必须写（Postman 中不写会报错），Servlet 常用 http，HTTPS 则是 https://   |
| ---------------- | ------------------------------------------- | ------------------------------------------------------------------------ |
| 服务器 IP / 域名 | [localhost](https://localhost/) / 127.0.0.1 | 本地测试用[localhost](https://localhost/)，远程服务器写域名 / 公网 IP    |
| 端口号           | :8080                                       | Tomcat 默认 8080，若改了端口则写对应数字；80 端口可省略（http 默认 80）  |
| 项目上下文路径   | /myweb                                      | 项目部署到服务器的根路径（web.xml 或 tomcat 配置中设置，空项目可省略）   |
| Servlet 映射路径 | /userServlet                                | web.xml 中`<url-pattern>`或注解`@WebServlet("/userServlet")`配置的路径   |
| 参数（GET 方式） | ?id=1&name=test                             | 参数用`?`开头，多个参数用`&`分隔；POST 参数则放在 Body→form-data/raw 里 |


# 测试场景

### 含有JWT验证

原来需要获取一个jwt，然后给每个请求都加上这个jwt，十分麻烦

**解决**：设置请求前的一个脚本，会给每个请求都加上，然后就不用重复的写jwt了

#### Pre-request Script

1.**代码**：pm.request.addHeader("Authorization:AAAAAAAAAAAAAAAAAAAAAA");
