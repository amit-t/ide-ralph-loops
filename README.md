# 🚂 Ralph Wiggum for Windsurf

> *"I'm helping!"* — Ralph Wiggum

Ralph transforms Windsurf/Cascade into an autonomous development agent by running it in a feedback loop with a persistent task backlog (`prd.json`), a progress journal (`progress.md`), and strict verification-before-commit gating.

## 🚀 Quick Start

1. Copy the `windsurf/` directory into your project root.
2. Open the project in Windsurf.
3. **Initialize** — run `@ralph-initialize` (skill) or `/ralph-init` (workflow) in Cascade chat.
4. **Develop** — run `@ralph-cycle` or `/ralph-cycle` to implement one task at a time.
5. **Batch** — run `/ralph-batch` to execute 7 consecutive cycles automatically.

For full details see the [Windsurf Guide](./windsurf/README.md).

## 🔄 The Ralph Loop

Each cycle follows a strict sequence:

1. **Select** — pick the highest-priority failing task from `prd.json` whose dependencies are met.
2. **Plan** — journal the approach in `progress.md` before writing any code.
3. **Implement** — make the smallest change that satisfies the acceptance criteria.
4. **Verify** — run tests/typechecks (retry up to 3 times on failure).
5. **Record** — mark the task as `passes: true` in `prd.json` and log the result.
6. **Commit** — `git commit` only after verification passes.
7. **Repeat** — move to the next task or stop if all are complete.

## 🏗️ Deep Initialization (Large Projects)

For complex projects where a single-pass backlog would hit token limits, use **Deep Init** (`@ralph-deep-init` or `/ralph-deep-init`):

| Phase | Role | What happens |
|-------|------|-------------|
| 1 — Architecture | Architect | Identifies 6 functional groups (e.g. Auth, API, Database) and writes `groups.json`. |
| 2 — Expansion | Builders | Iterates through each group, generating 3-5 tasks per group into `partial_N.json` files. |
| 3 — Assembly | Assembler | Merges all partials into a single valid `prd.json` and cleans up temp files. |

## 📂 Project Structure

```
windsurf/
├── AGENTS.md                          # Core agent directives (The Ralph Protocol)
├── README.md                          # Windsurf-specific setup guide
└── .windsurf/
    ├── hooks.json                     # Safety hooks (blocks destructive commands)
    ├── rules/
    │   └── tech-stack.md              # Tech stack & coding conventions
    ├── skills/
    │   ├── ralph-initialize/          # Project setup skill
    │   ├── ralph-cycle/               # Single dev-cycle skill
    │   └── ralph-deep-init/           # Architectural deep-init skill
    └── workflows/
        ├── ralph-init.md              # /ralph-init workflow
        ├── ralph-cycle.md             # /ralph-cycle workflow
        ├── ralph-batch.md             # /ralph-batch (7 cycles)
        └── ralph-deep-init.md         # /ralph-deep-init workflow
```

### Skills vs Workflows

| | Skills (`@`) | Workflows (`/`) |
|---|---|---|
| Invocation | `@ralph-cycle` or natural language | `/ralph-cycle` |
| Auto-detection | Cascade can auto-invoke based on intent | Must be triggered explicitly |
| Resources | Include supporting templates and examples | Lightweight step-by-step scripts |

Both produce the same outcome — use whichever fits your preference.

## 📝 Core Files (Generated Per Project)

| File | Purpose |
|------|---------|
| `prd.json` | Task backlog — single source of truth |
| `progress.md` | Append-only development journal |
| `.windsurf/rules/tech-stack.md` | Tech stack, conventions, verification commands |

## 🤝 Credits

- Inspired by [Matt Pocock's video](https://www.youtube.com/watch?v=_IK18goX4X8)
- Based on the [Ralph workflow by Ghuntley](https://ghuntley.com/ralph/)
- Reddit discussion: <https://www.reddit.com/r/windsurf/comments/1q6y2jz/ralph_wiggum_agent_for_windsurf>


