---
name: execute-plan
description: Structured execution of an approved plan — dispatches agents in batches with checkpoints between each. Use after plan-first produces an approved plan.
---

## When to activate

- A plan from plan-first has been approved by the user
- DO NOT activate without an approved plan
- DO NOT activate if user wants to implement manually

## Process

### 1. Parse the plan

Extract from the approved plan:
- Subtasks with their assigned agents
- Dependencies between subtasks
- Batch grouping (parallel vs sequential)
- Files each agent will touch

### 2. Execute in batches

For each batch in order:

1. **Announce** — Tell the user which batch is starting and what it includes
2. **Dispatch** — Spawn agents for the batch:
   - Independent subtasks in the same batch → dispatch agents **in parallel**
   - Pass each agent: the subtask description, files in scope, and relevant context from previous batches
   - If TDD skill is active: agents follow RED-GREEN-REFACTOR per subtask
3. **Verify batch** — After all agents in the batch complete:
   - Run build — must compile
   - Run tests in affected area — must pass
   - Commit the batch with a descriptive message
4. **Checkpoint** — Present batch results to user:
   ```
   ## Batch N complete

   ### Done
   - Subtask X: [summary of what was implemented]
   - Subtask Y: [summary]

   ### Build: PASS / FAIL
   ### Tests: X passed, Y failed

   ### Next batch
   - Subtask Z: [what's coming]

   Continue? [y / adjust / stop]
   ```
5. **Wait for user** — Do not proceed to next batch without user confirmation

### 3. Handle failures

- **Build fails**: Fix in the current batch before moving on. Do not proceed with broken build.
- **Test fails**: Diagnose and fix. If the fix is outside this batch's scope, flag to user.
- **Agent conflict**: If two agents touched the same file (shouldn't happen with good planning), stop and resolve with user.

## Rules

- Never skip checkpoints. The user must see progress between batches.
- Never proceed past a failing build.
- Each batch should be a coherent, committable unit of work.
- If the plan needs adjustment mid-execution, stop and re-plan with user approval.
