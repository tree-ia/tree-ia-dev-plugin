---
name: code-review
description: Structured code review cycle — spec compliance check, quality review, and feedback incorporation. Use after implementation, before finalize.
---

## When to activate

- After execute-plan completes all batches
- After manual implementation of a planned task
- When user explicitly requests a review
- DO NOT activate for trivial single-file changes unless requested

## Process

### Phase 1: Spec compliance

Check implementation against the approved plan:

- [ ] All planned subtasks are implemented
- [ ] Files listed in the plan were modified (no missing pieces)
- [ ] No unplanned files were modified (scope creep)
- [ ] Behavior matches what was specified
- [ ] Edge cases from the plan are handled

Output:
```
## Spec compliance: PASS / PARTIAL / FAIL
- [x] Subtask 1: implemented as planned
- [ ] Subtask 2: missing validation on X
- [!] Unplanned: file Y was modified outside plan scope
```

### Phase 2: Code quality

Review all changed files for:

- **Logic**: correctness, edge cases, error handling
- **Patterns**: consistency with existing codebase conventions
- **Types**: no `any`, proper null checks, safe casts
- **Performance**: N+1 queries, unnecessary re-renders, missing indexes
- **Security**: injection, auth bypass, exposed secrets (defer to security agent for deep audit)
- **Tests**: coverage of new behavior, test quality

Output by severity:
```
## Code quality

### CRITICAL
- file:line — [issue] — [why it matters]

### IMPORTANT
- file:line — [issue] — [recommendation]

### MINOR
- file:line — [suggestion]
```

### Phase 3: Feedback incorporation

1. Present combined findings (spec + quality) to user
2. User decides which items to fix
3. Agents apply the approved fixes
4. Re-run affected tests to verify fixes don't break anything
5. If new issues are introduced by fixes, flag immediately

## Rules

- Phase 1 is skipped if there was no plan (ad-hoc implementation).
- Never auto-fix without user approval — present findings first.
- Focus on substance, not style. Don't nitpick formatting if the project has no linter.
- If the QA agent already ran, reference its findings instead of duplicating work.
