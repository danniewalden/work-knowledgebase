---
title: Domain Discovery
type: concept
created: 2026-06-13
updated: 2026-09-04
sources: [dilger-automatic-domain-discovery-claude-code, eventmodeling-what-is-event-modeling, dilger-flea-market-model-to-deploy, fritzsche-what-ai-changes-is-which-work-stays-hard]
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

## Human-led discovery by drawing screens (Dilger, flea-market)

The agent-driven case has a low-tech twin: [[dilger-flea-market-model-to-deploy|Dilger's flea-market
vignette]] shows discovery run **conversationally with a non-technical stakeholder by drawing the screens**
— "just by drawing the screens as we usually do she could easily follow along," without her ever being
taught (or told the name of) the method. Ordinary questions ("what happens after someone registers?", "how
do you track who's paid?") surface the events, commands, and read models. It's the same *understand-first*
step as the agent walk-through, but the source of truth is the **stakeholder's mental model** elicited live
rather than a running UI inspected by an agent — the discovery front-end of [[vibe-modeling]].

## Why it matters here

It extends [[event-modeled-agent-design]] to the **front** of the workflow. Most agent-modeling
evidence in the KB is about using the model to *constrain a build* (e.g.
[[jwilger-agent-skills-event-modeling]], [[dilger-keep-command-handlers-pure]]); discovery is the
inverse — using an agent to *bootstrap the model* from an existing system. It also contrasts with
tools that generate models from a *textual description* ([[qlerify]]): here the source of truth is the
**live UI behavior**, which can catch the gap between intended and actual design.

**Why it becomes visible now (Fritzsche, 2026-09-04).** [[rico-fritzsche]]
([[fritzsche-what-ai-changes-is-which-work-stays-hard]]) supplies a mechanism rather than a slogan:
*"Nothing has changed in that regard. **What AI changes is which part of that work remains difficult**"* —
and the checkable version, *"thanks to AI agents, it's becoming increasingly clear that **developers often
created and solved problems that had absolutely nothing to do with the domain or the business
problem**."* The claim is that **accidental complexity becomes visible once its production cost falls
toward zero**, which is a different argument from "agents write the boring code": it predicts that the
share of work traceable to the domain *rises* without the domain work getting any easier. His fundamentals
list — *"system design, reliability, data, consistency, system structure and boundaries"* — with the
corollary that *"a framework isn't a foundation… if you focus on them, then you yourself become
interchangeable."*

**Markers: PRACTITIONER OPINION, unmeasured, in a LinkedIn post, and it is his own standing thesis
winning.** It converges with [[addyosmani-human-judgment-relocates]] ("human judgment doesn't leave the
software factory. It relocates") and [[laycock-citizens-build-agents-execute-experts-govern]] — **three
converging opinions, still not a measurement.** Nothing in the KB tests the accidental-complexity claim,
and it is the most instrumentable of the three.

## Caveats / open

Vendor self-report; no captured detail on how UI exploration maps to event-model elements
(events/commands/read models), no accuracy measure, and the "15 minutes" / autopilot claims are
unverified. Whether UI-walk discovery produces a *valid* event model or just an annotated click-map is
open.

_Sources: [[dilger-automatic-domain-discovery-claude-code]] · [[eventmodeling-what-is-event-modeling]] · [[dilger-flea-market-model-to-deploy]] · [[fritzsche-what-ai-changes-is-which-work-stays-hard]]._
