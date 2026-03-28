---
name: plan-first
description: Use before any implementation task that touches 2+ files or multiple layers. Creates a structured plan for user approval.
---

## When to activate

- Task modifies 2+ files
- Task crosses layers (DB + API, API + frontend, etc.)
- Task involves new feature, refactoring, or architectural change
- DO NOT activate if user says to implement directly or task is a single-file fix

## Process

1. **Research** — Read existing code in the affected area. Use Context7 for library docs. Understand current patterns BEFORE proposing anything.

2. **Decompose** — Break the task into subtasks that are:
   - Independent (can be implemented and tested alone)
   - Ordered by dependency (DB first, then API, then frontend)
   - Assigned to a specific agent (backend, frontend)
   - Scoped to specific files (no file shared between agents)

3. **Present plan** with this structure:
   ```
   ## Plan: [title]

   ### Subtask 1: [title]
   - Agent: backend / frontend
   - Files: list of files to create/modify
   - What: description
   - Depends on: subtask N (or "none")

   ### Execution order
   1. [sequential/parallel grouping]

   ### Risks / decisions needed
   - [anything requiring user input]
   ```

4. **Wait for approval** — Do NOT proceed until user approves or requests changes.

5. **Execute** — Spawn agents per the plan. Commit after each logical block is finalized.
