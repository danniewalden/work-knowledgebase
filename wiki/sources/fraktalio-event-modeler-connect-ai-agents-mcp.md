---
title: "Fraktalio — Connect AI Agents to Your Board (Event Modeler + MCP)"
type: source
created: 2026-06-14
updated: 2026-06-14
sources: [fraktalio-event-modeler-connect-ai-agents-mcp]
tags: [event-modeling, agentic-ai, model-context-protocol, tool, given-when-then, focus]
---

# Fraktalio — Connect AI Agents to Your Board (Event Modeler + MCP)

LinkedIn company-page post by **[[fraktalio]]** (2026-06-13, "1d" before capture) announcing **Direct
AI Agent Integration via MCP** for their **Event Modeler** board. The second tool in the KB — after
[[prooph-board]] — to ship an [[model-context-protocol|MCP]] server letting a coding agent *do* Event
Modeling on the canvas. Raw capture: `raw/articles/fraktalio-event-modeler-connect-ai-agents-mcp.md`.

## Key points

- **What it is.** An AI co-pilot that doesn't just chat but "interacts live with your event modeling
  canvas — reading schemas, understanding context, and building entire system flows," connected via a
  `/mcp` endpoint that the agent authenticates to directly.
- **Worked demo (Hotel Booking).** Prompted to "Create a Hotel Booking event model and feel free to
  design a custom flow," the agent loaded the schemas, mapped a **Happy Path** (BookRoom →
  ConfirmBooking → ProcessPayment → CheckIn → Checkout), and anticipated edge cases by generating a
  **Cancellation & Refund Path**.
- **GWT generation is the headline.** "It doesn't just place blocks. It generates deep, production-ready
  specifications, including full **Given/When/Then scenarios for every command** — covering
  domain-specific business exceptions like RoomAlreadyBooked, PaymentDeclined, and
  CannotCancelAfterCheckIn." This is exactly the [[event-modeled-agent-design]] GWT-per-command claim,
  realized as a feature.
- **Positioning.** "No more manual, repetitive wireframing for your event-driven architectures … the
  open-standard Model Context Protocol … bridges the gap between AI reasoning and visual domain
  engineering." Attached doc "Modeler and MCP" shows the blueprint (Screen/Automation/Command/Event/
  Projection swimlanes) beside an agent/MCP pane. Hashtags: #EventModeling #AIAgents
  #ModelContextProtocol #DomainModeling #SoftwareArchitecture.

## Why it matters

A second independent vendor putting an **MCP-for-doing-Event-Modeling** server into a product
strengthens rung (3) of [[event-modeled-agent-design]]'s evidence ladder — "agents are being built to
*practise* Event Modeling directly" — which previously rested mainly on [[prooph-board]]. The
auto-generated **GWT-per-command (incl. business exceptions)** is the most direct tooling instance of
the method's slice/acceptance-criteria output becoming a machine artifact, complementing
[[jwilger-agent-skills-event-modeling]] (GWT as TDD gates) and [[dilger-model-is-a-living-spec-always-on-agent]]
(slice → tests-as-harness). Direction of fit: here the agent **authors** the model; in jwilger/Dilger
the model **governs** the agent — together they close the loop.

## Caveats

Vendor announcement; small page (71 followers), no independent review, no metrics. The `lnkd.in`
shortlink to the live tool wasn't resolved in capture. Whether the generated GWT specs are *correct*
(vs. plausible) is unverified — the same model-authors-the-spec quality question that
[[dilger-keep-command-handlers-pure]] raises about agent drift.

## Links

Entities: [[fraktalio]], [[prooph-board]], [[qlerify]], [[eventmodelers-ai]]. Concepts:
[[model-context-protocol]], [[event-modeling]], [[event-modeled-agent-design]],
[[spec-driven-development]], [[agentic-coding]], [[domain-driven-design]].
Related sources: [[proophboard-skills-ai-agent-event-modeling]],
[[jwilger-agent-skills-event-modeling]], [[dilger-model-is-a-living-spec-always-on-agent]],
[[qlerify-event-modeling-tool-ai]].
