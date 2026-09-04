---
title: "Source: Fritzsche — Event Sourcing is not an audit feature (LinkedIn)"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [fritzsche-event-sourcing-is-not-an-audit-feature]
raw_file: [raw/notes/fritzsche-event-sourcing-is-not-an-audit-feature.md]
tags: [event-sourcing, business-capabilities, agent-explainability, substrate, focus]
---

# Source: Fritzsche — Event Sourcing is not an audit feature (LinkedIn)

LinkedIn post by **[[rico-fritzsche]]**, 2026-08-31. Raw capture:
`raw/notes/fritzsche-event-sourcing-is-not-an-audit-feature.md` — captured verbatim via **live logged-in
Chrome** (the headless watch cannot render this feed); only edit is collapsing LinkedIn's `hashtag\n#x`
markup. **Date is accurate to the day, not the hour** (derived from the relative age stamp at retrieval).

**Short-form restatement.** The post's closing paragraph points to "my latest article… the advantages of
not being tied to a centralized database schema" via a shortened link (`https://lnkd.in/eRqNcKDd`,
**not resolved at capture**). The article captured at
[[fritzsche-how-event-sourcing-grows-with-the-business]] (2026-08-30, one day earlier) **contains this
post's argument almost verbatim** in its "History Is a Consequence, Not a Cause" section, so it is very
likely the linked piece — an inference from wording and date, not a resolved URL. **Cite that article as
the fuller primary.**

**Register:** PRACTITIONER POSITION, explicitly — "In my experience", "For me, the real motivation".
IMPRESSION NOT MEASUREMENT.

## Summary

Six short paragraphs making one claim: **"Anyone who thinks Event Sourcing is an audit feature has
misunderstood its purpose."** He reports the common justification pattern — ES is sold on "it provides a
complete history," and conversely dismissed with "event sourcing would not be necessary if a history were
not needed" — and rejects both: "the fact that the history is preserved is a **consequence** of that very
property, but it is not the reason for it."

His stated motivation instead: "to provide **domain capabilities that are independent of one another and
not tied to a central, shared data structure**. At the same time, this avoids entity-oriented thinking.
By using events, the domain language is brought to the forefront, and the actual processes become
apparent." And the closing diagnosis: "The problem with entity-centric thinking is **less of a technical
nature**."

## Key points

- **The inversion:** history is an *effect* of making facts the record, not the *purpose* of doing so.
  The corollary he draws is the one that bites — a team that does not need history may still need ES,
  because the payoff is capability independence.
- **Three benefits named, in his order:** independent domain capabilities; no central shared data
  structure; avoidance of entity-oriented thinking. Domain language surfacing is a fourth, framed as a
  consequence.
- **"Less of a technical nature"** locates the entity problem in how teams think and who owns what — the
  same ownership framing as [[fritzsche-vsa-does-not-fix-entity-centered-thinking]] ("That is an
  ownership problem").

## Connections / contrast

- **This is the KB's standing objection to the vendor audit pitch.** [[axoniq]] sells event sourcing
  precisely as an explainability/audit capability, in both captures
  ([[axoniq-ai-agent-explainability-why-infrastructure-needs-to-remember]],
  [[axoniq-government-ai-explainability-requirements]]) — and the second one's whole argument is
  regulatory audit. [[goeleven-event-sourcing-not-auditing-for-free]] attacks the same framing from a
  third side (auditing is not something ES hands you free). Three positions to hold together: the vendor
  sells the consequence, Fritzsche says the consequence is the wrong motivation, Goeleven says the
  consequence isn't even automatic.
- **Tension inside his own corpus.** [[fritzsche-thinking-in-events]] (2026-07-03) lists "strong
  auditability" among the conditions that make ES "especially compelling." Reconcilable (a real benefit,
  a bad motivation) but unreconciled by him; his position appears to have **hardened over July–August
  2026**, and neither month should be quoted as his settled view.
- **Reinforces [[autonomous-domain-capabilities]] as the *reason* for ES**, not a consequence of it —
  which is the same ordering as [[command-context-consistency]] (the principle first, the store second).
- Adjacent: [[event-sourcing]] · [[business-capabilities]] · [[agent-explainability]] ·
  [[decision-trace]] · [[fritzsche-choosing-storage-is-choosing-what-your-system-forgets]].

## Limits

- **~180 words of assertion.** No evidence, no example, no engagement with the obvious counter (that for
  regulated domains, audit *is* a legitimate primary motivation — the case
  [[axoniq-government-ai-explainability-requirements]] makes at length).
- **Short-form restatement of an article**; the linked article was not resolved at capture (see above).
- Day-accurate date only.

_Source: `raw/notes/fritzsche-event-sourcing-is-not-an-audit-feature.md`._
