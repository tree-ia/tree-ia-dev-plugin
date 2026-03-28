# tree-dev

A Claude Code plugin that brings structure and discipline to your development workflow. It provides specialized agents, reusable skills, and session hooks — all stack-agnostic. Agents read your project's `CLAUDE.md` and adapt automatically.

Built by [Tree IA](https://tree.ia.br).

## Why

Claude Code is powerful but defaults to jumping straight into implementation. This plugin enforces a **research → plan → implement → review** cycle through agents with clear boundaries and skills that gate each phase. The result: fewer wasted tokens, cleaner code, and better architectural decisions.

## What's included

### Agents

| Agent | Model | Role | Edits files? |
|-------|-------|------|:------------:|
| `researcher` | Opus | Deeply investigates a domain, technology, or architecture area before planning | No |
| `backend` | Opus | Implements server-side code — APIs, services, database, queues | Yes |
| `frontend` | Opus | Implements client-side code — pages, components, styles, UI | Yes |
| `security` | Opus | Audits code for vulnerabilities, auth flaws, data exposure, and attack surfaces | No |
| `qa` | Opus | Runs build, tests, reviews code quality, validates against plan | No |

- **researcher**, **security**, and **qa** are read-only by design — they analyze and report, they don't write code.
- **backend** and **frontend** have strict file ownership — they never touch each other's files.
- All agents start by reading the project's `CLAUDE.md` to adapt to the stack.

### Skills

| Skill | Trigger |
|-------|---------|
| `brainstorm` | Requirements are vague, multiple approaches exist, or scope needs refinement |
| `plan-first` | Task touches 2+ files or crosses layers (DB, API, frontend) |
| `verification` | Before declaring any task as done — requires fresh build/test evidence |
| `debugging` | Investigating bugs or unexpected behavior — systematic root-cause analysis |
| `security-audit` | Code handles auth, payments, user data, or exposes API endpoints |

### Hooks

- **SessionStart** — Injects discipline rules on every session start, `/clear`, and `/compact`:
  1. Research the codebase before implementing
  2. Be direct — no filler, no post-action summaries
  3. Never implement without an approved plan (unless told to go direct)
  4. Run build/tests before declaring anything as done
  5. Commit as implementation blocks are finalized

## Install

### From marketplace (recommended)

Add the marketplace and install in one go:

```bash
claude plugin marketplace add tree-ia/tree-ia-dev-plugin
claude plugin install tree-dev@tree-ia/tree-ia-dev-plugin
```

Or interactively inside Claude Code:

```
/plugin marketplace add tree-ia/tree-ia-dev-plugin
/plugin install tree-dev@tree-ia/tree-ia-dev-plugin
```

### Local (for development/testing)

```bash
claude --plugin-dir /path/to/tree-ia-dev-plugin
```

### Verify installation

```bash
claude agents
```

You should see:

```
Plugin agents:
  tree-dev:researcher · opus
  tree-dev:backend · opus
  tree-dev:frontend · opus
  tree-dev:security · opus
  tree-dev:qa · opus
```

## Useful CLI combinations

The plugin works out of the box, but these flags complement it well:

```bash
# Standard session (plugin loads automatically after install)
claude

# Parallel work — isolated git worktree per feature
claude -w feature-auth
claude -w feature-payments --tmux    # split panes with tmux

# Continue where you left off
claude -c                            # most recent session
claude -r "session-name"             # resume by name

# Name your session for easy resuming
claude -n "auth-refactor"

# Use Sonnet for quick tasks (overrides plugin's Opus default for main session)
claude --model sonnet

# Headless / CI — non-interactive with budget cap
claude -p --max-turns 10 --max-budget-usd 5.00 "run tests and report"

# Restrict tools for read-only exploration
claude --tools "Read,Glob,Grep,Bash"
```

### Shell aliases (optional)

Add to your `~/.zshrc` or `~/.bashrc` for convenience:

```bash
alias cc='claude'
alias ccw='claude -w'
alias ccn='claude -n'
alias ccc='claude -c'
```

## Workflow

```
You send a task
    │
    ├─ Ambiguous? ──→ brainstorm skill ──→ refine scope
    │
    ├─ Need research? ──→ researcher agent ──→ expert knowledge
    │
    ▼
plan-first skill ──→ decompose into subtasks + file ownership
    │
    ▼
You approve (or adjust) the plan
    │
    ▼
backend + frontend agents (parallel when possible)
    │
    ├─ commits per logical block
    │
    ▼
security agent ──→ vulnerability audit (when auth/payments/data involved)
    │
    ▼
qa agent ──→ build + code review + plan compliance
    │
    ▼
verification skill ──→ evidence-based completion
```

Not every task needs every step. A single-file bug fix skips straight to implementation. A full-stack feature uses the complete pipeline.

## Design principles

- **Stack-agnostic** — agents read `CLAUDE.md` and adapt. Works with Next.js, Express, NestJS, React Native, Hono, or whatever your project uses.
- **File ownership** — backend and frontend agents have strict boundaries. No conflicts, no overwrites.
- **Read-only review** — researcher, security, and qa agents cannot edit files. Separation of concerns.
- **Plan before code** — the default behavior. Skip it explicitly when you want to go fast.
- **Evidence over claims** — "should work" is not accepted. Build must pass.
- **Conditional spawning** — only the agents the task actually needs are spawned. Backend-only change? No frontend agent.

## Customization

The plugin works out of the box but is designed to complement your project's `CLAUDE.md`. Agents will follow your project-specific conventions (commit style, naming, directory structure, build commands) as long as they're documented in `CLAUDE.md`.

## Requirements

- Claude Code v2.1.32+
- Claude Opus 4.6 (agents are configured for Opus)

## License

MIT
