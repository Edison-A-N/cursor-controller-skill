# Cursor Controller Skill

[![OpenClaw](https://img.shields.io/badge/OpenClaw-Skill-blue)](https://openclaw.ai)
[![GitHub](https://img.shields.io/badge/GitHub-cursor--controller-black?logo=github)](https://github.com/Edison-A-N/cursor-controller)

[English](README.md) | [简体中文](README.zh-CN.md)
> ℹ️ **Important**: This is an OpenClaw Agent **Skill**, not a standalone tool.
> It enables OpenClaw agents to control Cursor AI via the `agent` CLI.
> See [SKILL.md](./SKILL.md) for technical specification.
>
Control Cursor AI agent directly from OpenClaw terminal to write, review, and modify code.

## 🎯 What This Skill Does

This skill enables OpenClaw agents to:
- Control Cursor's AI agent for coding tasks
- Perform code review and security analysis via Cursor
- Run automated code modifications and refactoring
- Integrate Cursor into CI/CD pipelines
- Continue previous Cursor sessions
- Push tasks to Cursor Cloud Agent

## 📦 Installation

### Prerequisites

Before using this skill, you need to install the Cursor CLI:

```bash
# macOS / Linux / WSL
curl https://cursor.com/install -fsS | bash

# Windows PowerShell
irm 'https://cursor.com/install?win32=true' | iex
```

Verify installation:
```bash
agent --version
```

### Install This Skill

**Option 1: Project Level** (recommended for team projects)

```bash
cd your-project
mkdir -p .openclaw/skills/cursor-controller
curl -L https://raw.githubusercontent.com/Edison-A-N/cursor-controller-skill/master/SKILL.md \
  -o .openclaw/skills/cursor-controller/SKILL.md
```

**Option 2: Global Level** (available in all projects)

```bash
mkdir -p ~/.config/openclaw/skills/cursor-controller
curl -L https://raw.githubusercontent.com/Edison-A-N/cursor-controller-skill/master/SKILL.md \
  -o ~/.config/openclaw/skills/cursor-controller/SKILL.md
```

**Option 3: Clone Repository**

```bash
git clone https://github.com/Edison-A-N/cursor-controller-skill.git
cd cursor-controller-skill

# Install to project
mkdir -p /path/to/your/project/.openclaw/skills/cursor-controller
cp SKILL.md /path/to/your/project/.openclaw/skills/cursor-controller/

# Or install globally
mkdir -p ~/.config/openclaw/skills/cursor-controller
cp SKILL.md ~/.config/openclaw/skills/cursor-controller/
```

## 🚀 Quick Start

Once installed, start using Cursor agent from OpenClaw:

```bash
# Interactive mode
agent

# Run a specific task
agent -p "refactor auth module to use JWT"

# Review code
agent -p "review src/ for security issues" --output-format text

# Continue a previous session
agent resume
```
## 🔐 Authentication

Before using Cursor agent, you need to authenticate. Cursor CLI supports two methods:

### Browser Authentication (Recommended)

The easiest way to authenticate using your browser:

```bash
# Log in using browser flow
agent login

# Check authentication status
agent status

# Log out and clear stored authentication
agent logout
```

The `agent login` command will open your default browser and prompt you to authenticate with your Cursor account. Once completed, your credentials are securely stored locally.

### API Key Authentication

For automation, scripts, or CI/CD environments, use API key authentication:

1. **Generate an API key** in your Cursor dashboard under **Integrations > User API Keys**

2. **Set the API key** using one of these methods:

**Option 1: Environment variable (recommended)**
```bash
export CURSOR_API_KEY=your_api_key_here
agent "implement user authentication"
```

**Option 2: Command line flag**
```bash
agent --api-key your_api_key_here "implement user authentication"
```

### Troubleshooting

- **"Not authenticated" errors:** Run `agent login` or ensure your API key is correctly set
- **SSL certificate errors:** Use the `--insecure` flag for development environments
- **Endpoint issues:** Use the `--endpoint` flag to specify a custom API endpoint

---

## 📖 Common Use Cases

### Code Tasks
```bash
agent -p "refactor src/auth.ts to use async/await"
agent -p "add unit tests for utils module"
agent -p "fix memory leak in worker.js"
agent -p "optimize database queries"
```

### Code Review
```bash
agent -p "review git diff for issues" --output-format text
agent -p "review src/api/*.ts for best practices"
agent -p "scan codebase for security vulnerabilities" --output-format text
```

### CI/CD Integration
```bash
# Review PR changes
agent -p "review current git diff for issues" --output-format text

# Check code quality
agent -p "check code style and best practices" --output-format text
```

## 🔧 Modes

| Mode | Description | Command |
|------|-------------|---------|
| **Agent** | Full access for complex coding | Default (no flag) |
| **Plan** | Design approach first | `--plan` or `/plan` |
| **Ask** | Read-only exploration | `--mode=ask` or `/ask` |

```bash
# Plan mode
agent --plan "migrate to TypeScript"

# Ask mode (read-only)
agent --mode=ask "explain this codebase"
```

## ☁️ Cloud Agent

Push tasks to Cursor Cloud Agent to continue running while away:

```bash
# Start in cloud mode
agent -c "refactor auth module and add tests"

# Or use & prefix in interactive mode
& refactor the auth module
```

Access Cloud Agent tasks at: https://cursor.com/agents

## 📝 Sessions

Resume previous conversations to maintain context:

```bash
# List all previous chats
agent ls

# Resume latest conversation
agent resume

# Resume specific conversation
agent --resume="chat-id-here"
```

## 📚 Documentation

- [Cursor CLI Documentation](https://cursor.com/docs/cli/overview)
- [OpenClaw Skills](https://openclaw.ai/docs/skills/)

## 🤝 Contributing

Contributions are welcome! Please feel free to submit issues or pull requests.

## 📄 License

MIT License - feel free to use in personal and commercial projects.

---

**Note**: This is an OpenClaw Agent Skill. Make sure you have OpenClaw installed to use it.
