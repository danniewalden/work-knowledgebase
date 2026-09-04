---
title: "Dilger — The First Event Modeling Conference (Munich, Oct 2025) — recap"
type: source
created: 2026-06-30
updated: 2026-06-30
sources: [dilger-first-event-modeling-conference-munich-recap]
raw_file: [raw/articles/dilger-first-event-modeling-conference-munich-recap.md]
tags: [event-modeling, event-sourcing, dynamic-consistency-boundaries, agentic-coding, conference, focus]
---

# Dilger — The First Event Modeling Conference (Munich, Oct 2025)

Recap by **[[martin-dilger]]** on eventmodelers.ai/Nebulit (published 2025-11-28), captured verbatim.
Source: `raw/articles/dilger-first-event-modeling-conference-munich-recap.md`.

**Important dating note:** this is the **inaugural** Event Modeling Conference (held **October 2025**,
recap Nov 2025) — **not** the **2nd** conference of **25–26 June 2026**, whose recap/recordings were
still unpublished as of the 2026-06-30 watch. Filed because it is new to the wiki and squarely
on-thread; the June-2026 recap remains an open watch item.

## Format

40 practitioners, two days in Munich, deliberately **not** a talks-at-attendees conference — five
parallel rooms each modeling a different problem, a dot-voted "marketplace" of community-pitched
topics, and live group modeling. Dilger's thesis: practitioner-to-practitioner collision compresses
years of pattern recognition into two days.

## The bits that matter for the KB

- **Announcements (Day-1 keynote, [[adam-dymitruk]]):** a planned **Event Modeling Certification
  program**, and a **joint venture between Dymitruk and Dilger — a new company focused on Tooling and
  Standardization for Event Modeling** ("the engineering part"). A governance/standardization signal
  for the method itself; watch for what this entity ships.
- **The marketplace's top topic — [[dynamic-consistency-boundaries|DCB]] vs. Aggregates** — with
  [[allard-buijze]] ([[axoniq]]) and Dymitruk in the room. Verdict from Dilger after "hundreds of
  systems": *"it depends"* — keep aggregates and risk later scaling pain, or invest in DCB upfront.
  A live, balanced read of the debate the KB tracks via
  [[dilger-dcb-is-what-event-sourcing-should-have-been]] and
  [[rico-fritzsche-es-does-not-require-aggregates-ccc-vs-dcb]].
- **AxonIQ AI-codegen demo (Day-2 keynote, Buijze)** — the new AxonIQ platform turning **Event Models
  into working code automatically**. This is the concrete "agent generates from the model" artifact
  the KB's [[event-modeled-agent-design]] gap keeps asking for — though it's a vendor keynote demo,
  not an independent published worked model. Pairs with the explainability case in
  [[axoniq-ai-agent-explainability-why-infrastructure-needs-to-remember]].
- **The headline insight — "the model is not the implementation."** *"Just because the event is in the
  Event Model doesn't mean it has to be in the code later."* The model is a **design/communication
  tool — a guide, not a blueprint**; in code you make pragmatic decisions (drop an event, merge three,
  split one along team boundaries). This is a notable **counterweight to Dilger's own
  [[dilger-is-code-still-the-source-of-truth|"model is the source of truth, code is disposable"]]
  framing** — here he stresses *freedom to diverge* in implementation. Worth flagging as a tension to
  watch, not a contradiction: source-of-truth for *intent*, latitude for *realization*.
- **The "zoom-in" / two-model approach** — keep the main Event Model high-level (information flow);
  for a complex automation/algorithm/workflow slice, create a second **zoom-in model** for the detail.
  A practical answer to the recurring *"how do I model automations / where does the logic go?"*
  question that dominated the live session — directly relevant to [[event-modeled-agent-design]]
  (where an agent's Automation logic lives).
- **Ecosystem maturing:** **OpenCQRS 1.0** (Frank Scheffler, Java) and **Cratis** (Einar
  Ingebrigtsen, .NET) presented alongside AxonIQ — three event-sourcing stacks across ecosystems.

## Why it matters here

Primary, first-person evidence on the focus area from the people who define the method: a
standardization JV, a live DCB-vs-aggregate reading, a real AxonIQ model→code demo, and two reusable
modeling patterns (model≠implementation; zoom-in models). Caveat: Dilger's own promotional venue
(closes with a workshop sales pitch), single-voice account, and the model→code demo is vendor-staged.

## Touches

[[martin-dilger]] · [[adam-dymitruk]] · [[allard-buijze]] · [[axoniq]] · [[nebulit]] ·
[[eventmodelers-ai]] · [[event-modeling]] · [[dynamic-consistency-boundaries]] ·
[[event-modeled-agent-design]] · [[event-sourcing]] · [[dilger-is-code-still-the-source-of-truth]]

_Source: `raw/articles/dilger-first-event-modeling-conference-munich-recap.md`._
