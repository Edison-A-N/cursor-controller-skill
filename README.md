# Cursor Controller Skill

[![OpenClaw](https://img.shields.io/badge/OpenClaw-Skill-blue)](https://openclaw.ai)
[![GitHub](https://img.shields.io/badge/GitHub-cursor--controller-black?logo=github)](https://github.com/Edison-A-N/cursor-controller-skill)

[English](README.md) | [简体中文](README.zh-CN.md)

> ℹ️ **Important**: This is an OpenClaw Agent **Skill**, not a standalone tool.
> It enables OpenClaw agents to control Cursor AI via the `agent` CLI.

Control Cursor's AI agent directly from the terminal to write, review, and modify code.

## 📦 Installation

### Prerequisites

Install the Cursor CLI (`agent` command):

```bash
# macOS / Linux / WSL
curl https://cursor.com/install -fsS | bash

# Windows PowerShell
irm 'https://cursor.com/install?win32=true' | iex
```

### Install This Skill

> **Note**: This Skill is a documentation-only package. The actual functionality requires [Cursor CLI](https://cursor.com/docs/cli/overview) to be installed separately.

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

## 🚀 Quick Start

```bash
# Run a specific task
agent -p "refactor auth module to use JWT"

# Review code
agent -p "review src/ for security issues" --output-format text

# Continue a previous session
agent resume
```

## 📚 Full Documentation

For complete documentation including:
- Authentication (browser login & API keys)
- All modes (Agent, Plan, Ask)
- Sessions and Cloud Agent
- CI/CD integration
- Advanced features

**See [SKILL.md](./SKILL.md)**

## 📄 License

MIT License - feel free to use in personal and commercial projects.

---

**Note**: This is an OpenClaw Agent Skill. Make sure you have OpenClaw installed to use it.
