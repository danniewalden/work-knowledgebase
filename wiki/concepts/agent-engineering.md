---
title: Agent Engineering
type: concept
created: 2026-06-11
updated: 2026-09-04
sources: [langchain-state-of-agent-engineering-2026, anthropic-building-effective-agents, fowler-bockeler-harness-engineering, langchain-anatomy-of-an-agent-harness, cao-agentic-software-restructuring-software-paradigm, guo-survey-question-answering-to-task-completion-harness-design, mcateer-evolution-of-the-agent-harness]
tags: [agentic-ai, discipline, engineering, reliability]
---

# Agent Engineering

[[langchain]]'s framing of an emerging discipline: **the iterative process of harnessing LLMs
into reliable systems**. Because agents are nondeterministic, engineers must rapidly iterate
to refine and improve agent quality, rather than expecting correctness by construction.

In practice it spans the activities the KB's sources describe: choosing the right
[[agentic-workflow-patterns]] and avoiding unnecessary complexity ([[anthropic]]), managing
context ("context engineering"), building [[agent-observability-and-evals]], and routing
across multiple models by complexity/cost/latency. The market analog is the gap between a
working demo and a production system — "that's when the work begins"
([[svitla-agentic-ai-market-trends-2026]]).

Its environment-and-controls arm is **[[harness-engineering]]** — building and continuously
improving the [[agent-harness]] (everything around the model) so a non-deterministic model does
reliable work. The "context engineering" mentioned above now has its own page:
[[context-engineering]].

## An academic definition arrives — and a relocation of judgement (2026-06)

[[cao-agentic-software-restructuring-software-paradigm|Cao (arXiv:2606.05608)]] proposes **"Agentic
Engineering"** as "an expansion of the software engineering discipline into a new paradigm, distinct in its
**core object of study** (agent systems rather than static source code), its **control model** (LLM-driven
rather than human-predefined), and its **human role (intent architect rather than code author)**." It is a
**single-author arXiv position preprint — not peer-reviewed** — from a private company rather than an academic
lab, arguing a paradigm rather than reporting an experiment, and it was **retitled between versions** (v1: "The
End of Software Engineering…"; v2, current: "Agentic Software…"), which is itself a datum about how strongly the
claim survived a week.

Its significance here is narrow and real: **the KB's relocation-of-judgement thesis is no longer
practitioner-only.** [[addyosmani-earning-taste-and-judgment]], [[dilger-harness-is-20-percent-requirements-are-80]],
[[dilger-describing-without-solving-burns-you-out]], [[spec-driven-development]] and [[event-modeling]] all hold
that the human's work has moved from producing the artifact to specifying intent and adjudicating quality. Cao
states that as an academic claim. **It is an academic *statement* of the thesis, not academic *evidence* for
it.** His four "new human differentiators" — **intent articulation** ("specify goals with sufficient clarity
and constraint that agents can operate autonomously"), **architectural oversight** ("how multiple agents should
coordinate, what memory should be shared, and where human judgment must intervene"), **quality calibration**
("defining what 'good' looks like and building evaluation frameworks that agents can use for self-correction")
and **ethical governance** — map almost one-to-one onto [[spec-driven-development]],
[[multi-agent-orchestration]], [[agent-observability-and-evals]] and [[agent-governance]]. Treat that neatness
with some suspicion: a four-item list of virtues is easy to write and hard to falsify.

**Do not quote the three-role phrasing** — the one naming intent, coordination and audit roles — often
attributed to this paper — the capture could not verify it as a verbatim sentence, so it is not filed as a
quote here. Use the abstract's own wording above. One tension to record rather than resolve: Cao's "the agent
itself is the software, and its decision logic is generated at runtime" cuts against this KB's substrate thread
([[event-sourcing]], [[decision-trace]], [[agent-readable-model-artifacts]]), which argues agent behaviour must
leave durable inspectable artifacts.

For where this discipline is heading according to its two other 2026 statements — a four-rung ladder ending in
**agent-native training and co-evolution** ([[guo-survey-question-answering-to-task-completion-harness-design|Guo
et al.]], *preprint*) and the **train → absorb → shed** account of harness work
([[mcateer-evolution-of-the-agent-harness]], practitioner essay) — see [[harness-engineering]] and
[[harness-absorption]].

_Source pages: [[langchain-state-of-agent-engineering-2026]] · [[anthropic-building-effective-agents]] · [[fowler-bockeler-harness-engineering]] · [[langchain-anatomy-of-an-agent-harness]] · [[cao-agentic-software-restructuring-software-paradigm]] · [[guo-survey-question-answering-to-task-completion-harness-design]] · [[mcateer-evolution-of-the-agent-harness]]._
