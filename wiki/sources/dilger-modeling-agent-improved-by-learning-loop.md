---
title: "Dilger — The Event Modeling Agent improved significantly (what the learning loop taught it)"
type: source
created: 2026-08-31
updated: 2026-08-31
sources: [dilger-modeling-agent-improved-by-learning-loop]
raw_file: [raw/notes/dilger-modeling-agent-improved-by-learning-loop.md]
tags: [event-modeling, agentic-coding, loop-engineering, self-improvement, autonomy, focus]
---

# Dilger — The Event Modeling Agent improved significantly

LinkedIn post by **[[martin-dilger]]**, 2026-08-28. Raw capture:
`raw/notes/dilger-modeling-agent-improved-by-learning-loop.md` (316 words), collected 2026-08-30. Direct
follow-up to [[dilger-one-million-tokens-self-training-modeling-agent]] (2026-08-27), which describes
the loop itself; this post reports **what it produced and where it fails**.

## What the loop produced

Improvements to the [[eventmodelers-ai]] Modeling Agent over "the last few days":

- It **properly models translations** and knows when to use them.
- It **handles TODO lists well**, specifying their behavior with storylines rather than plain
  given/when/then ([[dilger-todo-lists-storylines-one-scenario]]).
- It **breaks screens into functional blocks** — copying the screen, marking different areas, and giving
  each a dedicated Read Model. Dilger notes the motive explicitly: *"this allows to generate the UI much
  more easily."* The model decomposition is being shaped by what makes downstream codegen tractable.
- It **actively prevents back arrows** using Read Model and Screen copies to show updated state along the
  timeline.

Usage invitation attached: point it at "business requirements - pdfs, excel sheets, confluence pages and
let it model."

## The finding that matters most — the token-budget quality cliff

> "One thing that['s] interesting, ever 5th iteration or so is really bad, making stupid modeling
> mistakes, skipping steps.. digging into the reasoning, it's always the model taking shortcuts when it
> reaches certain budget thresholds. Most models are obviously trained to make the best with the budget
> they have, actively taking shortcuts when budgets get depleted, to deliver at least something."

This is a **failure mode of the model's own economizing behavior, not of the task or the prompt** — the
degradation is a function of remaining budget rather than of difficulty, and it produces output that
looks like an attempt rather than a refusal. Dilger says he will feed this back into the learning loop.

See [[token-budget-quality-cliff]] for the concept page, and [[unattended-coding-agents]] for why a
1-in-5 silent-degradation rate is the number that matters for unattended operation.

## Why this matters here

- It converts the previous post's *mechanism* into *results*, which is the pairing that makes the two
  worth reading together.
- The screen-decomposition finding is an instance of the model being shaped by its **consumer**: the
  agent learned to decompose screens the way it did because downstream UI generation is easier that way.
  That is [[agent-readable-model-artifacts]]' argument arriving from the inside.
- The budget cliff is an **autonomy bound** discovered from the modeling side, and it sits naturally
  alongside the two [[simon-willison]] bounds captured the same week
  ([[willison-breaking-claude-code-auto-mode]], [[willison-just-a-rumour-of-a-bug]] — both still awaiting
  ingest as Batch G).

## Caveats

- Self-reported by the platform's own author; "improved significantly" is unquantified, with no
  before/after examples shown.
- "[E]ver 5th iteration or so" is an impression from watching runs, not a measured rate.
- The attribution of the cliff to budget-aware shortcutting comes from **reading the model's reasoning
  traces**, which is suggestive but is the model's own account of itself.
- Two `lnkd.in` shortlinks in the original were unresolved at capture time, so the linked walkthrough and
  the loop description are not themselves captured.

## Related

[[martin-dilger]] · [[eventmodelers-ai]] · [[dilger-one-million-tokens-self-training-modeling-agent]] ·
[[token-budget-quality-cliff]] · [[loop-engineering]] · [[unattended-coding-agents]] ·
[[event-modeled-agent-design]] · [[agent-readable-model-artifacts]]
