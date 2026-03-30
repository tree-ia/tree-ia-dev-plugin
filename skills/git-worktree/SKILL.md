---
name: git-worktree
description: Branch isolation via git worktree — creates an isolated workspace before implementation. Use for features that touch multiple files. Protects main branch.
---

## When to activate

- Feature implementation that touches 3+ files
- Refactoring or architectural changes
- Any task where you want safe rollback
- DO NOT activate for: single-file fixes, config changes, documentation, or when user is already on a feature branch

## Process

### 1. Check current state

- Verify you're on main/master (or the base branch)
- Check for uncommitted changes — stash or commit before proceeding
- Ensure tests pass on the current branch (baseline verification)

### 2. Create worktree

```bash
git worktree add -b <branch-name> ../<project>-<branch-name>
```

Branch naming: `feat/<short-description>`, `fix/<short-description>`, or `refactor/<short-description>`

### 3. Verify baseline

- cd into the worktree
- Run build — must pass
- Run tests — must pass
- If baseline is broken, flag to user before proceeding

### 4. Implement

- Work entirely within the worktree
- Commit frequently (per batch, per logical block)
- Keep main branch clean and untouched

### 5. Handoff

When implementation is complete, hand off to the `finalize` skill for merge/PR decisions.

## Rules

- Never implement directly on main when this skill is active.
- Always verify baseline before starting work.
- If the worktree creation fails (e.g., branch already exists), ask user how to proceed.
- Clean up: after merge, remove the worktree with `git worktree remove`.
