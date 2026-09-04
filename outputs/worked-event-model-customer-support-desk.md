---
title: "Worked Event Model — An Autonomous Customer-Support Desk (multi-agent system)"
type: deliverable
created: 2026-06-15
sources: [dymitruk-event-modeling-future-proof-agents, event-modeled-agent-design, anthropic-building-effective-agents, langchain-state-of-agent-engineering-2026, confluent-agentic-event-driven-systems-architecture, solace-multi-agent-systems-real-time-context-eda, model-context-protocol, rico-fritzsche-autonomous-domain-capabilities-ccc]
tags: [event-modeling, agentic-ai, multi-agent, customer-support, agent-governance, worked-example, focus]
---

# Worked Event Model — An Autonomous Customer-Support Desk

A **second** worked Event Model of a multi-agent system, in a different domain from the coding factory
(`outputs/worked-event-model-autonomous-coding-factory.md`), to show Event Modeling *the method*
generalizes. The domain is the KB's most-cited production use case,
[[customer-support-agents]] ([[langchain-state-of-agent-engineering-2026]],
[[svitla-agentic-ai-market-trends-2026]]). It applies the same agent-as-user / agent-as-processor
mapping ([[dymitruk-event-modeling-future-proof-agents]], [[event-modeled-agent-design]]) and the
"agents subscribe→reason→publish, never call each other directly" discipline from
[[confluent-agentic-event-driven-systems-architecture]] / [[solace-multi-agent-systems-real-time-context-eda]].

> **Status / honesty:** an in-house illustration, internally consistent with the sources but not built
> or validated. Like the coding-factory model, it closes "no worked example" — not "no independent one."

---

## 1. System and scope

**Goal:** resolve an inbound customer **ticket** autonomously — triage, retrieve context, draft a
reply, take any side-effecting action (refund, plan change) under policy, send, and learn from the
outcome — escalating to a human only when policy or confidence demands.

**Consistency boundary (DCB-style, [[dynamic-consistency-boundaries]]):** the **ticket** is the decision
scope. A reply or action may be appended *iff* the ticket's relevant event stream still satisfies the
guard (e.g. not already escalated/closed). The ticket is the capability-owned unit
([[rico-fritzsche-autonomous-domain-capabilities-ccc]] / [[business-capabilities]]).

---

## 2. Swimlanes (actors on top, capability processors below)

```
 TOP (actors)
 ─ Customer (human, USER)                  — raises the ticket, replies, rates
 ─ Support Agent (human)                    — handles escalations

 BOTTOM (automations / capabilities)
 ─ Triage Agent        (PROCESSOR)          — classify + route + set priority
 ─ Knowledge Agent     (PROCESSOR)          — retrieve context (RAG / account lookup via MCP)
 ─ Resolution Agent    (PROCESSOR)          — draft the reply / propose an action
 ─ Policy/Guardian Agent (PROCESSOR)        — approve, redact, or escalate before anything is sent
 ─ Action/Fulfilment   (PROCESSOR, det.)    — execute approved side-effects (refund, plan change) via MCP tools
 ─ Comms Automation    (PROCESSOR, det.)    — send the message, record delivery
```

Deterministic processors (Action, Comms) are guardrails; the LLM-driven ones (Triage, Knowledge,
Resolution, Guardian) carry the nondeterminism — the same split as the coding factory.

---

## 3. The event-modeled timeline

`[Command]` → `(Event)` → `{Read Model}`.

### Slice A — Raise the ticket  *(state-change; agent-as-user)*
```
Customer ─ [Open Ticket] ─▶ (Ticket Opened) ─▶ {Open Tickets View}
```

### Slice B — Triage  *(automation; translation)*
```
{Open Tickets View} ─▶ Triage Agent ─ [Classify Ticket] ─▶ (Ticket Classified) ─▶ {Routing View}
```
Sets intent, topic, priority; routes to a capability. Business exceptions (e.g. "abusive content")
are their own events, per Fraktalio-style GWT-with-exceptions.

### Slice C — Gather context  *(automation; translation via MCP)*
```
{Routing View} ─▶ Knowledge Agent ─ [Retrieve Context] ─▶ (Context Assembled) ─▶ {Ticket Context View}
```
The **Translation pattern**: MCP tools ([[model-context-protocol]]) turn external systems (orders,
account, KB articles) into local `Context Assembled` facts — real-time context, the
[[solace-multi-agent-systems-real-time-context-eda]] requirement.

### Slice D — Draft reply / propose action  *(automation)*
```
{Ticket Context View} ─▶ Resolution Agent ─ [Draft Reply] ─▶ (Reply Drafted)
                                            [Propose Action] ─▶ (Action Proposed)   (e.g. $20 refund)
                                                                      │
                                                                      ▼
                                                              {Pending Resolution View}
```

### Slice E — Govern before send  *(automation; guardian-as-subscriber, the veto)*
```
{Pending Resolution View} ─▶ Policy/Guardian Agent ─ [Review Resolution] ─▶ (Resolution Approved)
                                                                          ├▶ (Resolution Redacted)
                                                                          └▶ (Escalation Raised) ─▶ {Human Queue View}
```
The Guardian checks tone, PII redaction, refund limits, compliance. **High-risk → escalate** to the
Support Agent (the autonomy dial, [[autonomy-ladder]]): in Conservative mode every action over a
threshold escalates; in Full mode only policy violations do. Governance = the veto event + audit log
([[agent-governance]]).

### Slice F — Act + send  *(state-change; deterministic)*
```
(Resolution Approved) ─▶ Action/Fulfilment ─ [Execute Action] ─▶ (Action Executed)   (refund issued via MCP)
(Resolution Approved) ─▶ Comms Automation  ─ [Send Reply]     ─▶ (Reply Sent) ─▶ {Ticket Timeline View}
```
**DCB guard:** `Reply Sent` / `Action Executed` may append *iff* a `Resolution Approved` exists for this
ticket and no later `Escalation Raised`.

### Slice G — Close the loop  *(state-change; agent-as-user again)*
```
Customer ─ [Rate Resolution] ─▶ (Resolution Rated) ─▶ {CSAT / Quality View}  → feeds Triage & Resolution priors
```
`Resolution Rated` is the outcome signal — the feedback that improves future runs (the
check→decide→act→record→improve flywheel), and the input to [[agent-observability-and-evals]].

---

## 4. The four EM patterns here

| Pattern | Where |
| --- | --- |
| **State change** | Open Ticket→Ticket Opened; Send Reply→Reply Sent; Rate→Resolution Rated |
| **State view** | {Open Tickets}, {Routing}, {Ticket Context}, {Pending Resolution}, {Human Queue}, {CSAT} |
| **Translation** | Knowledge Agent + Action/Fulfilment turning MCP tool I/O into Context Assembled / Action Executed |
| **Automation** | Triage, Knowledge, Resolution, Guardian — every capability processor working a view |

Same vocabulary as a human user; agents differ only by swimlane and determinism — Dymitruk's claim, a
second time over.

---

## 5. Given-When-Then (samples)

> **Guarded send**
> **Given** a ticket has `Resolution Approved` and no `Escalation Raised`
> **When** Comms issues `Send Reply`
> **Then** a `Reply Sent` event is appended; **no** `Reply Sent` may exist without a prior `Resolution Approved`

> **Refund limit escalation**
> **Given** an `Action Proposed` of a refund above the autonomy threshold
> **When** the Guardian issues `Review Resolution`
> **Then** an `Escalation Raised` event is appended and the ticket moves to `{Human Queue View}` — the
> Action/Fulfilment processor must not `Execute Action`

---

## 6. Harness / governance mapping

| EM construct | Analog |
| --- | --- |
| Ticket event stream | append-only audit trail — the log *is* the compliance record ([[agent-governance]]) |
| {Ticket Context View} | retrieved, in-context state ([[context-engineering]]); MCP-sourced |
| Guardian veto + escalation | [[guardian-agents]] + human-in-the-loop dial ([[autonomy-ladder]]) |
| Swimlane = capability | agent ownership boundary (RPU, [[rico-fritzsche-autonomous-domain-capabilities-ccc]]) |
| Resolution Rated → priors | online evals / quality feedback ([[agent-observability-and-evals]]) |

---

## 7. What it shows — and doesn't

**Shows:** the method scales to a second, very different multi-agent domain with no new notation;
guardian/escalation governance and the autonomy dial fall out naturally; MCP tool calls are just the
Translation pattern; and the per-ticket DCB guard enforces "nothing is sent/executed without approval."
Two worked models (coding + support) now triangulate [[event-modeled-agent-design]] from both of the
KB's flagship agent use cases ([[agentic-coding]] + [[customer-support-agents]]).

**Doesn't:** validate against a live system, and remains in-house. Independent, published worked event
models of multi-agent systems are still the wanted capture; [[esaa-event-sourcing-for-autonomous-agents]]
stays the nearest external analog (event *sourcing*, not the method).

---

*Sources: [[dymitruk-event-modeling-future-proof-agents]] · [[event-modeled-agent-design]] ·
[[anthropic-building-effective-agents]] · [[langchain-state-of-agent-engineering-2026]] ·
[[confluent-agentic-event-driven-systems-architecture]] · [[solace-multi-agent-systems-real-time-context-eda]] ·
[[model-context-protocol]] · [[rico-fritzsche-autonomous-domain-capabilities-ccc]].
Companions: `outputs/worked-event-model-autonomous-coding-factory.md`, `outputs/denoting-an-agent-in-an-event-model.md`.*
