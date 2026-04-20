# YunGouOS

是一个第三方支付代理，专门解决独立开发者没有商户号的苦恼。


**场景**：

* 在微信小程序中唤起微信支付实现支付。
* 在App中实现跳转到（支付宝/微信）完成支付。

**问题**：没有商户号不能正真的支付

**作用**：YunGouOS是一个支付流程中的一个中间代理，他有商户号能实现支付，卡在后端到微信支付官方中间。

* 能实现真实的资金流动
* 也能模拟出原生官方API的大部分流程

# 规则

1.**资金流动规则**

* 交易的金额在次日到达账户
* 查看交易，资金管理网站：[https://pay.weixin.qq.com/guide/miniapp\_assistant.shtml](https://pay.weixin.qq.com/guide/miniapp_assistant.shtml "https://pay.weixin.qq.com/guide/miniapp_assistant.shtml")
* 银行收到账的名字，是YunGouOS的自己公司名字。
* 费率：0.6%

2.**违规操作**

* 要同时遵循微信的限制和YunGouOS的限制。

3.**签名**

* YunGouOS和微信的签名算法一致
* 只有文档中的必传参数才参与前面
* 官方验签工具：[https://pay.weixin.qq.com/doc/v2/tool/sign\_verify](https://pay.weixin.qq.com/doc/v2/tool/sign_verify)

## 开发的微信小程序如何实现支付

1.**在微信小程序中无法实现支付**

2.**需要将小程序运行在手机的微信上才能实现。**：且必须是**体验版**，或者**正式版**
