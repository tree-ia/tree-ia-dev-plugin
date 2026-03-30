---
name: finalize
description: Branch completion — final checks, merge/PR decision, and cleanup. Use after code-review and verification are done.
---

## When to activate

- All implementation is complete
- Code review issues are resolved
- Verification skill has passed (build + tests green)
- DO NOT activate if there are unresolved critical/important review findings

## Process

### 1. Final checks

Run one last time:
- Build — must pass
- Full test suite — must pass (not just affected area)
- Check for uncommitted changes — everything should be committed

### 2. Generate summary

```
## Changes summary

### What was done
- [bullet list of changes, grouped by area]

### Files modified
- [list of files with brief description of changes]

### Tests
- X new tests added
- Y existing tests modified
- Full suite: Z passed, 0 failed

### Breaking changes
- [list any breaking changes, or "None"]
```

### 3. Merge decision

Present options to user:

- **Merge to main** — if working in a worktree/feature branch, merge and cleanup
- **Create PR** — generate PR with the summary above as description
- **Keep branch** — leave as-is for further work later

### 4. Execute user's choice

**If merge:**
1. Switch to main branch
2. Merge the feature branch (prefer `--no-ff` for clean history)
3. Run tests on main after merge
4. Remove worktree if applicable: `git worktree remove <path>`
5. Delete feature branch: `git branch -d <branch>`

**If PR:**
1. Push branch to remote
2. Create PR using `gh pr create` with the summary as body
3. Return PR URL to user

**If keep:**
1. Confirm branch name and current state
2. Note any pending work for future sessions

## Rules

- Never merge without user's explicit choice.
- Never force-push or rebase without user approval.
- If tests fail during final checks, go back to fix — don't merge broken code.
- Clean up worktrees after successful merge.
