---
name: cursor-controller
description: "Control Cursor AI agent via CLI to write, review, and modify code. Use when: user wants to use Cursor's AI agent for coding tasks, code review, or automation. NOT for: manual Cursor editor usage, non-Cursor AI tools, or GUI-only operations. Requires 'agent' CLI to be installed."
homepage: https://cursor.com/docs/cli/overview
metadata:
  {
    "openclaw":
      {
        "emoji": "🎯",
        "os": ["darwin", "linux", "win32"],
        "requires": { "bins": ["agent"] },
        "install":
          [
            {
              "id": "cursor-macos-linux",
              "kind": "shell",
              "command": "curl https://cursor.com/install -fsS | bash",
              "bins": ["agent"],
              "label": "Install Cursor CLI (macOS/Linux)",
            },
            {
              "id": "cursor-windows",
              "kind": "shell",
              "command": "irm 'https://cursor.com/install?win32=true' | iex",
              "bins": ["agent"],
              "label": "Install Cursor CLI (Windows PowerShell)",
            },
          ],
      },
  }
---

# Cursor Controller

Control Cursor's AI agent directly from the terminal to write, review, and modify code.

## When to Use

✅ **USE this skill when:**

- User wants to use Cursor's AI agent for coding tasks
- Code review and security analysis via Cursor
- Automated code modifications and refactoring
- Running Cursor in CI/CD pipelines or scripts
- Continuing previous Cursor sessions
- Cloud Agent tasks that run while away

❌ **DON'T use this skill when:**

- Manual GUI editor usage is needed → open Cursor app directly
- Using other AI tools (Claude Code, Codex, etc.)
- Tasks requiring IDE-specific features (debugger, etc.)

## Installation

```bash
# macOS / Linux / WSL
curl https://cursor.com/install -fsS | bash

# Windows PowerShell
irm 'https://cursor.com/install?win32=true' | iex
```

## Basic Usage

### Interactive Mode

Start a conversational session with the agent:

```bash
# Start interactive session
agent

# Start with initial prompt
agent "refactor the auth module to use JWT tokens"
```

### Non-Interactive Mode (Print Mode)

For scripts, CI pipelines, or automation:

```bash
# Run with specific prompt
agent -p "find and fix performance issues"

# Use specific model
agent -p "optimize database queries" --model "gpt-5.2"

# Output as text for piping
agent -p "review these changes" --output-format text
```

## Modes

Switch between modes using flags or slash commands:

| Mode      | Description                                           | Flag/Command                         |
| :-------- | :---------------------------------------------------- | :----------------------------------- |
| **Agent** | Full access to all tools for complex coding tasks     | Default (no `--mode` value)          |
| **Plan**  | Design approach before coding with clarifying questions | `--plan`, `--mode=plan`, `/plan`     |
| **Ask**   | Read-only exploration without making changes          | `--mode=ask`, `/ask`                 |

```bash
# Start in Plan mode
agent --plan "migrate to TypeScript"

# Start in Ask mode (read-only)
agent --mode=ask "explain this codebase"
```

## Sessions

Resume previous conversations to maintain context:

```bash
# List all previous chats
agent ls

# Resume latest conversation
agent resume

# Continue the previous session
agent --continue

# Resume specific conversation
agent --resume="chat-id-here"
```

## Cloud Agent

Push tasks to Cloud Agent to continue running while you're away:

```bash
# Start in cloud mode
agent -c "refactor the auth module and add comprehensive tests"

# Send a task to Cloud Agent mid-conversation
# (Use & prefix in interactive mode)
& refactor the auth module and add comprehensive tests
```

Access Cloud Agent tasks at: https://cursor.com/agents

## Common Commands

### Code Tasks

```bash
# Refactor code
agent -p "refactor src/auth.ts to use async/await"

# Add tests
agent -p "add unit tests for the utils module"

# Fix bugs
agent -p "fix the memory leak in worker.js"

# Optimize performance
agent -p "optimize the database query in models.py"
```

### Code Review

```bash
# Review with git changes included
agent -p "review these changes for security issues" --output-format text

# Review specific files
agent -p "review src/api/*.ts for best practices"
```

### Documentation

```bash
# Generate documentation
agent -p "generate JSDoc for all public functions in src/"

# Update README
agent -p "update README.md with new installation steps"
```

## Advanced Options

### Sandbox Controls

Configure command execution settings:

```bash
# Disable sandbox (allow all commands)
agent --sandbox disabled "run npm install"

# Enable sandbox (default)
agent --sandbox enabled "run npm install"

# Toggle in interactive mode
/sandbox
```

### Max Mode

Toggle Max Mode on supported models:

```bash
# Enable Max Mode
agent --max-mode "complex architecture design"

# Toggle in interactive mode
/max-mode on
```

### Model Selection

```bash
# Use specific model
agent -p "task" --model "gpt-5.2"

# Use specific model
agent -p "task" --model "claude-3-5-sonnet"
```

## Workflows

### CI/CD Integration

```bash
# Review PR changes
agent -p "review the current git diff for issues" --output-format text

# Check for security issues
agent -p "scan codebase for security vulnerabilities" --output-format text

# Verify code quality
agent -p "check code style and best practices" --output-format text
```

### Batch Processing

```bash
# Process multiple files
for file in src/*.ts; do
  agent -p "add error handling to $file" --output-format text
done
```

### Session-Based Workflow

```bash
# Start a session for a complex task
agent "implement user authentication"

# Later, resume the same session
agent --continue

# Or list and pick a specific session
agent ls
agent --resume="auth-implementation-abc123"
```

## Notes

- **Sudo password prompting**: Cursor displays secure masked prompts for `sudo` commands. Password flows directly to `sudo` via secure IPC; AI never sees it.
- **Output formats**: Use `--output-format text` for non-interactive/scripting scenarios
- **Rate limits**: Be mindful of API rate limits when running automated tasks
- **Context**: Sessions maintain context across interactions; use `--continue` or `agent resume` to preserve context
- **Cloud Agent**: Tasks pushed with `-c` or `&` run on Cursor's cloud infrastructure
