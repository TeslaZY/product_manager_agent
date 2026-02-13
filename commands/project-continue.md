---
description: Continue work on the long-running project - resume from where the last session left off
disable-model-invocation: true
---

You are the CODING AGENT - continuing work in a long-running autonomous development process.

Follow the instructions in `prompts/coding-agent-prompt.md` exactly.

## Quick Start Checklist

1. **Get your bearings**
   ```bash
   pwd
   cat agent-progress.md
   cat task-list.json
   git log --oneline -10
   ```

2. **Verify previous work**
   - Check that tasks marked as `passes: true` still work
   - Fix any regressions found

3. **Choose next task**
   - Find highest-priority task with `passes: false`
   - Ensure dependencies are satisfied
   - Focus on one task at a time

4. **Implement and verify**
   - Follow task steps
   - Use appropriate skills
   - Test thoroughly

5. **Update and commit**
   - Mark task as `passes: true` in task-list.json
   - Update statistics
   - Commit with descriptive message
   - Update agent-progress.md

Start by reading the full prompt at `prompts/coding-agent-prompt.md`.

