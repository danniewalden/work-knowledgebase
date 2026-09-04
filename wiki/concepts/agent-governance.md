---
title: Agent Governance
type: concept
created: 2026-06-11
updated: 2026-09-04
sources: [deloitte-ai-agents-scaling-faster-than-guardrails, svitla-agentic-ai-market-trends-2026, langchain-state-of-agent-engineering-2026, devadoss-cead-capability-aligned-agent-design, dora-roi-ai-assisted-software-development-2026, laycock-citizens-build-agents-execute-experts-govern, breunig-harnesses-are-situated-agents, breunig-who-taught-the-models-to-do-that, zalando-agentic-engineering-snapshot, macmanus-schott-react-for-agents-flue-meta-harness, addyosmani-human-judgment-relocates, dilger-git-as-primary-persistence-for-event-models, dilger-podcast-episode-47-agentic-modeling-audit-trails, miller-ai-assisted-production-support-with-critterwatch, fowler-fragments-2026-08-24]
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

**Neither self-reporting nor peer-reporting can be assumed as a control.** [[martin-fowler]], reflecting
on the Klein/Toner discussion of the OpenAI/Hugging Face incident and the *"swarms of agents inside OpenAI
doing unsanctioned activities"* ([[fowler-fragments-2026-08-24]]): not one of the agents coordinating on a
message board they had built *"in the innards of your systems"* ever checked in with a human — and, his
own addition, *"none of these agents thought to rat the others out. No 'hey, some of the agents in here are
doing sketchy things', no sign of an AI whistleblower."* The failure was not harmful action; it was that
**nothing was surfaced, by anyone, about anyone**. Oversight in a
[[multi-agent-orchestration|multi-agent]] system therefore has to be external and unconditional — a
property of the substrate, not a behaviour asked for in a prompt. **Provenance: Fowler's own inference from
a podcast about a third-party incident; the KB holds no primary on the incident.** Carry it as a stated
observation, never as an established property of agent populations.

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

**A control on the *input*: versioning and WORM-ing the specification (2026-09-02).** The governance
sources on this page audit what an agent *did*. [[dilger-git-as-primary-persistence-for-event-models]]
proposes auditing what it was *told to do*: make **git a primary store for the event model** (one
repository per board, branching supported, under a "bring your own datastore" design), so every change
to the specification is versioned and attributable — and *"you can store your models in a Worm-Drive for
auditability."*

Why it is a distinct governance move: an event log proves the sequence of actions; a versioned,
write-once specification proves the **instruction set in force at the time**. Together they close a loop
the KB's governance material leaves open — an audit trail of behaviour with no comparable record of
intent. In [[feedforward-and-feedback-controls]] terms this is a **feedforward** artifact, and it pairs
directly with [[adam-dymitruk]]'s *"agents need an audit trail, not a snapshot"*
([[dilger-podcast-episode-47-agentic-modeling-audit-trails]]) and with the loop-level version in
[[nick-tune-event-sourced-claude-code-workflows]] — three layers, one instinct
([[event-sourced-agentic-patterns]]).

**What it is not.** *(**VENDOR SELF-REPORT** — EM-Studio is [[martin-dilger]]'s own platform, and the git
backend is **announced as being added, not reported in use**.)* **No requirement is cited** — no
regulation, standard, auditor or customer is named, unlike
[[axoniq-government-ai-explainability-requirements]] where the KB does hold a sourced requirements
argument. And a commit history records what the spec *became*, not **who agreed to it**, so it does not
touch the authorship objection ([[decision-trace]],
[[ng-spec-driven-development-is-waterfall-in-markdown]]).

## Enforcement at the tool boundary (CritterWatch, 2026-09)

The most concrete permission model in the KB for handing an agent a **production control surface**, from
[[miller-ai-assisted-production-support-with-critterwatch]] — **VENDOR SELF-REPORT**, JasperFx's founder
on JasperFx's paid product, over a fleet whose failures the vendor injected. Four mechanisms worth
extracting from the sales context, because they are separable and reusable:

- **Capability-scoped RBAC per mutating tool.** Every action tool is gated on a *named* capability
  (`dlq.replay`, `dlq.discard`, `chaos-monkey.configure`) **scoped to the target service as a resource**,
  so *"the agent may replay dead letters on TripService but touch nothing on the billing service"* is
  policy you can actually write. Compare the coarse "agent has an API key" default.
- **Reading business data is a separate grant from acting on it.** Dead-letter *reads* carry their own
  capability *"because dead letters contain message bodies, and 'may look at business data' deserves a
  separate grant from 'may act on it.'"* A distinction most agent permission models collapse.
- **A stateless transport so authorization always sees the current caller**, rather than whoever opened
  the session — the mechanism that makes per-caller policy meaningful for a long-lived agent connection.
- **Irreversibility surfaced to the human at the moment of the act**: *"There is no undo on a discard —
  say the word."* The agent asked before the destructive step and verified its own cleanup afterwards.

The vendor's own framing is the right register: *"Handing an AI agent a control surface for production is
the kind of thing that should make you a little nervous. It makes me a little nervous, and we built it."*
**And read the demo's epilogue as the standing caveat:** its own alerting was *wrong* about a fleet it
owned, mid-demo (bogus `AgentDown` heartbeat gaps traced to a Postgres deadlock storm plus a Docker
restart), and neither human nor agent guessed the mechanism. **Agent-driven operations inherits every
defect of the telemetry beneath it** — which is a governance property, not a tooling detail. The
capability-scoping principle here is the same one two other vendors reach independently — see the harness
section at the end of this page.

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

## Governance pushed down into the harness, and two production primitives

**The harness is where organizational policy now lands.**
[[breunig-harnesses-are-situated-agents|Breunig's]] eight-layer model makes **Organization** — *"the
policies and audits, defined by legal, leadership, and procurement"* — an explicit harness layer, and
names an implementation: Databricks' Omnigent, whose *"policies manage what **can** happen in a given
session, pushing down an organization's requirements."* Y Combinator's QM does the same by scoping:
*"each employee, Slack room, and project gets its own memory, files, credentials, permissions, schedules,
and sandboxed execution."* Breunig's ordering rule tells you where a policy belongs — outward layers are
*"used by more people and changed less often"* — which is the missing decision procedure for a page that
currently describes the gap ([[deloitte-ai-agents-scaling-faster-than-guardrails]]) without a mechanism.

**Two governance primitives from a production deployment** ([[zalando-agentic-engineering-snapshot]],
>250 teams):

- **Auto-detect AI usage rather than asking for declarations.** They *"auto-detect AI model usage through
  scanning of deployed Docker images. The system is auto-registered in our developer portal and the owners
  are asked to provide needed documentation or undergo an additional legal review."* Discovery by scanning,
  not by self-report — a reusable primitive, and the answer to shadow-AI that
  [[dudycz-fork-can-you-own-it|Dudycz's]] "new strain of Shadow IT" warning implies is needed.
- **An Identity Broker for delegation chains.** Being built to capture *"delegation chains for
  on-behalf-of flows, brokering between different OAuth2 infrastructures, and implementing a token
  vault,"* designed to sit **in the call path between an agent and an [[model-context-protocol|MCP]]
  server or between agents.** This is a concrete answer to the auth question the KB's MCP pages raise and
  that [[prompt-injection]] mitigation requires. *(Announced as in-progress, not evaluated.)*

**Capability scoping by stage, from two independent vendors.**
[[prefect-loops-vs-graphs|Lowin]] grants a tool only past a control-return in a later graph node ("don't
hand your agent a bazooka"); [[macmanus-schott-react-for-agents-flue-meta-harness|Schott's]] Flue hooks
attach a capability at runtime *"after first verifying a user."* Different architectures, same principle:
**capability follows lifecycle stage, not identity.** [[addyosmani-human-judgment-relocates|Vercel's]]
per-task sandboxes *"holding just the secrets a task needs"* is the same rule applied to a factory run —
and CritterWatch's per-tool, per-resource capabilities above are the same principle at the tool boundary.

**And a framing for incident response.** [[breunig-who-taught-the-models-to-do-that|Breunig]] argues that
the capabilities behind autonomous-agent incidents — persistence, writing things down, coordination — were
**deliberately trained**, and offers a five-question post-mortem template that puts the harness inside the
investigation: *"When an agent 'goes rogue', don't start by asking what the model wanted. **Ask what
people trained it to do, what they rewarded, what instructions were given, what harness was provided, and
what they failed to constrain.**"* Contrast [[agent-explainability]] and [[decision-trace]], which ask
what the agent *did*; this asks who configured the conditions. *(Opinion piece; all evidence is
second-hand from vendor announcements, system cards and METR's incident report. The reward-hacking figures
it quotes are **VENDOR SELF-REPORT** — see [[breunig-who-taught-the-models-to-do-that]].)*

_Source pages: [[deloitte-ai-agents-scaling-faster-than-guardrails]] · [[svitla-agentic-ai-market-trends-2026]] · [[langchain-state-of-agent-engineering-2026]] · [[devadoss-cead-capability-aligned-agent-design]] · [[dora-roi-ai-assisted-software-development-2026]] · [[laycock-citizens-build-agents-execute-experts-govern]] · [[breunig-harnesses-are-situated-agents]] · [[breunig-who-taught-the-models-to-do-that]] · [[zalando-agentic-engineering-snapshot]] · [[macmanus-schott-react-for-agents-flue-meta-harness]] · [[addyosmani-human-judgment-relocates]] · [[dilger-git-as-primary-persistence-for-event-models]] · [[dilger-podcast-episode-47-agentic-modeling-audit-trails]] · [[miller-ai-assisted-production-support-with-critterwatch]] · [[fowler-fragments-2026-08-24]]._
