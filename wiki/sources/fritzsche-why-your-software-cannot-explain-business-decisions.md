---
title: "Fritzsche — Why Your Software Cannot Explain Its Business Decisions"
type: source
created: 2026-08-03
updated: 2026-08-03
sources: [fritzsche-why-your-software-cannot-explain-business-decisions]
raw_file: [raw/articles/fritzsche-why-your-software-cannot-explain-business-decisions.md]
tags: [agent-explainability, autonomous-domain-capabilities, command-context-consistency, event-sourcing, rpu, focus]
---

# Fritzsche — Why Your Software Cannot Explain Its Business Decisions

Blog article by **[[rico-fritzsche]]** (ricofritzsche.me, orig. Medium, 2026-07-23). The thesis:
**make the path from command → outcome explicit in the architecture; how you store state (relational or
event-sourced) is a separate decision.** Raw:
`raw/articles/fritzsche-why-your-software-cannot-explain-business-decisions.md`.

## The argument

- **The outcome alone can't explain the decision.** A row `{status: "cancelled"}` (or even a
  `ReservationCancelled` event) shows *what* happened, not *why* it was accepted — was the requester
  allowed? was the cancellation window still open? To explain a decision you need the **command** (the
  intention), the **relevant context** (only the facts a rule reads — not the whole `Reservation`
  object), the **rule applied**, and proof the context was **still valid at commit**.
- **A decision needs a *visible processing path*.** When command, context, rule, consistency-guard, and
  outcome exist scattered across a controller + a generic repository + a reused policy object + an ORM,
  every step may be present yet no structure *owns* the decision. The fix is the **Request Processing
  Unit (RPU)** — one request toward one **Domain Capability**, `command → obtain context → decide →
  guard-context-at-commit → record outcome → coordinate effects → return`. A developer explaining a
  decision **starts at `process_cancel_reservation`** and follows the same path the app followed.
- **Command Context Consistency, applied to explainability.** "A command is accepted only when the
  context it relied on is still valid at the moment the result is committed" — enforced by locks +
  constraints (relational) or a conditional append (event store). A guard conflict is **mapped to a
  business outcome** (a doubly-booked night → `BookingRejected: listing_unavailable`), not raised as a
  technical error.
- **The database protects state, not its meaning.** `SELECT … FOR UPDATE` / `FOR SHARE` and unique keys
  keep the Application State integral under concurrency, but "a database may protect the Application State
  — it must not invent its business meaning." **Storage is an explicit decision**: an event history
  retains outcomes in sequence and derives state; a relational model can retain decision-relevant facts
  in columns / decision records. Event Sourcing is *one* way to meet the obligation, not a prerequisite.
- **[[given-when-then|FC/IS]] is an implementation choice**: the Imperative Shell obtains context +
  commits + effects; the Functional Core is the pure `decide`. The RPU is defined by the *whole* path.

## Why it matters here

- The KB's most concrete architecture recipe for [[agent-explainability]] — reframing it from an
  event-store *storage* property ([[axoniq-ai-agent-explainability-why-infrastructure-needs-to-remember|AxonIQ]],
  [[roden-event-sourcing-meets-mcp-whole-story-for-llms|Roden]]) to an **architecture** property (the
  explicit command→outcome path via the RPU), with storage as a downstream choice. Ties
  [[autonomous-domain-capabilities]] (RPU as the boundary), [[command-context-consistency]] (the commit
  guard), and [[event-sourcing]] (one storage option). The "explain a decision months later" framing is
  the same regulatory driver as AxonIQ (EU AI Act / GDPR Art. 22).
- Caveat: single-author practitioner primary; a design argument with worked code, no external data.

## Links

Entities: [[rico-fritzsche]], [[ralf-westphal]]. Concepts: [[agent-explainability]],
[[autonomous-domain-capabilities]], [[command-context-consistency]], [[event-sourcing]], [[cqrs]],
[[given-when-then]].
Related sources: [[axoniq-ai-agent-explainability-why-infrastructure-needs-to-remember]],
[[roden-event-sourcing-meets-mcp-whole-story-for-llms]],
[[fritzsche-choosing-storage-is-choosing-what-your-system-forgets]],
[[fritzsche-command-context-consistency-principle]].

_Raw source: `raw/articles/fritzsche-why-your-software-cannot-explain-business-decisions.md`._
