---
name: verification
description: Use after implementation is complete, before declaring any task as done.
---

## Rule

Never declare work as done without fresh evidence.

## Process

1. Run the project's build command — everything must compile
2. Run existing tests in the modified area
3. Read the actual output — don't assume success
4. If build fails, fix and re-run (don't report partial success)
5. Only after green build + passing tests, report completion with evidence

## Forbidden

- "Should work" / "Probably fine" / "I believe this is correct"
- Declaring done without running build
- Skipping test run because "changes are minor"
