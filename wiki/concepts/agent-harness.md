---
title: Agent Harness
type: concept
created: 2026-06-11
updated: 2026-09-04
sources: [langchain-anatomy-of-an-agent-harness, firecrawl-what-is-an-agent-harness, anthropic-effective-harnesses-long-running-agents, ahe-agentic-harness-engineering, guo-survey-question-answering-to-task-completion-harness-design, ning-code-as-agent-harness, mcateer-evolution-of-the-agent-harness, wang-rethinking-evaluation-of-harness-evolution-for-agents, breunig-harnesses-are-situated-agents, macmanus-schott-react-for-agents-flue-meta-harness, breunig-fable-and-the-end-of-the-free-lunch, willison-gpt6-astra, fowler-fragments-2026-09-01, willison-codex-bundles-libreoffice, willison-claudes-new-system-prompt, willison-understanding-chatgpt-work]
tags: [harness-engineering, agent-harness, primitives, architecture]
---

# Agent Harness

**Agent = Model + Harness.** "If you're not the model, you're the harness"
([[langchain-anatomy-of-an-agent-harness]]). The harness is every piece of code, configuration,
and execution logic that isn't the model itself — the software infrastructure that turns a
stateless text generator into a capable [[agentic-ai|agent]]. The model supplies intelligence;
the harness makes that intelligence useful. *Building and improving the harness* is
[[harness-engineering]].

## Why it's needed

Out of the box, models take data in and emit text; they can't keep durable state across sessions,
execute code, fetch realtime knowledge, or set up environments. These are **harness-level
features**. Without one, long-running agents fail predictably — see [[context-rot]], hallucinated
tool calls, and lost state on failure ([[firecrawl-what-is-an-agent-harness]]).

## Core components / primitives

- **System prompts; tools, Skills, MCPs** ([[model-context-protocol]]) and their descriptions.
- **Bundled infrastructure:** filesystem (the most foundational primitive — workspace, offload,
  cross-session persistence, collaboration surface; git adds versioning), sandbox, browser.
- **Bash + code execution** as a general-purpose tool ("give the model a computer").
- **Memory & search:** context-injection memory files (AGENTS.md), web search for post-cutoff knowledge.
- **Context management:** compaction, tool-call offloading, Skills via progressive disclosure.
- **Retained reasoning state across requests.** Preserving the model's own (often opaque) reasoning state
  between calls so it *reuses* prior work instead of reconstructing it. Named as one of the two mechanisms
  in OpenAI's Provider Adapter harness ([[willison-gpt6-astra]]) and, one generation earlier, in
  [[mcateer-evolution-of-the-agent-harness]]. **Both are OpenAI self-reports.**
- **Supervision of the trajectory** (as distinct from execution). A second process watching for
  **stagnation and repeated unproductive cycles** and redirecting strategy, while the main agent keeps
  deciding what to inspect and change — NVIDIA's AVO, via [[fowler-fragments-2026-09-01]]; **NVIDIA's own
  self-report, relayed secondhand.** Compare the test-run supervisor in
  [[miller-pondering-continuous-integration-ai-world-order]] and the loop-termination rules on
  [[loop-engineering]]: three independent supervisors, three different things being supervised.
- **A bundled operating environment.** Not a metaphor: the Codex/ChatGPT desktop runtime ships **1.7GB**
  of Python, Node, Poppler, git and **headless LibreOffice**, *plus skills that tell the agent where those
  binaries are and how to use them* ([[willison-codex-bundles-libreoffice]]). Document-format capability
  here is environment, not model ability — a useful corrective whenever capability is attributed to a
  model by default.
- **Orchestration logic:** subagent spawning, handoffs, model routing ([[multi-agent-orchestration]]).
- **Hooks/middleware:** deterministic checks, continuation ([[ralph-loop]]), verification.

A research framework makes this list concrete and editable: [[ahe-agentic-harness-engineering|AHE (Lin et
al. 2026)]]'s NexAU substrate enumerates **seven orthogonal, file-level component types** — system prompt,
tool description, tool implementation, middleware, skill, sub-agent configuration, and long-term memory —
deliberately decoupled so each is independently editable and revertible. Its ablation finds the reliability
gain concentrated in **tools, middleware, and long-term memory**, with the system prompt alone *regressing*
— evidence that "the harness" is not prompt-shaped and that these components carry transferable engineering
experience the model leans on more the weaker it is. *(An arXiv **preprint**, not peer-reviewed, and its
headline gain is contested — see [[harness-evolution]].)*

## A harness is a "situated agent" — eight layers ([[breunig-harnesses-are-situated-agents|Breunig, 2026-08-14]])

The KB's strongest definitional framing for this page since Böckeler's guides/sensors. Breunig keeps
Harrison Chase's four elements of an agent — **system prompt, planning tool, file system, subagents** — as
*"the core loop the developer controls with the keyboard,"* and defines the **harness as everything
beyond it: "the world the developer sits within."* Zoom out from one agent at the keys and the harness
manages:

1. **Session** — the current task and context, *"as both a trajectory and a durable, branchable log. You
   can zoom backwards, fork, and replay it."*
2. **Environment** — the instance: sandbox, terminal, worktree, computer, container.
3. **Repo** — the project: code, history, current work, `AGENTS.md`, guides, hooks, versioned in Git.
4. **Memory** — *"the person's predilections, accrued over time, managing progress and past decisions."*
5. **Skills** — the domain: reusable workflows or domain knowledge *"worth wielding in this situation."*
6. **Team** — colleagues: shared rooms, shared traces, project tracking, issues, bug reports.
7. **Organization** — *"the policies and audits, defined by legal, leadership, and procurement."*
8. **Model** — the LLMs, *"the common artifact shared by all."*

**The ordering rule is the genuinely new idea:** *"As we move outward, each layer is used by more people
and changed less often."* That converts a flat inventory into a **rate-of-change gradient**, which is what
you need in order to decide *where a given policy belongs*. Compare
[[langchain-anatomy-of-an-agent-harness]] and [[firecrawl-what-is-an-agent-harness]], both of which stop
at the Repo layer — the KB had no place for Team, Organization or Model before this.

**What a harness does, in one line:** *"Harnesses account for the above layers, fanning out from the
agent, to determine what ends up in the context, how the loop runs, and what gets saved."*

**The Aug-2026 census, worth dating because it will age fast:** **Omnigent** (Databricks) — a
*meta-harness* calling out to Claude Code, Codex, Pi and others; **DeepSeek Harness** — *"totally
modular: models, tools, skills, sessions, sandboxes, storage, loops, scheduling, and the UI are all
swappable"*; **Buzz** (Block) — a Nostr social network for agents and humans; **QM** (Y Combinator) —
**org-shaped scoping**, where *"each employee, Slack room, and project gets its own memory, files,
credentials, permissions, schedules, and sandboxed execution"*; **Flue** (Cloudflare) — declarative, and
it **hides the loop from users**; **Muse Code** (Meta) — model **co-trained with the harness itself**;
plus OpenClaw, NanoClaw, Hermes, Conductor, Prime Agent. Breunig's read: *"they're more alike than
different,"* with innovation happening **per layer**.

**Two consequences the KB should carry.** (1) **Stickiness.** *"It's trivial to jump from Claude Code to
Codex… but if the entire org and team have already set up a system that manages all of the above, it's
really hard to shift… It's going to be funny if the network effects the AI labs have been searching for
end up looking just like the network effects of the SaaS era."* (2) **Model-harness co-training may be
routine and undisclosed** — on Meta training Muse Spark to know its harness, *"much like others, they just
don't write about it…"* If true, that complicates every benchmark claiming to isolate harness quality
from base-model strength, including [[ahe-agentic-harness-engineering|AHE]]'s frozen-model design. An
unevidenced aside; carry it as an open question, not a refutation.

*(Limits: a ~870-word opinion post, no measurement; the census is a list of launch announcements, mostly
from vendor blogs, none evaluated; the lock-in claim is an unfalsified prediction. The cited companion
"Overfitting the Harness" (2026-05-10) is **not in `raw/`**, so the co-training aside cannot be followed
from this capture.)*

## "There is no agent without a harness" ([[macmanus-schott-react-for-agents-flue-meta-harness|Schott, 2026-08-15]])

The strongest statement of harness-primacy in the KB, from someone who bet a product on it. Fred Schott
(creator of Astro; Cloudflare) on **Flue**: *"Our early bet was that **the harness is actually not a
feature, but it's fundamental to what you think an agent is. There is no agent without a harness.**"*
And its corollary: *"Instead of you and your code driving the LLM and telling it what to do with scripts,
**you're putting the agent into this harness, and it is able to drive itself and work through
problems**."*

- **Two generations of agent framework, distinguished by whether the harness was designed in.** The
  *"OG agent frameworks"* — Vercel's AI SDK, Cloudflare's own Agents SDK, Mastra — *"weren't created with
  a harness as the central concept"* and are adding harnesses now as **a feature**; Flue and Vercel's
  **eve** both have them built in. *(A vendor's competitive characterisation of competitors, not an
  audited one.)*
- **Flue is an opinionated take on Pi, an open source minimal harness** — the relation Vite has to Astro:
  *"it doesn't do too much, but it gives the right APIs."* A useful two-tier split for this page:
  **minimal harness** vs **opinionated framework over it.**
- **"Meta-harness" is not yet a defined term**, per someone selling in the category: *"there's confusion
  about what the term meta-harness even means at this early stage."* Schott declines a
  one-API-across-all-harnesses design because *"the framework and the harness are very intertwined."*
- **Hooks: a mechanism for the dynamic capability this page only asserts.** An agent is a JavaScript
  function that *"re-renders on every turn"*; 16 built-in hooks including `useSkill()`, `useTool()`,
  `useSubagent()` *"attach different resources and capabilities dynamically to enhance themselves at
  runtime."* His motivating example is a **security** pattern: a support agent *"might bring in an
  account management tool **after first verifying a user**"* — capability scoping **by lifecycle stage**,
  which is [[prefect-loops-vs-graphs|Lowin's]] per-node scoping ("don't hand your agent a bazooka")
  implemented *inside* one agent instead of across graph nodes.
- **A design lesson worth generalising:** *"file based magic is an antipattern."* Flue 1 ported
  file-based routing from web frameworks and it failed, because the unit turned out to be different —
  *"for a lot of people building with Flue, especially the bigger customers, **their whole company is one
  agent**. They don't care about routing."* A caution for every borrowed abstraction in this space,
  including React's, which Schott is now borrowing.
- **Period marker.** Bret Taylor (Sierra CEO, OpenAI chairman), quoted in the same piece: *"We're sort of
  in the **jQuery era of agents**, not the react era."*

*(Vendor launch interview: no benchmark, no adoption figures, no independent user reports. Flue 2 is its
first stable release; the whole framework census is date-bound to Aug 2026.)*

## What the harness is *responsible for* — six coupled runtime duties (Guo et al. 2026)

The primitive list above says what a harness *contains*. [[guo-survey-question-answering-to-task-completion-harness-design|Guo
et al. (arXiv:2606.20683)]] decompose what it must *do*, in a survey whose organising question is "where does
the bottleneck in agent performance reside, in the foundation model, in the execution harness, or in the
coupling between them?" Their answer is the coupling: an agent is "a foundation model **coupled with** an
execution harness", and agent quality "emerges from the interaction between model capability, runtime
infrastructure, task structure, and evaluation design." *(arXiv preprint — not peer-reviewed.)* The six
responsibilities, verbatim:

| Responsibility | What it does |
| --- | --- |
| **Observation interface** | "transforms raw environment signals into model-usable observations" |
| **Context manager** | "determines what information enters the model context, when and in form" ([[context-engineering]]) |
| **Control loop** | "orchestrates the observe-reason-act-feedback cycle" ([[react-loop]], [[loop-engineering]]) |
| **Action interface** | "maps model outputs to executable operations" ([[model-context-protocol]]) |
| **State and artifact store** | "persists execution state and products" ([[long-running-agents]], [[decision-trace]]) |
| **Verification and governance layer** | "checks, constrains, and repairs execution" ([[feedforward-and-feedback-controls]], [[agent-governance]]) |

Read this as **orthogonal to, not competing with**, [[ahe-agentic-harness-engineering|AHE]]'s seven editable
component files above: Guo et al. name *what the harness must do*, AHE names *what you can edit*. Holding both
is more useful than choosing. The survey's own emphasis is on the word **coupled** — it devotes a subsection to
cross-layer interactions, which is the same non-additivity AHE measured empirically.

**The four-paradigm ladder** the same survey draws puts this page in sequence: **prompt engineering → workflows
and context engineering → harness engineering → agent-native training and co-evolution.** The rung boundaries
are crisply stated: prompting "addresses an expression problem"; context engineering "remains fundamentally
**feedforward**"; **harness engineering "closes the loop"** — "the model acts, observes environment responses,
and reasons over observations to decide its next step"; and paradigm 4 is "**internalization**; agentic
behaviors are increasingly trained into model parameters", plus co-evolution. That last rung is the academic
form of [[harness-absorption]]. *(Preprint.)* [[graph-engineering-era-of-llm-agents-system-intelligence|Feng et
al.]] independently name the same first three rungs but a different fourth ([[loop-engineering]]) and a fifth
([[graph-engineering]]) — see [[harness-engineering]] for both ladders.

## The harness is not a fixed surface — it gets absorbed ([[harness-absorption]])

[[mcateer-evolution-of-the-agent-harness|McAteer (Latent.Space, 2026-08-22)]] argues the harness and the model
improve on **two curves** — "what the harness asks of the model, and what the model can deliver in practice" —
whose gap *is* agent effectiveness, and that the 2025-26 jump in agent usefulness was the two curves crossing
rather than either one leaping. The consequence is a loop: **train → absorb → shed → repeat.** Models trained
inside their harness absorb harness capabilities into their weights (his cleanest instance: the
GPT-5.1-Codex-Max launch line, "The first model natively trained to operate across multiple context windows
through compaction" — auto-compaction migrating out of harness code into weights), after which the harness can
delete the scaffold. His metric follows: **"the measure of the pace of agent harness evolution is how much of
the harness you get to delete, while retaining the same capability level."** *(Practitioner essay, not a
paper.)*

Two things to hold with it. First, **the KB holds the opposite trend claim too**: [[langchain]]'s Harrison
Chase argues better models *expand* what harnesses must do rather than shrinking them (Claude Code 512k+ LOC
and growing — [[langchain-anatomy-of-an-agent-harness]]). Both can be true (prompt shrinks, codebase grows),
and the wiki should not pick. Second, **his numbers are all secondhand and must carry that marker**: the
much-quoted **Harness-Bench** spread — same model, 106 tasks, different harnesses, **52.4 → 76.2, a 23.8-point
spread with zero model change**, glossed "half the agent is the harness" — appears in the capture with no
author, venue or link, and **no primary capture of Harness-Bench exists in this KB**; the ARC-AGI-3 tripling
(GPT-5.6 Sol, 13.3% → 38.3% from retained reasoning + compaction) is [[openai]]'s own result about its own
model (**vendor self-report**, also relayed) — now traceable to a named harness one generation on, see
*Harness leverage* below; the "deleted 80% of Claude Code's system prompt" claim is
[[anthropic]]'s about its own product, and is at least corroborated first-hand in
[[willison-fireside-chat-claude-code-team]] (per frontier model, not globally). Where he predicts the harness
**inverts** into an interface to scarce human attention, see [[attention-interface]].

## Architecture patterns ([[firecrawl-what-is-an-agent-harness]])

Single-agent supervisor · **initializer-executor split** (see [[long-running-agents]]) ·
multi-agent coordination.

## Harness leverage, on one public benchmark, from two labs (Sept 2026)

The clearest quantitative support for *agent = model + harness* arrived within two days of itself, on
**ARC-AGI-3** (released March 2026), from two different vendors — and **both are vendor self-reports about
their own harnesses**, so read them as a convergence rather than as measurement.

- **[[openai]] / GPT-6 Astra** ([[willison-gpt6-astra]], 2026-09-03): **99.9% for $19K using OpenAI's
  custom "Provider Adapter harness"**, while **the default ARC-AGI harness scored 62.7% for $26K** — a
  **37.2-point spread on the same benchmark with the same model, and the better score cost less.** The
  harness, per the ARC-AGI blog, *"preserves opaque reasoning state between requests and uses compaction
  for longer conversations, allowing the model to reuse prior work."* **Marker: the 99.9% is in OpenAI's
  own launch material (VENDOR SELF-REPORT); the harness attribution and the dollar figures are reported by
  ARC Prize, the benchmark maintainer, which is better provenance but NOT INDEPENDENT of the benchmark's
  standing. Claude Fable 5 has no published ARC-AGI-3 result, so this is not a model-vs-model comparison.**
- **NVIDIA / AVO** (relayed by [[martin-fowler]] in [[fowler-fragments-2026-09-01]], 2026-09-01):
  **100% on ARC-AGI-3** using **Claude Opus 5 plus a harness called AVO**, whose two named mechanisms are
  *"persistent memory and supervision"* — memory that carries forward implementations, evaluation results,
  compiler and profiler output *"allowing the agent to resume from the current state rather than repeatedly
  reconstructing the search"*, and a supervisor that *"monitors the broader trajectory for stagnation or
  repeated unproductive cycles and can redirect the main agent toward alternative strategies."* The same
  harness had previously run a GPU kernel-optimization task for **seven days**. **Marker: VENDOR
  SELF-REPORT (NVIDIA on its own harness) and secondhand — Fowler relaying; the NVIDIA post is not in
  `raw/`, and no methodology, cost or replication is available.**

**What the pair is worth.** Two labs, two base models, two different sets of harness mechanisms, one
benchmark, both reporting large gains attributable to the harness alone. That is the best available
evidence for this page's thesis and it is still entirely vendor-supplied — **a convergence, not independent
confirmation.** It also **upgrades a claim the KB previously held as folklore**:
[[mcateer-evolution-of-the-agent-harness]] carried, secondhand and
unlinked, that *"GPT-5.6 Sol's ARC-AGI-3 score tripled from 13.3% to 38.3%"* by "adding only retained
reasoning and compaction" — the *same two mechanisms* the Provider Adapter harness names, now with a named
harness, a linked benchmark-maintainer post, and costs. Traceable, not independent.

**And note what is now conspicuously missing.** The KB's most-quoted harness number — Harness-Bench's
**23.8-point spread over 106 tasks with zero change to the model** — still has no author, venue, link or
primary capture, and must be marked **secondhand at every use**. Finding it remains the highest-value
follow-up for this page.

## The harness you rent is not the harness you can read

Two Willison captures from the same week establish this for both major vendors, and it changes how any of
the components above can be *verified* in a product you did not build:

- **[[anthropic]]** publishes consumer system prompts with full revision history (Willison diffs them in
  [`simonw/claude-system-prompts`](https://github.com/simonw/claude-system-prompts)) — but **not** for
  Claude Code or Cowork, and, per the model's own account, the published core prompt is followed by
  *"feature- and tool-specific blocks that get added depending on what's enabled for the session"* which
  *"aren't part of the published core prompt"* ([[willison-claudes-new-system-prompt]]). **That claim is a
  MODEL SELF-REPORT, not documentation.**
- **[[openai]]** publishes neither prompts nor tool descriptions, so Willison had to get a ChatGPT Work
  session to inventory **its own** tools and skills — the agent reported **223 registered tools and 44
  skills** ([[willison-understanding-chatgpt-work]]). **Also a model self-report.** His diagnosis: *"If the
  ChatGPT Work documentation included the exact system prompt and tool descriptions used by the agent I
  wouldn't have needed to write this post."*

**The asymmetry to keep in mind:** harness legibility is high for the layer you build (repo artifacts,
linters, skills — see [[openai-harness-engineering-codex]], [[hashimoto-my-ai-adoption-journey]]) and low
for the layer you rent, where the only available instrument is asking the agent about itself. Every
component list on this page is therefore *verifiable* for your own harness and *hearsay* for a vendor's.

## Not the same as…

- **Framework** = libraries/abstractions for building agents (LangChain, LlamaIndex).
- **Harness** = the runtime that *executes* agents with tools, memory, state.
- **Orchestrator** = the control flow deciding when/how to call the model.

LangChain's DeepAgents is a harness built on the LangChain framework. The [[claude-agent-sdk]] is
described as a general-purpose agent harness. Note the **model↔harness co-evolution**: products are
post-trained with their harness in the loop, so the best harness for a task isn't necessarily the
one a model shipped with ([[langchain-anatomy-of-an-agent-harness]]) — and per
[[breunig-harnesses-are-situated-agents|Breunig]] that co-training may be routine and undisclosed, which
would complicate any benchmark claiming to isolate harness quality from base-model strength.

## The substrate claim: code, not prose ([[ning-code-as-agent-harness]])

A 42-author survey ([[ning-code-as-agent-harness|Ning et al., arXiv:2605.18747]] — **preprint, not
peer-reviewed**) frames the harness by its medium: "code is no longer only a target output. It increasingly
serves as an **operational substrate** for agent reasoning, acting, environment modeling, and execution-based
verification." Three layers — harness *interface* (code for reasoning / acting / environment modelling),
harness *mechanisms* (planning, memory, tool use, feedback-driven control), and *scaling* the harness to
multi-agent settings "where shared code artifacts support multi-agent coordination, review, and verification."
Its §3.4 headings land almost verbatim on this KB's vocabulary — "**Planning as Contract Formation**",
"Sandboxed Execution and Permissioned State Transition", "**Verification through Deterministic Sensors**"
(cf. [[feedforward-and-feedback-controls]], [[esaa-event-sourcing-for-autonomous-agents]]) — reached by a
different community. It closes by calling for a "**science of harness engineering**", i.e. a large survey
declaring the topic real and underdeveloped rather than new. Being a survey, it corroborates *no number*.

## Related

[[token-budget-quality-cliff]] · [[harness-engineering]] · [[harness-evolution]] ·
[[harness-absorption]] · [[attention-interface]] · [[loop-engineering]] · [[context-engineering]] ·
[[breunig-harnesses-are-situated-agents]] ·
[[macmanus-schott-react-for-agents-flue-meta-harness]] · [[breunig-fable-and-the-end-of-the-free-lunch]]

_Sources: [[langchain-anatomy-of-an-agent-harness]] · [[firecrawl-what-is-an-agent-harness]] · [[anthropic-effective-harnesses-long-running-agents]] · [[ahe-agentic-harness-engineering]] · [[guo-survey-question-answering-to-task-completion-harness-design]] · [[ning-code-as-agent-harness]] · [[mcateer-evolution-of-the-agent-harness]] · [[breunig-harnesses-are-situated-agents]] · [[macmanus-schott-react-for-agents-flue-meta-harness]] · [[willison-gpt6-astra]] · [[fowler-fragments-2026-09-01]] · [[willison-codex-bundles-libreoffice]] · [[willison-claudes-new-system-prompt]] · [[willison-understanding-chatgpt-work]]._
