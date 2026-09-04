---
title: Agentic Coding
type: concept
created: 2026-06-11
updated: 2026-07-31
sources: [anthropic-building-effective-agents, langchain-state-of-agent-engineering-2026, svitla-agentic-ai-market-trends-2026, jwilger-agent-skills-event-modeling, jwilger-agent-skills-factory-pipeline, dilger-spec-driven-development-applied, dilger-keep-command-handlers-pure, tornhill-codescene-unhealthy-code-agentic-token-cost, borg-tornhill-code-for-machines-not-just-humans, miller-codebase-is-the-prompt-vertical-slices-ai, dymitruk-ai-trained-on-dysfunction-agents-are-a-must, dudycz-fork-can-you-own-it, fowler-agentic-programming, willison-agentic-engineering-patterns, willison-vibe-engineering]
tags: [agentic-ai, use-case, software-development, coding]
---

# Agentic Coding

Software development is one of [[anthropic]]'s two showcase agent domains and, per
[[langchain-state-of-agent-engineering-2026]], the **most-used agent type in daily
workflows**. Coding is a strong fit because solutions are **verifiable through automated
tests**, agents can iterate using test results as feedback, the problem space is structured,
and output quality is objectively measurable. Anthropic's coding agents resolve real GitHub
issues on **SWE-bench Verified** from the PR description alone — though human review remains
crucial.

## Definition ([[fowler-agentic-programming|Fowler]])

[[martin-fowler]]'s bliki entry gives the vendor-neutral definition and draws the boundaries the KB
uses: developers **prompt an LLM to write code, then review the results** — "a profound change to the
nature of programming." He prefers the name **"agentic programming."** Two distinctions pin it down:
it is *not* [[vibe-modeling|vibe coding]] (where humans never look at the code) — in agentic
programming they **review the code in detail** — and it is *not* in-IDE autocomplete; agentic tools
work in a **terminal**, manipulating the source tree directly (create/modify files, run code, evaluate
tests, continue for long stretches) while humans review code, tests, and **sensor outputs**. Fowler
names **[[harness-engineering]]** ("guides and sensors around the LLM") as the central new skill, and
flags **understanding the domain** + iterative collaboration with users — the same upstream emphasis as
[[dilger-harness-is-20-percent-requirements-are-80|Dilger's 80%]] and [[spec-driven-development]].

The practitioner counterpart is [[simon-willison]]'s term **"agentic engineering"**
([[willison-agentic-engineering-patterns]]), landing on the same boundary from the hands-on side. He
first coined it **"vibe engineering"** ([[willison-vibe-engineering]], 2025-10-07) — the *accountable*
counterpart to [[vibe-modeling|vibe coding]] — before the ecosystem re-settled on "agentic engineering"
(his own 2026-02-23 update); that post's core claim is that **coding agents amplify existing senior
practice** (tests, planning, docs, version control, review, QA), so LLMs "reward top-tier software
engineering." His
definition is the crispest in the KB — **"agents run tools in a loop to achieve a goal,"** where the
defining capability for coding agents is that one tool **executes code**, letting them "iterate towards
software that demonstrably works." He adds the harness insight directly: **"LLMs don't learn from their
past mistakes, but coding agents can, provided we deliberately update our instructions and tool
harnesses"** — [[harness-engineering]] as accumulated, edited context — and keeps the same narrow
[[vibe-modeling|vibe-coding]] boundary Fowler draws.

## State of play

- Daily-driver tools named by practitioners: **Claude Code, Cursor, GitHub Copilot, Amazon
  Q, Windsurf, Antigravity** ([[langchain-state-of-agent-engineering-2026]]).
- GitHub Copilot reportedly generates ~41% of code where used; [[gartner]] forecasts ~75% of
  developers using AI coding agents by 2028 (vs <10% in 2023).
- The shift is from autocomplete → agents that **plan, execute, test, and iterate** with
  minimal guidance.

## Caution

Letting agents commit/deploy without review amplifies quality risk — one cited report finds
AI-written code carries ~1.7× the issue rate and ~45% security-flaw rate, and agents tend to
avoid refactoring ([[svitla-agentic-ai-market-trends-2026]]). Reinforces the
[[agent-observability-and-evals]] and [[agent-governance]] themes.

The risk runs the other way too — **bad existing code degrades the agent**. CodeScene research shared
by [[adam-tornhill]] ([[tornhill-codescene-unhealthy-code-agentic-token-cost]]) claims agents "perform
worst where they are needed most," in the highest-technical-debt legacy code, and that **unhealthy
code increases agent token spend by 35–45%** (Java/C++/Python). So **code health is an input to agent
cost and reliability**, not just an output to guard — a cost argument for the maintainability-sensor
side of [[harness-engineering]] ([[fowler-bockeler-maintainability-sensors]]). That token-spend figure
is a vendor claim, but the underlying thesis now has a **peer-reviewed primary**:
[[borg-tornhill-code-for-machines-not-just-humans]] (FORGE 2026) shows on 5,000 Python files that LLMs
break **Healthy code (CodeHealth ≥ 9)** far less often — a **15–30% refactoring-risk reduction** — and
that **CodeHealth predicts refactoring correctness better than perplexity or SLOC**, with a test-pass
oracle rather than marketing. Its recommendation — use code health to **route** AI work (low-risk where
Healthy, human oversight where Unhealthy) — is a concrete [[feedforward-and-feedback-controls|sensor]]
policy. Code *structure* is the same kind of input:
[[jeremy-miller]] ([[miller-codebase-is-the-prompt-vertical-slices-ai]]) argues "the codebase is part of
the prompt" — layered code forces the agent to load 6–7 scattered files per change, collapsing context
signal-to-noise, while [[vertical-slice-architecture|vertical slices]] keep a feature local
([[locality-of-reference]]) and cut tokens per task.

## The ownership caveat — "LLM as a fork" ([[oskar-dudycz|Dudycz]])

A counter-weight to "vibe coding" optimism: [[dudycz-fork-can-you-own-it|Dudycz]] argues LLMs change
the cost of **producing** code, not of **owning** it — "writing the small thing was never the hard part;
owning, understanding, maintaining, being on the hook at 2 a.m. is." The old "install and move on"
becomes "vibe it and move on" — "same missing decision, new flavour," a new strain of Shadow IT. Cheap
generation doesn't dissolve the responsibility for what gets shipped — the same point
[[tornhill-cannot-trust-agent-codescene-mcp|Tornhill]] makes about quality ("ship code you confirmed
works") and [[addyosmani-loop-engineering|Osmani]] about [[loop-engineering|loops]] ("stay the engineer").

## Building trust: harness engineering

The emerging answer to that risk is **[[harness-engineering]]** — wrapping the coding agent in
guides and sensors ([[feedforward-and-feedback-controls]]) that raise first-try quality and let it
self-correct before code reaches human review. See [[openai-harness-engineering-codex]] (zero
hand-written code at scale), [[anthropic-effective-harnesses-long-running-agents]]
([[long-running-agents]] across context windows), and [[fowler-bockeler-harness-engineering]]
(the user-side mental model).

The frontier of this use case is **[[unattended-coding-agents]]** — agents that run with no human in
the loop until a PR is ready. [[stripe-minions-one-shot-coding-agents|Stripe's minions]] reportedly merge 1,000+
such PRs/week; [[mitchell-hashimoto]] documents the individual-developer version (background and
"always-running" agents).

A complementary thread is **[[spec-driven-development|spec-driven]]** agentic coding: rather than
prompting freely, the human first produces a specification the agent builds against. [[john-wilger]]'s
`agent-skills` ([[jwilger-agent-skills-event-modeling]], [[jwilger-agent-skills-factory-pipeline]]) uses
[[event-modeling]] for that spec — vertical slices and Given-When-Then scenarios become TDD acceptance
gates in an autonomous [[software-factory|factory]] pipeline (the model is the *upstream, human-authored
spec that drives a team of coding agents*) — directly linking [[agentic-coding]] to
[[event-modeled-agent-design]]. [[martin-dilger]]
makes the same case from practice: prompt engineering "didn't work," so you design the environment
(the spec) instead ([[dilger-spec-driven-development-applied]]). His Claude Code anecdote is a sharp
illustration of the drift risk above — the agent ignored the event model and tried to put a business
rule in the routing layer, so a written skill had to be **enforced**, not just stated
([[dilger-keep-command-handlers-pure]]). [[adam-dymitruk]] gives the blunt rationale
([[dymitruk-ai-trained-on-dysfunction-agents-are-a-must]]): AI was "trained on dysfunction," so it
won't produce best-practice software on its own — the value is in the spec/scaffolding you impose to
*constrain* it toward good structure.

_Source pages: [[anthropic-building-effective-agents]] · [[langchain-state-of-agent-engineering-2026]] · [[svitla-agentic-ai-market-trends-2026]] · [[jwilger-agent-skills-event-modeling]] · [[jwilger-agent-skills-factory-pipeline]] · [[dilger-spec-driven-development-applied]] · [[dilger-keep-command-handlers-pure]] · [[tornhill-codescene-unhealthy-code-agentic-token-cost]] · [[borg-tornhill-code-for-machines-not-just-humans]] · [[miller-codebase-is-the-prompt-vertical-slices-ai]] · [[dymitruk-ai-trained-on-dysfunction-agents-are-a-must]] · [[willison-agentic-engineering-patterns]] · [[willison-vibe-engineering]]._
