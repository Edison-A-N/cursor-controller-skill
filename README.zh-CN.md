# Cursor Controller Skill

[![OpenClaw](https://img.shields.io/badge/OpenClaw-Skill-blue)](https://openclaw.ai)
[![GitHub](https://img.shields.io/badge/GitHub-cursor--controller-black?logo=github)](https://github.com/Edison-A-N/cursor-controller)

[English](README.md) | [简体中文](README.zh-CN.md)
> ℹ️ **重要提示**：这是一个 OpenClaw Agent **Skill**，不是独立工具。
> 它让 OpenClaw agent 可以通过 `agent` CLI 控制 Cursor AI。
> 技术规范请参阅 [SKILL.md](./SKILL.md)。
>

从 OpenClaw 终端直接控制 Cursor AI agent，进行代码编写、审查和修改。

## 🎯 功能介绍

此 Skill 让 OpenClaw agent 能够：
- 控制 Cursor 的 AI agent 完成编码任务
- 通过 Cursor 执行代码审查和安全分析
- 运行自动化代码修改和重构
- 将 Cursor 集成到 CI/CD 流水线
- 继续之前的 Cursor 会话
- 推送任务到 Cursor Cloud Agent

## 📦 安装

### 前置条件

使用此 Skill 前，需要先安装 Cursor CLI：

```bash
# macOS / Linux / WSL
curl https://cursor.com/install -fsS | bash

# Windows PowerShell
irm 'https://cursor.com/install?win32=true' | iex
```

验证安装：
```bash
agent --version
```

### 安装此 Skill
> **注意**：此 Skill 是一个纯文档包。安装它意味着将 `SKILL.md` 文件复制到你的 OpenClaw skills 目录。实际功能需要单独安装 [Cursor CLI](https://cursor.com/docs/cli/overview)（`agent` 命令）。


**选项 1：项目级别安装**（推荐用于团队项目）

```bash
cd your-project
mkdir -p .openclaw/skills/cursor-controller
curl -L https://raw.githubusercontent.com/Edison-A-N/cursor-controller/master/SKILL.md \
  -o .openclaw/skills/cursor-controller/SKILL.md
```

**选项 2：全局级别安装**（所有项目可用）

```bash
mkdir -p ~/.config/openclaw/skills/cursor-controller
curl -L https://raw.githubusercontent.com/Edison-A-N/cursor-controller/master/SKILL.md \
  -o ~/.config/openclaw/skills/cursor-controller/SKILL.md
```

**选项 3：克隆仓库**

```bash
git clone https://github.com/Edison-A-N/cursor-controller.git
cd cursor-controller

# 安装到项目
mkdir -p /path/to/your/project/.openclaw/skills/cursor-controller
cp SKILL.md /path/to/your/project/.openclaw/skills/cursor-controller/

# 或全局安装
mkdir -p ~/.config/openclaw/skills/cursor-controller
cp SKILL.md ~/.config/openclaw/skills/cursor-controller/
```

## 🚀 快速开始

安装完成后，当你已经安装了 [Cursor CLI](https://cursor.com/docs/cli/overview)（`agent` 命令），就可以从 OpenClaw 启动 Cursor agent：

```bash
# 交互模式
agent

# 执行特定任务
agent -p "refactor auth module to use JWT"

# 代码审查
agent -p "review src/ for security issues" --output-format text

# 继续之前的会话
agent resume
```
## 🔐 认证

使用 Cursor agent 之前，需要先完成认证。Cursor CLI 支持两种认证方式：

### 浏览器认证（推荐）

最简单的认证方式，使用浏览器完成登录：

```bash
# 使用浏览器流程登录
agent login

# 检查认证状态
agent status

# 退出登录并清除本地存储的认证信息
agent logout
```

`agent login` 命令会打开默认浏览器，提示你使用 Cursor 账号登录。完成后，你的凭证会安全地存储在本地。

### API Key 认证

适用于自动化脚本、CI/CD 环境等场景：

1. **生成 API Key**：在 Cursor Dashboard 的 **Integrations > User API Keys** 页面创建

2. **设置 API Key**，有以下两种方式：

**方式一：环境变量（推荐）**
```bash
export CURSOR_API_KEY=your_api_key_here
agent "implement user authentication"
```

**方式二：命令行参数**
```bash
agent --api-key your_api_key_here "implement user authentication"
```

### 故障排除

- **"Not authenticated" 错误**：运行 `agent login` 或检查 API Key 是否正确设置
- **SSL 证书错误**：开发环境可使用 `--insecure` 参数
- **端点问题**：使用 `--endpoint` 参数指定自定义 API 端点

---

## 📖 常见用例

### 代码任务
```bash
agent -p "refactor src/auth.ts to use async/await"
agent -p "add unit tests for utils module"
agent -p "fix memory leak in worker.js"
agent -p "optimize database queries"
```

### 代码审查
```bash
agent -p "review git diff for issues" --output-format text
agent -p "review src/api/*.ts for best practices"
agent -p "scan codebase for security vulnerabilities" --output-format text
```

### CI/CD 集成
```bash
# 审查 PR 变更
agent -p "review current git diff for issues" --output-format text

# 检查代码质量
agent -p "check code style and best practices" --output-format text
```

## 🔧 工作模式

| 模式 | 描述 | 命令 |
|------|------|------|
| **Agent** | 完整权限，适合复杂编码 | 默认（无 flag） |
| **Plan** | 先设计方案，带有澄清问题 | `--plan` 或 `/plan` |
| **Ask** | 只读模式，不做修改 | `--mode=ask` 或 `/ask` |

```bash
# Plan 模式
agent --plan "migrate to TypeScript"

# Ask 模式（只读）
agent --mode=ask "explain this codebase"
```

## 🔧 高级功能

### 沙盒模式

控制命令执行安全性：
```bash
# 禁用沙盒（允许所有命令）
agent --sandbox disabled "run npm install"

# 在交互模式中切换
/sandbox
```

### Max 模式

为复杂任务启用最大 token 使用量：
```bash
# 启用 Max 模式
agent --max-mode "complex architecture design"

# 在交互模式中切换
/max-mode on
```

### 模型选择

为你的任务选择特定模型：
```bash
# 使用特定模型
agent -p "task" --model "gpt-5.2"
agent -p "task" --model "claude-3-5-sonnet"
```

### 批处理

循环处理多个文件：
```bash
# 处理多个文件
for file in src/*.ts; do
  agent -p "add error handling to $file" --output-format text
done
```

## ☁️ Cloud Agent

将任务推送到 Cursor Cloud Agent，离开后仍可继续运行：

```bash
# 启动 cloud 模式
agent -c "refactor auth module and add tests"

# 或在交互模式中使用 & 前缀
& refactor the auth module
```

访问 Cloud Agent 任务：https://cursor.com/agents

## 📝 会话管理

恢复之前的对话以保持上下文：

```bash
# 列出所有历史对话
agent ls

# 恢复最近对话
agent resume

# 恢复特定对话
agent --resume="chat-id-here"
```

## 📚 文档

- [Cursor CLI 文档](https://cursor.com/docs/cli/overview)
- [OpenClaw Skills](https://openclaw.ai/docs/skills/)

## ⚠️ 安全与注意事项

### 安全说明

Cursor 会为 `sudo` 命令显示安全掩码提示。密码通过安全 IPC 直接流向 `sudo`；AI 永远不会看到它。

### 速率限制

运行自动化任务时请注意 API 速率限制。

## 🤝 贡献

欢迎提交 issues 或 pull requests！

## 📄 许可证

MIT 许可证 - 可自由用于个人和商业项目。

---

**注意**：这是一个 OpenClaw Agent Skill。使用前请确保已安装 OpenClaw。
