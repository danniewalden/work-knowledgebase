---
title: Domain Discovery
type: concept
created: 2026-06-13
updated: 2026-06-13
sources: [dilger-automatic-domain-discovery-claude-code, eventmodeling-what-is-event-modeling]
tags: [event-modeling, event-storming, domain-discovery, agentic-coding, focus]
---

# Domain Discovery

The **understand phase** of modeling a system: surfacing what the domain actually does — its flows,
actors, events, and edge cases — *before* designing or changing it. In [[event-modeling]] and
[[event-storming]] this is the opening, human-intensive step (the "brainstorm events" / swimlane
mapping that starts the workshop). The KB's interest is the emerging twist: **an AI agent performing
discovery automatically.**

## Agent-driven discovery (Dilger)

[[martin-dilger]]'s "Automatic Domain Discovery using Claude Code"
([[dilger-automatic-domain-discovery-claude-code]]) points an agent at a **running product's UI** —
not its code or docs — and has it click through flows "the way a real user would," producing a
**visual storyboard / timeline of how the product actually works, not how you think it works.** It
surfaces confusing navigation, contradictory screens, and broken flows — "a mirror, and mirrors
aren't always flattering." The pitch: it replaces hours of manual workshop prep (screenshots, flow
documentation) so teams start from "a real, honest starting point," and it was built as a ~15-minute
Claude Code **skill** wired into [[eventmodelers-ai]].

## Why it matters here

It extends [[event-modeled-agent-design]] to the **front** of the workflow. Most agent-modeling
evidence in the KB is about using the model to *constrain a build* (e.g.
[[jwilger-agent-skills-event-modeling]], [[dilger-keep-command-handlers-pure]]); discovery is the
inverse — using an agent to *bootstrap the model* from an existing system. It also contrasts with
tools that generate models from a *textual description* ([[qlerify]]): here the source of truth is the
**live UI behavior**, which can catch the gap between intended and actual design.

## Caveats / open

Vendor self-report; no captured detail on how UI exploration maps to event-model elements
(events/commands/read models), no accuracy measure, and the "15 minutes" / autopilot claims are
unverified. Whether UI-walk discovery produces a *valid* event model or just an annotated click-map is
open.

_Sources: [[dilger-automatic-domain-discovery-claude-code]] · [[eventmodeling-what-is-event-modeling]]._
