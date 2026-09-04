---
title: "Dilger — How does DCB affect Event Modeling?"
type: source
created: 2026-07-06
updated: 2026-07-06
sources: [dilger-how-does-dcb-affect-event-modeling]
raw_file: [raw/articles/dilger-how-does-dcb-affect-event-modeling.md]
tags: [event-modeling, dcb, event-sourcing, given-when-then, agentic-coding, code-generation, focus]
---

# Dilger — How does DCB affect Event Modeling?

Source: [[martin-dilger]], *"How does DCB affect Event Modeling?"*, LinkedIn Pulse (his
**"Event Modeling applied"** newsletter, ~1,500 subscribers), **2026-07-06**. Raw capture:
`raw/articles/dilger-how-does-dcb-affect-event-modeling.md`. On the tight
[[event-modeled-agent-design|EM×agents]] focus and the [[dynamic-consistency-boundaries|DCB]] substrate.

## Summary

Dilger answers a question the KB has tracked since the [[dilger-first-event-modeling-conference-munich-recap|Munich conference]]
("how do I model the Decision Model / where does DCB fit in an event model?"): after modeling several
systems with [[dynamic-consistency-boundaries|DCB]], his conclusion is that Event Modeling is **"not
affected at all — quite the opposite, everything gets simpler."** The piece doubles as a compact
statement of how [[event-modeling]], [[given-when-then|GWT]], and AI code-generation interlock.

## Key points

- **Aggregates = "Static Consistency Boundaries."** Structuring events into streams via aggregates
  forces an up-front "what belongs to Customer Management vs Course Subscriptions" decision that is
  "set in stone" by production and costly to revisit. DCB instead treats **all events within a bounded
  context as one global stream** and focuses on "what actually happened." (Restates his
  [[dilger-dcb-is-what-event-sourcing-should-have-been|Static-vs-Dynamic CB]] naming line.)
- **DCB *simplifies* Event Modeling.** With DCB you model **one swimlane per system / bounded
  context**, and swimlanes revert to their intended purpose — **showing integration between systems and
  teams** (e.g. Payments = a different team's system), *not* stream design. "Whenever information
  crosses a lane, we need to pay attention" — the lanes are integration points.
- **You do not model a separate "Decision Model."** The information a command handler needs to decide
  is supplied automatically by the **GIVEN** part of the [[given-when-then|GWT]] scenarios. "How do we
  model the Decision Model...? We don't." Aggregates or DCB — no effect on the event model itself.
- **DCB makes decisions granular (command-by-command).** Where an aggregate meant loading all its
  guarded events (and cross-aggregate consistency meant sagas / compensations / snapshots as a cache),
  DCB decides per command. In the **Axon Framework** each command handler declares a **Criteria** — an
  SQL-like query fetching exactly the events needed to decide (e.g. "all `CustomerRegistered` for this
  email + all `SubscribedToCourse` for this email+course"). 
- **Codegen from the spec (the agent seam).** Writing those Criteria by hand is cumbersome, "so we
  typically generate this code directly from the specifications. AI is really good at that" — the
  **Axon Build Kit** for the [[eventmodelers-ai|Eventmodelers platform]] translates the event model to
  executable code **and generates the test cases**; changing rules = adding GWTs, reflected in code
  automatically. (Extends [[dilger-build-kits-model-to-generated-code|build kits]] and the
  [[dilger-event-modeling-agent-harness|Agent Harness]].)
- **Tags are indices, not domain concepts.** The most-asked question ("how do you model Tags?") — you
  don't; a tag is a technical optimization, not essential to the business, so it has no place in the
  model. To let a handler/agent query events, they must be tagged, expressed via a **publicly documented
  schema** so any code generator can plug in. For now he **reuses the `id`-attribute** (the identifying
  attribute already used to identify a stream) rather than adding an `indexed` attribute — "I'm slow in
  changing the public schema." "AI can figure this out by itself pretty well," but he prefers some control.
- **Two session types.** **Discovery** (no technical details — "stakeholders care least") vs
  **Detailed-Modeling** (add tags/meta to support codegen, "often just with engineers before handing the
  slice to an Agent"). Cleanly separates the human-alignment phase from the agent-handoff phase.

## Why it matters

Resolves several open KB threads at once. It closes the Munich-recap's recurring *"where does the logic
/ Decision Model go?"* question (answer: nowhere new — read the GWT **GIVEN**), and it reframes the
[[dynamic-consistency-boundaries|DCB-vs-aggregates]] debate from the *modeling* side: DCB is not just a
storage-layer choice but one that **removes** modeling ceremony (stream design) and lets swimlanes mean
*integration* again. It also sharpens the [[event-modeled-agent-design|agent]] seam — model → GWT →
generated Criteria + tests via the Axon Build Kit — and the [[given-when-then|GWT]]-as-decision-context
insight is new to the KB. Caveat: vendor-adjacent (promotes the Eventmodelers platform + Axon Build Kit;
his own DCB-favorable framing), single-author opinion, worked via one course-registration example.

## Links

[[dynamic-consistency-boundaries]] · [[event-modeling]] · [[given-when-then]] · [[event-modeled-agent-design]] ·
[[dilger-dcb-is-what-event-sourcing-should-have-been]] · [[dilger-build-kits-model-to-generated-code]] ·
[[dilger-event-modeling-agent-harness]] · [[event-sourcing]] · [[cqrs]] · [[axoniq]] · [[allard-buijze]] ·
[[eventmodelers-ai]] · [[martin-dilger]]

_Source: [[dilger-how-does-dcb-affect-event-modeling]] (raw: `raw/articles/dilger-how-does-dcb-affect-event-modeling.md`)._
