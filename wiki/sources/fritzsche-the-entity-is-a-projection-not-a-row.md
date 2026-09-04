---
title: "Source: Fritzsche — The entity is a projection, not a row (LinkedIn)"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [fritzsche-the-entity-is-a-projection-not-a-row]
raw_file: [raw/notes/fritzsche-the-entity-is-a-projection-not-a-row.md]
tags: [event-sourcing, ddd, entity-centric-thinking, substrate, focus]
---

# Source: Fritzsche — The entity is a projection, not a row (LinkedIn)

LinkedIn post by **[[rico-fritzsche]]**, 2026-08-28. Raw capture:
`raw/notes/fritzsche-the-entity-is-a-projection-not-a-row.md` — captured verbatim via **live logged-in
Chrome** (the headless scheduled watch cannot render this feed); the only edit is collapsing LinkedIn's
rendered `hashtag\n#x` markup. **Date accuracy:** derived from the relative age stamp at retrieval
(2026-09-04 11:08 UTC), so **accurate to the day, not the hour**.

**This is short-form restatement, not the primary.** The capture note identifies it as the companion post
to his article *Why the Entity Model Is an Illusion*, and the post itself closes with "In my latest
article I discuss why the entity we think we are storing is an illusion. Full article:
`https://lnkd.in/eD2uyvCP`" (shortened link, not resolved at capture). **The fuller primary is captured
at [[fritzsche-why-the-entity-model-is-an-illusion]] — cite that page for the argument; cite this one
only for the compressed formulation or for the fact that he pushed it to LinkedIn.**

**Register:** PRACTITIONER POSITION with the vehicle-rental worked example as illustration, **not
evidence** — IMPRESSION NOT MEASUREMENT.

## Summary

A ~200-word compression of the article's thesis. "I am more convinced than ever that, for years, we have
been laboring under the misconception that we must model objects that represent the real world." Trapped
there, "we often forget that things happen and that business processes consist of more than just an input
form to store data in a table." He rejects pre-defined entities on epistemic grounds — "To have a
finished data model, we'd need to know every aspect - which is rarely the case" — runs the vehicle
registration example (`VehicleAcquired -> VehicleReceived -> VehicleInfleeted -> VehicleReleasedForRental`,
because "the car rental company doesn't actually 'create' a vehicle"), and lands on the title claim: the
"Vehicle" - quoting him with his own hedge intact - "From my current perspective, it is not an entity in
our system. It is something that can appear in different forms as a projection."

## Key points

- **The row is the residue of the last write:** "In the entity-centric approach the database contains one
  row for each vehicle. The row resembles the vehicle itself, and is actually only the result of the last
  write. It holds the values that survived the last update and says nothing about how they got there."
- **Physical existence ≠ software entity:** "The vehicle physically exists, but in our system we only
  hold a reference. Every form that someone needs is derived from these events."
- **`CreateVehicle` is a database operation wearing a domain name** — the naming test that recurs across
  this batch.
- **The post is NOT sharper than the article - it is the same hedged sentence.** The article reads "From
  my current perspective, it is not an entity in our software"; the post reads "From my current
  perspective, it is not an entity in our system." The hedge is present in BOTH captures. Any page
  quoting the claim must keep it: he never states flatly that the entity is not in the software.

## Connections / contrast

- **Part of a four-capture arc in this batch** arguing one connected thesis:
  [[fritzsche-why-the-entity-model-is-an-illusion]] (the root article),
  [[fritzsche-how-event-sourcing-grows-with-the-business]] (the additive-schema sequel), this note, and
  [[fritzsche-vsa-does-not-fix-entity-centered-thinking]] (the architectural corollary: slice-shaped
  folders don't fix it). The batch deltas propose a dedicated concept page so the thesis is not smeared
  across four source pages.
- **Where the disagreement lies in the KB.** [[oskar-dudycz]] keeps the entity as the home of business
  rules ("business logic goes per entity or aggregate",
  [[dudycz-vertical-slices-ownership-and-external-dependencies]]) — a substantive conflict with this
  post's claim, filed in the same batch.
- Adjacent: [[event-sourcing]] · [[cqrs]] (the projection side) · [[autonomous-domain-capabilities]] ·
  [[business-capabilities]] · [[domain-driven-design]].

## Limits

- **Short-form social post**: no argument development, no counter-case, no engagement with normalization,
  querying or migration cost. Everything of substance is in the linked article.
- **Nothing measured**; a single illustrative sequence.
- The **shortened article link was not resolved at capture**; the identification with the captured article
  rests on the capture note and on the near-identical wording, not on a resolved URL.
- Date is **day-accurate only** (relative-timestamp derivation).

_Source: `raw/notes/fritzsche-the-entity-is-a-projection-not-a-row.md`._
