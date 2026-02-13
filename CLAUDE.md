# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with this repository.

## Project Overview

**P2C Agent (Product-to-Code)** - 基于 [Anthropic Long-Running Agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents) 方法论的全栈开发插件。

**核心理念：** 用户只需说出产品想法，Agent 自动完成需求追问、文档生成、原型设计、代码开发。

**Long-Running 模式：** 通过 `task-list.json` 和 `agent-progress.md` 跨多个上下文窗口保持连续性。

## Quick Reference

### 7 Commands

| Command | Purpose |
|---------|---------|
| `/p2c-agent:project-init` | Initialize new project |
| `/p2c-agent:project-continue` | **Core** - Resume work on next task |
| `/p2c-agent:project-status` | View current progress |
| `/p2c-agent:project-tasks` | List all tasks |
| `/p2c-agent:add-feature <desc>` | Add new feature |
| `/p2c-agent:update-feature <desc>` | Modify existing feature |
| `/p2c-agent:project-verify` | Verify completeness before deploy |

### Workflow

```
/p2c-agent:project-init → /p2c-agent:project-continue → /p2c-agent:project-continue → ... → /p2c-agent:project-verify → deploy
```

### Mode Detection

| Condition | Mode |
|-----------|------|
| No `task-list.json` | 0-1 Mode (new project) |
| Tasks pending | Continue Mode |
| `Product-Spec.md` exists + new request | Iteration Mode |
| All tasks passing | Complete Mode |

## Plugin Architecture

```
p2c-agent/
├── CLAUDE.md                  # This file (project context)
├── agents/project_manager.md  # Agent execution logic
├── prompts/                   # Session prompts
│   ├── initializer-prompt.md
│   └── coding-agent-prompt.md
├── commands/                  # 7 user commands
├── skills/                    # Core skill definitions
└── docs/                      # Documentation
    ├── DEPENDENCIES.md        # Dependency installation guide
    ├── WORKFLOW_DEMO.md       # Complete workflow demo
    └── templates/             # Task list & progress templates
```

## Key Principles

1. **task-list.json is truth** - Single source of truth for all tasks
2. **One task per session** - Focus on completing one task perfectly
3. **Never modify tasks** - Only mark `passes: false` → `passes: true`
4. **Clean state handoff** - Each session ends with committed, working code
5. **Document everything** - `agent-progress.md` is the memory between sessions

## References

- [Effective Harnesses for Long-Running Agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents)
- [Claude Quickstarts: Autonomous Coding](https://github.com/anthropics/claude-quickstarts/tree/main/autonomous-coding)
- [docs/WORKFLOW_DEMO.md](docs/WORKFLOW_DEMO.md) - Complete workflow example
- [agents/project_manager.md](agents/project_manager.md) - Detailed execution logic
