---
title: "Source: Miller — New stuff in Critter Stack AI Skills 1.10"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [miller-new-stuff-in-critter-stack-ai-skills-1-10]
raw_file: [raw/articles/miller-new-stuff-in-critter-stack-ai-skills-1-10.md]
tags: [agent-legibility, harness-engineering, critter-stack, vendor-self-report, release-note, short]
---

# Source: Miller — New stuff in Critter Stack AI Skills 1.10

Release-note post by **[[jeremy-miller]]**, 2026-09-02. Raw capture:
`raw/articles/miller-new-stuff-in-critter-stack-ai-skills-1-10.md`. **Deliberately short page: this is a
product release note, and it should be read as one.**

> **VENDOR SELF-REPORT.** A JasperFx release announcement by JasperFx's founder for a **priced** product
> (Solo $250 / Team $1,000 / Team Large $2,000, or bundled with CritterWatch Professional and Enterprise).
> The skill count, the pricing, and the claims that the skills yield *"more terse code and in many cases,
> more performant code"* and *"more testable code"* are the vendor's own, with no evaluation of any kind.

## Summary

Eleven new skills bring the catalogue to a claimed **102** across the [[critter-stack]] tools — up from
the **81** recorded on [[miller-jasperfx-ai-skills-agent-skills]] (2026-07-10), so roughly +26% in eight
weeks. New coverage: Wolverine Sagas (including from HTTP endpoints), two projection-troubleshooting
skills, Marten event versioning/upcasting, archiving and stream compaction, full-text/NGram search,
`Marten.PgVector` AI features, gRPC, MCP servers for your own app, and CritterWatch alerts. Also new: a
`projection-run` CLI "projection stepper" in `JasperFx.Events`, shipped in Marten and Polecat.

## Key points

The only durable content is Miller's restated **definition of what an AI Skill is for**, which is
consistent with his July framing and is the reason the KB tracks this product line at all:

> "AI Skills are structured documentation written for the coding agent rather than for you. **Not API
> reference — the agent can already read that** — but the accumulated *'here's what this actually means,
> here's the trap, here's what to check next'* that otherwise only exists in the heads of the people who
> built the thing."

Two of the new skills' *contents* are the kind of thing that definition predicts, and are worth recording
because they are checkable facts about the libraries rather than claims about the product:

- **Wolverine.HTTP**: the *first* return value of an endpoint method is the response body, so returning a
  `Saga` serializes saga state to the caller; the `Saga` must be a later tuple member, and `[EmptyResponse]`
  exists for no-body cases. Miller: *"That one fact reshapes the whole topic, and it's exactly the kind of
  thing that is obvious in retrospect and expensive in the moment."*
- **Marten archiving**: *"archiving alone doesn't shrink anything."* `ArchiveStream` sets a flag; it is
  `UseArchivedStreamPartitioning` that moves archived events to separate physical storage and buys the
  query performance — *"and it quietly weakens a stream-identity guarantee on the way."*

One process note, offered as the method: he tested the projection-stepper skill *"by pointing an agent at
a projection I'd deliberately broken and watching where it got stuck"* — i.e. skills are validated against
a seeded failure, the same technique as the CritterWatch chaos-monkey demo. And on how the catalogue grows:
*"If there's a corner of the Critter Stack you keep having to re-explain to your agent, tell us. That's
genuinely how most of these get picked."* A demand-driven [[harness-engineering]] backlog.

## Limits

- **A release note.** No evaluation, no before/after, no agent-success measurement — nothing establishes
  that any skill improves agent output. The "102 skills" is inventory, not efficacy.
- **The count is not comparable over time without care**: skills can be split or re-scoped, and no
  definition of a skill's granularity is given.
- The claims about terser/more performant/more testable generated code are **vendor assertions**.
- The linked companion piece ("AI Skills and the Critter Stack CLI") is **not in `raw/`**, per the capture
  note — a known gap if a later sweep wants the worked session.

## Connections / contrast

- Supersedes the **81 skills** figure on [[miller-jasperfx-ai-skills-agent-skills]], [[jeremy-miller]] and
  [[critter-stack]] with **102** as of 2026-09-02 — the only edit this capture really justifies.
- The Marten **event versioning and upcasting** skill and the **archiving/stream compaction** skill are
  the vendor-side counterparts to [[event-versioning-and-upcasting]] and
  [[dudycz-archiving-events-stream-lifetime-slicing]]: the same problems, now packaged as agent-facing
  guidance. The archiving fact (flag vs partitioning, and the identity-guarantee cost) is a substantive
  detail those pages do not currently carry.
- The `MCP servers for your own app` skill (twenty tools across `Marten.Mcp`, `Polecat.Mcp`,
  `WolverineFx.Mcp` — query event streams, fetch aggregate state, daemon status, scaffold a vertical
  slice) is the *application-facing* half of the operations-facing surface in
  [[miller-ai-assisted-production-support-with-critterwatch]]. See [[model-context-protocol]].
- The pattern itself — vendor-maintained, source-verified skills so the agent *"stops guessing from stale
  training data"* — remains the KB's main example of the **Skills primitive** shipped as a product; see
  [[agent-legibility]] and [[harness-engineering]].

## Related

[[jeremy-miller]] · [[critter-stack]] · [[agent-legibility]] · [[harness-engineering]] ·
[[miller-jasperfx-ai-skills-agent-skills]] · [[miller-ai-assisted-production-support-with-critterwatch]] ·
[[event-versioning-and-upcasting]] · [[model-context-protocol]] · [[agent-readable-model-artifacts]]
