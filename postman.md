![image.png](/assets/d2b84aeb-fffb-48fa-bfa7-27d03e5c98ac.png)


* Eclipse 打开浏览器的 404：只显示 “请求的资源不可用”，信息很笼统；
* Postman 的 404：能看到完整的请求 URL（比如`/firtweb_test/BServ`）、请求方法（POST/GET）、响应头，方便你快速核对 “URL 是否写错、项目名是否正确”。

## Postman作用

1.用 Postman 可以**直接修改 URL / 参数重新测试**（比如改项目名、调整路径大小写），不用重启浏览器 / 项目；

2.浏览器访问需要手动输入 URL，修改后还要刷新，效率更低。

3.不用等前端写好再测试，可以直接
