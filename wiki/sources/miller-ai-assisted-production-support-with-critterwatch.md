---
title: "Source: Miller — AI Assisted Production Support with CritterWatch"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [miller-ai-assisted-production-support-with-critterwatch]
raw_file: [raw/articles/miller-ai-assisted-production-support-with-critterwatch.md]
tags: [model-context-protocol, agent-governance, agent-observability-and-evals, event-sourcing, critter-stack, vendor-self-report, focus]
---

# Source: Miller — AI Assisted Production Support with CritterWatch

Post by **[[jeremy-miller]]**, 2026-09-01, on *The Shade Tree Developer*. Raw capture:
`raw/articles/miller-ai-assisted-production-support-with-critterwatch.md`.

> **VENDOR SELF-REPORT.** This is a JasperFx product post by JasperFx's founder about JasperFx's own
> commercial product. Miller says so himself in the opening line — *"Like probably all software tool
> companies, JasperFx is working very hard to create a compelling story about the utilization of
> AI-assisted development with our tools"* — and closes by noting **every capability shown is paid-tier**.
> Every figure below is the vendor's own, from a session the vendor ran, on a fleet the vendor built, with
> failures the vendor injected. Carry this marker wherever these claims travel.

## Summary

The longest and most substantive Miller capture in this batch: a worked transcript of an agent doing
**production support** over an event-sourced .NET fleet through **[[model-context-protocol|MCP]]**.
CritterWatch's console host mounts an MCP server in two lines
(`AddCritterWatchMcp()` / `MapCritterWatchMcp()`) exposing **48 tools — 21 read, 27 action** — over
streamable HTTP, *"deliberately configured stateless so every tool invocation sees the actual caller's
identity for authorization."* Claude, pointed at it, works four scenarios: fleet health, dead-letter
triage end-to-end, tracing one message id through its causal neighbourhood, and diagnosing a poisoned
projection. The session is real and recorded; **the trouble in it was manufactured** with CritterWatch's
own chaos-monkey tools, which Miller states plainly up front.

## Key points

**1. The read↔action loop closes inside the agent.** Dead-letter triage runs
`summarize_dead_letters` → `query_dead_letters` → `replay_dead_letters` → `discard_dead_letters`, with
envelope ids flowing between tools and *"no console tab was harmed in the making of this triage."* Of 40 seeded dead letters, 25 drained on
replay and 15 bounced back, all `InvalidOperationException`; the agent classified those as deterministic
poison and **asked before the irreversible discard** (*"There is no undo on a discard — say the word."*).
The second scenario scales it: 2,100 dead letters, replayed in pages of 200 with the agent narrating the
drain.

**2. The most durable single item is a refusal, not a capability.** The read tools fan out across every
physical message database a service owns and return `databasesAnnounced` vs `databasesAnswered` plus a
`partial` flag, and the paired skill enforces: **"an empty result with `partial: true` means some stores
did not report — never answer 'the queue is empty.'"** Miller says this exists *"because of a real
production failure mode where a console rendered 'no dead letters found' over a queue quietly holding 42
of them."* A tool designed so the agent **cannot** confuse "no data" with "no answer" is
[[feedforward-and-feedback-controls]] built into the tool contract, and it is the transferable design
lesson of the post regardless of what you think of the product.

**3. Diagnosis by *shape*, taught rather than prompted.** The agent read "many exception types across many
message types" as transient infrastructure trouble and "one message type, one exception type" as a poison
message — and in the projection case distinguished *"your handler threw"* from *"your aggregate fold
threw"* purely from the exception's origin (`ApplyEventException` from the event store's apply pipeline),
which is what decides where to look. Miller is careful about provenance here: *"That 'the shape here
matters' reasoning isn't something I prompted for"* — but it **is** something the AI Skill teaches, and he
says so later: *"Every time the agent in this session checked `databasesAnswered` before declaring
victory, that was the skill talking."*

**4. Tools and skills as two halves of one artifact — stated as an internal rule.** *"A pile of tools
doesn't make an agent good at operations — an agent also needs to know the discipline… We hold ourselves
to a standing rule internally: any time CritterWatch exposes new information through an MCP tool, the
paired skill work ships with it. **A tool with no skill coverage is an under-leveraged tool.**"* The DLQ
skill teaches the *loop* (summarize → query → act, in that order) rather than listing the four tools. This
is the sharpest vendor statement in the KB that MCP surface area alone is not [[harness-engineering]] —
and it is the same tool↔skill pairing visible from the outside in
[[willison-codex-bundles-libreoffice]].

**5. Governance is in the tool layer, not the prompt.** Three gates, worth recording as a pattern for
[[agent-governance]]: a **license check** on every tool (unlicensed hosts get a `LicenseMissing` envelope
rather than data); **opt-in RBAC per named capability** (`dlq.replay`, `dlq.discard`,
`chaos-monkey.configure`) scoped to the target service as a resource, so *"the agent may replay dead
letters on TripService but touch nothing on the billing service"* is writable policy; and **separate
grants for reading vs acting on dead letters**, *"because dead letters contain message bodies, and 'may
look at business data' deserves a separate grant from 'may act on it.'"* The stateless transport exists so
those checks always see the current caller. Miller's own framing: *"Handing an AI agent a control surface
for production is the kind of thing that should make you a little nervous. It makes me a little nervous,
and we built it."*

**6. Event-sourcing-specific diagnostics.** The failure named the exact event (`#5784` on a given stream),
and the **projection stepper** replays a stream one event at a time showing projected state before/after
each apply — *"No more 'add a `Console.WriteLine` to the Apply method and rebuild.'"* Message provenance
came from OpenTelemetry spans Wolverine already emits (`messaging.message_id`, `conversation_id`, handler
type), reconstructed into the causal neighbourhood of one message: born inside a **Marten async daemon
page** processing events #2030–2034, sent as `ContinueTrip` over RabbitMQ, handled OK, with three sibling
messages from the same batch. `describe_lifecycle` returns a message type's structural path across every
monitored service — publisher → transport → handler → cascaded messages → appended events → projections —
as JSON **and a ready-to-paste Mermaid sequence diagram**. That is an [[agent-readable-model-artifacts]]
rung derived from a *running* system rather than from source.

**7. Deliberate over random chaos, for a stated reason.** Projection poison is keyed to an event *type*
(`set_chaos_monkey_projection_poison("TripStarted")`) rather than a failure *rate*, *"because with a rate,
the alert, the dead-letter drill-in, and the projection stepper each land on a different random event,
which is exactly what a diagnosis story can't use."* A good note on designing failure injection so a
causal chain stays traceable — and, read the other way, an admission that the demo needed a single
nameable cause.

**8. The honest epilogue.** The `AgentDown` alerts were wrong: they claimed a four-minute heartbeat gap
when the poison had been armed for two, and lingered over a daemon SQL showed advancing every second.
Cause: *"a Postgres deadlock storm, a docker daemon picking the worst possible moment to restart, and a
feedback loop that made a merely-slow pipeline read as a dead one"* — fixed for 1.1, full diagnosis
promised in a later post. Also unprompted: the agent noticed sampled `Trip` documents all had
`"Traveled": 0` and connected it to the scheduled-message backlog the alerting had flagged — a real finding
Miller says he had not made himself, and the one moment in the post where the agent produced something the
scenario did not plant.

## Limits

- **Vendor demo end to end.** Vendor's product, vendor's fleet (25 services, 29 nodes, ~1,049 endpoints,
  6,356 trip documents), vendor's injected failures, vendor's transcript *"lightly trimmed for length."*
  One session, one operator, one afternoon.
- **The failures were manufactured and, in the key case, deliberately single-caused.** Real incidents do
  not arrive with one nameable poisoned event type. Miller is upfront (*"a demo that waits around for
  production to genuinely catch fire makes for a long blog post"*) — which is honest and also exactly the
  limit.
- **Nothing is measured.** No time-to-diagnosis baseline, no comparison against a human on the console UI,
  no error rate for the agent's classifications, no count of wrong turns. The agent's diagnoses in the
  post are *correct* because the answer was planted.
- **Tool counts are the vendor's** (48 tools = 21 read + 27 action; "dozens" of skills). Unverified.
- **All of it is paid-tier and license-gated**, so the artifact is not independently inspectable.
- Read the demo's own epilogue as the standing caveat: the monitoring system was **wrong about a fleet it
  owned**, in the middle of the demo, and neither human nor agent guessed the mechanism. Agent-driven ops
  inherits every defect of the telemetry beneath it.

## Connections / contrast

- **The strongest concrete instance in the KB of [[model-context-protocol]] as an *operations* surface
  rather than a design-time one** — and it extends the MCP page's "MCP as the bridge to an event store"
  section from reads to **guarded writes**. The RBAC-per-capability + separate read/act grants pattern is
  new to the KB and belongs on [[agent-governance]].
- **It answers a question [[agent-observability-and-evals]] leaves open**: what an agent needs from
  observability is not dashboards but *tools that report their own completeness*. Compare
  [[tornhill-cannot-trust-agent-codescene-mcp]] — same instinct (give the agent an instrument, not a
  narrative), different domain.
- **It is the production-support end of [[event-sourced-agentic-patterns]]:** the event log is what makes
  "which event broke the fold, and what was the state before it" a mechanically answerable question. An
  agent over a non-event-sourced service could not be handed this diagnosis.
- **Against [[jeremy-miller]]'s standing position** ("the codebase is the prompt"): this is the runtime
  counterpart — *the running fleet is the prompt* — and it completes the [[critter-stack]] AI strategy
  announced in [[miller-jasperfx-critterstack-ai-event-modeling-strategy]] (which promised CritterWatch as
  MCP+CLI surface) with a worked demonstration.
- **Contrast with [[miller-pondering-continuous-integration-ai-world-order]]**, published the day before:
  there he reports his *own* CI substrate buckling under agent-driven load. The two together are a candid
  pairing — the tooling he sells for operating agent-era systems, and the tooling he uses buckling in the
  agent era.
- The Bobcat/Microsoft-Testing-Platform "supervisor" mentioned in the strategy post reappears here in
  spirit: supervise, retry selectively, reset the environment. Compare the AVO supervisor in
  [[fowler-fragments-2026-09-01]] — same idea one layer up.

## Related

[[model-context-protocol]] · [[agent-governance]] · [[agent-observability-and-evals]] ·
[[jeremy-miller]] · [[critter-stack]] · [[event-sourcing]] · [[event-sourced-agentic-patterns]] ·
[[harness-engineering]] · [[agent-readable-model-artifacts]] · [[feedforward-and-feedback-controls]] ·
[[agent-explainability]] · [[decision-trace]] · [[miller-jasperfx-ai-skills-agent-skills]] ·
[[miller-new-stuff-in-critter-stack-ai-skills-1-10]]
