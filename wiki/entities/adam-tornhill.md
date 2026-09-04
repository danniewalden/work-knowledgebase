---
title: Adam Tornhill
type: entity
created: 2026-06-14
updated: 2026-08-14
sources: [tornhill-five-programming-books-that-changed-how-i-think, tornhill-codescene-unhealthy-code-agentic-token-cost, borg-tornhill-code-for-machines-not-just-humans, tornhill-clear-design-principles-agentic-age, tornhill-hidden-design-decisions-control-coupling, tornhill-merge-conflicts-agentic-bottleneck, tornhill-ai-readable-code-series, tornhill-opinionated-guide-to-naming, tornhill-cannot-trust-agent-codescene-mcp, tornhill-why-human-level-ai-wont-be-enough]
tags: [person, code-health, technical-debt, agentic-coding, harness, agent-legibility]
---

# Adam Tornhill

Founder of **CodeScene** and author of *Your Code as a Crime Scene* / *Software Design X-Rays* —
known for **behavioral code analysis** (mining version-control history to find hotspots, coupling, and
technical debt). His 2026 angle relevant to this KB is **code health as a lever on AI-agent cost and
reliability**: CodeScene research he shares claims unhealthy code raises agent token spend 35–45% and
that agents perform worst in high-technical-debt legacy code
([[tornhill-codescene-unhealthy-code-agentic-token-cost]]). That thesis is now grounded in a
peer-reviewed study he co-authored with **[[markus-borg]]** et al.,
[[borg-tornhill-code-for-machines-not-just-humans]] (FORGE 2026): healthier code yields a 15–30% lower
AI-refactoring break rate, and CodeHealth predicts refactoring correctness better than perplexity or
SLOC.

Beyond the CodeScene company blog he writes a personal Substack, **"Code for Humans and Machines"**
(adamtornhill.substack.com), on *AI-readable code* — practical refactoring patterns and design
principles for codebases that agents can safely evolve. Its flagship piece introduces
**[[tornhill-clear-design-principles-agentic-age|CLEAR]]** (Conceptual alignment, Local reasoning,
Explicit intent, Avoid search luck, Reduce the edit surface): a re-framing of design for agents around
limiting *reconstruction work* and the change blast-radius, explicitly positioned against SOLID's
human-maintainability target.

The Substack is a running **[[ai-readable-code|AI-Readable Code]]** series
([[tornhill-ai-readable-code-series]]): CLEAR distilled from concrete refactoring walkthroughs, of
which **[[tornhill-hidden-design-decisions-control-coupling|Hidden Design Decisions]]** (boolean flag →
Strategy + domain type) is the latest. He also extends the argument to the multi-agent scale —
**[[tornhill-merge-conflicts-agentic-bottleneck|merge conflicts as a socio-technical signal]]**, where
his behavioral-code-analysis lineage (*Your Code as a Crime Scene*) meets parallel agents — and adds two
useful counter-weights: *Compressed Cognition* (speed paid for in decision density) and *SDD and the
Illusion of Known Scope* (a pragmatic challenge to spec-first optimism).

Two further 2026-06 pieces sharpen the thread: **[[tornhill-opinionated-guide-to-naming|a naming guide]]**
(Jun 23) — naming as cognitive compression, the highest-leverage AI-readable-code move, with a cited LLM
result that identifier-name improvements "yielded the largest returns"; and
**[[tornhill-cannot-trust-agent-codescene-mcp|"you cannot trust your coding agent to produce maintainable
code"]]** (Jun 22) — an LLM can't reliably self-assess code health, so the fix is a **deterministic
external sensor** (the CodeScene MCP) rather than "follow SOLID" prompts or LLM self-review; he's coded
100% agentically for nine months.

A 2026-06-30 essay steps up from tactics to thesis:
**[[tornhill-why-human-level-ai-wont-be-enough|"Why Human-Level AI Won't Be Enough"]]** argues that even
best-human-expert-level coding agents won't suffice, because AI *raises its own quality bar* through
**scale** (Lehman's laws; defect opportunities grow with code + change volume) and **speed**
(orders-of-magnitude faster generation → higher churn/fault risk = "wrong at scale"), while the
stochastic core guarantees rare errors recur across millions of decisions. He rejects chasing
"superhuman code quality" and prescribes the opposite — **"create environments where unreliable agents
reliably produce acceptable outcomes."** This is the load-bearing *why* under his code-health tooling:
the value is in the environment, not a better model — the KB's environment-over-model through-line.

In the KB he connects the **code-health / technical-debt** angle to [[harness-engineering]] (a
cost/quality argument adjacent to [[fowler-bockeler-maintainability-sensors]]), [[agentic-coding]], and
now [[agent-legibility]] / [[locality-of-reference]] / [[ai-readable-code]] (via CLEAR and the series).
Watched in `watch-config.json` (the Substack is his on-thread personal primary; the LinkedIn feed mixes
on-thread items with off-thread LLM-culture commentary).

Not everything he writes is on this thread. **[[tornhill-five-programming-books-that-changed-how-i-think|Five
Programming Books That Changed How I Think]]** (2026-08-11) is a pre-2015 reading list — SICP, Beck's
*Smalltalk Best Practice Patterns*, Norvig's *PAIP*, Glass, *Thinking Forth*, Shiffman — filed for
completeness rather than evidence. Two asides connect: his jab at "AI adoption metrics… back to
productivity mistaken for lines of code produced," and his endorsement of Coplien's **commonality /
variability analysis** as "the foundation of great software design" — an ancestor of the
[[business-capabilities]] boundary-finding the KB tracks. Also worth noting for taste calibration: he
declines to recommend *Clean Code* ("too narrow and a bit too dogmatic"), consistent with his
[[tornhill-clear-design-principles-agentic-age|CLEAR-over-SOLID]] argument.

_Source pages: [[tornhill-codescene-unhealthy-code-agentic-token-cost]] ·
[[borg-tornhill-code-for-machines-not-just-humans]] ·
[[tornhill-clear-design-principles-agentic-age]] · [[tornhill-hidden-design-decisions-control-coupling]] ·
[[tornhill-merge-conflicts-agentic-bottleneck]] · [[tornhill-ai-readable-code-series]] ·
[[tornhill-opinionated-guide-to-naming]] · [[tornhill-cannot-trust-agent-codescene-mcp]] ·
[[tornhill-why-human-level-ai-wont-be-enough]] ·
[[tornhill-five-programming-books-that-changed-how-i-think]] (off-thread reading list, 2026-08-11)._
