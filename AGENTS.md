# Agent instructions for this repo

This repository is a **mirror of the ASD-STE100 anti-slop kit** (skill, linter, hooks, experiment). Use it as the single source when the user asks for plain writing, STE-style prose, or less AI slop.

## What to load

| Goal | File |
|------|------|
| Full rules (Layer 1 words + Layer 2 reply shape) | [`asd-ste100/SKILL.md`](asd-ste100/SKILL.md) |
| Shorter always-on style (Claude Code output style) | [`asd-ste100/output-style.md`](asd-ste100/output-style.md) |
| STE recurring error replacements | [`asd-ste100/references/ste-recurring-errors.md`](asd-ste100/references/ste-recurring-errors.md) |
| Kit layout, install, linter, hooks | [`README.md`](README.md) |

## Agents that cannot run code

Paste **`asd-ste100/SKILL.md`** into system instructions, custom instructions, or a project doc. Optionally add **`asd-ste100/output-style.md`** if you want the condensed version. You do not need the linter or hooks for basic use.

## Agents that can run code (optional)

Lint a draft before sending long prose:

```bash
node asd-ste100/hooks/run-python.cjs asd-ste100/scripts/ste-lint.py --fail-over 2.5 DRAFT.md
```

Claude Code full install (symlink skill, output style, hooks):

```bash
node asd-ste100/hooks/run-python.cjs asd-ste100/install.py
```

## Upstream

Source: [woosal1337/blog — ep01-the-cure-for-ai-slop](https://github.com/woosal1337/blog/tree/main/videos/ep01-the-cure-for-ai-slop). See [`ATTRIBUTION.md`](ATTRIBUTION.md) and [`SYNC-FROM-UPSTREAM.md`](SYNC-FROM-UPSTREAM.md) to refresh this copy.
