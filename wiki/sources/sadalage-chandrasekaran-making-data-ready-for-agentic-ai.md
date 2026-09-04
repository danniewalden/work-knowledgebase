---
title: "Sadalage & Chandrasekaran — Making Your Data Ready for Agentic AI"
type: source
created: 2026-08-31
updated: 2026-08-31
sources: [sadalage-chandrasekaran-making-data-ready-for-agentic-ai]
raw_file: [raw/articles/sadalage-chandrasekaran-making-data-ready-for-agentic-ai.md]
tags: [business-capabilities, agentic-ai, data-architecture, agent-governance, autonomy, prompt-injection, model-context-protocol, compliance, focus]
---

# Sadalage & Chandrasekaran — Making Your Data Ready for Agentic AI

Article by **[[pramod-sadalage]]** and **[[prem-chandrasekaran]]** ([[thoughtworks]]), published on
[[martin-fowler]]'s site 2026-08-27. Raw capture:
`raw/articles/sadalage-chandrasekaran-making-data-ready-for-agentic-ai.md` (9,941 words).
The article discloses that AI assistance was used in writing it.

A data-architecture argument that arrives at the **[[business-capabilities]]** boundary from outside
the DDD/Event Modeling tradition, and lands two ideas this KB did not previously hold: **reversibility
as the predictor of safe autonomy**, and **"retrieved text informs, it never gates"** as a structural
answer to [[prompt-injection]].

## The thesis

For thirty years data systems were built for a human consumer who supplies the missing context and
**hesitates** at a number that looks wrong. An agent supplies neither:

> "A human hesitates at data that looks wrong; an agent acts on it anyway."

Every piece of implicit labor the analyst did for free has to move into the data itself. The authors
name **five attributes** of AI-ready data — Trusted, Contextual, Traceable, Governed, Operational —
each the flip side of a human job, and argue the failure mode when one is missing is not graceful
degradation but **confident failure**. Four topics build them, in order: data contracts and quality;
traceability and governance; the context layer; and searchable→actionable access.

## Key points

- **Agents can't smell bad data.** The worked scenario is a pricing agent quoting a stale $49.99
  against a real $59.99. Every step is technically correct; the data is the problem. Cited support:
  Precisely/Drexel LeBow's 2026 *State of Data Integrity and AI Readiness* (505 leaders, **87% believe
  their data is AI-ready, 43% name data readiness their biggest barrier**) and a KPMG Global AI Pulse
  survey (2,145 leaders, nearly half of executives seeing AI costs exceed benefits).
- **Data contracts as code.** Schema is law, not a suggestion — an explicit reversal of "schemaless is
  flexible," on the grounds that loose schemas are merely inconvenient for humans and dangerous for
  agents. Written in the Open Data Contract Standard, validated in CI/CD. Includes a **freshness SLA**
  keyed to *when the data was last successfully loaded*, not when a value last changed — so steady data
  isn't flagged stale and a stalled pipeline can't masquerade as fresh.
- **The quarantine pattern.** Contract validation is a gate in front of the agent-accessible store;
  failures go to a dead-letter queue with alerts. The agent then says "I don't have current pricing
  data" instead of quoting confidently. *"A better model won't rescue you from bad data."*
- **Medallion tiers, plus Adaptive Gold.** Bronze (raw) and Silver (validated) exist for lineage and
  human investigation; **agents see only Gold and above**. The proposed fourth tier, *Adaptive Gold*,
  has agents curate datasets from their own query patterns — extrapolated from Apple's DataHub CONTEXT
  2025 account of agents as "digital stewards" of the *catalog*, which the authors flag as an
  extrapolation.
- **The same rules for unstructured data.** The stale-price scenario has a RAG twin: a policy document
  updated but not re-embedded. The freshness SLA measures *when the index was last successfully rebuilt*,
  which catches both the unindexed document and the silently-stopped indexer. Contracts move to the
  surrounding metadata (source, version, timestamp, access scope per chunk).
- **Confidence-threshold routing, driven by data signals.** Below threshold, defer to a human — but the
  score must be driven by *data-level* signals (freshness, completeness, consistency), not just model
  confidence, because "a model can be sure of a stale answer." The authors are honest that composing one
  score is an **open design problem**: start with a hard gate (any SLA breach forces a human) and only
  add weighted scoring once it beats the simple rule.
- **The audit gap: from *what* to *why*.** Traditional logs record which tables were queried by which
  service account. They cannot say why the agent checked sanctions before credit terms, or what
  alternatives it rejected. **Agentic lineage** closes this with traces and spans borrowed from
  distributed-systems observability (Jaeger/Zipkin lineage; Langfuse, Arize Phoenix, OpenTelemetry as
  the agentic tooling).
- **The regulatory teeth.** EU AI Act **Article 12** (automatic lifetime logging so operation can be
  traced) and **Article 19** (retain ≥ 6 months); breach sits in the middle penalty tier at up to €15M
  or 3% of global turnover. The authors' broader point does not depend on the law: *"A system you can't
  explain is one you can't fully trust, defend, or fix."*
- **Staged autonomy, with observability un-staged.** A four-stage ladder (Shadow → Supervised →
  Autonomous-with-guardrails → Full). The load-bearing caveat: **autonomy is staged, observability is
  not** — instrumentation goes in at full strength on day one because retrofitting it is painful.
  Promotion should turn on evidence (tests, evals with mocked/replayed tool interactions), not a hunch.
- **Three security patterns:** *delegated access* (the agent acts with Alice's permissions, not a broad
  service account — "shared service accounts destroy attribution"), *just-in-time credentials* (a token
  scoped to one API for one customer for five minutes), and *least privilege*. These shrink what a
  hijacked agent can reach, breaking [[willison-lethal-trifecta]].
- **The context layer is three models, not one.** The **domain model** says what exists (entities,
  relationships, meaning rules; *consulted, never executed* — no query path runs through it); the
  **semantic model** says how numbers are computed (one versioned formula per metric, compiled to the
  same SQL every time); the **capability model** says what the agent may do. All three live as code in
  source control. What unites them is not meaning — "the capability model plainly is not" about meaning
  — but that *each is a place where a guarantee is declared once, in version control, instead of being
  worked out afresh by the model on every request*. **"The definitions are the layer; the interface, MCP
  today, is just the door."**
- **The access spectrum.** Retrieval (RAG) → real-time query → **write-back**, framed from Microsoft's
  Cloud Adoption Framework as RAG + MCP-Read + MCP-Write. [[model-context-protocol]] primitives sit on
  the same risk gradient: Resources (read-only) → Prompts → Tools (change state). Expose Resources
  first, graduate to Tools under governance.
- **Antipattern: naive API-to-MCP conversion.** Wrapping every REST endpoint one-to-one produces tool
  sprawl — 50 barely-distinguished tools, and LLM accuracy drops sharply as tool count climbs. On the
  Thoughtworks Radar at **HOLD**. *"Five to ten well described business capabilities will outperform 50
  thin API wrappers almost every time."* Explicitly protocol-agnostic: the properties that make access
  agent-ready (rich descriptions, parameterized access, clear schemas) survive whatever replaces MCP.

## The two claims that most change this wiki

### 1. Reversibility, not transaction size, predicts safe autonomy

Every capability declares **permissions** (who may invoke it, acting as whom) and an **owner** (who is
accountable when it misbehaves). Acting capabilities declare two more: **preconditions**, checked
against live state *at the moment of acting* rather than against what the agent read earlier in its
plan; and a **reversibility class** — cleanly reversible, reversible at a cost through a compensating
transaction, or irreversible.

> "Reversibility predicts safe autonomy better than the size of the transaction."

The worked contrast: a $50,000 internal ledger correction you can back out is safer to automate than a
$200 payment to an external account you cannot claw back. The prescription is to key guardrails to
reversibility rather than to transaction size, and to require human approval for irreversible actions
**whatever stage the agent has reached** — i.e. reversibility cuts *across* the autonomy ladder rather
than sitting on it. See [[autonomy-ladder]].

### 2. Retrieved text informs, it never gates

Business rules stay written in prose where the business writes them, but a rule that **gates** an action
must not be read and interpreted at the moment of acting. Rules are extracted ahead of time, curated by
a human, and stored as declared preconditions in the capability model, each with a provenance link back
to the passage it came from. At action time the agent may still read a ticket or a contract clause to
work out what to *propose*; only the declared rules decide what is *permitted*, checked deterministically
against live state.

The authors are careful about how strong a security claim this is. Removing retrieved text from the
authorization path means a poisoned document **cannot grant a permission the agent did not already
have** — stronger than merely shrinking a hijacked agent's reach. But it is *not* a complete defence:
injected text can still influence what the agent proposes, and a human approver shown fabricated
evidence may wave it through. They are equally careful about provenance: *"Detecting that a document
changed is easy; knowing that the change invalidated a precondition derived from it is a judgement, not
a diff."* What the link buys is a review queue, not an automatic invalidation.

## Where it sits relative to what the KB already holds

- The capability model — permissions, owner, preconditions, reversibility class — is a **data-architecture
  restatement of the [[business-capabilities]] boundary**, and a close sibling of
  [[devadoss-cead-capability-aligned-agent-design]]'s Agent Capability Contract. Neither cites the other;
  the convergence is the interesting part.
- "Agentic lineage" makes the [[agent-explainability]] argument from the *data* side rather than the
  event-store side — compare [[axoniq-ai-agent-explainability-why-infrastructure-needs-to-remember]] and
  [[fritzsche-why-your-software-cannot-explain-business-decisions]], which reach the same place from
  event sourcing.
- **Preconditions checked against live state at the moment of acting** is, in Event Modeling terms, the
  *given* of a command slice. The article arrives at the given/when/then decision shape without the
  vocabulary — see [[given-when-then]].
- "Design capabilities, not endpoints" is the capability boundary applied to tool design, and is the
  sharpest statement in the KB of why [[model-context-protocol]] surface area is an architecture
  decision rather than a wiring one.

## Caveats

- **Vendor-adjacent in places.** Thoughtworks Radar placements are cited as support for the authors'
  own positions; the Radar is a Thoughtworks artifact. The technical claims stand on their own, but the
  Radar citations are not independent corroboration.
- **Adaptive Gold is explicitly an extrapolation** by the authors' own admission, one step beyond
  Apple's catalog-curation account.
- **The confidence-score composition problem is unsolved**, and the article says so rather than papering
  over it.
- The survey figures (87%/43%, KPMG) are self-reported leader perception, not measured data quality.

## Related

[[business-capabilities]] · [[autonomy-ladder]] · [[agent-explainability]] · [[prompt-injection]] ·
[[model-context-protocol]] · [[context-engineering]] · [[given-when-then]] ·
[[devadoss-cead-capability-aligned-agent-design]] · [[thoughtworks]] · [[martin-fowler]]
