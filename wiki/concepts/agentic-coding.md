---
title: Agentic Coding
type: concept
created: 2026-06-11
updated: 2026-09-04
sources: [anthropic-building-effective-agents, langchain-state-of-agent-engineering-2026, svitla-agentic-ai-market-trends-2026, jwilger-agent-skills-event-modeling, jwilger-agent-skills-factory-pipeline, dilger-spec-driven-development-applied, dilger-keep-command-handlers-pure, tornhill-codescene-unhealthy-code-agentic-token-cost, borg-tornhill-code-for-machines-not-just-humans, miller-codebase-is-the-prompt-vertical-slices-ai, dymitruk-ai-trained-on-dysfunction-agents-are-a-must, dudycz-fork-can-you-own-it, fowler-agentic-programming, willison-agentic-engineering-patterns, willison-vibe-engineering, zalando-agentic-engineering-snapshot, addyosmani-code-agent-orchestra, addyosmani-agentic-code-quality, morris-humans-and-agents-in-software-engineering-loops, macmanus-prs-not-welcome-software-factories, tornhill-compressed-cognition-cost-of-faster-coding, willison-more-than-just-code-review, laycock-maybe-we-shouldnt-be-reviewing-all-this-code, willison-introducing-wrapture]
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

**The boundary, stated by a maintainer about his own project (2026-08).** Graham Dumpleton (author of
`wrapt`, `mod_wsgi`, New Relic's Python agent), on shipping the `wrapture` library, relayed in
[[willison-introducing-wrapture]]:

> "Every line of code and documentation in wrapture was written by an AI assistant working under my
> direction… **This was not vibe coding**, where a one-shot prompt produces a pile of generated code and
> the person driving hopes for the best because they lack the knowledge to judge what came back… I have
> spent a long time in this particular corner of Python and knew exactly what the result needed to be, and
> **the AI was the means of producing it rather than the source of the design**."

"The means of producing it rather than the source of the design" is the crispest statement in the KB of
where this page's line falls: not in tooling, review volume or output quality, but in **who holds design
authority and could judge what came back**. **Markers: a SELF-REPORT ABOUT HIS OWN PROCESS, relayed
secondhand by Willison, about a library weeks old with no defect, review or maintenance data.** It is a
usable definition; it is not evidence that agent-driven authorship works. Note also the selection effect
running through all three of the KB's late-2026 cases of agent-authored libraries shipped under a
maintainer's own name (this one, [[willison-sqlite-utils-4-mostly-written-by-fable]], and the prompt-diff
system in [[willison-claudes-new-system-prompt]]): every one has a maintainer with deep prior ownership of
the problem.

## State of play

- Daily-driver tools named by practitioners: **Claude Code, Cursor, GitHub Copilot, Amazon
  Q, Windsurf, Antigravity** ([[langchain-state-of-agent-engineering-2026]]).
- GitHub Copilot reportedly generates ~41% of code where used; [[gartner]] forecasts ~75% of
  developers using AI coding agents by 2028 (vs <10% in 2023).
- The shift is from autocomplete → agents that **plan, execute, test, and iterate** with
  minimal guidance.

## A non-vendor production account at scale ([[zalando-agentic-engineering-snapshot|Zalando, 2026-08-14]])

The KB's second non-vendor, production-scale account of agentic engineering after
[[stripe-minions-one-shot-coding-agents]], and the first that is about **organization** rather than
tooling: >250 engineering teams, 2.5 years, and — unusually — **no productivity claim at all.** Its
headline finding is the honest one: *"**AI amplifies the good and bad practices across our
organization.**"*

What actually turned out to matter, none of which appears in any practitioner-loop source:

- **An LLM proxy from day one** (LiteLLM, January 2024) fronting OpenAI, AWS Bedrock and Google Vertex, so
  engineers could experiment freely while the platform team got *"a single point to measure adoption via:
  MAU, WAU, model, User-Agent."* With post-call hooks for anonymized cost tracking, **pre-call hooks
  enforcing client version upgrades** (*"For self-managed client installations, unfortunately blocking
  access is the only effective measure. Same goes for retiring models. **There is always a long-tail group
  of users who do not adjust their local configurations**"*), and **auto-injected prompt-caching
  checkpoints** *"which reduced costs for custom agents while their authors still learn about prompt
  caching."*
- **Vendor independence as policy, and a behavioural finding against it.** *"We have never centrally
  mandated the use of a single tool."* But: *"we see users **becoming too attached** to the coding agent
  they had been using for a while… **The hesitance to switch tools on psychological level exists despite
  the rather low switching costs**."* And a structural reason to keep the option: *"moving off
  closed-weight models requires switching to open tools."*
- **Deliberate non-convergence.** *"With >200 teams innovating and broadly exploring the ecosystem, the
  question arises whether and when to converge. **We believe it's way too early for this.**"* Instead:
  transparency mechanisms — an internal **Tech Radar** now tracking **practices** as well as tools
  (*"the cambrian explosion of AI tools… increased the need for clearer guidance on practices that are
  proven and those that are still early stage"*), an **LLM guild** running weekly since 2024, and
  topic-seeded hackathons used to *"explore parallel paths and choose what tools to invest in."* Contrast
  [[em-standardization-foundation]] and [[laycock-citizens-build-agents-execute-experts-govern]].
- **A centralized agent-skill collection**, grouped into plugins, spanning disciplines and languages, with
  **migration skills the most popular type** — *"skills that guide teams in adopting new platform tools or
  infrastructure practices."* Second-order benefit: *"By encouraging broad contribution of skills that
  teams found useful, we got an opportunity to **discover and disseminate best practices across the
  organization**."*
- **Two vendor-ecosystem gaps reported as recurring:** tools using **generic `User-Agent` headers** (so
  clients are unidentifiable at the proxy), and **no support for custom auth commands** — only static
  credentials or subscription defaults, so *"tokens expire and need to be refreshed manually which
  involves restarting the applications."*
- **Observed codebase effects, offered as illustration and not causation.** PR sizes have grown for two
  years, with growth in the [500,1k) and [1k,2k) buckets since Sonnet 4 (Q2/2025); commit messages *"carry
  the footprint of coding agents, typically around the 5k character mark"* (one contained a full unit-test
  log). Commit-level cyclomatic-complexity curves across four codebases show *"inflection points… at a
  time when coding agents come into the picture,"* and for the agent-native codebase *"complexity to build
  up very quickly with growth fading out"* — with the question left open: *"one would hope this means that
  the time to build has been drastically reduced. **Time will show whether this is the case.**"*
- **A caveat they raise against their own results, and against everyone else's.** *"Across industry, many
  AI wins and increases in PR throughput are reported for **monorepos** where the leverage is high. While
  we have a few monorepos, we largely use separate repositories for our microservices."* A caution about
  every monorepo-based factory result in this KB.
- **And a finding that cuts against the trend:** in training sessions, *"the temptation of participants to
  use coding agents as a shortcut to achieve results is high. **Yet, using coding agents usually inhibits
  learning**"* — which is why they now *"state explicitly when manual coding is expected."* See
  [[comprehension-debt]].

*(Two markers, both true. **Non-vendor about the market** — Zalando sells fashion, not agent tooling, and
this is practice at scale rather than a pitch, which is why it is valuable. **VENDOR SELF-REPORT about
itself** — every figure is Zalando's own account of its own internal tooling: the 33% low-risk /
20–40% lead-time numbers (see [[autonomy-ladder]]), and the complexity analysis, which is **four codebases
with no control arm** and agent adoption partly inferred from `Co-authored-by` markers the author says are
inconsistent. All four figures are untranscribed images. No defect, incident, throughput or cost-per-change
data is reported.)*

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

**Felt speed is not measured speed, and the gap is measurable.** The strongest caution on this page is
not about code quality but about the productivity claim itself.
[[tornhill-compressed-cognition-cost-of-faster-coding|Tornhill]] relays a controlled trial of
experienced open-source developers in which the AI-assisted group **estimated a 20% speedup** and were
**19% slower** than the control group — "even expert developers overestimate the AI impact on developer
productivity." **Cite this carefully: he names no study, date or link** ("one of my favourite
studies"), so it is *an unnamed controlled trial as relayed by Tornhill* and **must never be
attributed to a named study, lab or set of authors, however tempting the guess** — and the two
figures must stay distinct — one is what developers felt, one is what was measured. His proposed
mechanism is **self-interruption**: agentic work is a stream of questions, diffs, failed tests and
almost-right changes, each of which "pulls you into a new review-verify-steer decision." Everything on
this page that reports a speedup as an impression (and most of the KB's practitioner speed claims are
impressions) should be read against it. See [[attention-bottleneck]].

**And the verification cost has its own dispute now.** Who reads agent-written code, and what replaces
reading, is an open five-way argument among Brewster, Laycock, Tornhill, Osmani and Willison — held on
[[verification-burden]] rather than resolved here. The short version: [[simon-willison]] —
*"eyeballing every line of code has never been the most effective way to validate a change"*
([[willison-more-than-just-code-review]]); [[rachel-laycock]] — don't automate review, move what review
is *for* earlier and review by exception ([[laycock-maybe-we-shouldnt-be-reviewing-all-this-code]]).

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

_Source pages: [[anthropic-building-effective-agents]] · [[langchain-state-of-agent-engineering-2026]] · [[svitla-agentic-ai-market-trends-2026]] · [[jwilger-agent-skills-event-modeling]] · [[jwilger-agent-skills-factory-pipeline]] · [[dilger-spec-driven-development-applied]] · [[dilger-keep-command-handlers-pure]] · [[tornhill-codescene-unhealthy-code-agentic-token-cost]] · [[borg-tornhill-code-for-machines-not-just-humans]] · [[miller-codebase-is-the-prompt-vertical-slices-ai]] · [[dymitruk-ai-trained-on-dysfunction-agents-are-a-must]] · [[willison-agentic-engineering-patterns]] · [[willison-vibe-engineering]] · [[zalando-agentic-engineering-snapshot]] · [[addyosmani-code-agent-orchestra]] · [[addyosmani-agentic-code-quality]] · [[morris-humans-and-agents-in-software-engineering-loops]] · [[macmanus-prs-not-welcome-software-factories]] · [[tornhill-compressed-cognition-cost-of-faster-coding]] · [[willison-more-than-just-code-review]] · [[laycock-maybe-we-shouldnt-be-reviewing-all-this-code]] · [[willison-introducing-wrapture]]._
