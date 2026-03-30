---
name: tdd
description: Test-Driven Development — enforces RED-GREEN-REFACTOR cycle. Use when implementing new features or fixing bugs where tests are possible.
---

## When to activate

- New feature implementation (not a quick config change)
- Bug fix where the bug can be reproduced with a test
- Refactoring that changes behavior
- DO NOT activate if: project has no test infrastructure, task is purely config/docs, or user explicitly says to skip tests

## First step — always

Read the project's CLAUDE.md to identify:
- Test framework (Jest, Vitest, Mocha, pytest, Go test, etc.)
- Test commands (`npm test`, `pnpm test`, etc.)
- Test file conventions (`.test.ts`, `.spec.ts`, `__tests__/`, etc.)
- Existing test patterns (read 1-2 existing test files to match style)

## The cycle: RED → GREEN → REFACTOR

### RED — Write a failing test first

1. Write a test that describes the expected behavior
2. Run it — it **must fail**. If it passes, the test is wrong or the feature already exists
3. The failure message should clearly describe what's missing

### GREEN — Implement the minimum to pass

1. Write the **minimal** code that makes the test pass
2. Run the test — it **must pass** now
3. Do not add extra functionality beyond what the test requires
4. Run the full test suite in the affected area — no regressions

### REFACTOR — Clean up while green

1. Improve code quality: remove duplication, improve naming, simplify logic
2. Run tests after each refactor step — they must stay green
3. Do not change behavior — only structure
4. Commit when the refactor is clean

## Rules

- One test at a time. Don't write 10 tests then implement all at once.
- Test behavior, not implementation. Tests should survive refactoring.
- If you can't write a test first, explain why and get user approval to skip.
- Match the project's existing test patterns — don't introduce a new style.
- Integration tests over mocks when the project favors real dependencies.
- After the full cycle: run the complete test suite, not just the new test.

## Edge cases

- **No test infrastructure**: Flag it. Ask user if they want to set it up or skip TDD.
- **Legacy code without tests**: Write a characterization test first (captures current behavior), then proceed with RED-GREEN-REFACTOR for the change.
- **UI components**: Use the project's testing approach (React Testing Library, Expo testing, etc.). If none exists, focus on logic tests over visual tests.
