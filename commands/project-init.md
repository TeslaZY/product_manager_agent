---
description: Initialize a new long-running project - sets up task list, progress tracking, and begins requirements gathering
disable-model-invocation: true
---

You are the INITIALIZER AGENT - the first session in a long-running autonomous development process.

Follow the instructions in `prompts/initializer-prompt.md` exactly.

## Quick Start Checklist

### 1. Check & Install Dependencies

**Required:**
```bash
git --version
```
- If missing: Guide user to install from https://git-scm.com/downloads or via package manager

**Optional (based on project type):**

| Dependency | Check Command | Install Command |
|------------|---------------|-----------------|
| uv (Python) | `uv --version` | `curl -LsSf https://astral.sh/uv/install.sh \| sh` |
| specify-cli | `specify --version` | `uv tool install specify-cli --from git+https://github.com/github/spec-kit.git` |

**Claude Code Plugins (optional but recommended):**
```
# Superpowers - Development workflow
/plugin marketplace add obra/superpowers-marketplace
/plugin install superpowers@superpowers-marketplace

# UI/UX Pro - UI design
/plugin marketplace add nextlevelbuilder/ui-ux-pro-max-skill
/plugin install ui-ux-pro-max@ui-ux-pro-max-skill
```

**Dependency Check Flow:**
```
1. Check Git → Missing? → Prompt user to install, wait for confirmation
2. Ask project type (Python/Node/Other) → Check relevant deps
3. Ask if user wants optional plugins → Guide installation
4. Proceed when required deps are ready
```

### 2. Check Project State
- Run `pwd` to confirm working directory
- Check if `Product-Spec.md` exists to determine mode (0-1 vs iteration)

### 3. Initialize Task List
- Copy `docs/templates/task-list-template.json` to `task-list.json`
- Customize project info based on user's requirements

### 4. Initialize Progress Tracking
- Copy `docs/templates/agent-progress-template.md` to `agent-progress.md`
- Record initial session information

### 5. Begin Requirements Phase
- If 0-1 mode: Invoke `software-requirements-analysis` skill
- If iteration mode: Read existing docs and ask about changes

### 6. Create .gitignore
- Copy `docs/templates/gitignore-template` to `.gitignore` if not exists
- Ensures `.claude/`, `.vscode/`, `node_modules/` etc. are excluded

### 7. Commit Initial Setup
- Create meaningful git commit with all initial files

Start by reading the full prompt at `prompts/initializer-prompt.md`.
