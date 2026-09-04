---
title: Agent Explainability
type: concept
created: 2026-06-21
updated: 2026-09-04
sources: [axoniq-ai-agent-explainability-why-infrastructure-needs-to-remember, roden-event-sourcing-meets-mcp-whole-story-for-llms, akka-event-sourcing-backbone-agentic-ai, confluent-agentic-event-driven-systems-architecture, martinfowler-prince-building-reliable-agentic-ai-systems, fritzsche-why-your-software-cannot-explain-business-decisions, fritzsche-choosing-storage-is-choosing-what-your-system-forgets, sadalage-chandrasekaran-making-data-ready-for-agentic-ai, axoniq-government-ai-explainability-requirements]
tags: [agentic-ai, agent-governance, event-sourcing, compliance, focus]
---

# Agent Explainability

The ability to reconstruct and communicate **why** an autonomous AI system made a specific decision —
the conditions that existed, the inputs it acted on, and the sequence of events that led to the
outcome. For consequential automated decisions (loans, claims, transaction flags, clinical
recommendations) this is a regulatory requirement under the **EU AI Act, SR 11-7, GDPR Article 22**,
and OCC/CFPB guidance.

## The core claim: explainability is an infrastructure problem, not a model problem

[[axoniq]] ([[axoniq-ai-agent-explainability-why-infrastructure-needs-to-remember]]) argues the causal
chain that produced an agent decision begins **before** the model's inference — in the events,
commands, and state transitions that shaped the context. **State-based architectures overwrite that
history**; no model-level interpretability tool can recover what the infrastructure never captured.
[[event-sourcing]] is the architecture that captures it: every decision becomes a permanent,
immutable, replayable, queryable record, so "the system already knows" why.

## Event store vs. event stream

A distinction AxonIQ makes load-bearing: an event **stream** (Kafka/Confluent) *moves data* and
records *what* happened (built for throughput); an event **store** (Axon Server) *captures decisions
with full causal context* and records *why* (built for auditability/replay). For agent explainability,
the store is required and the stream is not sufficient — a sharper line than the streaming-centric
[[agentic-event-driven-systems]] sources draw.

## Relationship to neighbours

- **Same backbone, two payoffs.** [[event-sourcing]]'s immutable log delivers both *explainability*
  (this page, AxonIQ's audit/compliance angle) and *context quality* for the model itself
  ([[golo-roden|Roden's]] "events are the whole story for LLMs", [[roden-event-sourcing-meets-mcp-whole-story-for-llms]],
  [[context-engineering]]). The same store answers "why did it decide that?" and "what does it need to
  decide well?"
- **Governance.** The event log *is* the audit trail — a concrete mechanism for [[agent-governance]]
  and a place for [[guardian-agents]] to subscribe and veto.
- **Corroboration.** [[akka-event-sourcing-backbone-agentic-ai|Akka]] (auditability/perfect recall),
  [[confluent-agentic-event-driven-systems-architecture|Confluent]] (decision-level observability,
  deterministic replay), and the non-vendor [[esaa-event-sourcing-for-autonomous-agents|ESAA]] preprint
  reach the same conclusion.

## Explainability in practice — citation-based grounding (PRINCE, 2026-06)

[[martinfowler-prince-building-reliable-agentic-ai-systems|Bayer's PRINCE]] shows a complementary,
*application-level* explainability mechanism for a regulated (pharma) setting: every generated claim is
grounded with **per-sentence citations** back to the source chunk — document, page number, and exact
quote — plus visible intermediate steps (queries formed, tools used) and human-in-the-loop sign-off on
regulatory drafts. Where AxonIQ's argument is about the *infrastructure* recording **why** a decision was
made, PRINCE's is about making the *answer* verifiable at the point of use. The two are layers of the
same goal (traceability/reviewability), and PRINCE's regulated-domain framing is corroboration that explainability is a hard production requirement,
not a nice-to-have — though **not independent** corroboration in the sense the KB needs: it is
Thoughtworks-authored, and Thoughtworks coined [[harness-engineering]]. The genuinely independent
support on this page is the non-vendor ESAA preprint and the EU AI Act's own text. See [[thoughtworks]].

## The regulatory map, widened — and where it comes from (AxonIQ, 2026-08)

[[axoniq-government-ai-explainability-requirements]] takes the page's three instruments (EU AI Act, SR
11-7, GDPR Art. 22) to roughly a dozen across nine jurisdictions: US FOIA and records-retention rules
plus federal AI guidance and state algorithmic-accountability laws; **Canada's Directive on Automated
Decision-Making** (impact assessment and meaningful explanations, scaled by impact level); the EU AI Act
layered over GDPR and national administrative law's duty to give reasons; the **UK's Algorithmic
Transparency Recording Standard**; South Korea's AI framework law, Singapore's Model AI Governance
Framework, Japan's national guidelines; Australia's voluntary guardrails pending mandatory high-risk
ones; New Zealand's **Algorithm Charter**; Brazil's PL 2338/2023. AxonIQ's framing: "None of these
frameworks asks it in quite the same words, but the direction is clear" — and an agency treating each as
a separate compliance project "will run that project forever."

It also supplies a driver specific to the public sector that no other KB source carries: **explainability
as legitimacy** rather than compliance, and **retention on institutional timescales** — a decision
questioned "in a decade, by an oversight body that does not yet exist, under a legal standard that has
not yet been set," where "institutional memory lives in retired databases, departed employees, and file
formats nobody can open."

**Read it as a checklist of instruments to verify, not as a statement of obligation:** this is a
**vendor's** reading (AxonIQ sells an event store), unverified against primary law here, with a corporate
byline. Its single number — an 80% reduction in audit-preparation time at an unnamed large US bank — is a
**VENDOR SELF-REPORT** and must carry that marker at every use. And the post contains **no agent-specific
evidence**: the AI section is argument, with nothing measured about an agent decision being explained.

## Caveat

Articulated mainly by event-sourcing vendors ([[axoniq]], [[golo-roden]], [[akka]]), so "you need an
event store" is motivated. What holds up under that discount: the **regulatory drivers are real and
external** (EU AI Act Arts. 12/19, cited from the text below, not from a vendor paraphrase), and the
architecture argument recurs across sources with different interests — the non-vendor
[[esaa-event-sourcing-for-autonomous-agents|ESAA]] **preprint** (arXiv, not peer-reviewed) and the
data-architecture arrival below. **Not** counted as independent here: the Bayer/PRINCE case, which is
Thoughtworks-authored, and Thoughtworks coined [[harness-engineering]] — see [[thoughtworks]] on the
concentration problem.

## Explainability as an *architecture* property, not just storage (Fritzsche, 2026-07)

The vendor sources above locate explainability in the **event store**. [[rico-fritzsche|Fritzsche]] adds
the **architecture-side** complement: a decision is explainable when the app makes its
`command → context → decide → guard → outcome` path **explicit** — owned by a **Request Processing Unit**
— so a developer can follow the exact path the app followed instead of reconstructing it across a
controller + generic repository + reused policy + ORM
([[fritzsche-why-your-software-cannot-explain-business-decisions]]). *Storage is a separate, deliberate
decision*: an event history or a relational model with retained decision-records can both answer "why,"
because ([[fritzsche-choosing-storage-is-choosing-what-your-system-forgets|the discipline of the record]])
"overwritten records keep state; appended records keep facts" — the "why" survives only while its records
do. This reframes the KB's event-store-centric account: the store must *not forget*, but the **explicit
decision path** ([[autonomous-domain-capabilities|RPU]] + [[command-context-consistency|CCC]]) is what
makes the retained facts add up to an explanation.

## The same argument from the data side — "agentic lineage" (Sadalage/Chandrasekaran, 2026-08)

A third arrival at this page's core claim, this time from **data architecture** rather than from an
event store or an application architecture ([[sadalage-chandrasekaran-making-data-ready-for-agentic-ai]]).
The framing is the cleanest statement of the gap the page is about:

> "Traditional audit logs can tell you **what** happened, but they can't tell you **why**."

Their **agentic lineage** extends data lineage from *which sources were accessed* to *why the agent
decided to access X, because it found Y in source Z*, using the **traces and spans** model borrowed
directly from distributed-systems observability (Jaeger/Zipkin; Langfuse, Arize Phoenix and
OpenTelemetry as the agentic tooling). A trade-finance worked example: one trace per letter of credit,
spans for the KYC retrieval, the sanctions check and the credit-terms evaluation, and a final span
carrying the decision, its confidence score, and the full reasoning chain.

Two contributions beyond what the page already held:

- **The regulatory driver, named precisely.** EU AI Act **Article 12** requires automatic lifetime
  logging so operation can be traced; **Article 19** requires ≥ 6 months retention; breach sits in the
  middle penalty tier at up to €15M or 3% of global turnover. This is the specific citation behind the
  "regulatory drivers are real and external" claim in the caveat above, which previously rested on
  vendor paraphrase.
- **Instrumentation is not staged.** Whatever the [[autonomy-ladder]] stage, observability goes in at
  full strength on day one, because retrofitting is far harder. The authors also decouple the argument
  from regulation entirely: *"A system you can't explain is one you can't fully trust, defend, or fix."*

Note that this source is **not** an event-sourcing vendor, which strengthens the caveat's rebuttal —
though it is Thoughtworks-authored and cites Thoughtworks Radar placements in support of its own
tooling recommendations.

## Related

[[event-sourcing]] · [[agent-governance]] · [[agentic-event-driven-systems]] ·
[[event-sourced-agentic-patterns]] · [[model-context-protocol]] · [[context-engineering]] ·
[[axoniq]] · [[golo-roden]] · [[axoniq-government-ai-explainability-requirements]]

_Sources: [[axoniq-ai-agent-explainability-why-infrastructure-needs-to-remember]] · [[roden-event-sourcing-meets-mcp-whole-story-for-llms]] · [[akka-event-sourcing-backbone-agentic-ai]] · [[confluent-agentic-event-driven-systems-architecture]] · [[fritzsche-why-your-software-cannot-explain-business-decisions]] · [[fritzsche-choosing-storage-is-choosing-what-your-system-forgets]] · [[sadalage-chandrasekaran-making-data-ready-for-agentic-ai]] · [[axoniq-government-ai-explainability-requirements]]._
