# P2C Agent (Product-to-Code)

> 从产品想法到生产代码 - 基于 Anthropic Long-Running Agents 方法论的全栈开发 Agent 插件

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Version](https://img.shields.io/badge/version-2.1.0-blue.svg)](https://github.com/TeslaZY/product-to-code)

## 概述

P2C Agent (Product-to-Code Agent) 是一个基于 [Anthropic 的 Long-Running Agents 方法论](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents) 构建的 Claude Code 插件。它让 AI 能够跨多个上下文窗口稳定运行，完成完整的软件开发流程：

```
需求调研 → 技术规格 → UI/UX 设计 → 架构规划 → 编码实现 → 测试验证 → 代码审查 → 部署交付
```

**核心理念：** 用户只需说出产品想法，剩下的需求追问、文档生成、原型设计、代码开发就自动完成。

**Long-Running 模式：** 每个会话都能从上一个会话继续工作，通过结构化任务列表和进度文件保持连续性。

## 特性

- 🔄 **Long-Running 架构** - 跨多个上下文窗口稳定运行
- 📋 **任务列表系统** - `task-list.json` 作为唯一真实来源
- 🎯 **7 个精简命令** - 用户只需 `/p2c-agent:project-init` → `/p2c-agent:project-continue` → `/p2c-agent:project-verify`
- 📝 **文档驱动开发** - Spec-Driven Development + 文档同步
- 🔧 **自动依赖管理** - `/p2c-agent:project-init` 时自动检测并引导安装
- 🧪 **验证测试** - 每次开始前验证之前的工作仍然正常

## 安装

在 Claude Code 中执行：
```
# 添加 marketplace
/plugin marketplace add TeslaZY/product-to-code

# 安装插件
/plugin install p2c-agent@product-to-code
```

### 验证安装

在 Claude Code 中，在目标项目目录下执行：
```
/help
```

应看到 7 个命令：`/p2c-agent:project-init`, `/p2c-agent:project-continue`, `/p2c-agent:project-status`, `/p2c-agent:project-tasks`, `/p2c-agent:add-feature`, `/p2c-agent:update-feature`, `/p2c-agent:project-verify`

## 快速开始

### 0-1 模式（新建项目）

在 Claude Code 中执行：
```
/p2c-agent:project-init        # 首次会话：初始化项目、收集需求
/p2c-agent:project-continue    # 后续会话：自动执行下一任务
/p2c-agent:project-continue    # 继续执行...
/p2c-agent:project-verify      # 部署前验收
```

### 迭代模式（修改现有项目）

在 Claude Code 中执行：
```
/p2c-agent:add-feature 添加用户个人资料页面   # 添加新功能
# 或
/p2c-agent:update-feature 修改登录流程           # 修改现有功能

/p2c-agent:project-continue    # 实现新任务
/p2c-agent:project-verify      # 验收
```

## 可用命令

| 命令 | 描述 | 使用时机 |
|------|------|----------|
| `/p2c-agent:project-init` | 初始化项目 + 依赖检测 | 开始新项目 |
| `/p2c-agent:project-continue` | **核心命令** - 继续执行下一任务 | 每个后续会话 |
| `/p2c-agent:project-status` | 查看当前项目进度 | 了解状态 |
| `/p2c-agent:project-tasks` | 列出所有任务和状态 | 查看任务列表 |
| `/p2c-agent:add-feature <描述>` | 添加新功能 | 迭代模式 |
| `/p2c-agent:update-feature <描述>` | 修改现有功能 | 迭代模式 |
| `/p2c-agent:project-verify` | 对照产品文档验收 | 部署前 |

## 依赖管理

运行 `/p2c-agent:project-init` 时会自动检测依赖并引导安装：

- **必需**：Git
- **可选**：uv（Python）、specify-cli（规格驱动开发）
- **插件**：superpowers（开发工作流）、ui-ux-pro（UI 设计）

详见 [docs/DEPENDENCIES.md](docs/DEPENDENCIES.md)

## 任务自动执行流程

`/p2c-agent:project-continue` 根据 `task-list.json` 自动执行对应阶段：

| 阶段 | 任务 ID | 自动调用的技能 |
|------|---------|---------------|
| 1. 需求收集 | req-001~004 | software-requirements-analysis |
| 2. 技术规格 | spec-001~004 | spec-kit |
| 3. UI/UX 设计 | ui-001~002 | ui-prompt-generator |
| 4. 架构规划 | arch-001~004 | spec-kit, superpowers:brainstorming |
| 5. 前端开发 | fe-001+ | ui-ux-pro, superpowers:tdd |
| 6. 后端开发 | be-001+ | superpowers:tdd |
| 7. 测试验证 | test-001+ | superpowers:verification |
| 8. 代码审查 | review-001+ | superpowers:code-review |
| 9. 部署交付 | deploy-001~002 | superpowers |

## 项目结构

```
p2c-agent/
├── CLAUDE.md                    # 项目级上下文（AI 自动加载）
├── agents/
│   └── project_manager.md       # Agent 执行逻辑
├── prompts/                     # 会话提示词
│   ├── initializer-prompt.md    # 首次会话
│   └── coding-agent-prompt.md   # 后续会话
├── commands/                    # 7 个用户命令
├── skills/                      # 核心技能定义
└── docs/                        # 文档
    ├── DEPENDENCIES.md          # 依赖安装说明
    ├── WORKFLOW_DEMO.md         # 完整工作流演示
    └── templates/               # 任务列表 & 进度模板
```

## 核心原则

1. **task-list.json 是真相** - 任务列表是唯一真实来源
2. **每会话一个任务** - 专注完美完成一个任务
3. **永不修改任务** - 只标记 `passes: false` → `passes: true`
4. **干净状态交接** - 每个会话以可提交、可工作的代码结束
5. **记录一切** - `agent-progress.md` 是会话间的记忆

## 文档导航

| 文档 | 内容 |
|------|------|
| [CLAUDE.md](CLAUDE.md) | 项目级上下文、快速参考 |
| [agents/project_manager.md](agents/project_manager.md) | 详细执行逻辑、会话协议 |
| [docs/WORKFLOW_DEMO.md](docs/WORKFLOW_DEMO.md) | 完整工作流演示 |
| [docs/DEPENDENCIES.md](docs/DEPENDENCIES.md) | 依赖安装说明 |

## 参考资料

- [Effective Harnesses for Long-Running Agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents)
- [Claude Quickstarts: Autonomous Coding](https://github.com/anthropics/claude-quickstarts/tree/main/autonomous-coding)
- [superpowers](https://github.com/obra/superpowers) - 开发工作流技能
- [ui-ux-pro](https://github.com/nickg/ui-ux-pro) - UI/UX 设计技能

## License

MIT
