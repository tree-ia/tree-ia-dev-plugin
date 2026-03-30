---
name: verification
description: Use after implementation is complete, before declaring any task as done.
---

## Rule

Never declare work as done without fresh evidence.

## Process

1. Run the project's build command — everything must compile
2. Run the **full test suite** (not just the modified area) — all must pass
3. Read the actual output — don't assume success
4. If build or tests fail, fix and re-run (don't report partial success)
5. **Plan compliance** — if a plan was approved, verify all subtasks were implemented
6. **Test coverage** — if the project has coverage tooling configured, run it and report:
   - Coverage of new/modified code
   - Any uncovered branches in critical paths
   - Do NOT enforce arbitrary thresholds — report the numbers, user decides
7. Only after all checks pass, report completion with evidence:
   ```
   ## Verification: PASS

   - Build: OK
   - Tests: X passed, 0 failed
   - Coverage: Y% on new code (if available)
   - Plan compliance: all N subtasks implemented (if plan exists)
   ```

## Forbidden

- "Should work" / "Probably fine" / "I believe this is correct"
- Declaring done without running build
- Skipping test run because "changes are minor"
- Running only affected tests — run the full suite
