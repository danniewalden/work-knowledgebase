---
title: "Fritzsche — Who Owns a Rule Shared Across Domain Capabilities?"
type: source
created: 2026-08-03
updated: 2026-08-03
sources: [fritzsche-who-owns-a-rule-shared-across-domain-capabilities]
raw_file: [raw/articles/fritzsche-who-owns-a-rule-shared-across-domain-capabilities.md]
tags: [business-capabilities, autonomous-domain-capabilities, command-context-consistency, coupling-cohesion, dry, focus]
---

# Fritzsche — Who Owns a Rule Shared Across Domain Capabilities?

Blog article by **[[rico-fritzsche]]** (ricofritzsche.me, 2026-07-30), answering a reader's challenge to
[[rico-fritzsche-rpu-reactor-vocabulary|"the domain is capabilities, not object models"]]: if every RPU
owns its whole decision path, how do you stop shared invariants (identity, money, compliance) from either
**drifting** across capabilities or rebuilding a **central service layer**? Raw:
`raw/articles/fritzsche-who-owns-a-rule-shared-across-domain-capabilities.md`. Directly advances the
flagged-important [[business-capabilities]] thread.

## The core move — separate *kinds* of shared knowledge

Treating "identity, money, compliance" as one bucket ("shared invariants") hides the design decision.
Fritzsche splits them by **architectural home**:

| Kind of knowledge | Example | Home |
| --- | --- | --- |
| **State invariant** | a listing-night belongs to ≤1 active reservation | Application State, enforced **at commit** |
| **External fact** | a subject authenticated at an assurance level | a **Provider**, optionally recorded as a fact |
| **Stable semantics** | money has an amount + a currency | a small **pure type** / generated local code |
| **Shared policy** | AML-42 release 2026-07 in a jurisdiction | a **versioned policy authority**; applied by the RPU |
| **Capability decision** | release or reject this payout | the owning **RPU** |

## Key points

- **An invariant is a property of state** (Lamport: true in every reachable state), enforced **at the
  commit boundary** — not by a shared helper. Two RPUs may both call `is_night_available()` and still
  both accept; only a unique/exclusion constraint (relational) or a conditional append (event store)
  rejects the second write. "A shared helper keeps implementations textually consistent; concurrent-write
  safety comes from the commit mechanism" (echoes invariant-confluence: independent execution is safe
  only when independently-valid results stay valid when combined).
- **Shared *code* ≠ shared *knowledge*** (the DRY-misread from *The Pragmatic Programmer*): two validators
  with identical code but different reasons to change should **not** be merged. Capability-local
  duplication is fine when owners/reasons differ.
- **One policy, many local evaluators.** A shared regulation gets **one authoritative immutable release**
  (id, content digest, jurisdiction, effective period) distributed to each RPU as generated code / a pure
  package / a policy bundle; each release ships a **conformance suite** (accepted/rejected/boundary/
  missing-fact/expired cases) run against every evaluator → *semantic consistency with local execution*.
  Activation is its own recorded fact; if the active release changes before commit, CCC fails and the RPU
  re-decides. (OPA bundles as one technical form — but distribution is eventually consistent, so a hard
  legal cutoff needs controlled activation.)
- **`GenericService.isAllowed()` is the anti-pattern** for all three (identity/money/compliance): it
  hides the facts that explain the answer. Identity in particular decomposes into domain identity /
  identifier uniqueness (a state concern) / proofing+authentication (a Provider, per NIST 800-63-4) /
  authorization (the RPU's call).

## Why it matters here

- The most direct answer yet to "**does capability autonomy break down on shared rules?**" — it doesn't,
  if you name the kind of knowledge and give each its own authority while the **final decision stays with
  the owning capability**. Strengthens [[business-capabilities]] and [[autonomous-domain-capabilities]],
  grounds [[command-context-consistency]] (the commit-time enforcement), and gives a concrete
  coupling-taxonomy reading (shared semantic primitives are an acknowledged, explicit, versioned
  dependency — cf. [[balanced-coupling]]).
- Caveat: single-author practitioner primary; the policy-authority machinery is described, not measured.

## Links

Entities: [[rico-fritzsche]]. Concepts: [[business-capabilities]], [[autonomous-domain-capabilities]],
[[command-context-consistency]], [[coupling-taxonomy]], [[balanced-coupling]], [[event-sourcing]].
Related sources: [[rico-fritzsche-rpu-reactor-vocabulary]],
[[rico-fritzsche-autonomous-domain-capabilities-ccc]], [[fritzsche-command-context-consistency-principle]],
[[devadoss-cead-capability-aligned-agent-design]].

_Raw source: `raw/articles/fritzsche-who-owns-a-rule-shared-across-domain-capabilities.md`._
