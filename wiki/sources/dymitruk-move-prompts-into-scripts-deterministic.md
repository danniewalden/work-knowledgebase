---
title: "Dymitruk — Move prompts into scripts; deterministic behaviour is the goal"
type: source
created: 2026-08-31
updated: 2026-08-31
sources: [dymitruk-move-prompts-into-scripts-deterministic]
raw_file: [raw/notes/dymitruk-move-prompts-into-scripts-deterministic.md]
tags: [event-modeling, event-sourcing, harness-engineering, loop-engineering, agentic-coding, focus]
---

# Dymitruk — Move prompts into scripts; deterministic behaviour is the goal

LinkedIn post by **[[adam-dymitruk]]**, 2026-08-15. Raw capture:
`raw/notes/dymitruk-move-prompts-into-scripts-deterministic.md`. Reproduced in full below — it is four sentences.

> "Move as much from your prompts and agent md files into scripts. Deterministic behaviour is your goal.
> Evidence of how things work should be intermediate text files in directories that correspond to steps
> in your processes - even inboxes and outboxes. You'll naturally arrive at #EventModeling and
> #EventSourcing."

## Why a three-sentence post gets a page

Because it is **the method's creator stating the KB's central thesis in its most compressed form**, and
because the direction of the claim is unusual. Most of the KB argues *from* Event Modeling *to* agent
practice — start with the method, apply it to harnesses. Dymitruk argues the reverse: **do harness
engineering well enough and you reinvent the method.** "You'll naturally arrive at" is a convergence
claim, not an advocacy one.

Three moves worth separating:

1. **Prompts → scripts.** Move behaviour out of natural language into code, because *"deterministic
   behaviour is your goal."* This is the [[harness-engineering]] instinct — engineer the environment,
   don't trust the prompt — stated as a migration path. Compare
   [[dilger-loop-engineering-never-argue-with-agent]] and
   [[bockeler-context-engineering-coding-agents]].
2. **Evidence as intermediate files in step-shaped directories.** An append-only, inspectable record of
   what happened at each stage — the [[decision-trace]] idea arrived at from the filesystem side, and
   the same instinct as [[anthropic-effective-harnesses-long-running-agents]]'s progress files.
3. **"Even inboxes and outboxes."** The tell, and the reason the convergence claim is more than
   rhetorical: inbox/outbox is a messaging pattern, and once your steps have them you have processors
   consuming and emitting — which is the **Automation pattern** in Event Modeling terms, and the
   transactional outbox in [[event-sourcing]] terms. He is pointing at a structure people build by
   accident.

## What it is not

It is not evidence. No worked example, no measurement, no named system — an assertion by the method's
creator that a particular convergence is natural. The KB should treat "you'll naturally arrive at" as a
hypothesis with an obvious test: do harnesses built without any Event Modeling exposure actually develop
event-shaped intermediate state? [[loop-engineering]]'s five-primitives literature is where to look, and
the un-ingested loop-engineering cluster (Batch F) is full of practitioners describing exactly these
file-and-directory conventions without the vocabulary.

## Caveats

- Four sentences; everything above the caveats is compression of a very small source.
- From the method's creator about the method's inevitability — maximally motivated.
- Two images accompanied the post and were not transcribed; they may contain the worked structure.

## Related

[[adam-dymitruk]] · [[harness-engineering]] · [[loop-engineering]] · [[event-modeling]] ·
[[event-sourcing]] · [[decision-trace]] · [[event-modeled-agent-design]] ·
[[anthropic-effective-harnesses-long-running-agents]] · [[process-managers-and-todo-lists]]
