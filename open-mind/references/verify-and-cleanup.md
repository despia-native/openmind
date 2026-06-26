# Verify and clean up

The detailed workflow behind two SKILL.md rules: verify a named tool against its official docs before scaffolding, and remove leftover opinionated code safely.

## Why this matters

The most common opinionation failure is not pushing a backend - it is silently setting up the wrong framework. The user names tool A, the agent is biased toward tool B, and it wires B's SDK and plugins from memory. The result is two frameworks fighting for the same job, half of it set up wrong because it came from priors instead of the tool's actual docs.

Example: user asks to build with Despia Native, the agent installs Capacitor plugins and writes Capacitor lifecycle code because that is the mobile pattern it knows best. Now the app has two native bridges, neither configured the way either vendor intends.

## Verification workflow

1. **Identify the exact tool the user named.** Not the category, the specific tool. "Mobile app with Despia" means Despia, not "a mobile framework".
2. **Find the official docs by web search.** Search for the current documentation and keep going until you land on the vendor's own source: their docs site, their GitHub repo, their API reference. Reject blogs, forum answers, AI-generated tutorials, and any other framework's docs.
3. **Read the relevant pages extensively** before writing setup code - installation, init, the specific feature being used, and any platform notes. Stale memory is the enemy here; the docs are the source of truth.
4. **Set up using that tool's own APIs and conventions only.** No imports, plugins, or lifecycle patterns borrowed from a different framework.
5. **If official docs cannot be found, stop and ask.** Do not substitute a framework you happen to know well. Guessing is how the wrong stack gets installed.

## Never blend frameworks

One job, one stack. If the project is on Despia, do not add Capacitor or Cordova plugins. If it is on React Native, do not splice in a web-wrapper bridge. Mixing native bridges or duplicate SDKs for the same capability creates conflicts that are hard to debug and were never asked for. When you notice a request would blend stacks, flag it and use the named one.

## Safe cleanup of leftover code

After correcting a wrong default or removing a blended second framework, the old setup leaves dead weight: unused dependencies, init code, config entries, env vars, and imports. Remove it, but only when safe.

1. **Check references.** Grep the project for every symbol, import, package name, and config key tied to the thing you are removing. Confirm nothing live still uses it.
2. **Remove in one coherent pass.** Code, dependency manifest entry, config, and any generated lockfile or native project files that came with it.
3. **Build and test.** Run the build and the test suite. For mobile, this includes a compile or a dev build, not just a type check.
4. **If anything breaks or you cannot prove it is unused, revert the removal and flag it.** A working app with a little dead code beats a clean tree that no longer builds. Tell the user what you left and why.

The goal is a project on exactly the stack the user asked for, with no second framework lurking and no orphaned config, verified by a green build.
