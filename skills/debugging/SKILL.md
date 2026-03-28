---
name: debugging
description: Use when investigating bugs, errors, or unexpected behavior. Systematic root-cause analysis before any fix.
---

## Phase 1: Investigate (no code changes)

1. Read the error message carefully — full stack trace
2. Reproduce: understand the exact conditions
3. Trace backward through the call stack to the original trigger
4. Check recent changes (`git log`, `git diff`)
5. Find working examples of similar code in the codebase

## Phase 2: Hypothesize

- Form ONE hypothesis about the root cause
- Find evidence for or against
- If disproven, form next hypothesis
- Do NOT guess-and-fix multiple things simultaneously

## Phase 3: Fix

1. Implement the minimal fix
2. Verify it resolves the issue
3. Run full build to check for regressions

## Rules

- 3+ failed fix attempts: stop. Question your assumptions, not the symptom.
- Never patch symptoms. Fix the root cause.
- If the bug is in unfamiliar code, read the surrounding context first.
