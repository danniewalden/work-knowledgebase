---
title: "Dilger — From Idea to Event Model to Code, and Back (Craft Conf talk)"
type: source
created: 2026-06-14
updated: 2026-06-14
sources: [dilger-craft-conf-idea-to-event-model-to-code]
tags: [event-modeling, event-sourcing, cqrs, spec-driven-development, agentic-coding, focus]
---

# Dilger — From Idea to Event Model to Code, and Back (Craft Conf talk)

Conference-talk listing for **[[martin-dilger]]** at **Craft Conference, Budapest** (Jun 4–5, 2026),
titled *"From Idea to Event Model to Code — and Back: A Structured Approach to Building Scalable Systems
with Event Modeling, Event Sourcing, and Agentic Coding."* Raw capture (talk abstract + speaker bio,
from the AxonIQ event listing): `raw/notes/dilger-craft-conf-idea-to-event-model-to-code.md`.

## Summary

The talk's framing question — *"What if your requirements were something you could run?"* — is the
sharpest one-line statement in the KB of the [[event-modeled-agent-design]] focus. Dilger argues most
teams play an expensive **"telephone game"**: ideas become written specs, specs become tickets,
tickets become code, and the original intent leaks out along the way, producing systems that surprise
their builders and disappoint users.

His alternative: combine **[[event-modeling]]** and **[[event-sourcing]]** to build a shared, *visual*
understanding of a system — behavior, decisions, data flow — that business and engineering can read,
challenge, and refine **before** any production code. Crucially the model doesn't stop at
documentation: it becomes a **living specification**, the single source of truth that **drives code
generation** and acts as the foundation for **[[agentic-coding]]**. *"When the model changes, the
system changes with it — not the other way around."*

## Key points

- **Models don't rot** — they're actively worked on, not archived (counters the standard
  documentation-decay objection to up-front modeling).
- **The model is the source of truth** — readable by business, engineering, and management alike.
- **Changes are welcome** — they *extend* systems rather than break them (the
  [[open-closed-principle]] / flat-feature-cost claim that recurs across the Event Modeling sources).
- Closes with a **live demo of the full loop**: idea → visual model → generated code → and back again.

## In the KB

This is the **conference-talk crystallization** of Dilger's running LinkedIn thesis — the same
"model as a runnable/[[spec-driven-development|living spec]]" argument as
[[dilger-model-is-a-living-spec-always-on-agent]] and [[dilger-spec-driven-development-applied]], but
stated as a single structured arc (idea→model→code→back). It also names the **EM + ES + CQRS +
agentic-coding** stack explicitly, tying the focus area to the design substrate
([[event-sourcing]], [[cqrs]]). It's a talk *abstract*, not a transcript — strong on framing, no new
worked artifact, so it reinforces rather than extends [[event-modeled-agent-design]] (the standing gap,
a worked multi-agent event model, remains open). Provenance note: Dilger is here billed as **founder of
[[nebulit]] GmbH** and author of *"Understanding Eventsourcing"* (the first German-language book on
Event Modeling).

## Links

Entities: [[martin-dilger]], [[nebulit]]. Concepts: [[event-modeling]], [[event-sourcing]], [[cqrs]],
[[spec-driven-development]], [[agentic-coding]], [[event-modeled-agent-design]], [[open-closed-principle]].
Related sources: [[dilger-model-is-a-living-spec-always-on-agent]],
[[dilger-spec-driven-development-applied]], [[dilger-hold-my-beer-engineer]].
