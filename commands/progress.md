---
description: Show current project progress and status
---

Check for Product-Spec.md existence and display the current development phase.
- If Product-Spec.md doesn't exist: Project not started, suggest /new
- If Product-Spec.md exists but no UI-Prompts.md: Requirements complete, suggest /ui
- If UI-Prompts.md exists but no code: Design phase, suggest /design
- If code exists: Development in progress, suggest /develop or /test
