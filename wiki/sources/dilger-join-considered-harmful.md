---
title: "Dilger — Join considered harmful"
type: source
created: 2026-08-31
updated: 2026-08-31
sources: [dilger-join-considered-harmful]
raw_file: [raw/notes/dilger-join-considered-harmful.md]
tags: [event-modeling, cqrs, slice, data-modeling, focus]
---

# Dilger — Join considered harmful

LinkedIn post by **[[martin-dilger]]**, 2026-08-24. Raw capture:
`raw/notes/dilger-join-considered-harmful.md`. 45 reactions, **34 comments** — by some distance the most
argued-with Dilger capture in the KB, which is itself the signal.

## The claim

> "Every SQL statement is essentially a 'select * from ? where ?'. As the data views are special and
> tailor made to each use case, there is simply no need to join in 99.9% of all use cases."
>
> "Does that mean we embrace redundant data? yes. **That's actually a precondition for sliced
> architectures.**"

Made jointly with Marc Klefter in a workshop, and Dilger enjoys the reaction — "every DBA now gasping for
air… always enjoying this moment."

## Why it matters here

This is the **data-modelling consequence of slicing**, and the KB had it nowhere. If a [[slice]] owns a
read model tailored to one use case, the query degenerates to a filtered select and the join disappears —
but only because the shape was decided upstream, at modelling time. The redundancy is the price, and he
argues it is a precondition rather than a compromise.

Two qualifications the post does not make, and the wiki should:

- **The redundancy is *derived*, not duplicated authority.** Read models are projections rebuilt from the
  event log, so there is still one source of truth; this is not the same as denormalising a relational
  schema and hoping writes stay consistent. That distinction is what makes the claim defensible and it
  goes unstated — plausibly why 34 comments happened. See [[event-sourcing]], [[cqrs]].
- **"99.9%" is rhetoric, not measurement.** No basis is given.

The provocation is deliberate and the framing is an allusion to Dijkstra's "Go To Statement Considered
Harmful" — a genre marker for "this thing you were taught is a default is actually a choice."

## Caveats

- Workshop anecdote, no data, deliberately provocative.
- The comment thread — where the actual argument happened — was not captured. Worth a targeted pull on a
  live sweep, since it likely contains the strongest available objections to slicing from a data
  perspective.

## Related

[[slice]] · [[cqrs]] · [[event-sourcing]] · [[event-modeling]] · [[vertical-slice-architecture]] ·
[[martin-dilger]] · [[triplet-architecture]]
