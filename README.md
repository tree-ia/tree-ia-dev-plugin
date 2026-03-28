# tree-dev

Structured development workflow plugin for Claude Code — agents, skills and hooks for multi-layer projects.

## What's included

### Agents (4)

| Agent | Role |
|-------|------|
| `researcher` | Deeply investigates a domain before planning. Read-only. |
| `backend` | Implements server-side code. Adapts to project stack. |
| `frontend` | Implements client-side code. Adapts to project stack. |
| `qa` | Reviews code, runs build/tests, validates against plan. Read-only. |

### Skills (5)

| Skill | When to use |
|-------|-------------|
| `brainstorm` | Requirements are vague or multiple approaches exist |
| `plan-first` | Task touches 2+ files or crosses layers |
| `verification` | Before declaring any task as done |
| `debugging` | Investigating bugs or unexpected behavior |
| `security-audit` | Code handles auth, payments, user data, or APIs |

### Hooks (1)

- **SessionStart** — Injects discipline rules on every session start, `/clear`, and `/compact`

## Install

### From marketplace

```bash
/plugin marketplace add tree-ia/tree-ia-dev-plugin
/plugin install tree-dev@tree-ia/tree-ia-dev-plugin
```

### Local development

```bash
claude --plugin-dir /path/to/tree-ia-dev-plugin
```

## Workflow

```
Task received
    │
    ├─ Ambiguous? → brainstorm skill → refine scope
    │
    ├─ Need research? → researcher agent → expert knowledge
    │
    ▼
plan-first skill → decompose into subtasks
    │
    ▼
User approves plan
    │
    ▼
backend + frontend agents (parallel when possible)
    │
    ├─ commits per logical block
    │
    ▼
qa agent → build + review + plan compliance
    │
    ▼
verification skill → evidence-based completion
```

## Design principles

- **Agents adapt to the project** — they read CLAUDE.md first, no hardcoded stack
- **File ownership** — backend and frontend never touch each other's files
- **Read-only review** — researcher and qa agents cannot edit files
- **Plan before code** — unless explicitly told to implement directly
- **Evidence over claims** — build must pass before declaring done

## License

MIT
