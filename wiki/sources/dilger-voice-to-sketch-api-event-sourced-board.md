---
title: "Dilger — Voice-to-sketch API, and the board's event history as the agent's alibi"
type: source
created: 2026-08-31
updated: 2026-08-31
sources: [dilger-voice-to-sketch-api-event-sourced-board]
raw_file: [raw/notes/dilger-voice-to-sketch-api-event-sourced-board.md]
tags: [event-modeling, event-sourcing, agent-explainability, agentic-coding, tooling]
---

# Dilger — Voice-to-sketch API, and the board's event history as the agent's alibi

LinkedIn post by **[[martin-dilger]]**, 2026-08-14. Raw capture:
`raw/notes/dilger-voice-to-sketch-api-event-sourced-board.md`. Two board images not transcribed.

Mostly a light feature demo — but it contains one incidental detail worth more than the feature.

## The demo

Testing a **voice-to-sketch API** on the [[eventmodelers-ai]] platform, running **Qwen3.6:27B and Claude
Code behind vLLM**. A single spoken instruction places three chapters in a specific spatial arrangement,
adds commands in named grid cells (`A2`, `B2`, `C2`), adds a feedback lane with red nodes, and draws
decorations. Cost: "the best 14k tokens I spent today."

The cell references are the [[agent-readable-model-artifacts|coordinate-addressability]] bet in use —
you can only say "add 3 commands each in A2, B2 and C2" because every element has a handle
([[dilger-planning-like-excel-legible-to-human-and-ai]]).

## The part that matters

Before drawing, the agent checked the board's own event history and pre-emptively disclaimed something:

> "I need to flag something before continuing: the board's event history shows that right after our last
> round of edits, everything got deleted. **I didn't issue those deletes myself.**"

Dilger's aside — "good we are event sourced" — undersells it. This is a small, unplanned instance of
something [[agent-explainability]] argues for in the abstract: **the agent consulted an append-only log
of its own working surface and used it to establish what it had and had not done.** Not the system
explaining the agent after the fact, but the agent reading the record to locate itself in a history it
partly authored.

Two things follow, neither claimed by the source:

- It is an accountability mechanism that **required no design** — it fell out of the board being event
  sourced. Compare [[axoniq-ai-agent-explainability-why-infrastructure-needs-to-remember]]'s argument
  that explainability is an infrastructure property, not a model property.
- It is a **read** use of the log by the actor, where the KB's explainability sources almost all describe
  a human or auditor reading it later. Whether agents routinely benefiting from their own audit trail is
  a real pattern or a one-off is open.

## Caveats

- A throwaway weekend post; the observation above is the wiki's reading, not his argument.
- n=1, undemonstrated, and the deletion incident is unexplained — nothing establishes what actually
  deleted the board.
- Vendor demo of the author's own platform.

## Related

[[eventmodelers-ai]] · [[agent-explainability]] · [[event-sourcing]] · [[agent-readable-model-artifacts]] ·
[[dilger-planning-like-excel-legible-to-human-and-ai]] · [[martin-dilger]] · [[decision-trace]]
