---
title: Fraktalio
type: entity
created: 2026-06-14
updated: 2026-08-31
sources: [fraktalio-event-modeler-connect-ai-agents-mcp]
tags: [tool, platform, company, event-modeling, agentic-ai, model-context-protocol, focus]
---

# Fraktalio

A Belgrade-based IT services / tooling company ("Automate Your Information Flow and Business
Processes") building **Event Modeler**, a visual [[event-modeling]] board. As of 2026-06-13 it ships
**Direct AI Agent Integration via [[model-context-protocol|MCP]]**: an agent connects to a `/mcp`
endpoint and builds the model on the canvas — placing blocks and generating Given-When-Then specs per
command ([[fraktalio-event-modeler-connect-ai-agents-mcp]]). Known to the KB only from its LinkedIn
company page so far (small reach, ~71 followers); this page is provisional. Added to `watch-config.json`
as a watched entity at Dannie's request (2026-06-14).

## Where it sits

One of the cluster of **AI-assisted Event Modeling tools** in the KB, alongside [[prooph-board]]
(online EM tool + Cody Engine + agent skills/MCP), [[qlerify]] (generates models + code from
descriptions), and [[eventmodelers-ai]] ([[martin-dilger]]'s spec-driven agentic platform).
Fraktalio's distinctive angle is an **MCP server where the agent authors the model and its
GWT specifications** — the second independent vendor (after prooph board) to make
"agents that *do* Event Modeling" a shipped feature, which is why it matters to
[[event-modeled-agent-design]]. Contrast the direction of fit: Fraktalio has the agent **author** the
model; [[jwilger-agent-skills-event-modeling]] and [[dilger-model-is-a-living-spec-always-on-agent]]
have the model **govern** the agent.

## Caveats

Evidence is a single vendor announcement — no independent review, no metrics, correctness of the
auto-generated GWT unverified. Fraktalio also has prior (out-of-window) posts on event-driven design
generally; only the MCP-integration post is captured.

## Related

[[model-as-code-vs-model-as-language]]

_Source pages: [[fraktalio-event-modeler-connect-ai-agents-mcp]]._
