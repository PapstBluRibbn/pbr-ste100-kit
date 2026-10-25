# Fork customizations (keep on upstream sync)

When you run `SYNC-FROM-UPSTREAM.md`, re-apply these local edits if upstream overwrites them:

- `asd-ste100/SKILL.md` — conversation-first Layer 2, no forced time estimates, STE-flavored default
- `asd-ste100/output-style.md` — same
- `asd-ste100/hooks/ste-inject.py` — standing-rule card text
- `asd-ste100/hooks/ste-refresh.py` — mid-turn card text
- `AGENTS.md` — how bots should use lint vs checklist

Do not change `asd-ste100/scripts/ste-lint.py` unless you intentionally want different drift detection.
