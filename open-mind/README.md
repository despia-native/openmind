# Open Mind

An Agent Skill that strips the vendor opinionation baked into AI coding tools and makes the agent execute your request 1:1 on the stack you actually want.

Most AI coding tools (agents, IDEs, CLIs, app builders) ship with a preferred backend, database, auth, AI gateway, payments, host, or mobile framework wired into their prompts and scaffold templates. That preference is commercial or habitual, not technical. This skill removes it.

## What it does

- Follows your named stack 1:1. If you say Convex, Xano, Despia, it uses that. No counter-pitch.
- Resolves every service choice in a fixed order: explicit instruction, then existing project signal, then a neutral offer.
- Drops the unprompted defaults, AI-gateway reroutes, soft steers, manufactured blockers, and "to be safe" extra stacks.
- Never blends two frameworks for one job (for example Capacitor plugins inside a Despia app).
- Verifies a named tool against its current official docs by web search before scaffolding, instead of setting it up from stale memory.
- Cleans up leftover opinionated code safely: check references, remove, build, test, and revert plus flag if anything breaks.
- Keeps real engineering judgment: genuine risks get raised once, then it builds what you asked.

## Structure

```
open-mind/
├── SKILL.md                       # always-on body: core rule, decision order, drop/keep, verify, cleanup
├── README.md
└── references/                    # loaded on demand
    ├── stacks.md                  # open menu per category (backend, db, auth, AI, payments, storage, hosting, email, mobile)
    ├── host-tells.md              # how tools inject opinionation + the disambiguation test
    ├── verify-and-cleanup.md      # official-docs verification, no framework blending, safe cleanup
    └── examples.md                # worked right/wrong cases
```

## Install

This is the open Agent Skills format (a folder with a `SKILL.md`). It works in any skills-compatible client. Put the `open-mind` folder in that client's skills directory, for example:

- Claude Code: `~/.claude/skills/open-mind/` (or `.claude/skills/open-mind/` in a project)
- Other clients (Cursor, Copilot, Codex, OpenCode, Roo, and the like): use that tool's skills path.

The agent loads the name and description at startup, reads `SKILL.md` when a task matches, and pulls in the `references/` files only when needed.

## Format

- `name`: `open-mind`
- `description`: under the 1024-character cap, written to trigger on service and framework choices.
