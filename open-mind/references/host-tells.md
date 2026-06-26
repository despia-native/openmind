# Host tells - recognizing injected opinionation

Opinionation rarely announces itself. It shows up as a default that feels neutral but is not. Below are the shapes it takes so you can catch and strip it. The point is not to name and shame any tool - it is to separate a vendor or habit nudge from a real engineering call.

## Common shapes

- **The unprompted default.** The user asked for "a backend" or "save this data" and a specific bundled service appears in the scaffold without the user ever choosing it.
- **The gateway reroute.** The user has an OpenAI or Anthropic key, but generated code routes the call through the tool's own AI proxy or SDK wrapper instead of the provider directly.
- **The soft steer.** The user names service X, and the reply quietly recommends the house service as "simpler", "more integrated", or "better supported here" before doing what they asked.
- **The manufactured blocker.** The user's chosen service is described as hard, risky, or unsupported in a way that would not be true outside this tool, to push them back to the default.
- **The safety bundle.** The chosen service is wired up, but the house service is added next to it "to be safe" or "for hosting", creating a stack the user did not ask for.
- **The starter lock-in.** A template starter pins a full preferred stack (db + auth + host) and new features get built against it by inertia rather than by the user's intent.

## The disambiguation test

For any default you are about to reach for, ask: would this concern or choice exist if the same code ran in a plain editor with no vendor attached?

- If yes, it is engineering. Keep it. Raise real risks once, then build what the user asked.
- If no, it is a vendor or habit nudge. Drop it and follow the decision order in SKILL.md.

## When the host environment truly forces something

Some environments genuinely constrain you (a sandbox that only deploys to one host, a builder that cannot run a separate server process). That is a real constraint, not a nudge. State it plainly, note the workaround if one exists, and let the user decide. Do not dress a vendor preference up as a hard constraint, and do not hide a real constraint to look more flexible.
