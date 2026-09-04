---
title: "Source: Fritzsche — VSA does not fix entity-centered thinking (LinkedIn)"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [fritzsche-vsa-does-not-fix-entity-centered-thinking]
raw_file: [raw/notes/fritzsche-vsa-does-not-fix-entity-centered-thinking.md]
tags: [vertical-slice-architecture, business-capabilities, ddd, entity-centric-thinking, substrate, focus]
---

# Source: Fritzsche — VSA does not fix entity-centered thinking (LinkedIn)

LinkedIn post by **[[rico-fritzsche]]**, 2026-08-28. Raw capture:
`raw/notes/fritzsche-vsa-does-not-fix-entity-centered-thinking.md` — captured verbatim via **live
logged-in Chrome**; only edit is collapsing LinkedIn's `hashtag\n#x` markup. **Date accurate to the day,
not the hour.**

**This is the LinkedIn statement of the VSA × capability-ownership argument the 2026-09-04 sweep flagged
as a Medium-only gap.** He writes "I linked my full article in the first comment" — and **that comment
link was not resolved at capture, so the fuller primary is NOT in the KB.** Capturing it is a named gap
in the batch deltas. **Register:** PRACTITIONER ARGUMENT; the "test your design" list is a **heuristic he
proposes, not a study**.

## Summary

The sharpest statement in the KB of the limit of [[vertical-slice-architecture|VSA]]:
**"Vertical Slice Architecture (VSA) does not fix entity-centered thinking."** You can put endpoint,
handler, persistence and tests in one folder "and still organize the business around database
lifecycles." The tell is the folder listing: "When top-level folders are nouns and the requests beneath
them are Create, Get, Update, and Delete, the code is organized vertically. **Starting with the record
that changes makes the entity lifecycle the use-case boundary.** That is an ownership problem."

The distinction he draws is between locality and discovery: **"VSA improves locality *after* a team
chooses a request boundary. It does not discover that boundary. A CRUD-shaped request remains CRUD-shaped
inside its own slice."** The boundary should instead "follow what happens in the business and the language
used to describe it. Each business operation becomes the unit of change" — allocating an order, approving
credit, admitting a patient, settling a claim — because "database operations belong to the implementation
vocabulary."

He closes by extending the charge to Clean Architecture: "An entity-centered, CRUD-shaped Clean
Architecture implementation has the same issue. Horizontal layers and vertical slices arrange code
differently. **Both preserve the same ownership problem when entity lifecycles determine the use
cases.**"

## Key points

- **Locality ≠ boundary discovery.** This is the load-bearing sentence, and it is a claim no other KB
  source states this cleanly.
- **The three-part design test** (his heuristic, unvalidated):
  1. "List the business changes a generic update accepts."
  2. "Count how many slices depend on the shared entity model."
  3. "Change one business rule and observe what else must move."
  Note that (2) and (3) are effectively **coupling measurements by inspection** — the same quantity
  [[khononov-coupling-should-be-weighed-not-counted|Khononov]] wants *weighed*, and the same "what else
  must move" question [[balanced-coupling]] formalises.
- **Noun folders + CRUD verbs is the diagnostic silhouette** — the folder-tree analogue of
  [[event-modeling-anti-patterns|Dilger's board "shapes."]]
- **Framed as ownership, not aesthetics** — consistent with his "distributed technical ownership"
  critique of layering ([[rico-fritzsche-rpu-reactor-vocabulary]]).

## Connections / contrast

- **The counterweight [[vertical-slice-architecture]] most needed.** Every other agent-era claim on that
  page — [[bogard-vertical-slice-architecture-webinar-recording-whats-next|Bogard's]] "the blast radius
  stops at the slice boundary", [[miller-codebase-is-the-prompt-vertical-slices-ai|Miller's]] token
  argument, [[dilger-slicing-keeps-the-cost-curve-flat|Dilger's]] flat cost curve,
  [[nick-tune-enforced-application-architecture-agents-humans|Tune's]] build-time enforcement — is
  **conditional on the slice having been cut along a business operation.** This post says the cut is the
  hard part and VSA does not help with it. Filed in the same week as Bogard's post, they are best read as
  a pair.
- **Enforcement cuts both ways.** Tune's rule (no cross-feature imports, per-feature
  commands/queries/data-access) enforces slice *shape*; it would happily enforce a folder tree of
  `Orders/Create|Get|Update|Delete`. Mechanised boundaries make a bad boundary permanent — which is the
  strongest practical consequence of this post and neither author draws it.
- **Sharpens his own earlier objection.** The VSA page already carries his "a slice is only a local entry
  point into a larger shared structure" line; this post generalises it from *shared implementation*
  (models/repositories/aggregates) to *shared conceptualisation* (entity lifecycles as use cases) and
  extends it to Clean Architecture.
- **Partly disputed by Dudycz in the same batch.**
  [[dudycz-vertical-slices-ownership-and-external-dependencies]] agrees on the naming half — "If every
  operation is 'update the order', you have one feature and nothing to divide. Once you have
  `VerifyOrder`, `ConfirmOrder`, `RejectOrder`, you have folders, and each folder is named the way the
  business names the operation" — and cites Greg Young's Task-Based UI for the same reason. But Dudycz
  keeps **"business logic per entity or aggregate"** as a deliberate rule, which is exactly the shared
  entity model Fritzsche counts as a defect. Same diagnosis of CRUD naming, opposite conclusion about
  the entity.
- **Part of the four-capture entity-centred-thinking arc** in this batch (see
  [[fritzsche-why-the-entity-model-is-an-illusion]]).
- Adjacent: [[slice]] · [[business-capabilities]] · [[autonomous-domain-capabilities]] ·
  [[locality-of-reference]] · [[cqrs]] · [[fritzsche-clean-architecture-capability-over-layers]].

## Limits

- **Short-form post; the fuller article is uncaptured** (linked in the first comment, unresolved). This
  page is the only KB record of the argument, so it is thinner than the argument deserves.
- **No evidence.** No codebase, no before/after, no example of a team that reorganised and improved. The
  three-part test is a proposal.
- **No positive method for discovering the boundary.** "Follow what happens in the business and the
  language used to describe it" is the direction; [[event-modeling]] / [[event-storming]] are the obvious
  candidate methods and he names neither here.
- Day-accurate date only.

_Source: `raw/notes/fritzsche-vsa-does-not-fix-entity-centered-thinking.md`._
