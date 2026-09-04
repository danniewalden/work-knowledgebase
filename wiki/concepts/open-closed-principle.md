---
title: Open–Closed Principle
type: concept
created: 2026-06-13
updated: 2026-06-19
sources: [semaphore-dymitruk-event-modeling, eventmodeling-what-is-event-modeling, dilger-done-is-done-open-closed-new-slice]
tags: [software-design, principle, event-modeling]
---

# Open–Closed Principle

The **Open–Closed Principle (OCP)** — one of the SOLID design principles, originally
stated by Bertrand Meyer — holds that software entities should be **open for extension
but closed for modification**. You add new behaviour by adding new code, not by editing
existing, already-working code.

## Why it matters in this wiki

OCP is one of the neighbouring principles [[adam-dymitruk]] invokes to explain why
[[event-modeling]] behaves the way it does ([[semaphore-dymitruk-event-modeling]]).
Because an event-modeled system is a **timeline of immutable events**, each state
transition (command → event) can be extended independently: new features arrive as new
events, commands, and slices on the timeline rather than as edits to existing ones
([[eventmodeling-what-is-event-modeling]]). This is the mechanism behind Event Modeling's
headline payoff — the **flat feature-cost curve** that makes fixed-price, any-order
delivery plausible: if adding the Nth feature doesn't force you to reopen the first N−1,
cost stops compounding.

It is the same instinct as [[event-sourcing]]'s "no erasers" rule (append, never overwrite)
and a close relative of [[domain-driven-design]]'s emphasis on stable boundaries.

## "Done is Done" — OCP as a slice decision (Dilger, 2026-06-18)

[[martin-dilger]] operationalizes OCP as a question to ask before building: *"can I build this without
touching any existing code that already works?"* — his **"Done is Done"** principle
([[dilger-done-is-done-open-closed-new-slice]]). The payoff is that a genuinely distinct concept becomes
a **new [[vertical-slice-architecture|slice]]** (an *addition*) rather than an *extension* of existing
code. His worked example: "Guest Invitations" only superficially resemble "Invitations" (different rules
and lifecycle), so reusing-and-extending would **couple concepts that should stay separate** — and on a
live [[event-sourcing|event-sourced]] system, modifying an existing flow risks
[[event-versioning-and-upcasting|migrations/upcasters]] and full retesting. This is the coupling-over-reuse
view (cf. [[balanced-coupling]], [[business-capabilities]]) and a concrete
[[event-modeled-agent-design|model-a-slice-then-let-an-agent-build-it]] anecdote.

## Related

[[event-modeling]] · [[event-sourcing]] · [[domain-driven-design]] · [[cqrs]] ·
[[vertical-slice-architecture]] · [[balanced-coupling]]

_Sources: [[semaphore-dymitruk-event-modeling]] · [[eventmodeling-what-is-event-modeling]] · [[dilger-done-is-done-open-closed-new-slice]]._
