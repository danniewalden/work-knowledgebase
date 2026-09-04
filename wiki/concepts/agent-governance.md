---
title: Agent Governance
type: concept
created: 2026-06-11
updated: 2026-09-02
sources: [deloitte-ai-agents-scaling-faster-than-guardrails, svitla-agentic-ai-market-trends-2026, langchain-state-of-agent-engineering-2026, devadoss-cead-capability-aligned-agent-design, dora-roi-ai-assisted-software-development-2026, laycock-citizens-build-agents-execute-experts-govern]
tags: [agentic-ai, governance, risk, enterprise]
---

# Agent Governance

The organizational practice of keeping autonomous agents safe, accountable, and within
bounds — and, per the KB's sources, the **single biggest blocker between pilots and
production**.

## The gap

[[deloitte]]'s 2026 survey: **only 21% of organizations have a mature agentic-AI governance
model**; ~80% lack one even as adoption scales
([[deloitte-ai-agents-scaling-faster-than-guardrails]]). [[gartner]] expects **>40% of
agentic projects canceled by 2027**, partly over weak governance. Ungoverned agents can make
unseen mistakes, work at cross purposes, leak sensitive data, offend customers, or invite
cyberattacks — and these risks *compound* at scale.

## What "mature" looks like

- **Clear decision boundaries** — which decisions an agent makes autonomously vs which need
  human approval.
- **Real-time monitoring** that flags anomalies (overlaps with [[agent-observability-and-evals]]).
- **Audit trails** capturing the full chain of agent actions — conceptually the same
  immutable-log idea as [[event-sourcing]].
- **Cross-functional structure** — IT, legal, compliance, and business leaders setting
  policy, monitoring, and handling escalations.

## Approaches

Start with lower-risk use cases and scale deliberately; treat governance as a **design
constraint from day one**, not a retrofit. The emerging technical enforcement layer is
**[[guardian-agents]]**. Regulatory context (EU AI Act, US state laws) is evolving slower
than deployment.

## Governance supports design, it cannot replace it (CEAD, 2026-05)

[[john-devadoss|deVadoss's]] **CEAD** ([[devadoss-cead-capability-aligned-agent-design]]) sharpens what
governance is *for*. Its central claim inverts the usual framing: **governance is necessary but cannot
be the primary organizing abstraction** — the primary abstraction is *agent design* (capability
boundaries, autonomy allocation, tool/data authority, state/memory, verification). Governance is a
**supporting control and assurance plane** that *enforces the design, detects drift, and provides
accountability.* The evidence: a **governance-first but design-poor** 24-agent grid — strong policy,
audit, least-privilege, escalation — scored only 50.8% safe success versus **CEAD's 70.6%**; controls
lowered violations and raised audit coverage but could not compensate for weak capability decomposition.

The governance-relevant mechanisms CEAD adds:
- **The Agent Capability Contract (ACC)** as the governable unit — one contract per production agent
  declaring owner, purpose/non-purpose, **autonomy level (L0–L4)**, tool scopes, data classification,
  memory retention/deletion, verification gates, human-approval triggers, evaluation evidence, audit
  schema, and a **retirement path**. This *is* the "clear decision boundaries" and "audit trail" this
  page calls for, made into a first-class design artifact rather than a policy bolt-on.
- **Capability boundaries as the governance surface** — least privilege "follows design" (tool access
  scoped per task, data class, action, autonomy level); **agent proliferation** is itself a governance
  risk (duplicate/overlapping authority, ungoverned memory stores) to be reviewed and consolidated
  quarterly.
- **Safe success, not completion** — measure functional success ∧ ¬policy-violation ∧ ¬memory-poisoning;
  adopt **evaluation-as-release-gate**; plan **incident response** (kill switches, rollback, memory
  quarantine, forensic traces). Overlaps with [[agent-observability-and-evals]] and the events/audit-log
  substrate of [[event-sourcing]].

On the organization side, [[matthew-skelton]] adds that the *boundaries, practices, and governance* to
enable rapid value flow are exactly what unlock AI ROI ([[skelton-team-topologies-foundation-ai-roi]]) —
governance as value-flow stewardship, not just control.

## Governance is where the cost now lives (DORA ROI report, 2026)

The [[dora-roi-ai-assisted-software-development-2026|2026 DORA ROI report]] gives this page a financial
argument: because AI inference cost fell **~280×** (Nov 2022 → Oct 2024, Stanford AI Index), "the true
financial burden of adoption has shifted to governance" — managing the **verification tax** (reviewing
AI output), adjusting downstream workflows, and upskilling staff. It also quantifies an **instability
tax**: AI raises delivery instability (a sample change-fail rate rising 5% → 6% ≈ $344k downtime), so
the recommended controls are the automated-verification kind (CI, automated testing, small batches) —
governance as [[guardian-agents|automated guardrails]] rather than manual review gates. This makes
governance the cost centre of the AI transition, not an afterthought.

## "Experts govern" — the same inversion, from the people side (Laycock, 2026-08)

[[rachel-laycock]], CTO of [[thoughtworks]], reaches CEAD's conclusion by a different route
([[laycock-citizens-build-agents-execute-experts-govern]]). Her framing — *"Citizens build. Agents
execute. Experts govern."* — is explicitly **not about roles** but about where value moves: everyone can
now express ideas as software, agents increasingly execute, and neither reduces the need for expertise.

The claim this page should take from it is the **scarcity inversion**. Organisations optimised for
decades around the scarcity of people who could write code; what is scarce now is *"good engineering
judgement: knowing what good looks like, understanding the risks and knowing when something that works
is actually safe to trust in production."* The governance questions she lists are precisely the ones
absent from a demo — data protection, dependency failure, comprehensibility in two years, auditability,
scale — and they *"don't show up… unless an experienced engineer is in the room."*

Where this converges with CEAD is the **role of the expert**: not the review gate but the environment.
Experienced engineers become *"dramatically more leveraged,"* shifting from building features to
*"creating the environment in which thousands of features can be built safely by other people and by
agents"* — guardrails, platforms, practices, feedback loops. That is CEAD's "governance enforces the
design" restated as a job description, and it lines up with the DORA finding above that the automated-
verification controls are the ones that pay. Her summary: *"Organisations don't run on code. They run on
trust."* She names one antipattern and defers it: citizens building and throwing it to engineers to fix.

**Two markers.** This is **not independent** — Thoughtworks' CTO on martinfowler.com, evidenced by a
Thoughtworks event and conversations with Thoughtworks engineers — so it does not corroborate the other
Thoughtworks material this KB leans on (see [[thoughtworks]] on the concentration problem). And it is
**framing, not measurement**: a self-described ramble with no data and one anonymised team. The
convergence with CEAD is the interesting part precisely because CEAD *is* outside.

_Source pages: [[deloitte-ai-agents-scaling-faster-than-guardrails]] · [[svitla-agentic-ai-market-trends-2026]] · [[langchain-state-of-agent-engineering-2026]] · [[devadoss-cead-capability-aligned-agent-design]] · [[dora-roi-ai-assisted-software-development-2026]] · [[laycock-citizens-build-agents-execute-experts-govern]]._
