## 第一步：Apifox 项目初始化与公共配置

### 1. 创建项目

打开 Apifox → 左上角「新建项目」→ 项目名称填：`上门帮家政服务系统`

### 2. 设置环境变量

位置：左侧边栏「管理中心」→「环境管理」→ 点击「新建环境」

创建三个环境：


| 环境名称 | 基础URL（Base URL）            |
| -------- | ------------------------------ |
| 开发环境 | `http://localhost:8080`        |
| 测试环境 | `http://test.shangmenbang.com` |
| 生产环境 | `https://api.shangmenbang.com` |

每个环境中添加以下环境变量（在环境详情页的「环境变量」tab）：


| 变量名       | 类型   | 开发环境值              | 说明      |
| ------------ | ------ | ----------------------- | --------- |
| `baseUrl`    | string | `http://localhost:8080` | 基础地址  |
| `token`      | string | （空，运行时自动填充）  | JWT令牌   |
| `apiVersion` | string | `v1`                    | API版本号 |

### 3. 设置全局请求头

位置：项目根目录（左侧接口树最顶层文件夹）→ 右键 →「修改」→「Auth」tab 和「Header」tab

在「Header」tab 添加：


| 参数名          | 示例值                                           | 是否必填 | 说明           |
| --------------- | ------------------------------------------------ | -------- | -------------- |
| `Content-Type`  | `application/json;charset=UTF-8`                 | 是       | 请求内容类型   |
| `Accept`        | `application/json`                               | 是       | 接受响应类型   |
| `X-Api-Version` | `{{apiVersion}}`                                 | 是       | API版本号      |
| `X-Platform`    | `CLIENT_APP`/`WORKER_APP`/`SHOP_WEB`/`ADMIN_WEB` | 是       | 请求来源端标识 |

### 4. JWT 认证配置

位置：项目根目录 →「Auth」tab → 类型选「Bearer Token」→ Token 填 `{{token}}`

这样所有子文件夹和接口都会自动继承这个认证方式。登录和注册接口单独设置「Auth」为「No Auth」即可。

自动获取 token 的方式：在登录接口的「后置操作」中添加脚本：

<pre><div class="relative flex flex-col rounded-lg mt-4"><div class="text-text-300 absolute pl-3 pt-2.5 text-xs">javascript</div><div class="pointer-events-none sticky my-0.5 ml-0.5 flex items-center justify-end px-1.5 py-1 mix-blend-luminosity top-0"><div class="from-bg-300/90 to-bg-300/70 pointer-events-auto rounded-md bg-gradient-to-b p-0.5 backdrop-blur-md"><button class="flex flex-row items-center gap-1 rounded-md p-1 py-0.5 text-xs transition-opacity delay-100 hover:bg-bg-200 opacity-60 hover:opacity-100"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" fill="currentColor" viewBox="0 0 256 256"><path d="M200,32H163.74a47.92,47.92,0,0,0-71.48,0H56A16,16,0,0,0,40,48V216a16,16,0,0,0,16,16H200a16,16,0,0,0,16-16V48A16,16,0,0,0,200,32Zm-72,0a32,32,0,0,1,32,32H96A32,32,0,0,1,128,32Zm72,184H56V48H82.75A47.93,47.93,0,0,0,80,64v8a8,8,0,0,0,8,8h80a8,8,0,0,0,8-8V64a47.93,47.93,0,0,0-2.75-16H200Z"></path></svg><span class="text-text-200 pr-0.5">复制</span></button></div></div><div class="!my-0 !rounded-lg !text-sm !leading-relaxed"><code class="language-javascript"><span class="token">// 位置：登录接口 → 后置操作 → 添加「自定义脚本」</span><span>
</span><span></span><span class="token">var</span><span> response </span><span class="token">=</span><span> pm</span><span class="token">.</span><span class="token property-access">response</span><span class="token">.</span><span class="token method property-access">json</span><span class="token">(</span><span class="token">)</span><span class="token">;</span><span>
</span><span></span><span class="token control-flow">if</span><span> </span><span class="token">(</span><span>response</span><span class="token">.</span><span class="token property-access">code</span><span> </span><span class="token">===</span><span> </span><span class="token">200</span><span class="token">)</span><span> </span><span class="token">{</span><span>
</span><span>    pm</span><span class="token">.</span><span class="token property-access">environment</span><span class="token">.</span><span class="token method property-access">set</span><span class="token">(</span><span class="token">"token"</span><span class="token">,</span><span> response</span><span class="token">.</span><span class="token property-access">data</span><span class="token">.</span><span class="token property-access">token</span><span class="token">)</span><span class="token">;</span><span>
</span><span></span><span class="token">}</span></code></div></div></pre>

### 5. 创建接口文件夹结构

位置：左侧「接口」面板 → 右键根目录 → 「新建文件夹」

```
上门帮家政服务系统
├── 公共接口
│   ├── 验证码
│   └── 文件上传
├── 客户端（CLIENT）
│   ├── 认证模块
│   ├── 首页模块
│   ├── 分类模块
│   ├── 商品模块
│   ├── 订单模块
│   ├── 购物车模块
│   ├── 个人中心模块
│   └── 设置模块
├── 服务员端（WORKER）
│   ├── 认证模块
│   ├── 首页模块
│   ├── 任务模块
│   └── 个人中心模块
├── 商户端（SHOP）
│   ├── 认证模块
│   ├── 服务管理模块
│   ├── 员工管理模块
│   ├── 订单管理模块
│   ├── 数据统计模块
│   └── 店铺设置模块
└── 管理端（ADMIN）
    ├── 认证模块
    ├── 平台总览模块
    ├── 店铺管理模块
    ├── 服务人员管理模块
    └── 系统设置模块
```

### 6. 公共响应数据结构

位置：左侧「数据模型」→「新建数据模型」

创建以下公共模型：

**模型1：BaseResponse（统一响应体）**

<pre><div class="relative flex flex-col rounded-lg mt-4"><div class="text-text-300 absolute pl-3 pt-2.5 text-xs">json</div><div class="pointer-events-none sticky my-0.5 ml-0.5 flex items-center justify-end px-1.5 py-1 mix-blend-luminosity top-0"><div class="from-bg-300/90 to-bg-300/70 pointer-events-auto rounded-md bg-gradient-to-b p-0.5 backdrop-blur-md"><button class="flex flex-row items-center gap-1 rounded-md p-1 py-0.5 text-xs transition-opacity delay-100 hover:bg-bg-200 opacity-60 hover:opacity-100"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" fill="currentColor" viewBox="0 0 256 256"><path d="M200,32H163.74a47.92,47.92,0,0,0-71.48,0H56A16,16,0,0,0,40,48V216a16,16,0,0,0,16,16H200a16,16,0,0,0,16-16V48A16,16,0,0,0,200,32Zm-72,0a32,32,0,0,1,32,32H96A32,32,0,0,1,128,32Zm72,184H56V48H82.75A47.93,47.93,0,0,0,80,64v8a8,8,0,0,0,8,8h80a8,8,0,0,0,8-8V64a47.93,47.93,0,0,0-2.75-16H200Z"></path></svg><span class="text-text-200 pr-0.5">复制</span></button></div></div><div class="!my-0 !rounded-lg !text-sm !leading-relaxed"><code class="language-json"><span class="token">{</span><span>
</span><span>    </span><span class="token">"code"</span><span class="token">:</span><span> </span><span class="token">200</span><span class="token">,</span><span>
</span><span>    </span><span class="token">"msg"</span><span class="token">:</span><span> </span><span class="token">"操作成功"</span><span class="token">,</span><span>
</span><span>    </span><span class="token">"data"</span><span class="token">:</span><span> </span><span class="token">null</span><span class="token">,</span><span>
</span><span>    </span><span class="token">"timestamp"</span><span class="token">:</span><span> </span><span class="token">1700000000000</span><span>
</span><span></span><span class="token">}</span></code></div></div></pre>


| 字段名    | 类型    | 必填 | 说明       | 示例值        |
| --------- | ------- | ---- | ---------- | ------------- |
| code      | integer | 是   | 业务状态码 | 200           |
| msg       | string  | 是   | 提示信息   | 操作成功      |
| data      | object  | 否   | 响应数据   | {}            |
| timestamp | long    | 是   | 时间戳     | 1700000000000 |

**模型2：PageResult（分页响应体）**

<pre><div class="relative flex flex-col rounded-lg mt-4"><div class="text-text-300 absolute pl-3 pt-2.5 text-xs">json</div><div class="pointer-events-none sticky my-0.5 ml-0.5 flex items-center justify-end px-1.5 py-1 mix-blend-luminosity top-0"><div class="from-bg-300/90 to-bg-300/70 pointer-events-auto rounded-md bg-gradient-to-b p-0.5 backdrop-blur-md"><button class="flex flex-row items-center gap-1 rounded-md p-1 py-0.5 text-xs transition-opacity delay-100 hover:bg-bg-200 opacity-60 hover:opacity-100"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" fill="currentColor" viewBox="0 0 256 256"><path d="M200,32H163.74a47.92,47.92,0,0,0-71.48,0H56A16,16,0,0,0,40,48V216a16,16,0,0,0,16,16H200a16,16,0,0,0,16-16V48A16,16,0,0,0,200,32Zm-72,0a32,32,0,0,1,32,32H96A32,32,0,0,1,128,32Zm72,184H56V48H82.75A47.93,47.93,0,0,0,80,64v8a8,8,0,0,0,8,8h80a8,8,0,0,0,8-8V64a47.93,47.93,0,0,0-2.75-16H200Z"></path></svg><span class="text-text-200 pr-0.5">复制</span></button></div></div><div class="!my-0 !rounded-lg !text-sm !leading-relaxed"><code class="language-json"><span class="token">{</span><span>
</span><span>    </span><span class="token">"total"</span><span class="token">:</span><span> </span><span class="token">100</span><span class="token">,</span><span>
</span><span>    </span><span class="token">"pageNum"</span><span class="token">:</span><span> </span><span class="token">1</span><span class="token">,</span><span>
</span><span>    </span><span class="token">"pageSize"</span><span class="token">:</span><span> </span><span class="token">10</span><span class="token">,</span><span>
</span><span>    </span><span class="token">"pages"</span><span class="token">:</span><span> </span><span class="token">10</span><span class="token">,</span><span>
</span><span>    </span><span class="token">"list"</span><span class="token">:</span><span> </span><span class="token">[</span><span class="token">]</span><span>
</span><span></span><span class="token">}</span></code></div></div></pre>


| 字段名   | 类型    | 必填 | 说明     | 示例值 |
| -------- | ------- | ---- | -------- | ------ |
| total    | long    | 是   | 总记录数 | 100    |
| pageNum  | integer | 是   | 当前页码 | 1      |
| pageSize | integer | 是   | 每页条数 | 10     |
| pages    | integer | 是   | 总页数   | 10     |
| list     | array   | 是   | 数据列表 | []     |

### 7. 全局错误码

位置：可以在项目根目录的「说明」中维护，或者在 Apifox 的「项目设置」→「项目概览」中写入


| 错误码 | 说明               | 触发场景               |
| ------ | ------------------ | ---------------------- |
| 200    | 成功               | 请求正常处理           |
| 400    | 请求参数错误       | 参数校验失败           |
| 401    | 未认证             | token缺失或过期        |
| 403    | 无权限             | 角色权限不足           |
| 404    | 资源不存在         | 请求的资源未找到       |
| 409    | 资源冲突           | 重复注册、订单已被抢等 |
| 422    | 业务校验失败       | 业务逻辑不满足         |
| 429    | 请求过于频繁       | 触发限流               |
| 500    | 服务器内部错误     | 系统异常               |
| 1001   | 验证码错误         | 验证码不匹配或过期     |
| 1002   | 账号或密码错误     | 登录校验失败           |
| 1003   | 账号已被禁用       | 管理员禁用账号         |
| 2001   | 订单已被接单       | 抢单冲突               |
| 2002   | 订单状态不允许操作 | 非法状态流转           |
| 3001   | 店铺审核未通过     | 店铺未审核或被拒       |
| 3002   | 店铺已停业         | 店铺营业状态关闭       |

---

## 第二步：接口文档（全部四端）

接口地址统一格式：`{{baseUrl}}/api/{{apiVersion}}/{端标识}/{模块}/{操作}`

端标识：`client`、`worker`、`shop`、`admin`、`common`

---
