---
name: finish-branch
description: Use when implementation is complete, all tests pass, and you need to decide how to integrate the work.
---

# Finishing a Development Branch

## Overview

Complete development work by verifying everything works, presenting structured options, and executing the chosen path.

**Announce at start:** "I'm using the finish-branch skill to complete this work."

## Step 1: Final Verification

Before presenting options, verify:

- [ ] All tests pass
- [ ] Lint/typecheck passes (if applicable)
- [ ] No uncommitted changes
- [ ] Branch is up to date with main

## Step 2: Present Options

Present 3 completion paths:

**Option 1: Merge to main**
```bash
git checkout main
git pull
git merge <branch>
git push
```

**Option 2: Create Pull Request**
```bash
git push -u origin <branch>
# Create PR via gh CLI or GitHub UI
```

**Option 3: Clean up only**
```bash
# Keep branch locally, just verify state
git status
```

## Step 3: Execute Choice

After user chooses:

1. Confirm the action
2. Execute step-by-step
3. Verify result
4. Report completion

## Decision Matrix

| Scenario | Recommended |
|----------|-------------|
| Simple change, tests pass | Merge to main |
| Complex change, needs review | Create PR |
| Experimental/WIP | Clean up only |

## Post-Completion

After merging/PR:
- Delete local branch (optional)
- Update documentation if needed
- Mark tasks as complete in todo list

## Remember
- Never force push to main
- Always verify tests pass before merging
- Clean working directory before switching branches
