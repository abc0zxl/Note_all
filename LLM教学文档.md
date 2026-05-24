# LLM + Agent 完整教学文档

> 面向零基础小白，从"什么是 AI"讲起，手把手教会你 Agent、Tool、MCP、Skill 这些概念到底是什么。
>
> 配套项目：`E:\LLM测试空间\going_out_agent`

---

## 目录

1. [第一章：基础概念 - 到底什么是 LLM？](#第一章基础概念---到底什么是-llm)
2. [第二章：什么是 Agent（智能体）？](#第二章什么是-agent智能体)
3. [第三章：什么是 Tool（工具）？](#第三章什么是-tool工具)
4. [第四章：什么是 MCP（模型上下文协议）？](#第四章什么是-mcp模型上下文协议)
5. [第五章：什么是 Skill（技能）？](#第五章什么是-skill技能)
6. [第六章：完整工作流程（逐步骤拆解）](#第六章完整工作流程逐步骤拆解)
7. [第七章：代码逐行解读](#第七章代码逐行解读)
8. [第八章：用到的技术和原理](#第八章用到的技术和原理)
9. [第九章：自己动手扩展](#第九章自己动手扩展)
10. [第十章：常见问题 FAQ](#第十章常见问题-faq)

---

## 第一章：基础概念 - 到底什么是 LLM？

### 1.1 通俗理解

**LLM** = Large Language Model = 大语言模型。

你可以把它想象成一个**超级聪明的实习生**：

- 它读过全互联网的书、文章、代码（这就是"训练"）
- 它懂很多知识，但**没有实时信息**（它的知识截止于训练那天）
- 它能理解你说的话，也能组织语言回复你
- 但它**不能自己上网**，**不能自己执行代码**，**不能查数据库**

> LLM 就像一个被困在图书馆里的人：书里的知识他都懂，但外面现在下没下雨他完全不知道。

### 1.2 LLM 能做什么、不能做什么


| 能做的                               | 不能做的           |
| ------------------------------------ | ------------------ |
| 理解自然语言（你说"查天气"它懂）     | 联网查实时数据     |
| 做推理（"下雨要带伞"这个逻辑它懂）   | 执行代码           |
| 组织语言回复（写文章、写诗）         | 操作文件           |
| 做决策（"这种情况应该调用哪个工具"） | 访问数据库         |
| 翻译、总结、改写                     | 记住对话之外的事情 |

### 1.3 我们用的 LLM：DeepSeek

我们项目用的是 **DeepSeek**（深度求索公司的大模型）。

为什么选它：

- **便宜**：比 OpenAI 的 GPT 便宜很多
- **中文好**：在中国公司做的，对中文理解更好
- **兼容 OpenAI 格式**：代码写法跟调用 GPT 一样，随时可以切换

### 1.4 API 是什么？

**API** = Application Programming Interface = 应用程序接口。

通俗理解：**一个"投递口"**。

```
你（写代码） ──→ [投递口/API] ──→ DeepSeek 服务器
                    ↑
             把你的问题传进去
             把 DeepSeek 的回答取出来
```

你在代码里调用 API，就相当于通过这个"投递口"把问题发给 DeepSeek，然后等它回复。

**我们的 API Key**：`sk-60afd1e3dc244c1f8c7c14bd935474f6`

这个 Key 就像你的"通行证"，每次调 API 都要带上它，DeepSeek 才知道是谁在调用、该扣谁的钱。

---

## 第二章：什么是 Agent（智能体）？

### 2.1 通俗理解

**Agent** = 智能体 = 一个**能自主完成任务的程序**。

对比一下就明白了：


| 传统程序                                     | Agent                       |
| -------------------------------------------- | --------------------------- |
| 你写死逻辑："如果用户说查天气，就调天气 API" | 让 LLM 自己判断用户想要什么 |
| 只能做你写好的功能                           | 能根据情况自己决定怎么做    |
| 用户说"帮我看看外面要不要带伞"，程序听不懂   | Agent 能理解"这是要查天气"  |

**Agent = LLM（大脑）+ Tools（手脚）+ MCP（神经）+ Skills（技能）**

### 2.2 Agent 的工作哲学

Agent 的工作方式不是"if-else"，而是**推理-行动-观察**循环：

```
1. 用户说了一句话
2. Agent 推理：他说这话是什么意思？需要我做什么？
3. Agent 决定行动：我需要查天气 → 调用天气工具
4. Agent 观察结果：天气工具返回了数据
5. Agent 再次推理：根据天气数据，我应该建议用户带伞
6. Agent 回复用户
```

这叫做 **ReAct 模式**（Reasoning + Acting，推理+行动），是 Agent 的核心思想。

### 2.3 我们的项目中的 Agent

在 `E:\LLM测试空间\going_out_agent\agent\core.py` 中：

```python
class GoingOutAgent:
    """出门助手 Agent"""

    def __init__(self):
        self.llm = LLMClient()           # ① 大脑：DeepSeek
        self.mcp = MCPProtocol()         # ② 神经：MCP 协议
        self.skill_manager = SkillManager(...)  # ③ 技能

    async def chat(self, user_input):
        # ① 大脑理解问题
        # ② 大脑决定调什么工具
        # ③ 神经把指令传给对应的工具
        # ④ 工具干活，返回结果
        # ⑤ 大脑综合结果，组织语言回复
        return final_response
```

---

## 第三章：什么是 Tool（工具）？

### 3.1 为什么要 Tool？

你说一个问题就知道了：

> "今天北京天气怎么样？"

LLM 的知识是训练时的，它**不知道此时此刻的天气**。那怎么办？

**方案一**：让 LLM 自己上网查 → 但 LLM 没有联网能力（安全原因）
**方案二**：给 LLM 一个"查天气"的按钮 → 这就是 Tool

**Tool 就是 LLM 的"外挂器官"**：

- 需要实时数据 → 给 LLM 挂一个「查天气」工具
- 需要计算 → 给 LLM 挂一个「计算器」工具
- 需要查数据库 → 给 LLM 挂一个「SQL 查询」工具

### 3.2 Tool 的三大要素

每个 Tool 必须告诉 LLM 三件事：

```
┌─────────────────────────────────────────────┐
│  Tool 的名字：     "get_weather"              │
│  这个工具是干嘛的：  "查询指定城市的天气"        │
│  需要什么参数：     "需要城市名，类型是字符串"   │
└─────────────────────────────────────────────┘
```

LLM 看到这三个信息，就能决定：

1. "用户问天气 → get_weather 这个工具合适"
2. "用户提到了上海 → 参数 city 应该传'上海'"

### 3.3 代码中的 Tool

在 `tools/weather_tool.py` 中：

```python
class GetWeatherTool(BaseTool):
    # ① 工具名字（LLM 靠这个找到它）
    name = "get_weather"

    # ② 工具描述（LLM 靠这个判断是否该用它）
    description = "查询指定城市和日期的天气情况"

    # ③ 参数说明（LLM 靠这个知道要传什么参数）
    parameters = {
        "type": "object",
        "properties": {
            "city": {
                "type": "string",
                "description": "城市名称"
            }
        },
        "required": ["city"]  # 这个参数必须给
    }

    # ④ 真正的功能代码
    def execute(self, city="北京"):
        # 这里写查天气的真实逻辑
        return f"📍 {city} 天气：15-22°C"
```

### 3.4 灵魂拷问：为什么 LLM 会"知道"该调哪个工具？

这是一个很多人困惑的问题。答案是：

**LLM 在训练时学习过"函数调用"这种能力。**

训练数据里有大量这样的文本：

```
用户问天气 → 调用 get_weather(city) → 得到结果 → 回复用户
```

所以 LLM 学会了：当用户问天气时，我应该输出一个结构化的"工具调用请求"。

具体来说，当 LLM 看到：

```json
{
    "tools": [
        {
            "type": "function",
            "function": {
                "name": "get_weather",
                "description": "查询天气",
                "parameters": {...}
            }
        }
    ]
}
```

它会在内部推理：**"用户需求 ↔ 工具描述"匹配上了 → 我要输出一个 tool_call**

### 3.5 为什么 Tool 的描述这么重要？

因为 LLM 是靠**文字描述**来匹配用户需求和工具的。

坏的描述：

```python
description = "一个工具"
```

→ LLM 不知道什么时候该用它

好的描述：

```python
description = "查询指定城市和日期的天气情况，包括温度、天气状况和穿衣建议"
```

→ LLM 能准确判断：用户问天气 → 用这个工具

### 3.6 我们项目中有哪些 Tool？


| 工具名                 | 功能       | 用在什么时候       |
| ---------------------- | ---------- | ------------------ |
| `get_weather`          | 查天气     | 用户问天气、穿什么 |
| `get_season_advice`    | 季节性提醒 | 用户问某个季节     |
| `get_packing_list`     | 携带清单   | 用户问要带什么     |
| `get_safety_checklist` | 安全检查   | 用户问出门注意什么 |
| `get_today_info`       | 今日信息   | 需要日期信息时     |
| `get_schedule_advice`  | 时段建议   | 用户提到特定时间段 |

---

## 第四章：什么是 MCP（模型上下文协议）？

### 4.1 先理解"协议"是什么

**协议** = 双方约定好的沟通规则。

生活中的协议：

- 你打电话先说"喂" → 对方说"喂" → 这是通话协议
- 你网购 → 下单 → 付款 → 发货 → 这是交易协议

**MCP** 就是 LLM 和 Tool 之间的"通话协议"。

### 4.2 没有 MCP 会怎样？

如果每个项目都自己写一套工具调用逻辑：

```
项目A: LLM → 自己写的函数A → 工具
项目B: LLM → 自己写的函数B → 工具
项目C: LLM → 自己写的函数C → 工具
```

每个项目的写法都不一样，工具不能复用，混乱不堪。

**MCP 就是统一标准**：

```
任何 LLM → [MCP 标准接口] → 任何遵守 MCP 的工具
```

只要工具遵守 MCP 协议，任何支持 MCP 的 LLM 都能直接调用它。

> 就像 USB-C：任何支持 USB-C 的设备，插到任何 USB-C 口上都能用。

### 4.3 MCP 的工作流程

```
LLM 说："我要调 get_weather，参数 city=上海"
    │
    ▼
┌─────────────────────────────────────┐
│  MCP 协议层                          │
│                                      │
│  ① 收到 LLM 的请求                    │
│  ② 解析：要调 get_weather             │
│  ③ 查找：get_weather 注册过吗？       │
│  ④ 路由：找到 GetWeatherTool 这个类   │
│  ⑤ 执行：调用 execute(city="上海")    │
│  ⑥ 返回：标准格式的结果               │
└─────────────────────────────────────┘
    │
    ▼
结果返回给 LLM
```

### 4.4 代码中的 MCP

在 `agent/mcp_protocol.py` 中：

```python
class MCPProtocol:
    def __init__(self):
        self._tools = {}  # 工具注册表

    def register_tool(self, tool):
        """注册工具：把工具加入可用列表"""
        self._tools[tool.name] = tool

    def process_llm_tool_calls(self, tool_calls):
        """
        处理 LLM 发来的工具调用

        tool_calls 是 LLM 返回的"我想调用这些工具"
        格式：[{name: "get_weather", args: {city: "上海"}}, ...]
        """
        for call in tool_calls:
            # ① 从注册表找到对应的工具
            tool = self._tools[call.function.name]

            # ② 解析参数
            arguments = json.loads(call.function.arguments)

            # ③ 执行工具
            result = tool.execute(**arguments)

            # ④ 收集结果
            responses.append(result)

        return responses
```

### 4.5 MCP 中的两个核心数据结构

**请求（MCPRequest）**：

```python
class MCPRequest:
    tool_name: str      # 调哪个工具
    arguments: dict     # 传什么参数
    request_id: str     # 请求编号（用于追踪）
```

**响应（MCPResponse）**：

```python
class MCPResponse:
    success: bool       # 成功还是失败
    data: any           # 返回的数据
    error: str          # 如果失败，错误信息
```

### 4.6 为什么需要 request_id？

因为 LLM 可能**一次性调用多个工具**：

```
LLM 说："我需要同时查天气和查清单"
→ 发出两个请求：
  请求1: get_weather，编号 req_001
  请求2: get_packing_list，编号 req_002
→ 返回两个响应：
  响应1: 编号 req_001，内容是天气数据
  响应2: 编号 req_002，内容是清单数据
```

通过 request_id 能把请求和响应**一一对应**，不会搞混。

---

## 第五章：什么是 Skill（技能）？

### 5.1 从 Tool 到 Skill 的演进

**Tool** 是单个功能：查天气、查清单、查安全...

但真实场景中，**用户一个需求往往需要多个 Tool 配合**：

> 用户说："我要出门了"
>
> 你需要同时：
>
> 1. 查今天日期（GetTodayInfoTool）
> 2. 查天气（GetWeatherTool）
> 3. 查季节性提醒（GetSeasonAdviceTool）
> 4. 生成携带清单（GetPackingListTool）
> 5. 做安全检查（GetSafetyChecklistTool）

**如果让 LLM 每次自己决定调哪个，太慢了。**
**如果让 LLM 自己编排调用顺序，太容易出错。**

**Skill 就是预编排好的"多工具协作方案"**。

### 5.2 比喻理解


| 概念  | 比喻     | 说明                           |
| ----- | -------- | ------------------------------ |
| Tool  | 一根手指 | 只能做单一动作                 |
| Skill | 整只手   | 协调多根手指完成复杂动作       |
| Agent | 整个人   | 用脑（LLM）指挥手（Skill）做事 |

### 5.3 Skill 的预编排逻辑

在 `skills/weather_skill.py` 中：

```python
class WeatherCheckSkill(BaseSkill):
    name = "weather_check"
    description = "综合检查天气、季节、穿衣建议"

    async def execute(self, context):
        tool_executor = context["tool_executor"]

        # ⭐ 这就是"编排"：写死调用顺序
        results = []
        results.append(tool_executor("get_today_info", ...))    # 步骤1
        results.append(tool_executor("get_weather", ...))       # 步骤2
        results.append(tool_executor("get_season_advice", ...)) # 步骤3

        # 组合成一个完整的报告
        return "\n".join(results)
```

这个 Skill 固定了"先查日期 → 再查天气 → 再查季节建议"的顺序，形成一个完整的"天气检查"流程。

### 5.4 Tool vs Skill 对比表


| 对比项       | Tool               | Skill                          |
| ------------ | ------------------ | ------------------------------ |
| **功能**     | 单个原子功能       | 多个功能的组合编排             |
| **调用者**   | LLM 或 Skill 调用  | 被 Agent 或 Skill Manager 调用 |
| **复杂度**   | 简单，一步完成     | 复杂，可能包含循环、条件判断   |
| **可复用性** | 被多个 Skill 复用  | 被 Agent 直接调用              |
| **错误处理** | 工具自身的异常处理 | 可以包含重试、降级等逻辑       |

### 5.5 我们项目中有哪些 Skill？


| 技能名          | 组成                                 | 用途         |
| --------------- | ------------------------------------ | ------------ |
| `weather_check` | today_info + weather + season_advice | 全面检查天气 |
| `packing`       | packing_list + weather               | 生成携带清单 |
| `safety_check`  | safety_checklist + schedule_advice   | 安全检查     |

---

## 第六章：完整工作流程（逐步骤拆解）

这是**最核心的部分**。我们一步一步拆解当你说"我要出门了需要注意什么"时，整个系统内部发生了什么。

### 整体流程概览

```
你 ──①──→ GoingOutAgent.chat()
                │
                ├──②──→ LLM (DeepSeek)
                │           │
                │           ├──③ 决定调用工具
                │           │
                ├──④──→ MCP 协议层
                │           │
                │           ├──⑤ 路由到 Tool
                │           │      ├── get_today_info
                │           │      └── get_weather
                │           │
                ├──⑥──→ LLM 综合结果
                │
                ├──⑦──→ Skill 深度处理
                │
                └──⑧──→ 最终回复
                            │
                            ▼
                        你看到结果
```

### 步骤 ①：用户输入

```
你输入："我要出门了，需要注意什么？"
```

**为什么需要这个步骤？**
这是整个流程的起点。没有用户输入，Agent 就不知道要做什么。

**技术点**：命令行输入（`input()` 函数）

---

### 步骤 ②：LLM 接收消息

```python
# 在 agent/core.py 的 chat 方法中
self.llm.add_message("user", user_input)
```

Agent 把你的话加到"对话历史"里，然后发给 DeepSeek。

**对话历史**长这样：

```json
[
    {"role": "system", "content": "你是出门助手，..."},  // 系统设定（Agent 的人格）
    {"role": "user", "content": "我要出门了，需要注意什么？"}  // 你的问题
]
```

**为什么需要对话历史？**

- LLM 没有记忆，每次调用都是"一次性"的
- 为了让 LLM 记住上下文（比如你之前说了什么），必须把历史对话一起发过去
- 这就是为什么 Agent 能"记得"你刚才说过什么

**为什么需要 system 消息？**

- system 消息告诉 LLM："你现在扮演什么角色"
- 就像给员工发工牌：你现在的身份是"出门助手"，要用助手的语气说话
- 没有 system 消息，LLM 就不知道自己的定位

---

### 步骤 ③：LLM 做决策

```python
response = self.llm.get_chat_completion(tools=tools)
```

这一步把**可用工具列表**也发给 LLM：

```json
[
    {"role": "system", "content": "你是出门助手，..."},
    {"role": "user", "content": "我要出门了，需要注意什么？"},
    // 还附加了 tools 参数：
    "tools": [
        {
            "type": "function",
            "function": {
                "name": "get_weather",
                "description": "查询天气...",
                "parameters": {...}
            }
        },
        // ... 其他工具
    ]
]
```

**DeepSeek 收到后做了什么？**

1. **阅读**你的问题："我要出门了需要注意什么"
2. **理解**你的意图：用户在问出门前的注意事项
3. **思考**：要回答这个问题，我需要知道：
   - 今天是几号（需要调 `get_today_info`）
   - 今天天气如何（需要调 `get_weather`）
   - 有什么季节性的注意事项（需要调 `get_season_advice`）
   - 要带什么东西（需要调 `get_packing_list`）
   - 出门前要检查什么（需要调 `get_safety_checklist`）
4. **决定**：我先调 2 个最重要的工具，其他的让 Skill 去处理

**为什么 LLM 会"思考"这些？**

- LLM 在训练时见过大量"问答+工具调用"的例子
- 它学会了模式：当问题涉及"注意"时，通常需要多个工具配合
- 这不是写死的逻辑，而是 LLM 自己"推理"出来的

**技术点**：Function Calling（函数调用能力）

这是 LLM 的一项核心能力。不是所有 AI 模型都支持，但在 GPT-4、DeepSeek、Claude 等现代模型上都有。

---

### 步骤 ④：LLM 返回 Tool Call

DeepSeek 返回的不是普通文字，而是：

```json
{
    "finish_reason": "tool_calls",
    "message": {
        "content": null,
        "tool_calls": [
            {
                "id": "call_123",
                "type": "function",
                "function": {
                    "name": "get_today_info",
                    "arguments": "{\"detail\": \"full\"}"
                }
            },
            {
                "id": "call_456",
                "type": "function",
                "function": {
                    "name": "get_weather",
                    "arguments": "{\"city\": \"北京\"}"
                }
            }
        ]
    }
}
```

**注意**：`content` 是空的！因为 LLM 决定不直接回复，而是先调工具。

**finish_reason = "tool_calls"** 的意思是：

> "我要说的话还没完，我先调个工具，等结果回来再说。"

---

### 步骤 ⑤：Agent 判断 LLM 要调工具

```python
if choice.finish_reason == "tool_calls" and choice.message.tool_calls:
    # LLM 说：先调工具！
    for call in choice.message.tool_calls:
        print(f"LLM 决定调用: {call.function.name}")
```

**为什么需要这个 if 判断？**
因为 LLM 有两种可能的回复：

1. 直接回复文字（`finish_reason = "stop"`）
2. 要求调工具（`finish_reason = "tool_calls"`）

Agent 必须区分这两种情况，做不同的处理。

---

### 步骤 ⑥：记录 LLM 的工具调用

```python
self.llm.messages.append({
    "role": "assistant",
    "content": "",
    "tool_calls": [...]  # 把 LLM 的工具调用保存到对话历史
})
```

**为什么需要这一步？**

- OpenAI/DeepSeek 的 API 规范要求：tool 消息前面必须有对应的 tool_calls 消息
- 这是协议规定：你说要调工具 → 你确实说了要调工具 → 然后才是工具结果
- 不加这一步，API 会报错

---

### 步骤 ⑦：MCP 协议接收并执行

```python
mcp_responses = self.mcp.process_llm_tool_calls(tool_calls)
```

MCP 协议层做 4 件事：

**① 解析**：从 tool_calls 中提取工具名和参数

```python
tool_name = "get_weather"
arguments = {"city": "北京"}
```

**② 查找**：从注册表找到对应的工具

```python
tool = self._tools["get_weather"]  # 找到 GetWeatherTool 实例
```

**③ 执行**：调用工具的 execute 方法

```python
result = tool.execute(city="北京")
```

**④ 返回**：包装成标准格式

```python
MCPResponse(success=True, data="📍 北京 今日天气：15-22°C...")
```

**为什么需要 MCP 这一层？**

- **解耦**：MCP 把"调用工具"这件事标准化了
- 如果没有 MCP，Agent 要自己写：`if name=="get_weather": tool.execute()` — 写死了，不灵活
- 有了 MCP，Agent 只需要说"执行这个工具"——不管什么工具都能执行
- 加新工具不需要改 Agent 代码，只需要注册到 MCP

---

### 步骤 ⑧：将工具结果送回 LLM

```python
self.llm.add_tool_result(call_id, tool_name, result)
```

对话历史变成了：

```json
[
    {"role": "system", "content": "你是出门助手..."},
    {"role": "user", "content": "我要出门了，需要注意什么？"},
    {"role": "assistant", "content": "", "tool_calls": [...]},
    {"role": "tool", "tool_call_id": "call_123", "content": "📍 北京 今日天气：15-22°C..."},
    {"role": "tool", "tool_call_id": "call_456", "content": "📅 今天是 2026-05-18，星期一"}
]
```

**为什么要把工具结果加回对话？**

- LLM 需要看到工具的结果才能组织语言回复
- 如果 LLM 查到了天气但看不到结果，它还是不知道天气如何
- 把结果加回对话 = 让 LLM 看到工具返回的数据

---

### 步骤 ⑨：LLM 生成最终回复

```python
final_response = self.llm.get_chat_completion()
```

这次 LLM 看到了：

1. 你的问题："我要出门了需要注意什么"
2. 它自己刚才调了哪些工具
3. 工具返回的数据

基于这些信息，它**综合所有数据**生成回复。

**LLM 内部发生的推理**：

```
用户问出门注意什么
→ 我查到了今天天气是 15-22°C，晴转多云
→ 我查到了今天是星期一
→ 周一通常有早高峰
→ 春季早晚温差大
→ 所以回复应该包含：
   • 天气和穿衣建议
   • 早高峰提醒
   • 春季注意事项
```

这次 `finish_reason` 会是 `"stop"`，因为 LLM 不需要再调工具了。

---

### 步骤 ⑩：Skill 深度处理

```python
if self._should_use_skills(user_input, final_content):
    skill_result = await self.skill_manager.auto_select_and_execute(user_input, ...)
    final_content = self._merge_results(final_content, skill_result)
```

**为什么需要 Skill 深度处理？**

- LLM 的回复有时候比较简略
- Skill 可以触发预设的完整检查流程
- 比如 LLM 只说了天气，Skill 可以补充安全检查、携带清单等

**Skill 执行时又做了什么？**

以 `WeatherCheckSkill` 为例：

```python
class WeatherCheckSkill(BaseSkill):
    async def execute(self, context):
        tool_executor = context["tool_executor"]
        results = []

        # 按预设顺序调用工具
        results.append(tool_executor("get_today_info", detail="simple"))
        results.append(tool_executor("get_weather", city=city))
        results.append(tool_executor("get_season_advice", season=season))

        # 组合结果
        return "天气综合报告" + "\n".join(results)
```

它**不需要 LLM 的参与**，直接按照写好的逻辑调用工具、组合结果。

**Skill vs LLM 的区别**：

- LLM 做决策：灵活但慢、贵
- Skill 做编排：固定但快、便宜
- 两者结合：LLM 做核心决策，Skill 做批量执行

---

### 步骤 ⑪：最终回复给用户

```python
print(f"🤖 助手:\n{final_content}")
```

用户看到完整回复：

```
📅 今天是 2026-05-18，星期一
📍 北京：15-22°C，晴转多云
🌤 穿衣建议：带一件薄外套

🎒 携带清单：
   ✅ 手机  ✅ 钥匙  ✅ 钱包  ✅ 口罩

🔑 安全检查：
   ✅ 带钥匙了吗？ ✅ 灯关了吗？ ✅ 门锁好了吗？

🍃 春季提醒：
   • 花粉多，戴口罩
   • 温差大，带外套
   • 随身带伞
```

---

## 第七章：代码逐行解读

这一章我们逐行看最核心的代码，理解每一行在做什么。

### 7.1 config.py - 配置文件

```python
# DeepSeek 的 API 地址
DEEPSEEK_BASE_URL = "https://api.deepseek.com/v1"

# 你的 API Key（就像密码）
DEEPSEEK_API_KEY = "sk-60afd1e3dc244c1f8c7c14bd935474f6"

# 模型名称
DEEPSEEK_MODEL = "deepseek-chat"
```

**每一行的意义**：

- `DEEPSEEK_BASE_URL`：告诉程序 DeepSeek 的服务器在哪
- `DEEPSEEK_API_KEY`：验证身份，证明你有权使用
- `DEEPSEEK_MODEL`：选哪个版本的 DeepSeek（不同版本能力不同）

**为什么要有专门的配置文件？**

- 方便修改：要换 API Key，改一个文件就行
- 安全：不会把密码散落在代码里
- 可配置：想切到 OpenAI，改 3 行就行

---

### 7.2 tools/__init__.py - Tool 基类

```python
class BaseTool:
    name: str = ""              # ① 工具名
    description: str = ""       # ② 描述（LLM 靠这个发现工具）
    parameters: Dict = {}       # ③ 参数定义（JSON Schema）

    def execute(self, **kwargs) -> str:
        """真正的逻辑写在这里"""
        raise NotImplementedError()

    def to_openai_tool_format(self) -> Dict:
        """转成 LLM 能理解的格式"""
        return {
            "type": "function",
            "function": {
                "name": self.name,
                "description": self.description,
                "parameters": self.parameters,
            }
        }
```

**为什么要有抽象基类？**

- 定义一个"工具箱"，所有工具必须遵守这个格式
- 保证所有工具的接口一致（都有 name、description、execute）
- 方便 MCP 统一处理：不管什么工具，都通过 execute 方法调用

**to_openai_tool_format 为什么存在？**

- LLM（DeepSeek）有自己理解工具的格式
- 这个函数把我们的工具"翻译"成 LLM 能理解的格式
- 就像把中文菜单翻译成英文给外国人看

---

### 7.3 agent/llm_client.py - LLM 客户端

```python
class LLMClient:
    def __init__(self):
        # 创建与 DeepSeek 的连接
        self.client = OpenAI(
            api_key=config.DEEPSEEK_API_KEY,   # 用你的 Key
            base_url=config.DEEPSEEK_BASE_URL, # 连 DeepSeek 的服务器
        )
        self.model = config.DEEPSEEK_MODEL      # 用 deepseek-chat 模型
        self.messages = []                       # 对话历史

    def get_chat_completion(self, tools=None, tool_choice=None):
        # 构建消息（system prompt + 对话历史）
        messages = [{"role": "system", "content": "..."}] + self.messages

        kwargs = {
            "model": self.model,
            "messages": messages,
        }

        # 如果有工具，也传过去
        if tools:
            kwargs["tools"] = tools

        # 调用 DeepSeek API
        response = self.client.chat.completions.create(**kwargs)
        return response
```

**为什么用 OpenAI 库来调 DeepSeek？**

- DeepSeek 的 API 兼容 OpenAI 的格式
- 所以 OpenAI 的 Python 库可以直接用来调 DeepSeek
- 这叫"兼容性"——就像你的 Type-C 充电线可以给安卓和苹果用

**messages 参数详解**：

- `system`：告诉 LLM 它的身份和规则（不可见，但 LLM 会遵守）
- `user`：用户说的话
- `assistant`：LLM 之前的回复
- `tool`：工具返回的结果

---

### 7.4 agent/mcp_protocol.py - MCP 协议

```python
class MCPProtocol:
    def __init__(self):
        self._tools = {}  # 工具注册表：{工具名: 工具实例}

    def register_tool(self, tool):
        """注册工具：放入注册表"""
        self._tools[tool.name] = tool

    def process_llm_tool_calls(self, tool_calls):
        """处理 LLM 发来的工具调用"""
        responses = []
        for call in tool_calls:
            if call.type == "function":
                # ① 解析工具名和参数
                tool_name = call.function.name
                arguments = json.loads(call.function.arguments)

                # ② 从注册表找到对应的工具并执行
                tool = self._tools[tool_name]
                result = tool.execute(**arguments)

                responses.append(result)
        return responses

    def get_openai_tools(self):
        """把注册的所有工具转为 LLM 可读的格式"""
        return [tool.to_openai_tool_format() for tool in self._tools.values()]
```

**这段代码的核心思想**：

- `_tools` 字典就像一个**电话本**：名字 → 对应的人
- `register_tool` = 把一个人的电话存进去
- `process_llm_tool_calls` = 有人打电话来说"找张三"，你翻电话本找到张三
- 一切通过名字查询，不需要写 if-else！

---

### 7.5 agent/core.py - Agent 核心

```python
class GoingOutAgent:
    async def chat(self, user_input):
        # ① 记录用户消息
        self.llm.add_message("user", user_input)

        # ② 获取所有工具列表，发给 LLM
        tools = self.mcp.get_openai_tools()
        response = self.llm.get_chat_completion(tools=tools)
        choice = response.choices[0]

        # ③ 判断 LLM 是否要调用工具
        if choice.finish_reason == "tool_calls":
            # ④ 记录 LLM 的 tool_calls
            self.llm.messages.append({
                "role": "assistant",
                "content": "",
                "tool_calls": [...]
            })

            # ⑤ 通过 MCP 执行工具
            mcp_responses = self.mcp.process_llm_tool_calls(tool_calls)

            # ⑥ 将工具结果送回 LLM
            for call, resp in zip(tool_calls, mcp_responses):
                self.llm.add_tool_result(call.id, call.function.name, resp.data)

            # ⑦ LLM 生成最终回复
            final_response = self.llm.get_chat_completion()

        # ⑧ Skill 深度处理
        skill_result = await self.skill_manager.auto_select_and_execute(...)

        return final_content + skill_result
```

**这个方法的 8 个步骤，每一步都不能少：**


| 步骤               | 做什么                      | 为什么不能省                     |
| ------------------ | --------------------------- | -------------------------------- |
| ① 记录消息        | 保存用户输入                | 不保存就没对话上下文             |
| ② 发工具列表      | 告诉 LLM 有什么工具可用     | 不告诉的话 LLM 不知道可以调工具  |
| ③ 判断返回值      | 看 LLM 想直接回复还是调工具 | 不判断就不知道怎么处理           |
| ④ 记录 tool_calls | 满足 API 的格式要求         | 不加这一步 API 报错              |
| ⑤ 执行工具        | 真正干活                    | 不执行就没有数据                 |
| ⑥ 结果送回        | 让 LLM 看到工具返回的数据   | LLM 看不到数据就无法生成准确回复 |
| ⑦ LLM 回复        | 生成最终回答                | 这是用户要看到的东西             |
| ⑧ Skill 处理      | 补充更多深度信息            | 用户得到更全面的回答             |

---

## 第八章：用到的技术和原理

### 8.1 OpenAI API 兼容格式

我们用的 `openai` 库其实是给 OpenAI 的 GPT 模型用的。但 DeepSeek 也支持同样的格式。

**这背后的原理**：

- OpenAI 先定义了"标准"的 API 格式
- 其他公司（DeepSeek、通义千问、文心一言）都按这个格式做兼容
- 所以你用同一个代码，改个 `base_url` 就能切换模型

```
OpenAI 的 API 格式 = 行业标准
    ↑
DeepSeek 兼容这个格式 → 所以我们的代码能用
通义千问 兼容这个格式 → 换 URL 就能用
文心一言 兼容这个格式 → 换 URL 就能用
```

### 8.2 Function Calling（函数调用）

这是 LLM 最核心的能力之一。

**原理**：

1. 你告诉 LLM："有这些函数可以用"（提供 name、description、parameters）
2. LLM 在你的问题中找到线索，匹配到合适的函数
3. LLM 输出一个结构化的"函数调用请求"
4. 你的代码解析这个请求，执行对应的函数

**关键点**：LLM 不是真的"执行"了代码，而是**输出了一个调用请求**。真正的执行是在你的代码里完成的。

```
LLM 输出: {"name": "get_weather", "arguments": "{\"city\": \"北京\"}"}
              ↑
         这不是执行，这是"我希望你帮我执行这个"
              ↓
你的代码: tool.execute(city="北京")  ← 这才是真的执行
```

### 8.3 JSON Schema（参数描述格式）

用来描述"参数长什么样"的格式。

```json
{
    "type": "object",
    "properties": {
        "city": {
            "type": "string",
            "description": "城市名"
        },
        "days": {
            "type": "integer",
            "description": "天数"
        }
    },
    "required": ["city"]
}
```

这告诉 LLM：

- 这个工具的参数应该是一个对象（`"type": "object"`）
- 其中 `city` 是字符串，`days` 是整数
- `city` 是必须的，`days` 是可选的

**为什么需要这个？**

- 没有这个描述，LLM 就不知道该传什么参数
- 有了这个描述，LLM 能生成正确的参数
- 就像点餐时菜单上写了"可选：加辣/不加辣"，顾客才知道怎么选

### 8.4 异步编程（asyncio）

```python
async def chat(self, user_input):
    response = await self.agent.chat(user_input)
```

**为什么要异步？**

- Agent 调用 LLM API 需要等待网络（可能等几秒）
- 同步：等的时候啥也不能干，程序卡住
- 异步：等的时候可以做别的事
- 就像点外卖：同步是你站在店门口干等 30 分钟，异步是你回家干别的事，外卖到了再去拿

### 8.5 设计模式：策略模式

整个项目的架构本质上用的是**策略模式**：

```python
# 不这样写：
if tool_name == "get_weather":
    GetWeatherTool().execute()
elif tool_name == "get_packing_list":
    GetPackingListTool().execute()
# ... 加一个新工具就要加一个 elif

# 而是这样写（策略模式）：
self._tools[tool_name].execute()  # 不管什么工具，统一这样调用
```

**好处**：加新工具不需要改任何 if-else，直接注册就行。

### 8.6 依赖注入

```python
# 不这样写：
class WeatherCheckSkill:
    def execute(self):
        weather = GetWeatherTool().execute()  # 自己创建工具
        # 耦合死了，不好测试

# 而是这样写（依赖注入）：
class WeatherCheckSkill:
    def execute(self, context):
        tool_executor = context["tool_executor"]  # 别人把工具"注入"进来
        weather = tool_executor("get_weather", ...)
```

**好处**：

- 解耦：Skill 不关心工具怎么创建的
- 可测试：测试时可以注入假的工具
- 灵活：可以替换不同的实现

---

## 第九章：自己动手扩展

这一章教你如何在这个项目上自己加功能。

### 9.1 加一个新的 Tool

**目标**：加一个"查询地铁线路"的工具。

**步骤 1**：在 `tools/` 下新建文件 `subway_tool.py`：

```python
from tools import BaseTool

class GetSubwayInfoTool(BaseTool):
    name = "get_subway_info"
    description = "查询城市地铁线路和首末班车时间"

    parameters = {
        "type": "object",
        "properties": {
            "city": {
                "type": "string",
                "description": "城市名"
            },
            "line": {
                "type": "string",
                "description": "地铁线路号，如'1号线'"
            }
        },
        "required": ["city"]
    }

    def execute(self, city="北京", line=""):
        # 这里写查地铁的逻辑
        return f"📍 {city} {line} 首班车 5:30，末班车 23:00"
```

**步骤 2**：在 `main.py` 中注册：

```python
# 导入
from tools.subway_tool import GetSubwayInfoTool

# 注册（加一行）
self.agent.register_tools(
    GetWeatherTool(),
    GetSubwayInfoTool(),  # ← 新加的
    ...
)
```

**完成！** 现在当你问"北京1号线地铁几点开门"时，LLM 会自动调用这个新工具。

**为什么只需要改这两处？**

- 因为 LLM 靠 description 发现工具，不需要改任何调用逻辑
- 因为 MCP 靠注册表调度工具，不需要写 if-else

### 9.2 加一个新的 Skill

**目标**：加一个"约会出门准备"技能。

**步骤 1**：在 `skills/` 下新建文件 `date_skill.py`：

```python
from skills import BaseSkill

class DatePreparationSkill(BaseSkill):
    name = "date_preparation"
    description = "约会出门前的准备建议，包括穿搭、礼物、餐厅建议"
    required_tools = ["get_weather", "get_schedule_advice"]

    async def execute(self, context):
        executor = context["tool_executor"]
        city = context.get("city", "北京")

        results = []
        results.append(executor("get_weather", city=city))
        results.append(executor("get_schedule_advice", time_period="evening"))

        # 约会特别建议
        results.append(
            "💕 约会特别提醒：\n"
            "   • 提前查好餐厅位置和评价\n"
            "   • 注意仪容仪表\n"
            "   • 手机充满电（拍照、导航）\n"
            "   • 准备一个小礼物"
        )

        return "\n\n".join(results)
```

**步骤 2**：在 `main.py` 中注册：

```python
from skills.date_skill import DatePreparationSkill

# 注册
self.agent.register_skills(
    WeatherCheckSkill(),
    DatePreparationSkill(),  # ← 新加的
    ...
)
```

### 9.3 切换其他 LLM

**换成 OpenAI GPT**：

```python
# 在 config.py 中改
DEEPSEEK_API_KEY = "sk-your-openai-key"  # 换成你的 OpenAI Key
DEEPSEEK_BASE_URL = "https://api.openai.com/v1"
DEEPSEEK_MODEL = "gpt-4o"  # 换成 GPT-4o
```

**换成通义千问**：

```python
DEEPSEEK_API_KEY = "sk-your-dashscope-key"  # 阿里云的 API Key
DEEPSEEK_BASE_URL = "https://dashscope.aliyuncs.com/compatible-mode/v1"
DEEPSEEK_MODEL = "qwen-plus"
```

**为什么能这样换？**

- 因为这些模型都支持 OpenAI 兼容格式
- 代码里的 `openai` 库可以连任何兼容的服务器
- 就像 Type-C 充电器可以给任何支持 Type-C 的设备充电

---

## 第十章：常见问题 FAQ

### Q1：LLM 是怎么"知道"该调用哪个工具的？

A：LLM 在训练时学习了"函数调用"这种模式。当你提供工具列表时，LLM 会：

1. 分析用户问题的意图
2. 对比每个工具的 `description`
3. 选择匹配度最高的工具
4. 根据 `parameters` 生成参数

**不是写死的**，而是 LLM 自己推理出来的。

### Q2：为什么 LLM 不直接回复，而是要调工具？

A：因为 LLM 知道自己**没有实时数据**。当问题涉及"现在的天气"、"今天的日期"等实时信息时，LLM 知道自己回答不了，所以选择调工具获取数据。

### Q3：Tool 的参数为什么不直接用 Python 的默认参数，要用 JSON Schema？

A：因为 JSON Schema 是给 LLM"看"的。LLM 不是 Python 解释器，它看不懂 Python 的默认参数语法。JSON Schema 是一种**语言无关的描述格式**，LLM 在训练时学过这种格式。

### Q4：每个用户的问题都会调一遍所有工具吗？

A：不会。LLM 会选择性调用：

- 问天气 → 只调 get_weather
- 问要带什么 → 只调 get_packing_list
- 问出门注意 → 调多个相关工具

这取决于 LLM 的分析结果。

### Q5：为什么需要 MCP？直接调工具不行吗？

A：直接调也可以，但会有这些问题：

- 代码写死：`if name=="get_weather": ... elif name=="get_packing_list": ...`
- 加新工具要改代码
- 不同项目的工具调用方式不统一

MCP 提供了**统一标准**，就像 USB 统一了设备连接方式。

### Q6：Agent 有没有可能调错工具？

A：有可能。如果：

- 工具的 description 写得不好（LLM 理解错了）
- 用户的问题模棱两可
- LLM 本身能力有限

这就是为什么 description 要写得精准，以及为什么需要人工审核。

### Q7：这跟用 ChatGPT 网页版有什么区别？

A：ChatGPT 网页版也是一个 Agent，只是你看不到背后的工具调用：

- 你说"画一张图" → ChatGPT 内部调用了 DALL-E 工具
- 你说"分析这个文件" → ChatGPT 内部调用了文件读取工具
- 你说"搜一下最新新闻" → ChatGPT 内部调用了搜索工具

我们这个项目让你**看到了这一切是怎么发生的**。

### Q8：Skill 和 LLM 自己调工具有什么区别？


|          | LLM 自己调              | Skill 调             |
| -------- | ----------------------- | -------------------- |
| 决策者   | LLM                     | 开发者（你）         |
| 灵活性   | 高，能应对各种情况      | 低，只能做预设好的事 |
| 速度     | 慢（每次要等 LLM 决策） | 快（直接执行代码）   |
| 成本     | 高（每次调 LLM 花钱）   | 低（没有 LLM 调用）  |
| 适用场景 | 核心决策                | 批量执行、固定流程   |

好的做法是两者结合：LLM 做决策，Skill 做执行。

### Q9：为什么我的 API Key 调用失败了？

常见原因：

1. **余额不足**：API Key 要花钱，检查账户余额
2. **Key 写错了**：重新复制确认
3. **网络问题**：国内访问可能需要代理
4. **格式问题**：Key 前面不能有空格

我们的代码有**降级机制**：API 调用失败时自动切换到本地模拟模式，**项目功能不受影响**。

### Q10：对话历史会不会越来越长？会不会太贵？

会。对话历史越长，发给 LLM 的文本越多，费用越高。

解决方法（高级话题）：

1. **滑动窗口**：只保留最近 N 轮对话
2. **摘要压缩**：把旧对话总结成一句话
3. **向量数据库**：用 embedding 检索相关历史

---

## 总结：一张图看懂所有概念的关系

```
┌─────────────────────────────────────────────────────────┐
│                      用户                               │
│                  你问问题 → 得到回答                      │
└────────────────────────┬────────────────────────────────┘
                         │
┌────────────────────────▼────────────────────────────────┐
│  Agent（智能体）                                         │
│  协调所有组件，对外提供服务                                │
│  包含：                                                  │
│    ┌──────────────────────────────────────┐              │
│    │  LLM（大脑）                         │              │
│    │  DeepSeek 理解问题、做决策、组织回复   │              │
│    └──────────────┬───────────────────────┘              │
│                   │                                      │
│    ┌──────────────▼───────────────────────┐              │
│    │  MCP 协议（神经系统）                 │              │
│    │  标准化工具调用，路由请求到对应工具     │              │
│    └──────────────┬───────────────────────┘              │
│                   │                                      │
│    ┌──────────────┴───────────┐                          │
│    │  Tool 层（手指）         │  Skill 层（手掌）        │
│    │  查天气 查清单 查日期    │  天气技能 打包技能 安全技能 │
│    └──────────────────────────┘                          │
└─────────────────────────────────────────────────────────┘
```

**一句话总结**：

> Agent = 一个用 LLM 做大脑、用 MCP 做神经、用 Tool 做手指、用 Skill 做手掌的智能系统。

---

*文档结束。如果看到这里你仍然有疑问，欢迎继续提问！*
