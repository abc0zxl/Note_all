# Spring Security

它包含有用于处理认证授权的问题

## 认证

认证就是登陆，在我的毕业设计项目中，security是直接排除了这个登录地址。别的都要经过security




## 权限管理

#### 实例

演示前端请求地址，并携带token过来的场景

1.进入JwtInterceptor.java验证jwt

* 提取token：查redis，拿到信息
* 查数据库：查找这个用户在数据库中的角色
* 把用户的角色写入SecurityContext中
* 放行到下一个环境

2.进入到Security

* 匹配到相应要打开的这个网址，
* 从securitycontext中查看这个角色，
