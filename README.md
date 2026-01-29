# Clawdbot（现已更名为 Moltbot）完整配置指南｜官网地址与核心功能详解

Clawdbot（**现已更名为 Moltbot**）是一个开源的 **本地 AI 智能体（Local AI Agent）** 项目，由 **Peter Steinberger** 发起。  
该项目致力于将 AI 能力深度集成到本地设备中，在保证隐私与可控性的前提下，实现自动化任务执行与多渠道智能交互。

---

## 官方地址与 GitHub

- **最新版官网 & GitHub 地址**  
  👉 [https://github.com/moltbot/moltbot](https://github.com/moltbot/moltbot)

---

## Clawdbot（Moltbot）核心特点与功能

### 1. 本地运行与隐私控制

- Clawdbot 完全运行在本地设备上（如 **Mac、Linux 服务器、树莓派** 等），  
  所有数据、模型配置和记忆均存储在本地，确保用户对数据拥有 **100% 控制权**，  
  避免了云端 AI 服务可能带来的隐私与合规风险。

---

### 2. 多渠道聊天交互

- 支持多种通讯工具作为 AI 交互入口，包括但不限于：
  - WhatsApp
  - Telegram
  - iMessage
  - Slack  

- 用户可在熟悉的聊天界面中直接与 AI 对话，无需额外打开新应用，降低使用门槛。

---

### 3. 强大的任务执行能力

- Clawdbot 不仅是一个聊天机器人，更是具备 **实际操作能力的 AI Agent**，支持：
  - 浏览器自动化操作
  - 文件系统读写
  - 终端命令执行
  - 定时任务与工作流调度

- 可以用来自动完成任务如：
  - 邮件处理
  - 代码调试
  - 网页信息收集
  - 日程与任务管理  

真正实现 **“让 AI 帮你干活”**。

---

### 4. 持久化记忆与主动服务

- 内置的 **记忆系统**（Memory）可以长期保存：
  - 用户偏好
  - 对话历史
  - 任务上下文  

- 支持 **主动式服务**，如：
  - 定期提醒
  - 每日/每周工作简报
  - 系统状态监控
  - 自动化周期任务执行

---

### 5. 模块化架构设计

- Clawdbot 采用高度模块化设计，核心组件包括：
  - **Gateway（网关）**
  - **Agent（智能体）**
  - **Skills（技能模块）**
  - **Memory（记忆系统）**

- 用户可以根据需求扩展技能模块，集成第三方 API、内部系统或专用工具。

---

### 6. 国内用户 API 兼容与 Claude 接入方案（重要）

由于 **国内用户无法直接访问官方 Claude / Anthropic API**，  
可以通过以下开源项目实现兼容接入：

- **Claude Code（国内兼容方案）**  
  👉 [https://github.com/MosesLeopold8/claude-code](https://github.com/MosesLeopold8/claude-code)

---

## Moltbot 国内兼容 API 配置方法（实操）

### 7. 配置步骤说明

> **注：** 若你对步骤熟悉可直接跳过，不懂的请照着下面的步骤操作。本人已亲测，流程正常。

1. **安装步骤**

    运行以下一键安装命令，脚本将自动处理大部分配置：
    
    ```bash
    curl -fsSL https://molt.bot/install.sh | bash
    ```

    等待安装完成并保持网络畅通。

2. **选择模型**

    安装完成后，向导会询问选择的模型提供商：
    - **LLM 提供商**：选择 **Anthropic（Claude）**
    - 输入 **Claude Code** 中转站获取的密钥  
    - 其他配置保持默认。

3. **配置 Telegram 作为消息渠道**

    - **创建 Telegram 机器人**  
      打开 Telegram，搜索 **@BotFather**，发送 `/newbot` 按提示创建一个新机器人，获取 Bot Token。
    - **绑定到 Moltbot**  
      在服务器终端运行以下命令，输入刚刚获取的 Bot Token：
      
      ```bash
      clawdbot channels add telegram
      ```

    - **配对与启动 Gateway**  
      启动 Gateway 后，在 Telegram 机器人发送一条消息，记录下配对码：
      
      ```bash
      clawdbot gateway
      ```
      
      接着运行配对命令，完成配对：
      
      ```bash
      clawdbot pairing approve telegram <配对码>
      ```

4. **修改配置文件**

    配置完成后，编辑配置文件并重启 Moltbot：

    ```bash
    nano ~/.clawdbot/clawdbot.json
    ```

    在 `models` 部分新增以下内容，并替换你的 API 密钥：

    ```json
    "models": {
      "providers": {
        "anthropic": {
          "baseUrl": "https://new.ch-at.pw",
          "apiKey": "你的API密钥",
          "api": "anthropic-messages",
          "models": []
        }
      }
    }
    ```

    修改完成后，重启 Moltbot：

    ```bash
    clawdbot gateway restart
    ```

    现在，你就可以通过 Telegram 与 Moltbot 对话了。

---

## 总结

通过本指南，你可以在本地部署并配置 Moltbot，享受隐私控制、强大任务执行能力及多渠道交互的智能体验。对于国内用户，已提供兼容方案以确保能够顺利使用 Claude 模型。快来体验这一切，让 AI 成为你日常工作的得力助手！
