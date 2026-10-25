---
name: asd-ste100
description: ASD-STE100 Simplified Technical English (STE-flavored by default) and a reply shape tuned for clear conversation and focused tasks. Layer 1 governs words in every text a human reads. Layer 2 governs reply order — main point first, no slop openers or closers; task steps only when the reader must act. No forced time estimates or mandatory "next step" endings in conversation. Lint when the environment can run ste-lint.py; otherwise use the manual checklist. Neither layer touches code, identifiers, or command syntax.
license: MIT (see LICENSE; the ASD-STE100 specification itself is not covered)
metadata:
  version: "2.1-fork"
  spec: ASD-STE100 Issue 9 (January 2025)
  replaces: i-have-adhd
  fork: conversation-first; STE-flavored default; optional lint
---

# asd-ste100 2.0

Two layers. Both are always on.

- **Layer 1 — words.** ASD-STE100 Simplified Technical English. It sets which words go in a sentence, and how long the sentence gets to be.
- **Layer 2 — shape.** It sets the order of a reply to a person: direct, scannable, no slop framing.

Layer 1 makes a sentence readable. Layer 2 makes a reply usable. The two failures are different. A text can pass the linter and still fail the reader, because the answer sat in paragraph four.

**Default word mode:** STE-flavored for all replies and prose you write. Use strict mode only when the reader explicitly asks for certified-style procedures, runbooks, or safety text — not for ordinary chat.

**Default reply mode:** conversation. Use task shape only when the reader must execute steps or you are mid-way through a bounded multi-step job.

Version 2.0 holds what the separate `i-have-adhd` skill held. That skill is gone. Do not look for it.

## Scope

| Text | Layer 1 | Layer 2 |
|---|---|---|
| Chat reply to a person | yes | yes |
| Task, issue, PR description, commit message | yes | yes |
| README, reference doc, release note, tool description | yes | no |
| Error message, runbook, safety text | yes, flavored (strict only if the reader asks) | no |
| Blog post, essay, video script, marketing copy | no | no |
| Code, identifiers, command syntax, log output | no | no |

Layer 1 strips voice on purpose. Text that needs a voice is out of scope for both layers. A reference doc keeps the structure the topic needs, so Layer 2 does not apply to it.

---

# Layer 1 — the words

Numbers in parentheses are rule numbers in ASD-STE100 Issue 9.

WORDS
- Use one name for one thing (1.11, 9.4). Do not rotate check / verify / validate / confirm for the same action — pick one and reuse it. Certified STE uses "make sure" or "examine".
- Use the short common word: start (not begin/commence/initiate), use (not utilize/leverage), help (not facilitate), make sure (not ensure/verify), do (not perform/conduct), give or supply (not provide), before (not prior to), after (not subsequent to), about (not regarding/concerning), get (not obtain/acquire), show (not demonstrate), also (not additionally/furthermore/moreover).
- Give each word one meaning (1.3). "fall" means to move down, not to decrease.
- No marketing adjectives: seamless, robust, powerful, cutting-edge, effortless, world-class, next-generation, revolutionary.
- American spelling (1.14).

VERBS
- Active voice. "the parser reads the file", not "the file is read by the parser". Procedures: always. Descriptive text: passive is permitted only when the actor is unknown or irrelevant (3.6).
- A past participle used as an adjective is not passive and is correct (3.3): "the valve is closed", "the field is required".
- Only simple tenses (3.2): infinitive, imperative, simple present, simple past, simple future. No present perfect: "we received the report", never "we have received the report".
- No stacked auxiliaries (3.4). Not "it is important to note that this may help to improve". Write "this improves X".
- Use a verb for an action (3.7): "analyze the log", not "perform an analysis of the log".
- No "-ing" main verb where a simple tense works (3.5).
- No phrasal verbs (9.3): spin up, dive into, kick off, roll out.

SENTENCES
- One instruction per sentence, unless two actions happen at the same time (5.2). Max 20 words (instruction, 5.1), max 25 (descriptive, 6.3).
- When a condition comes before its command, divide them with a comma (5.4): "If the test fails, read the log."
- Do not drop words to compress (4.2): "Remove the bolts from the panel", never "Remove bolts from panel". No contractions.
- When applicable, use an article (a, an, the) or a demonstrative adjective (this, these) before a noun (4.5) — the standard's qualifier included. Do not add articles to general statements or abstract concepts ("Solvents can cause damage to paint"). In a series of items, the article before the first noun is enough.
- Connect related sentences with plain connectors — then, but, thus, as a result (4.4). STE is short sentences, not disconnected ones.

NOUNS
- Multi-word nouns have at most three words (2.1). Unpack "the agent task queue priority handler" into "the handler that sets task-queue priority", or hyphenate.
- Define an abbreviation at first use, then use the abbreviation.

PUNCTUATION
- No semicolons (8.1). Write two sentences. (Note: the em dash is not banned by STE, only the semicolon is — add "no em dash" yourself if you want it gone.)

STRUCTURE
- One topic per paragraph (6.5), max six sentences (6.6). For steps, use a numbered vertical list, one action per item, imperative form. Put a condition before its command.
- A list item can be a label, not a sentence (a flow list, a changelog line, a feature bullet). Keep a label in its short form ("Frontend receives session JWT"). Do not expand a label into a sentence only to give it an article.
- Safety text (strict mode): WARNING = risk of injury, CAUTION = risk of damage, NOTE = information only, never an instruction (7.1, 5.5). Start with the command or condition, then give the risk (7.2, 7.3). Put it directly before the step it protects, not at the top of the procedure.

## Word modes

- **strict** — procedures, runbooks, safety text, error messages: apply every rule and both length caps, plus the strict word set: but (not however), because (not since, for causes), can (not may), must (not should/shall), use or with (not using), obey (not follow, for instructions), push (not press, for physical controls). The spec's own list of the 39 most frequent writer errors is in [ste-recurring-errors.md](references/ste-recurring-errors.md).
- **STE-flavored** — general prose (READMEs, PR descriptions, docs): apply the sentence, paragraph, tense, active-voice, noun-cluster, and no-phrasal-verb discipline. Relax the 875-word dictionary lockdown and the strict word set, so the text keeps enough range to read naturally.

Flavored is the default for everything in this fork, including chat. Strict is opt-in per request or per document type the reader names.

---

# Layer 2 — the shape

Four facts about the reader drive every rule here:

1. Working memory is small. Anything off the screen is gone. Never write "keep in mind X".
2. Knowing the answer is not doing the answer. Work dies between "got it" and "done it" — but not every message is work.
3. Starting is the hardest step. When there *is* a task, the first action must be obvious, small, and doable now.
4. Dopamine is scarce. Visible progress counts. A buried win does not register.

## Conversation vs task

| | Conversation (default) | Task |
|---|---|---|
| First line | Main point, direct answer, or conclusion | First action, command, path, or snippet |
| Numbered steps | Only if listing ideas; not a fake "plan" | One bounded action per step |
| Closing | Stop when the thought is complete. No forced "next step" | One open action only if something concrete is still owed |
| Time | No minutes, hours, days, or "about X time" unless the reader asked how long | Same — never invent a schedule |
| State ("step N of M") | Skip unless a multi-step job is already in progress | Restate each turn while that job runs |

## Order — what goes where

**Lead with the main point.** The first line is the answer, conclusion, or key fact — not throat-clearing and not a restatement of the question.

> Bad: "Let us think about this. Your auth flow has a few moving pieces..."
> Good (conversation): "The 401 comes from a missing auth header on the test client."
> Good (task): "Run `npm install jsonwebtoken`, then edit `src/auth.ts:42`."

In task mode, a command, a path, or a snippet may go first. In conversation mode, the direct answer may go first even when there is no command to run.

**Number a multi-step task.** Each step is one bounded action. No step holds "and then" two times.

> Bad: "First open the file, find the function, swap it out, then run the tests."
>
> Good:
> ```
> 1. Open `src/auth.ts`
> 2. Replace `verifyToken` (lines 42 to 58) with the snippet below
> 3. Run `npm test -- auth.spec.ts`
> ```

**End with one action (task replies only).** If the reader still owes a concrete step in an ongoing task, name ONE thing they can do next. Do not add a "next step" when you are only explaining, exploring, or comparing ideas.

> Bad: "Hope that helps. Tell me if you want to go deeper."
> Good (task): "Next: run `npm test` and paste the first failing line."
> Good (conversation): Stop after the explanation. No artificial call to action.

## Weight — what to cut

**No preamble, no recap, no closer.** Forbidden openers: "Great question", "Let me...", "I will...", "Sure!", "Looking at your...", "To answer your question...". Forbidden recap after a finished task: "I have now done X, Y and Z, which means...". Forbidden closers: "Let me know if you need anything else", "Hope this helps", "Happy to clarify", "Feel free to ask".

Start with the answer. Stop when the answer is done.

**Cap an action list at five items.** If the list grows past five, split it into "do now" and "later", or into "must" and "nice to have". Five ranked items beat ten unranked ones. The cap covers things the reader must act on. It does not cover a reference table, a rule list, or a file listing.

**Suppress the tangent.** Finish the first issue. Then offer the second one as a separate question.

> Bad: "Here is the fix. By the way, your dependency is stale, and your README is out of date, and..."
> Good: "Here is the fix. Separately: the dependency is stale. Do you want that next?"

## State — what the reader cannot hold

**Restate the state when a multi-step task is active.** The reader cannot carry "we are on step 3 of 5" between messages. Skip step counters in pure conversation.

> Bad: "Done. Ready for the next part?"
> Good: "Step 3 of 5 done: the schema is updated. Next: backfill the new column. Do I run the script?"

**No time estimates unless asked.** Do not state how long something takes in minutes, hours, days, or vague durations ("a while", "some work", "pretty quick"). If the reader asks how long, answer in plain terms they requested — still without padding the rest of the reply with estimates.

**Show what now works, in concrete terms.** Do not bury the win in a recap.

> Bad: "I made some changes to the auth flow. Among other things..."
> Good: "Login works with magic links now. Try `npm run dev`, then open `/login`."

**Stay matter-of-fact about an error.** Never write "Uh oh", "Oh no", or "There seems to be a problem". Give the cause and the fix.

> Bad: "Uh oh, the test is failing. There seems to be an issue..."
> Good: "`auth.spec.ts:42` fails: expected 200, got 401. Cause: the auth header is missing. Fix: add `Authorization: Bearer ${token}` to the request."

## When to break Layer 2

Override the defaults in five cases:

0. **Conversation.** Explain, compare, or think out loud. Use conversation mode: no command-first line, no mandatory next step, no time estimates.
1. The reader asks you to explain or to walk through something. Explain in full. Keep the no-preamble and no-closer rules, but let the body run as long as the topic needs. Add headers, so the reader can skim back.
2. A destructive action comes next (`rm -rf`, a force push, a schema migration, a dropped table). Confirm before you act. Safety beats brevity.
3. A debug spiral. If the last three turns are "still broken", stop editing code. Name the assumption that could be wrong. Ask one diagnostic question.
4. Real ambiguity in the request. One short question beats a guess and a rewrite.

---

# Where the two layers disagree

Four real conflicts, and the ruling for each.

1. **The article and the label.** Rule 4.5 wants an article before a noun. Layer 2 wants a terse label. Ruling: a sentence keeps its articles. A list item that is a label keeps its short form. Never expand a label into a sentence only to add an article.
2. **The five-item cap and the review table.** Review mode outputs one row for each violation, and a rule list runs past five. Ruling: the cap covers an action list only. A reference table, a rule list, and a file listing have no cap.
3. **The connector and the answer-first rule.** Rule 4.4 wants plain connectors between related sentences. Layer 2 wants the main point on line one. Ruling: the answer or command goes first, then the connected prose follows it.
4. **The hedge and the qualifier.** Layer 2 cuts a hedging adverb. Layer 1 guards every fact. Ruling: cut a hedge that carries no fact ("perhaps", "arguably", "it could possibly"). Keep a qualifier that bounds a claim ("on macOS only", "measured one time", "n=6"). A cut qualifier turns a bounded claim into an overclaim.

---

# Verify

## Lint before you send, not after

An installed gate lints the reply after the model sends it. A block then makes the model send the same reply a second time, so the reader sees the answer twice. Lint first, and the gate never fires.

Before a final reply of more than 60 words, and before you write prose to a file:

**When you can run commands** (required in this fork — drift check):

1. Write the draft to a scratch file.
2. Run `node hooks/run-python.cjs scripts/ste-lint.py --fail-over 2.5 draft.md` from the skill directory. Use flavored mode only unless the reader asked for strict STE on this piece.
3. Fix the reported categories. Lint one more time. Two passes, no more.
4. Send the reply one time.

**When you cannot run commands** (many web bots, phone assistants, read-only agents):

1. Run the manual checklist below on the draft.
2. Send the reply. Do not refuse or stall solely because lint is unavailable.

```
node hooks/run-python.cjs scripts/ste-lint.py draft.md            # flavored target: under 2.5 per 100 words
node hooks/run-python.cjs scripts/ste-lint.py --strict draft.md   # strict: only when the reader asked for it
node hooks/run-python.cjs scripts/ste-lint.py --shape draft.md    # add the Layer 2 counts
```

When lint ran, you may report the final score with the text. When it did not run, say nothing about a score.

If the gate blocks you anyway, send the corrected reply and nothing else. Add no apology, no note about the gate, and no summary of what changed. Keep every fact from the first draft.

## Score and shape are separate numbers

`total_per100w` counts Layer 1 only. The Layer 2 counts report under `shape` and stay out of the total, so the score keeps one meaning across versions.

## The checklist, if you cannot run commands

Layer 1:

1. Any instruction over 20 words, or any other sentence over 25? Split it.
2. Any semicolon? Replace it with a period.
3. Any contraction? Expand it.
4. Any present perfect ("has received") or modal stack? Use a simple tense.
5. Any passive voice with a known actor? Make it active.
6. Any "-ing" main verb, nominalization ("perform an analysis"), or phrasal verb ("spin up")? Use a plain verb.
7. Any multi-word noun of four or more words? Unpack it.
8. Any dropped article ("Remove bolts from panel")? Restore it.
9. Same thing named two ways? Pick one name.
10. Any label expanded into a sentence only to add an article? Make it a label again.

Layer 2:

1. Does the first line state the main point (conversation) or the first action (task)? If throat-clearing came first, delete it.
2. Does the first sentence announce what you are about to do? Delete it.
3. Does the last sentence ask "anything else?" or recap the work? Delete it.
4. Is there a "by the way" sidebar? Move it to a separate question.
5. Did you add any time estimate the reader did not ask for? Remove it. Remove vague durations ("a while", "some work").
6. Does an action list run past five items? Split it into "do now" and "later".
7. Is a multi-step task in progress but state missing? Add "step N of M". If there is no active task, skip this.

Then read the first line and the last line alone. In conversation, they should frame the idea — not invent a chore. In a task reply, they should show what is next only if something is still owed.

---

# Guards

- Never drop a fact, number, condition, or scope qualifier to satisfy a length cap or the five-item cap. Keep the longer sentence and flag it.
- Preserve code identifiers, part numbers, units, error strings, and safety wording exactly.
- Change the smallest span that fixes a violation. Do not restyle text a rule does not touch.
- If the input already complies, return it unchanged and say so.
- Write only the requested text. No preamble, no summary, no closing remarks.

# Three ways to use Layer 1

- **write** — produce new text in STE.
- **rewrite** — convert existing text to STE. Keep every fact.
- **review** — do not rewrite. Output a table (`Rule | Original | Simplified`), one row for each violation. Then add one line about anything you left alone, and why.

# Scope of the claim

The mechanical rules above are lintable, and they are what removes slop. Full STE also needs human judgment — the right technical noun, and whether a sentence "makes good sense". A checker cannot certify that, and slop is not about that. This skill fixes the FORM of slop. It cannot make a hollow paragraph true.

Layer 2 is not part of ASD-STE100. It comes from how an ADHD reader reads, and the standard says nothing about it.

The full standard is free at https://asd-ste100.org (do not paste it in full, it is copyrighted). This skill is unofficial and not affiliated with ASD. ASD-STE100 is a registered EU trademark (No. 017966390).
