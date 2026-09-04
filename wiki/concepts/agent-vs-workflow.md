---
title: Agents vs Workflows
type: concept
created: 2026-06-11
updated: 2026-09-04
sources: [anthropic-building-effective-agents, svitla-agentic-ai-market-trends-2026, cao-agentic-software-restructuring-software-paradigm]
tags: [agentic-ai, architecture, definitions]
---

# Agents vs Workflows

[[anthropic]]'s foundational distinction within the umbrella of **agentic systems**:

- **Workflows** — LLMs and tools orchestrated through *predefined code paths*. Predictable,
  consistent; best for well-defined tasks.
- **Agents** — systems where the LLM *dynamically directs its own process and tool usage*,
  maintaining control over how it accomplishes the task. Better when flexibility and
  model-driven decisions are needed at scale.

The guidance: use the simplest thing that works. Often a single augmented LLM call is enough;
add a workflow when the task decomposes cleanly; reach for a true agent only for open-ended
problems where you can't hardcode the path (accepting higher cost and compounding-error risk).

## Why it matters

This is the conceptual root of two other KB ideas. The market's **[[autonomy-ladder]]**
(chain → workflow → partially/fully autonomous) is the same spectrum operationalized, and
**[[agentwashing]]** is what happens when low-autonomy workflows/assistants are marketed as
agents. See the full pattern catalog in [[agentic-workflow-patterns]].

**The far end of the distinction.** [[cao-agentic-software-restructuring-software-paradigm|Cao
(arXiv:2606.05608 — single-author position preprint, not peer-reviewed)]] pushes it past "the agent chooses
the path": "in [traditional software], code is the carrier of pre-written decision logic; in [agentic
software], **the agent itself is the software, and its decision logic is generated at runtime**", with code
"dynamically generat[ed] and discard[ed] as an instrumental resource". His delivery arc — licensed software →
SaaS → **Agent-as-a-Service** — reads each step as transferring complexity away from the user, "with the
agentic shift transferring not just operational complexity but **decision-making complexity itself**."
Record the tension rather than adopting the claim: if decision logic is generated at runtime and discarded,
auditability cannot live in the code, and has to come from a log
([[decision-trace]], [[event-sourced-agentic-patterns]], [[agent-explainability]]).

_Source pages: [[anthropic-building-effective-agents]] · [[svitla-agentic-ai-market-trends-2026]] · [[cao-agentic-software-restructuring-software-paradigm]]._
