# Demo: P2C Agent Workflow

This document demonstrates the complete workflow of the P2C Agent plugin.

## Scenario

We'll simulate building a simple **Todo App** from scratch.

---

## Session 1: Project Initialization

### User Action
```
/p2c-agent:project-init
```

### What Happens

1. **Dependency Check & Installation**

Agent checks and guides dependency installation:

```
Agent: Checking required dependencies...
$ git --version
git version 2.42.0 ✓

Agent: What type of project are you building?
1. Python backend
2. Node.js frontend
3. Other

User: 2

Agent: Checking Node.js dependencies...
$ node --version
v20.10.0 ✓

Agent: Would you like to install optional plugins?
- superpowers (Development workflow - TDD, debugging)
- ui-ux-pro (UI/UX design intelligence)

User: Yes, both please.

Agent: Run these commands to install:
/plugin marketplace add obra/superpowers-marketplace
/plugin install superpowers@superpowers-marketplace

/plugin marketplace add nextlevelbuilder/ui-ux-pro-max-skill
/plugin install ui-ux-pro-max@ui-ux-pro-max-skill

Let me know when done or skip to continue.
```

2. **Project State Detection**
```
Checking project state...
- task-list.json: NOT FOUND → 0-1 Mode
- Product-Spec.md: NOT FOUND → Starting fresh
```

3. **Task List Creation**

Creates `task-list.json` with:
```json
{
  "project_info": {
    "name": "Todo App",
    "description": "A simple task management application",
    "created_at": "2024-01-15T10:00:00Z",
    "tech_stack": {}
  },
  "statistics": {
    "total_tasks": 22,
    "completed_tasks": 0,
    "pending_tasks": 22
  },
  "phases": [...]
}
```

4. **Requirements Gathering**

Agent invokes `software-requirements-analysis` skill:
```
Agent: Tell me about your product idea. What problem does it solve?

User: I want a simple todo app to track my daily tasks.

Agent: Specific question: Who are the primary users? Just you, or a team?

User: Just personal use.

Agent: What happens when you complete a task? Does it disappear or stay visible?

User: I want completed tasks to stay visible but be crossed out.

Agent: Do you need to categorize or tag tasks?

User: Yes, I want to organize by projects like "Work", "Personal", "Shopping".

Agent: About priorities - how do you want to mark task importance?

User: High, Medium, Low priority levels.

... (more questions)
```

5. **Document Generation**

Creates:
- `Product-Spec.md` - Complete product specification
- `Product-Spec-CHANGELOG.md` - Version history (v0.1.0)

6. **First Commit**
```bash
$ git add .
$ git commit -m "Initial setup: Todo App project structure

- Created task-list.json with 22 tasks across 9 phases
- Generated Product-Spec.md
- Generated Product-Spec-CHANGELOG.md (v0.1.0)
"
```

### Session 1 End State
- Phase 1 (Requirements): 4/4 tasks completed
- Phase 2-9: pending
- Next: `/p2c-agent:project-continue` to start Technical Specification

---

## Session 2: Technical Specification

### User Action
```
/p2c-agent:project-continue
```

### What Happens

1. **Get Bearings**
```
Reading agent-progress.md...
Last session: Initialized project, completed requirements phase.

Reading task-list.json...
- Total: 22 tasks
- Completed: 4 (req-001 to req-004)
- Pending: 18

Checking git log...
eb0b886 Initial setup: Todo App project structure
```

2. **Verification Test**
```
Verifying Product-Spec.md exists... ✓
Verifying requirements are documented... ✓
All previous work validated successfully.
```

3. **Next Task Selection**
```
Finding next task...
- spec-001: Establish project constitution (priority: high, dependencies: req-004 ✓)
- Selected: spec-001
```

4. **Implementation**

Agent uses `spec-kit` skill to create:
- `.specify/memory/constitution.md` - Project principles

5. **Continue to spec-002, spec-003, spec-004**
```
Creating technical specifications...
- specs/add-todo/spec.md
- specs/complete-todo/spec.md
- specs/categorize-todo/spec.md
```

### Session 2 End State
- Phase 1: completed
- Phase 2: completed (4/4)
- Phase 3-9: pending
- Next: `/p2c-agent:project-continue` for UI/UX Design

---

## Session 3: UI/UX Design

### User Action
```
/p2c-agent:project-continue
```

### What Happens

1. **Generate UI Prompts**

Agent uses `ui-prompt-generator` skill:
```
Analyzing Product-Spec.md...
Generating UI prompts for:
- Main todo list view
- Add task modal
- Project sidebar
- Settings page

Created UI-Prompts.md
```

2. **User Reviews Prototypes**

```
Agent: I've generated UI prompts in UI-Prompts.md. You can use these with Midjourney, Gemini, or DALL-E.

User: [Uses prompts with external tool, gets prototype images]

User: The prototypes look good. Let's proceed with the dark theme version.

Agent: Documenting design decision. Marking ui-002 as complete.
```

### Session 3 End State
- Phase 1-2: completed
- Phase 3: completed (2/2)
- Phase 4-9: pending
- Next: `/p2c-agent:project-continue` for Architecture Planning

---

## Session 4: Architecture & Frontend

### User Action
```
/p2c-agent:project-continue
```

### What Happens

Agent continues through:
- Phase 4: Creates implementation plan
- Phase 5: Sets up React + Vite project, builds components

### Session 4 End State
- Phase 1-5: completed
- Phase 6-9: pending

---

## Session 5: Backend & Testing

### User Action
```
/p2c-agent:project-continue
```

### What Happens

- Phase 6: Sets up Node.js backend with Express
- Phase 7: Writes unit tests and E2E tests

---

## Session 6: Review & Deploy

### User Action
```
/p2c-agent:project-continue
```

Then:
```
/p2c-agent:project-verify
```

### What Happens

1. **Code Review**
```
Reviewing implementation against Product-Spec.md...

✓ All features implemented
✓ Test coverage: 85%
✓ No critical issues
⚠ Minor: Consider adding loading states

Report saved to review-report.md

2. **Final Audit**
```

2. **Final Audit**

```
╔══════════════════════════════════════════════════════════════╗
║                      AUDIT RESULTS                           ║
╠══════════════════════════════════════════════════════════════╣
║ Project: Todo App                                            ║
║ Version: v1.0.0                                              ║
║                                                              ║
║ Features: 6 total, 6 complete, 0 partial, 0 missing          ║
║ Tests: All passing                                           ║
║ Build: Success                                               ║
║                                                              ║
║ Issues: Critical: 0 | High: 0 | Medium: 1 | Low: 2          ║
║                                                              ║
║ Deployment: READY                                            ║
╚══════════════════════════════════════════════════════════════╝

Feature Checklist:
- [✓] Add task functionality
- [✓] Complete task functionality
- [✓] Categorize by project
- [✓] Priority levels
- [✓] Dark theme
- [✓] Responsive design

Detailed report saved to: audit-report.md
```

3. **Deployment**
```
Preparing for deployment...
- Building production bundle
- Running final tests
- Deploying to Vercel

Deployed successfully!
```

---

## Iteration Mode: Adding a Feature

### Scenario

After deployment, user wants to add a "Due Date" feature.

### User Action
```
/p2c-agent:add-feature Add due date to tasks
```

### What Happens

1. **Requirements Collection**
```
Agent: I understand you want to add due dates. Some questions:
- Should overdue tasks be highlighted?
- Do you want reminders/notifications?
- How should due dates be displayed in the list?
```

2. **New Tasks Added**

Updates `task-list.json`:
```json
{
  "id": "fe-new-001",
  "category": "frontend",
  "description": "Add due date picker to task form",
  "dependencies": ["fe-002"],
  ...
},
{
  "id": "be-new-001",
  "category": "backend",
  "description": "Add due date field to task model",
  "dependencies": ["be-001"],
  ...
}
```

3. **Statistics Updated**
```json
"statistics": {
  "total_tasks": 24,
  "completed_tasks": 22,
  "pending_tasks": 2
}
```

4. **Continue Development**
```
User: /p2c-agent:project-continue
Agent: Working on be-new-001: Add due date field to task model...
```

---

## Iteration Mode: Modifying a Feature

### Scenario

User wants to change the login flow to add 2FA.

### User Action
```
/p2c-agent:update-feature Add 2FA to login flow
```

### What Happens

1. **Requirements Collection**
```
Agent: I understand you want to modify the login flow. Some questions:
- What type of 2FA? (TOTP, SMS, Email)
- Should 2FA be optional or required?
- Do you need backup codes?
```

2. **New Modification Tasks Added**

Updates `task-list.json`:
```json
{
  "id": "fe-002-modify-001",
  "category": "frontend",
  "description": "Modify login flow to add 2FA",
  "dependencies": ["fe-002"],
  "modifies": "fe-002",
  ...
},
{
  "id": "be-001-modify-001",
  "category": "backend",
  "description": "Add 2FA verification to login API",
  "dependencies": ["be-001"],
  "modifies": "be-001",
  ...
}
```

---

## Summary

| Phase | Tasks | Sessions |
|-------|-------|----------|
| 1. Requirements | 4 | 1 |
| 2. Specification | 4 | 1 |
| 3. UI/UX Design | 2 | 1 |
| 4. Architecture | 4 | 1 |
| 5. Frontend | 2 | 1 |
| 6. Backend | 1 | 1 |
| 7. Testing | 2 | 1 |
| 8. Review | 1 | 1 |
| 9. Deployment | 2 | 1 |
| **Total** | **22** | **~9 sessions** |

---

## Key Commands Used

| Command | When | Result |
|---------|------|--------|
| `/p2c-agent:project-init` | Session 1 | Initialized project, checked deps, created task list |
| `/p2c-agent:project-continue` | Sessions 2-6 | Executed next task in sequence |
| `/p2c-agent:project-status` | Any time | Viewed current status |
| `/p2c-agent:project-tasks` | Any time | Listed all tasks |
| `/p2c-agent:add-feature` | Iteration | Added new feature tasks |
| `/p2c-agent:update-feature` | Iteration | Added modification tasks |
| `/p2c-agent:project-verify` | Before deploy | Verified completeness with detailed report |

---

## Files Created During Workflow

```
todo-app/
├── task-list.json              # Task tracking
├── agent-progress.md           # Session history
├── Product-Spec.md             # Product specification
├── Product-Spec-CHANGELOG.md   # Version history
├── UI-Prompts.md               # UI generation prompts
├── audit-report.md             # Final audit report (generated by /audit)
├── .specify/
│   └── memory/
│       └── constitution.md     # Project principles
├── specs/
│   ├── add-todo/
│   │   ├── spec.md
│   │   └── plan.md
│   ├── complete-todo/
│   │   └── spec.md
│   └── ...
├── src/                        # Frontend code
├── server/                     # Backend code
└── tests/                      # Test files
```
