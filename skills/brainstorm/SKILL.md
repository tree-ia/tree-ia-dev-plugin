---
name: brainstorm
description: Use when task is ambiguous, has multiple possible approaches, or requirements need refinement before planning.
---

## When to activate

- Requirements are vague or incomplete
- Multiple valid approaches exist and it's unclear which is best
- Task impacts architecture or multiple systems
- You're unsure about constraints, edge cases, or scope
- DO NOT activate for well-defined tasks with clear requirements

## Process

1. **Understand** — Research the codebase area affected. Read existing code.

2. **Ask** — Present 3-5 clarifying questions about:
   - Scope: what's in, what's explicitly out
   - Constraints: performance, compatibility, deadlines
   - Preferences: approach A vs B, tradeoffs the user cares about

3. **Explore** — After answers, present:
   ```
   ## Possible approaches

   ### Option A: [name]
   - How: [summary]
   - Pros: ...
   - Cons: ...

   ### Option B: [name]
   - How: [summary]
   - Pros: ...
   - Cons: ...

   ### Recommendation: [A or B] because [reason]
   ```

4. **Refine** — User picks or adjusts. Iterate if needed.

5. **Handoff** — Once scope is clear, activate plan-first skill.
