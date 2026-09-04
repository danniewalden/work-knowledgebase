---
title: Agent-Readable Model Artifacts
type: concept
created: 2026-08-14
updated: 2026-08-31
sources: [miller-jasperfx-critterstack-ai-event-modeling-strategy, dilger-eventmodelers-supports-esdm-export, dilger-highlighting-markers-give-context-to-agents, dilger-agentic-collaboration-freeform-drawings, dilger-planning-like-excel-legible-to-human-and-ai, dilger-event-modeling-knowledge-hub-emlang, dilger-drawio-model-in-code, esdm-event-sourced-domain-modeling, fraktalio-event-modeler-connect-ai-agents-mcp, proophboard-skills-ai-agent-event-modeling, dilger-adding-perspectives-to-event-modeling]
tags: [event-modeling, agentic-ai, interoperability, focus]
---

# Agent-Readable Model Artifacts

**What form does a design model have to take before an agent can actually use it?** The KB's focus area
([[event-modeled-agent-design]]) long asserted that the event model is the agent's spec. This page
tracks the separate, more mundane question of **surface and format** — the artifacts, coordinates and
channels through which a model is handed to a machine. It exists because by August 2026 the sources had
accumulated into a recognisable pattern rather than one-off features.

## The ladder of surfaces

Roughly in order of increasing machine-tractability, with the KB's evidence for each:

| Surface | What the agent gets | Source |
| --- | --- | --- |
| **Freeform whiteboard** | Nothing reliable — models "degrade without an owner" and can't be addressed | [[dilger-planning-like-excel-legible-to-human-and-ai]] |
| **Raw tool XML in git** (draw.io) | Bytes, but "no framework to follow, no rules" | [[dilger-drawio-model-in-code]] |
| **Grid coordinates** | A *handle* per element — "add a field in B3, adjust all dependents"; the agent can report back against the same reference | [[dilger-planning-like-excel-legible-to-human-and-ai]] |
| **Board via MCP tools** | Live read/write of model elements as tool calls | [[fraktalio-event-modeler-connect-ai-agents-mcp]], [[proophboard-skills-ai-agent-event-modeling]] |
| **A validated file format** | Version-controlled YAML + an offline linter; drift fails a PR check | [[esdm-event-sourced-domain-modeling]] |
| **Format-agnostic export on demand** | Any slice or chapter, in the format the agent asks for, over UI/API/MCP/CLI | [[dilger-eventmodelers-supports-esdm-export]] |
| **Freeform marks, both directions** | Spatial/graph context (inside a lasso, arrow direction) the agent reads — *and draws back* | [[dilger-agentic-collaboration-freeform-drawings]] |
| **Attention markers on screens** | What is salient *right now*, region-scoped; agents read, validate, and build UI from them | [[dilger-highlighting-markers-give-context-to-agents]] |
| **Derived export from code** *(off-ladder — see below)* | Slice definitions exported by CLI from a fluent API in the code, visualized on top; the model is a *projection*, not the source | [[miller-jasperfx-critterstack-ai-event-modeling-strategy]] |

## Three things the pattern shows

**1. Addressability is the hinge.** The recurring failure of freeform surfaces is not that agents can't
parse pictures; it is that there is **no stable handle** to instruct against or report against. The grid
supplies coordinates, the file format supplies document paths and schema names, MCP supplies tool
targets. Every rung that works, works by giving human and agent a *shared referent* — the modeling-layer
form of the argument [[ai-readable-code]] makes about code and [[agent-legibility]] about the workspace.

**2. Format neutrality arrived late and matters more than it looks.** The KB tracked two camps: file-first
([[esdm-event-sourced-domain-modeling|ESDM]] — any LLM reads the YAML, offline, linted) versus board+MCP
([[fraktalio]], [[prooph-board]], [[eventmodelers-ai]] — the agent authors on a hosted surface). The 2026-08-13
ESDM export collapses the distinction: the board becomes an authoring surface that can **emit a
third-party open format per slice on request** ([[dilger-eventmodelers-supports-esdm-export]]). The
significant part is not the feature but the *interop*: two tool-makers agreeing on a format is
[[em-standardization-foundation|standardization]] happening in practice rather than by committee. The
open gap is that ESDM encodes ES/DDD/CQRS structure, not the timeline/swimlane method — hence the
announced (unshipped) Dilger–Roden timeline extension.

**3. The agent-facing value keeps being discovered, not designed.** Markers, freeform drawings and the
Excel grid were all built as *human* affordances; in each write-up the agent use is reported as a
surprise ("again something I didn't think of"). Weak evidence on its own, but consistent, and it is the
modeling-layer echo of the [[ai-readable-code]] finding that what helps humans reconstruct intent tends
to help machines too. The corollary is the KB's own caution: nobody has yet *designed* a model surface
for agents from scratch and measured it.

## Read/write, not just read

Worth separating two verbs the sources conflate. Most rungs give the agent **read** access — the model
as input context. Three give it **write** access back onto the model: MCP element authoring
([[fraktalio-event-modeler-connect-ai-agents-mcp]]), drawing back onto the board
([[dilger-agentic-collaboration-freeform-drawings]]), and the `/wdyt` review returning annotations
in place. That write direction is what turns a spec into a **conversation surface**, and is the
mechanism behind the "agent critiques the model" direction of fit in [[event-modeled-agent-design]].
Projection into audience-specific views ([[dilger-adding-perspectives-to-event-modeling]]) is the same
idea aimed at humans: one model, many rendered surfaces.

## What's missing

- **No independent evaluation of any of it.** Every rung above the file-format one is vendor
  self-report — no measurement of how reliably agents parse markers, sketches, or grid references, and
  no comparison against just handing the agent prose.
- **No format actually carries the method.** The one open, linted format ([[esdm-event-sourced-domain-modeling|ESDM]])
  doesn't model the timeline; the formats that do (EmLang, the Eventmodelers JSON) are vendor-owned.
  Until the joint extension ships, "the model is the agent's spec" still depends on a proprietary
  representation.
- **No token/cost data.** The whole premise is that a structured model is cheaper context than a
  codebase ([[dilger-triplet-flexible-agent-enabled-architecture]]), but nothing captured measures it.
- **The derived rung is not on the same ladder at all** (see the section below).

## The derived rung — when the export is a projection of code (Miller, 2026-08)

Every surface in the table above shares an assumption the page never stated: **the model is authored
first, and the work is making it machine-tractable afterwards.** [[jeremy-miller]] rejects that premise
and is building the alternative ([[miller-jasperfx-critterstack-ai-event-modeling-strategy]]) —
*building*, not shipped: he introduces the list below as "the concept that I'm proposing so far."

What JasperFx is building is genuinely a model artifact an agent can consume — a fluent API in
`JasperFx.Events` declaring event types and read models, a Bobcat UI visualizing the resulting slices,
`dotnet watch` so you can "interactively doodle with slice definitions and see the model change," and
**CLI export of slice definitions for AI agent usage**. By this page's own criteria that scores well:
it is addressable, versioned (it *is* the repo), exportable on demand, and it cannot drift from the code
because it is derived from it.

The reason it is marked *off-ladder* rather than slotted in: the ladder ranks surfaces by how tractable
an **authored** model becomes, and a derived export inverts the dependency. Miller's own words —
*"have the specified model overridden when real code is built in the system"* — make the code
authoritative. So the two are not more and less tractable versions of one thing; they are opposite
directions of fit, and ranking them on one axis would smuggle in the conclusion.

**What each direction buys, stated fairly:**

| | Authored model | Derived export |
| --- | --- | --- |
| Cannot drift from code | ✗ (needs a linter / PR gate) | ✓ by construction |
| Reviewable by non-developers | ✓ | ✗ — you review code, or a rendering of it |
| Exists before the code | ✓ — can drive codegen | ✗ — nothing to build *from* |
| Gradeable against known-good models | ✓ (structural diff — [[dilger-one-million-tokens-self-training-modeling-agent]]) | Untested |

The last row is where the ladder's premise is currently strongest and Miller's weakest, and the third is
where the reverse holds. Neither side has published a comparison. See
[[model-as-code-vs-model-as-language]].

## Related

[[model-as-code-vs-model-as-language]] ·
[[event-modeled-agent-design]] · [[event-modeling]] · [[ai-readable-code]] · [[agent-legibility]] ·
[[context-engineering]] · [[model-context-protocol]] · [[em-standardization-foundation]] ·
[[spec-driven-development]] · [[eventmodelers-ai]]

_Sources: [[dilger-eventmodelers-supports-esdm-export]] · [[dilger-highlighting-markers-give-context-to-agents]] · [[dilger-agentic-collaboration-freeform-drawings]] · [[dilger-planning-like-excel-legible-to-human-and-ai]] · [[dilger-event-modeling-knowledge-hub-emlang]] · [[dilger-drawio-model-in-code]] · [[esdm-event-sourced-domain-modeling]] · [[fraktalio-event-modeler-connect-ai-agents-mcp]] · [[proophboard-skills-ai-agent-event-modeling]] · [[dilger-adding-perspectives-to-event-modeling]]._
