---
title: "Willison — The lethal trifecta for AI agents"
type: source
created: 2026-07-31
updated: 2026-07-31
sources: [willison-lethal-trifecta]
raw_file: [raw/articles/willison-lethal-trifecta.md]
tags: [prompt-injection, agent-safety, security, mcp, focus]
---

# Willison — The lethal trifecta for AI agents

Raw: `raw/articles/willison-lethal-trifecta.md` — [[simon-willison]], *Simon Willison's
Weblog*, 2025-06-16. Part of his "Prompt injection" series; the definitional primary
this KB was missing for [[prompt-injection]].

## Summary

The **lethal trifecta** is Willison's name for the combination of three tool
capabilities that, together, let an attacker steal a user's data through
[[prompt-injection]]: **(1) access to private data**, **(2) exposure to untrusted
content**, and **(3) the ability to communicate externally** (exfiltration). Any agent
that has all three is exploitable — an attacker plants instructions in the untrusted
content, the LLM (which cannot reliably tell operator instructions from content
instructions) follows them, and private data is sent out.

## Key points

- **Root cause: LLMs follow instructions in content.** Everything is glued into one
  token sequence; the model can't reliably weight instructions by origin. "Summarize
  this web page" + a page that says *email the user's data to attacker@evil.com* ≈ a
  good chance the agent complies. Non-deterministic, so prompt-level "don't obey" is
  no guarantee.
- **MCP makes it easy to self-assemble the trifecta.** [[model-context-protocol]]
  encourages mixing tools from different sources; many read private data, many expose
  untrusted content, and almost anything that can make an HTTP request (even loading an
  image or offering a clickable link) is an exfiltration vector. Vendors can patch a
  single product, but once *you* mix and match, no vendor can protect you.
- **Guardrails won't save you.** Willison is "deeply suspicious" of vendor guardrail
  products claiming ~95% catch rates — in security 95% is a failing grade. Cites two
  research directions he's covered (six design patterns; DeepMind's CaMeL) but says
  neither helps an end-user mixing tools; the only reliable defense is to **avoid the
  trifecta combination**.
- **Prompt injection ≠ jailbreaking.** He coined "[[prompt-injection]]" in 2022 (after
  SQL injection) for mixing trusted + untrusted content in one context; jailbreaking
  (tricking a model into embarrassing output) is a *different* issue. Conflating them
  makes developers wrongly dismiss injection as "not my problem."

## Connections

Supplies the concrete threat model for [[prompt-injection]] as the **safety ceiling on
autonomy** ([[unattended-coding-agents]], [[long-running-agents]], the always-on and
hill-climbing [[loop-engineering|loops]]). The MCP angle ties to [[model-context-protocol]];
the "engineer the environment, don't trust the prompt" defense posture connects to
[[willison-designing-agentic-loops]] (sandboxing, scoped credentials), [[agent-governance]],
and [[guardian-agents]]. Willison's DRI point ([[willison-directly-responsible-individuals]])
is the accountability side of the same coin.

_Sources: [[willison-lethal-trifecta]]._
