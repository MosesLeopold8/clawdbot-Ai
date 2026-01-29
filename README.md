# Clawdbot（Moltbot）完整配置指南｜官网地址与核心功能详解

Clawdbot（**现已更名为 Moltbot**）是一个开源的 **本地 AI 智能体（Local AI Agent）** 项目，由 **Peter Steinberger** 发起。  
该项目致力于将 AI 能力深度集成到本地设备中，在保证隐私与可控性的前提下，实现自动化任务执行与多渠道智能交互。

---

## Clawdbot / Moltbot 官方地址

- **最新版官网 & GitHub 地址**  
  👉 https://github.com/moltbot/moltbot

---

## Clawdbot（Moltbot）核心特点与功能

### 1. 本地运行与隐私控制

Clawdbot 完全运行在用户本地设备上（如 **Mac、Linux 服务器、树莓派** 等），  
所有数据、模型配置和记忆均存储在本地，用户对数据拥有 **100% 控制权**，有效避免云端 AI 服务可能带来的隐私与合规风险。

---

### 2. 多渠道聊天交互

支持将常用通讯工具作为 AI 交互入口，包括但不限于：

- WhatsApp  
- Telegram  
- iMessage  
- Slack  

用户可直接在熟悉的聊天界面中与 AI 对话，无需额外打开新应用，极大降低使用门槛。

---

### 3. 强大的任务执行能力

Clawdbot 不只是“聊天机器人”，而是具备 **实际动手能力的 AI Agent**，支持：

- 浏览器自动化操作  
- 文件系统读写  
- 终端命令执行  
- 定时任务与工作流调度  

可用于自动完成：

- 邮件处理  
- 代码调试  
- 网页信息调研  
- 日程与任务管理  

真正实现 **“让 AI 帮你干活”**。

---

### 4. 持久化记忆与主动服务

内置记忆系统（Memory），可长期保存：

- 用户偏好  
- 对话历史  
- 任务上下文  

并支持 **主动式服务**，例如：

- 定期提醒  
- 每日 / 每周工作简报  
- 系统状态监控  
- 自动化周期任务执行  

---

### 5. 模块化架构设计

Clawdbot 采用高度模块化设计，核心组件包括：

- **Gateway（网关）**  
- **Agent（智能体）**  
- **Skills（技能模块）**  
- **Memory（记忆系统）**

用户可按需扩展技能，例如集成第三方 API、内部系统或专用工具。

---

### 6. 国内用户 API 兼容与 Claude 接入方案（重要）

针对 **国内用户无法直接访问官方 Claude / Anthropic API** 的问题，可通过以下开源项目实现兼容接入：

- **Claude Code（国内兼容方案）**  
  👉 https://github.com/MosesLeopold8/claude-code

## 国内用户 Claude API 兼容方案（重点）

### 6. Claude API 国内可用方案（Claude Code）

由于国内网络环境限制，无法直连 Anthropic 官方 API，  
可使用以下开源项目进行兼容接入：

- **Claude Code（国内 Claude API 兼容项目）**  
  👉 https://github.com/MosesLeopold8/claude-code

该方案可作为 **Moltbot / Clawdbot 的 LLM 后端**，  
实现 Claude 模型在国内环境下的稳定调用。

---

## Moltbot 国内兼容 API 配置方法（实操）

### 7. 配置步骤说明（懂的直接上，不懂照着来）

#### 步骤 1：进入 Moltbot 根目录

- 文件方式：直接打开 Moltbot 项目根目录  
- 终端方式（推荐）：

```bash
cd moltbot
用终端 + vim / nano / VS Code 编辑，懂的都懂 😄

步骤 2：进入 .moltbot 隐藏目录
在项目 root 目录 下，找到并进入：

text
复制代码
.moltbot/
步骤 3：编辑 moltbot.json 配置文件
路径如下：

text
复制代码
.moltbot/moltbot.json
如果你在初始化时已经配置过模型，这个文件中会存在
agents 和 models 字段。

步骤 4：替换 Anthropic / Claude API 配置
在 models（或已有 anthropic 配置段）中，
将内容替换为以下示例：

json
复制代码
"anthropic": {
  "baseUrl": "https://new.ch-at.pw/v1",
  "apiKey": "你的API密钥",
  "api": "anthropic-messages"
}
📌 字段说明：

baseUrl：Claude Code 提供的国内可访问 API 地址

apiKey：你在 Claude Code / 中转服务中获取的密钥

api：使用 Anthropic 官方 messages 接口规范

步骤 5：保存并重启 Moltbot
保存 moltbot.json 后，重启 Moltbot 服务即可生效。


该项目通过中转与适配方式，使本地 AI Agent（如 Clawdbot / Moltbot）  
能够在国内环境下正常调用 **Claude 模型 API**，常见使用场景包括：

- 作为 Moltbot 的 LLM 后端  
- 替代官方 Claude API 直连  
- 与本地代理、环境变量配置结合使用  

⚠️ **使用建议**：

- 注意 API Key 与代理地址的安全管理  
- 避免在公网暴露未鉴权接口  
- 优先在本地或内网环境中部署测试  

---

### 7. 开源可定制，社区生态活跃

- 项目 **完全开源**，支持自由修改与二次开发  
- 社区提供大量教程、插件与实践案例  
- 适合开发者、极客及企业进行深度定制  

⚠️ **安全提示**：  
由于 Clawdbot 拥有较高系统权限，建议：

- 在独立设备或沙盒环境中运行  
- 合理配置权限与安全策略  
- 避免直接在生产主机上开放高危能力  

---

## 适合人群

- 本地 AI Agent / AutoGPT 类工具爱好者  
- 自动化与效率工具开发者  
- 注重数据隐私的个人与团队  
- 希望在国内稳定使用 Claude / 大模型的高级用户  

---

