# Multi-LLM Debugger 🧠⚡

<div align="center">

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![OpenAI](https://img.shields.io/badge/OpenAI-Compatible-00A67E?style=flat&logo=openai&logoColor=white)]()

**面向AI开发者和研究者的多模型并行对话、参数调试与响应对比工具**

[在线演示](#演示) • [功能特性](#-功能特性) • [快速开始](#-快速开始) • [使用指南](#-使用指南) • [API支持](#-支持的api格式)

</div>

---

## 📋 目录

- [项目简介](#-项目简介)
- [功能特性](#-功能特性)
- [技术栈](#-技术栈)
- [快速开始](#-快速开始)
- [使用指南](#-使用指南)
- [支持的API格式](#-支持的api格式)
- [详细配置说明](#-详细配置说明)
- [屏幕截图](#-屏幕截图)
- [浏览器支持](#-浏览器支持)
- [开发计划](#-开发计划)
- [常见问题](#-常见问题)
- [贡献指南](#-贡献指南)
- [许可证](#-许可证)
- [致谢](#-致谢)

---

## 🎯 项目简介

**Multi-LLM Debugger** 是一款专为AI开发者、研究人员和Prompt工程师设计的浏览器端调试工具。它采用高密度信息流的暗色工业风设计，类似专业的交易终端或IDE，让你能够：

- 🔄 **并行对比**：同时向多个模型发送相同请求，直观对比响应差异
- ⚙️ **参数微调**：为每个模型独立配置温度、Top P、Max Tokens等参数
- 🧠 **推理可视化**：支持展示模型的思考过程（Reasoning/Thinking）
- 📊 **性能监控**：实时显示TPS、TTFT、Token消耗等指标
- 🔧 **API调试**：查看完整的请求/响应JSON，方便调试API问题

> 💡 **适用场景**：模型选型对比、Prompt优化、参数调优、API接口调试、性能基准测试

---

## ✨ 功能特性

### 🎨 视觉设计

| 特性 | 描述 |
|------|------|
| **暗色主题** | 深灰/近黑背景，带细微噪点纹理，减少视觉疲劳 |
| **工业风格** | 荧光青绿 (#00FFC8) 主交互色，专业终端面板设计 |
| **字体搭配** | JetBrains Mono（代码/数据）+ Syne（UI界面） |
| **高信息密度** | 紧凑布局，最大化屏幕利用率 |
| **响应式布局** | 大屏并排、小屏堆叠，支持拖拽调整窗口宽度 |

### 🌟 核心功能

#### 1️⃣ 顶部全局配置区
- 🔗 **Base URL** 输入框 - 支持任意 OpenAI-compatible API
- 🔐 **API Key** 输入框 - 带显示/隐藏切换按钮
- 📥 **获取模型列表** - 自动调用 `GET /models` 接口
- 🟢 **连接状态** - 实时显示API连接状态（绿/红指示灯）
- ➕ **添加窗口** - 动态添加对比窗口（最多3个）
- 🐛 **调试模式** - 开启后可在控制台查看详细日志

#### 2️⃣ 多窗口对话区（水平并排）
- 📱 **最多3个独立窗口** - 每个窗口完全独立的对话历史
- 🔄 **独立状态管理** - 各窗口的模型、参数、消息互不干扰
- 📊 **实时对比** - 同时查看多个模型的响应
- 🎯 **模型选择** - 下拉框从获取的模型列表中选择
- ⚙️ **参数面板** - 可折叠的参数配置区域

#### 3️⃣ 丰富的参数配置

| 参数 | 范围 | 说明 |
|------|------|------|
| **Context Turns** | 0-50 | 上下文记忆条数（0表示无限） |
| **Thinking** | ON/OFF | 推理开关（仅支持推理的模型可用） |
| **Thinking Budget** | 1-10000 | 推理预算令牌数 |
| **Max Tokens** | 1-32768 | 最大生成令牌数 |
| **Temperature** | 0.0-2.0 | 随机性控制（滑块+数字输入） |
| **Top P** | 0.0-1.0 | 核采样阈值 |
| **Top K** | 1-200 | Top-K采样 |
| **Repetition Penalty** | 1.0-2.0 | 重复惩罚系数 |
| **System Prompt** | 文本 | 系统提示词 |

#### 4️⃣ 智能消息流展示
- 💬 **三种消息类型**：User（用户）、Assistant（助手）、System（系统）
- 🧠 **推理过程展示**：支持显示模型的思考过程（琥珀黄色调）
- 📝 **流式输出**：实时显示生成进度，打字机效果
- 🎨 **代码高亮**：使用 highlight.js 实现代码块语法高亮
- 📋 **一键复制**：代码块支持一键复制
- 📈 **性能指标**：
  - Tokens：Prompt / Completion / Total
  - TPS（tokens per second）
  - TTFT（Time To First Token）
  - 总耗时

#### 5️⃣ 请求/响应调试器
- 🔍 **完整JSON查看** - 点击 `{ } 查看请求` 查看详情
- 📤 **Request 标签** - 显示本次发送的完整请求体
- 📥 **Response 标签** - 显示原始响应JSON
- ✨ **语法高亮** - JSON格式化并高亮显示
- 📂 **折叠功能** - 可展开/折叠嵌套对象

#### 6️⃣ 全局输入区
- 📝 **多行输入框** - 支持 Shift+Enter 换行
- 📢 **广播发送** - 一键向所有窗口发送相同消息
- 🗑️ **清空对话** - 一键清空所有窗口的对话历史（带二次确认）
- ⏹️ **停止生成** - 使用 AbortController 取消进行中的请求

---

## 🛠️ 技术栈

- **前端框架**：纯原生 JavaScript（无框架依赖）
- **样式方案**：原生 CSS3 + CSS 变量
- **Markdown渲染**：[Marked.js](https://marked.js.org/)
- **代码高亮**：[Highlight.js](https://highlightjs.org/)
- **字体**：
  - [JetBrains Mono](https://www.jetbrains.com/lp/mono/) - 代码展示
  - [Syne](https://fonts.google.com/specimen/Syne) - UI界面
- **API协议**：OpenAI-compatible REST API
- **数据持久化**：localStorage（Base URL、API Key）
- **流式处理**：Fetch API + ReadableStream

---

## 🚀 快速开始

### 方式一：直接打开（推荐）

```bash
# 克隆仓库
git clone https://github.com/yourusername/multi-llm-debugger.git
cd multi-llm-debugger

# 用浏览器打开主文件
open multi-llm-debugger.html
# 或在文件管理器中双击打开
```

### 方式二：本地服务器（如需处理CORS）

```bash
# 使用 Python 3
python -m http.server 8080

# 或使用 Node.js
npx serve .

# 然后访问 http://localhost:8080/multi-llm-debugger.html
```

### 方式三：部署到静态托管

```bash
# 部署到 Vercel
vercel --prod

# 或部署到 Netlify
netlify deploy --prod --dir=.
```

---

## 📖 使用指南

### 第一步：配置API

1. 打开应用后，在顶部配置区输入：
   - **Base URL**: 你的API端点地址
     - OpenAI: `https://api.openai.com/v1`
     - 本地Ollama: `http://localhost:11434/v1`
     - 其他兼容API: 相应地址
   - **API Key**: 你的API密钥

2. 点击 **"获取模型列表"** 按钮
   - 成功后状态指示灯变为绿色
   - 所有窗口的模型下拉框会自动填充可用模型

### 第二步：设置窗口

1. 点击 **"添加窗口"** 按钮（最多3个）
2. 在每个窗口中：
   - 从下拉框选择要测试的模型
   - 点击 **⚙** 按钮展开参数面板
   - 调整 Temperature、Max Tokens 等参数
   - 输入 System Prompt（可选）

### 第三步：开始对话

1. 在底部输入框输入消息
2. 按 **Enter** 发送（Shift+Enter 换行）
3. 观察各窗口的响应：
   - 流式输出实时显示
   - 推理内容（如支持）以琥珀黄展示
   - 性能指标自动计算显示

### 第四步：对比分析

1. 观察不同模型的：
   - 响应质量差异
   - 生成速度（TPS）
   - Token消耗量
   - 推理过程（如开启Thinking）

2. 点击消息旁的 **{ } 查看请求** 可查看：
   - 完整请求JSON
   - 原始响应JSON
   - 便于调试API问题

### 快捷键

| 快捷键 | 功能 |
|--------|------|
| `Enter` | 发送消息 |
| `Shift + Enter` | 输入框换行 |
| `Ctrl/Cmd + Enter` | 发送消息 |

---

## 🔌 支持的API格式

### 标准OpenAI兼容API

```http
GET /models
Authorization: Bearer {api_key}
```

```http
POST /chat/completions
Authorization: Bearer {api_key}
Content-Type: application/json

{
  "model": "gpt-4",
  "messages": [
    {"role": "system", "content": "You are a helpful assistant."},
    {"role": "user", "content": "Hello!"}
  ],
  "stream": true,
  "max_tokens": 2048,
  "temperature": 0.7
}
```

### 已测试的API提供商

| 提供商 | Base URL 示例 | 支持状态 |
|--------|---------------|----------|
| **OpenAI** | `https://api.openai.com/v1` | ✅ 完全支持 |
| **Azure OpenAI** | `https://{resource}.openai.azure.com/openai/deployments/{deployment}` | ✅ 支持 |
| **Ollama** | `http://localhost:11434/v1` | ✅ 支持 |
| **LM Studio** | `http://localhost:1234/v1` | ✅ 支持 |
| **LocalAI** | `http://localhost:8080/v1` | ✅ 支持 |
| **SiliconFlow** | `https://api.siliconflow.cn/v1` | ✅ 支持 |
| **DeepSeek** | `https://api.deepseek.com/v1` | ✅ 支持 |
| **Anthropic (Claude)** | `https://api.anthropic.com/v1` | ⚠️ 需适配 |
| **Google (Gemini)** | `https://generativelanguage.googleapis.com/v1beta` | ⚠️ 需适配 |

### 推理功能支持

以下模型支持展示推理/思考过程：

- ✅ DeepSeek-R1 / DeepSeek-Reasoner
- ✅ OpenAI o1 / o1-preview / o1-mini
- ✅ Claude 3.5 Sonnet / Haiku
- ✅ Qwen 推理系列
- ✅ Llama 推理系列

---

## ⚙️ 详细配置说明

### 参数详解

#### Temperature（温度）
- **范围**: 0.0 - 2.0
- **默认**: 0.7
- **说明**: 控制输出的随机性。值越低，输出越确定；值越高，输出越随机有创意。
- **建议**: 
  - 代码生成/数学题：0.0 - 0.3
  - 对话/翻译：0.7 - 1.0
  - 创意写作：1.0 - 1.5

#### Top P（核采样）
- **范围**: 0.0 - 1.0
- **默认**: 1.0
- **说明**: 与 Temperature 二选一使用。从累积概率达到P的词汇中选择。
- **建议**: 通常保持1.0，或与低Temperature配合使用

#### Max Tokens
- **范围**: 1 - 32768（取决于模型）
- **默认**: 2048
- **说明**: 模型生成的最大令牌数。注意：这不包括输入的token。

#### Context Turns（上下文轮数）
- **范围**: 0 - 50
- **默认**: 10
- **说明**: 保留的对话历史轮数。设为0表示无限上下文（受模型长度限制）。
- **建议**: 根据模型上下文长度和成本考虑设置

#### Thinking / Thinking Budget
- **说明**: 仅部分推理模型支持。
- **Thinking Budget**: 分配给推理过程的token预算。
- **建议**: 复杂问题可设置为1000-4000，简单问题可关闭或设为500。

---

## 📸 屏幕截图

<div align="center">

*主界面 - 三窗口并排对比模式*

*[在此添加截图]*

---

*参数配置面板*

*[在此添加截图]*

---

*请求/响应调试器*

*[在此添加截图]*

</div>

---

## 🌐 浏览器支持

| 浏览器 | 最低版本 | 状态 |
|--------|----------|------|
| Chrome | 89+ | ✅ 完全支持 |
| Firefox | 86+ | ✅ 完全支持 |
| Safari | 14.1+ | ✅ 完全支持 |
| Edge | 89+ | ✅ 完全支持 |
| Opera | 75+ | ✅ 完全支持 |

> ⚠️ **注意**: 建议使用最新版本的浏览器以获得最佳体验。IE浏览器不支持。

---

## 🗺️ 开发计划

### 已实现 ✅
- [x] 多窗口并行对话
- [x] 参数独立配置
- [x] 流式响应展示
- [x] 推理过程可视化
- [x] 性能指标统计
- [x] 请求/响应调试器
- [x] 代码高亮与复制
- [x] 响应式布局
- [x] localStorage持久化

### 计划中 🚧
- [ ] 对话历史导出（JSON/Markdown）
- [ ] 预设参数模板保存/加载
- [ ] 批量测试功能（多Prompt轮询）
- [ ] 结果评分/标记系统
- [ ] 暗黑/亮色主题切换
- [ ] 多语言支持
- [ ] PWA离线支持
- [ ] WebSocket支持
- [ ] 团队协作功能

---

## ❓ 常见问题

### Q: 为什么无法获取模型列表？

**A**: 请检查以下几点：
1. Base URL 是否正确（通常以 `/v1` 结尾）
2. API Key 是否有效且有权限
3. 网络连接是否正常
4. API端点是否支持CORS（跨域）

**解决方案**：
- 打开浏览器开发者工具（F12）查看控制台错误
- 尝试使用本地代理服务器绕过CORS限制
- 确认API提供商的文档，检查是否需要特殊Headers

### Q: 为什么某些模型无法显示推理过程？

**A**: 推理功能需要模型本身支持。目前支持的模型包括：
- DeepSeek-R1 系列
- OpenAI o1 系列
- Claude 3.5 系列

普通模型（如 GPT-4、GPT-3.5）不支持推理过程展示。

### Q: 对话历史会保存吗？

**A**: 
- ❌ 对话历史存储在内存中，刷新页面会丢失
- ✅ Base URL 和 API Key 保存在 localStorage 中
- 💡 计划在未来版本添加导出功能

### Q: 如何支持非OpenAI格式的API？

**A**: 目前仅支持 OpenAI-compatible API。如需使用其他格式（如Anthropic原生API），可以使用适配器服务：
- [LiteLLM](https://github.com/BerriAI/litellm) - 统一的LLM API网关
- [One API](https://github.com/songquanpeng/one-api) - 多模型聚合平台

### Q: 最多支持多少个窗口？

**A**: 目前最多支持 **3个** 并行窗口。这是为了：
- 保证在小屏设备上的可用性
- 控制API并发请求数量
- 保持界面布局的合理性

如需更多窗口，可以复制标签页打开多个实例。

---

## 🤝 贡献指南

我们欢迎各种形式的贡献！

### 提交Bug报告

如果你发现了bug，请通过 [GitHub Issues](https://github.com/yourusername/multi-llm-debugger/issues) 提交，并包含：
- 问题的详细描述
- 复现步骤
- 浏览器版本和操作系统
- 控制台错误信息（如有）

### 功能建议

有新功能想法？欢迎提交 Feature Request：
- 描述功能的使用场景
- 尽可能详细的功能说明
- 如有参考截图更佳

### 代码贡献

1. Fork 本仓库
2. 创建功能分支：`git checkout -b feature/amazing-feature`
3. 提交更改：`git commit -m 'Add amazing feature'`
4. 推送分支：`git push origin feature/amazing-feature`
5. 提交 Pull Request

### 开发规范

- 保持代码简洁，避免引入外部依赖
- 遵循现有代码风格
- 确保在不同浏览器中测试通过
- 更新相关文档

---

## 📄 许可证

本项目采用 [MIT 许可证](LICENSE) 开源。

```
MIT License

Copyright (c) 2024 Multi-LLM Debugger Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

## 🙏 致谢

感谢以下开源项目和资源：

- [Marked.js](https://marked.js.org/) - Markdown渲染引擎
- [Highlight.js](https://highlightjs.org/) - 代码语法高亮
- [JetBrains Mono](https://www.jetbrains.com/lp/mono/) - 优雅的等宽字体
- [Google Fonts](https://fonts.google.com/) - 字体托管服务

特别感谢所有贡献者和用户的支持！

---

<div align="center">

**⭐ 如果这个项目对你有帮助，请给它一个Star！**

[🐛 提交Bug](https://github.com/yourusername/multi-llm-debugger/issues) • [💡 功能建议](https://github.com/yourusername/multi-llm-debugger/issues) • [❤️ 支持项目](#)

</div>
