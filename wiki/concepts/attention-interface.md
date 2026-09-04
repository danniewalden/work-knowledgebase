---
title: Attention Interface
type: concept
created: 2026-09-04
updated: 2026-09-04
sources: [mcateer-evolution-of-the-agent-harness, anthropic-effective-harnesses-long-running-agents]
tags: [harness-engineering, agent-harness, harness-absorption, attention-interface, prediction, focus]
---

# Attention Interface

**Once the model absorbs the computer-facing harness, the harness inverts and becomes a surface aimed at
the human.** Coined by [[mcateer-evolution-of-the-agent-harness|Dan McAteer (2026-08-22)]]: *"The harness
was born as the human interface to the model… The harness becomes the model's interface to our human
attention."* And, flatly: *"Absorption doesn't end the harness. Absorption inverts the harness."*

This is the second half of the [[harness-absorption]] thesis, and the half that carries a
**where-to-invest** claim rather than a description.

## The scarcity premise

The argument turns on which resource ran out. Quoting Ryan Lopopolo via the same piece: *"The only
fundamentally scarce thing is the **synchronous human attention** of my team."* Tokens became abundant;
attention did not. So the model↔harness gap that used to *be* agent effectiveness "migrates across the
human boundary" and becomes **"the space between what the agent asks of the human, and what the human is
able to answer."**

Read against the rest of the KB, that is the same bottleneck the verification thread reaches from the
other side — the constraint is not the agent's output but the human's capacity to receive it.

## The falsifiable prediction, with a date

Made **2026-08-22**: within a year, every agentic-AI company ships a **human attention policy surface** as
universally as `AGENTS.md` — a declared, versioned policy governing *"when it's allowed to interrupt you,
when it should keep working, which decisions it can make alone and which decisions need your approval"* —
and it becomes **learnable**, because *"every correction becomes useful data."*

**Diarise a check for ~2027-08.** This is the rare KB claim with a stated mechanism, a stated artifact and
a deadline, so it can actually be scored rather than argued about.

## Current sparks

Nothing yet is an attention policy surface, but several existing patterns are aimed at the same boundary:

- **Progress files and status artifacts** ([[anthropic-effective-harnesses-long-running-agents]]) — written
  for the *next session*, but read by the human as the interrupt-free status channel.
- **Agentic approval queues** — approval as a queued, deferrable item rather than a synchronous block.
- The KB's own [[append-and-review-note]] and [[decision-trace]] patterns, which exist precisely so a
  human can arrive late and still be able to answer.

## Caveats

**A practitioner prediction in an essay, with no evidence.** No product implements it, no user study
supports it, and the framing device it rests on (the two curves of [[harness-absorption]]) is narrative
rather than measured. It is filed because the prediction is dated and checkable, not because it is
supported.

## Related

[[agent-legibility]] · [[agent-governance]] · [[harness-absorption]] · [[agent-harness]] ·
[[autonomy-ladder]] · [[unattended-coding-agents]] · [[guardian-agents]] · [[harness-engineering]]

_Sources: [[mcateer-evolution-of-the-agent-harness]] · [[anthropic-effective-harnesses-long-running-agents]]._
