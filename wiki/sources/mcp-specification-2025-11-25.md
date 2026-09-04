---
title: "Source: Model Context Protocol — Specification (2025-11-25)"
type: source
created: 2026-06-11
updated: 2026-06-11
sources: [mcp-specification-2025-11-25]
raw_file: [raw/articles/mcp-specification-2025-11-25.md]
tags: [protocol, mcp, primary-source, agentic-ai, tools]
---

# Source: Model Context Protocol — Specification (2025-11-25)

The **primary** specification overview for [[model-context-protocol]] (version 2025-11-25),
from [[anthropic]]'s MCP project. Replaces reliance on the secondary Svitla description. Raw
capture: `raw/articles/mcp-specification-2025-11-25.md`.

## Summary

MCP is an open protocol for connecting LLM applications to external data and tools in a
standardized way, using **JSON-RPC 2.0** over stateful connections with capability
negotiation. Explicitly analogized to the **Language Server Protocol**: as LSP standardized
language support across editors, MCP standardizes context/tool integration across AI apps.

## Key points

- **Three roles:** *Hosts* (LLM apps that initiate connections), *Clients* (connectors inside
  the host), *Servers* (services providing context/capabilities).
- **Server features:** Resources (context/data), Prompts (templated workflows), Tools
  (functions the model executes). **Client features:** Sampling (server-initiated LLM calls),
  Roots (filesystem/URI boundaries), Elicitation (requests for user input).
- **Utilities:** configuration, progress tracking, cancellation, error reporting, logging.
- **Security is foundational and consent-centric:** user consent and control, data privacy,
  tool safety (tools = arbitrary code execution; annotations from untrusted servers are
  untrusted), and explicit approval of LLM sampling. MCP can't enforce these at the protocol
  level, so implementors **SHOULD** build consent/authorization flows and access controls.
- Spec is authoritative against the TypeScript `schema.ts`. A newer **2026-07-28** release
  candidate exists (stateless core, Extensions, Tasks, MCP Apps, auth hardening).

## Connections / contrast

The vertical (agent→system) layer in [[multi-agent-orchestration]], complementary to
[[agent2agent-protocol]] (horizontal). Concretely realizes the tool/retrieval/memory
augmentations of the [[augmented-llm]]. Its consent/tool-safety principles are protocol-level
support for [[agent-governance]]. Primary source — supersedes the secondary MCP framing in
[[svitla-agentic-ai-market-trends-2026]].
