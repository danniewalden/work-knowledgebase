---
title: Simon Willison
type: entity
created: 2026-07-06
updated: 2026-09-04
sources: [willison-vibe-engineering, willison-agentic-engineering-patterns, willison-designing-agentic-loops, willison-rewriting-bun-in-rust, willison-directly-responsible-individuals, willison-understand-to-participate, willison-sqlite-utils-4-mostly-written-by-fable, willison-fireside-chat-claude-code-team, willison-more-than-just-code-review, willison-conceptual-integrity-and-counting-lines-of-code, willison-brewster-cannot-review-180000-lines, willison-claudes-new-system-prompt, willison-understanding-chatgpt-work, willison-gpt6-astra, willison-claude-fable-5-1-animated-pelican, willison-codex-bundles-libreoffice, willison-introducing-wrapture]
tags: [person, agentic-coding, coding-agents, loop-engineering, prompt-injection, llm-tooling, watch-list]
---

# Simon Willison

Co-creator of **Django**, creator of **Datasette** and the **`llm`** CLI/Python library, and
the originator of the term **"prompt injection."** One of the most prolific, practical
LLM/AI commentators working today: near-daily long-form posts, blogmarks, quotations, and TILs
at **simonwillison.net** on model releases, tool use, LLM security, and — most relevant to this
KB — **coding agents**.

## Why he's in the KB

He is the one who **coined "vibe engineering"** ([[willison-vibe-engineering]], **2025-10-07**) as the
accountable counterpart to [[vibe-modeling|vibe coding]] — "seasoned professionals accelerate their
work with LLMs while staying proudly and confidently accountable." A dated **2026-02-23 update** on that
same post records the field settling on **"agentic engineering"** instead (he took the new tag and is
"working on a not-quite-a-book"). So the KB's naming trail is **Willison "vibe engineering" (Oct 2025) →
ecosystem "agentic engineering" (Feb 2026)**, the latter now the title of his living guide.

Author of the living guide **[[willison-agentic-engineering-patterns|Agentic Engineering Patterns]]**
(started 2026-02-23, the same week as that update), a practitioner playbook for getting results out of
coding agents (Claude Code, OpenAI Codex, Gemini CLI). He supplies:

- the term **agentic engineering** — a hands-on counterpart to [[martin-fowler]]'s
  "agentic programming" ([[fowler-agentic-programming]]), and the successor to his own "vibe engineering";
- the crisp working definition **"agents run tools in a loop to achieve a goal"** — the plain
  statement of the [[react-loop|tools-in-a-loop]] model under [[loop-engineering]] and the
  [[agent-harness]];
- the framing that **agents don't learn but harnesses do** ("deliberately update our
  instructions and tool harnesses") — [[harness-engineering]] as accumulated context;
- a defence of Karpathy's narrow sense of [[vibe-modeling|vibe coding]] vs reviewed
  [[agentic-coding|agentic engineering]].

He also has **priority on naming loop design**: [[willison-designing-agentic-loops|"Designing agentic
loops"]] (2025-09-30) named the skill nine months before the June-2026 [[loop-engineering]]
crystallization, and adds the **agent-safety** dimension (YOLO mode, sandboxing, [[prompt-injection]] —
a term he coined — tightly scoped credentials) that the later sources under-weight.

His **link-blog** is also a channel for **worked case studies** he curates: 
**[[willison-rewriting-bun-in-rust|"Rewriting Bun in Rust"]]** (2026-07-08) reads Jarred Sumner's
agentic Zig→Rust rewrite of Bun as a real-world stacked-loop instance — a TypeScript test suite (~1M
assertions) acting as a **language-independent conformance suite** (the grader loop), "prompting Claude
to edit the loop," and "fixing the process that generates the code instead of hand-fixing the code" (the
hill-climbing loop), at ≈$165k in tokens. Concrete evidence for the [[loop-engineering]] model he named.
And **[[willison-sqlite-utils-4-mostly-written-by-fable|"sqlite-utils 4.0rc2, mostly written by Claude
Fable"]]** (2026-07-05) is a first-person **maker≠checker** case on his own OSS: the agent reviews its own
release (5 "release blockers," incl. a data-loss bug), then a *different* model (GPT-5.5) reviews Fable's
work and finds 2 more P1 bugs fed into a fresh session — with an itemized **$149.25** cost breakdown, a
rare concrete agentic-coding cost datapoint.

He also weighs in on the **accountability** boundary of the loop:
**[[willison-directly-responsible-individuals|"Directly Responsible Individuals (DRI)"]]** (2026-07-12)
argues an LLM agent should *never* be a project's DRI — accountability is "uniquely human… machines
cannot" — quoting IBM's 1979 "a computer can never be held accountable" slide. The human-ownership
counterpart to [[addyosmani-own-the-outer-loop|Osmani's Answerability]] and the "stay the engineer"
caveat of [[loop-engineering]]. And he amplifies Geoffrey Litt's **"understand to participate"** framing
([[willison-understand-to-participate]], 2026-07-02) — you must understand the code deeply enough to stay
an *active participant* with the model, the guard against cognitive/comprehension debt ([[ai-readable-code]]).

He is a **[[agentic-coding]] / [[loop-engineering]] practitioner voice**, adjacent to the
harness/context-engineering thread — not an [[event-modeling]] voice. Positioned alongside
[[addy-osmani]] and [[swyx]] on the loop/harness side, and Fowler/[[birgitta-bockeler|Böckeler]]
on the conceptual side.

## Verification ≠ review, and the cognitive ceiling (2026-08/09)

Three August–September pieces make him a named voice in the [[verification-burden]] dispute.

**[[willison-more-than-just-code-review]]** (08-22, four sentences) is the pivot the whole dispute turns
on: the key skill is to *"confidently instruct"* an agent and *"confidently verify"* the result, and
*"**Eyeballing every line of code has never been the most effective way to validate a change**."* Note
the claim is about software engineering generally, not about agents — and that he keeps line-by-line
review on the shelf ("sometimes this involves reviewing every line"), which makes it a triage position
rather than an abolition. [[adam-tornhill]] arrives at the same claim six days later, independently:
the batch's strongest convergence. (They split on **lines of code** — see below.)

**[[willison-conceptual-integrity-and-counting-lines-of-code]]** (08-19, from a *Talking Postgres*
transcript) adds two things. A **defence of lines of code** — meaningful only because human output was
hard-capped, and only under his own provisos ("as long as the code is the same quality: maintainable,
tested" and "it takes a huge amount of skill") — and the constraint that matters more: *"the new
limiting factor is **cognitive capacity**… I don't have the cognitive capacity to stay on top of 100
times the amount of code. So you still need a team of engineers, so you can **load balance that
cognitive capacity across the team**."* That is the only remedy in the KB where **team size is itself a
verification instrument** ([[attention-bottleneck]]). The second half is the KB's primary for
**conceptual integrity** (Brooks): with agents, "your software grows little weird bumps in funny
different directions," because the friction that used to enforce discipline — "that would take me a
week — I cannot justify that" — is gone. All his numbers here are practitioner rules of thumb
("50 or 60 lines… 200 is an incredibly good day… a hundred times faster") and must not be promoted to
figures. His LOC defence is met head-on, and unengaged, by
[[tornhill-beyond-lambdas-raising-the-abstraction-level|Tornhill's]] *"lines of code are not a finite
resource"* the same fortnight.

**[[willison-brewster-cannot-review-180000-lines]]** (09-02) is a **quotation post**, and the entry
where his contribution is selection rather than argument: [[rick-brewster]] on ~180,000 agent-written
lines in Paint.NET — *"I cannot possibly review 180,000 lines of code."* Read against his own two
pieces, the pairing is pointed: Brewster is a **team of one** ("a team of one is a very badly designed
team") with no substitute instrument, which is what "there are other ways" looks like when nobody
supplies one.

## The Sept-2026 cluster — five captures, one structural finding

- **[[willison-claudes-new-system-prompt]]** + **[[willison-understanding-chatgpt-work]]** together
  establish the finding, one week apart, for both major vendors: **the harness layer you rent is not
  disclosed, and interrogating the agent about itself is the only available instrument.** Both key claims
  are therefore **MODEL SELF-REPORTS, not documentation** — the unpublished per-feature prompt blocks, and
  the "223 tools / 44 skills" inventory (cite it as *"the agent reported…"*, never as an OpenAI figure).
  His method is worth borrowing: he had **GPT-5.6 Luna**, not Claude, summarize the Claude prompt diffs,
  *"because I don't trust Claude to summarize its own system prompts when there's a risk that material
  from its system prompt might impact its opinions"* — a deliberate
  check-external-to-the-thing-checked choice.
- **[[willison-gpt6-astra]]** carries this batch's best number (ARC-AGI-3, 99.9%/$19K on OpenAI's custom
  "Provider Adapter harness" vs 62.7%/$26K default) *with its caveats attached* — the score is in
  **OpenAI's own launch material (VENDOR SELF-REPORT)** and the harness attribution and costs come from
  ARC Prize, the benchmark maintainer, which is better provenance but **NOT INDEPENDENT** of the
  benchmark's standing — and he notes he **had not used the model**. His handling is the contrast case
  for [[swyx-gpt6-astra-automated-ai-engineer]], which relays the same figure without the harness caveat
  that makes it interesting.
- **[[willison-claude-fable-5-1-animated-pelican]]** supplies the reasoning-effort cost ladder (~33× low to
  max) — kept for [[token-budget-quality-cliff]] — while he himself reports *"losing faith in the pelican
  benchmark"* except for within-family and across-effort comparisons.
- **[[willison-codex-bundles-libreoffice]]** and **[[willison-introducing-wrapture]]** are one-finding
  blogmarks: a harness ships 1.7GB of binaries plus skills that locate them; and Graham Dumpleton's
  design-authority line, *"the AI was the means of producing it rather than the source of the design."*
  The latter is a **SELF-REPORT ABOUT HIS OWN PROCESS, secondhand via Willison** — a usable *definition*,
  **not** evidence that agent-driven authorship works.

## Watch

On the watch-config **people list** (added 2026-07-06). His blog is a **static site and
headless-fetchable** (plain WebFetch works; Atom feed at simonwillison.net/atom/everything/) —
unlike the LinkedIn-gated people, no live Chrome needed for the primary channel. Also followed on
**LinkedIn** (linkedin.com/in/simonw) and **X** ([@simonw](https://x.com/simonw)); both are
login-walled/client-rendered and need a live logged-in Chrome session for a real sweep, but the
blog mirrors most substantive content. Watch for agents / agentic-coding / LLM-tooling material;
flag off-thread model-release commentary.

His interview-as-source **[[willison-fireside-chat-claude-code-team|Fireside Chat with the Claude Code
team]]** (2026-07-21) is an edited+annotated transcript with Cat Wu and Thariq Shihipar ([[anthropic]]) —
notable less for Willison's own argument than for the data points he surfaces: Claude Tag landing 65% of the
team's PRs (**VENDOR SELF-REPORT, relayed** — [[anthropic]]'s own figure about its own product team,
no methodology; the marker travels with it), code review moved off humans over months (with an eval-set
regression guard — a maker≠checker/hill-climbing loop), **markdown-file-per-channel** on-disk memory, and
the frontier-model prompting reversals (examples and "don't-do-X" lists now hurt; the system prompt
shrank ~80%).

_Sources: [[willison-vibe-engineering]], [[willison-agentic-engineering-patterns]], [[willison-designing-agentic-loops]], [[willison-rewriting-bun-in-rust]], [[willison-directly-responsible-individuals]], [[willison-understand-to-participate]], [[willison-sqlite-utils-4-mostly-written-by-fable]], [[willison-fireside-chat-claude-code-team]],
[[willison-more-than-just-code-review]], [[willison-conceptual-integrity-and-counting-lines-of-code]],
[[willison-brewster-cannot-review-180000-lines]], [[willison-claudes-new-system-prompt]],
[[willison-understanding-chatgpt-work]], [[willison-gpt6-astra]],
[[willison-claude-fable-5-1-animated-pelican]], [[willison-codex-bundles-libreoffice]],
[[willison-introducing-wrapture]]._
