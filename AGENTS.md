# Agent instructions for this repo

This is a **fork** of the woosal1337 ASD-STE100 kit with conversation-first Layer 2. See [`FORK-NOTES.md`](FORK-NOTES.md) before syncing upstream.

## What to load

| Goal | File |
|------|------|
| Full rules (custom 2.1-fork) | [`asd-ste100/SKILL.md`](asd-ste100/SKILL.md) |
| Condensed always-on style | [`asd-ste100/output-style.md`](asd-ste100/output-style.md) |
| STE recurring errors | [`asd-ste100/references/ste-recurring-errors.md`](asd-ste100/references/ste-recurring-errors.md) |

## Owner preferences (always apply)

1. **STE-flavored** for all replies. Strict STE only when the user explicitly asks for it.
2. **Both layers stay on** — Layer 1 words + Layer 2 shape.
3. **Conversation default** — main point first; no mandatory "next step" or time estimates (minutes/hours/days) unless the user asked how long something takes.
4. **Task shape** only when the user must execute steps or a multi-step job is already in progress.
5. **Lint** — run `ste-lint.py` (flavored, `--fail-over 2.5`) when the environment can execute commands; otherwise use the manual checklist in `SKILL.md`. Do not refuse to answer only because lint is unavailable.

## Lint command (when available)

```bash
node asd-ste100/hooks/run-python.cjs asd-ste100/scripts/ste-lint.py --fail-over 2.5 DRAFT.md
```

## Agents without code execution

Paste **`asd-ste100/SKILL.md`** (or **`output-style.md`**) into system or custom instructions. Follow the checklist in the skill; skip lint commands.

## Upstream

Base kit: [woosal1337/blog — ep01-the-cure-for-ai-slop](https://github.com/woosal1337/blog/tree/main/videos/ep01-the-cure-for-ai-slop). [`SYNC-FROM-UPSTREAM.md`](SYNC-FROM-UPSTREAM.md) refreshes upstream files; re-apply [`FORK-NOTES.md`](FORK-NOTES.md) after.
