---
title: "Source: Breunig — Harnesses are Situated Agents"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [breunig-harnesses-are-situated-agents]
raw_file: [raw/articles/breunig-harnesses-are-situated-agents.md]
tags: [harness-engineering, agent-harness, definition, harness-census, focus]
---

# Source: Breunig — Harnesses are Situated Agents

Source: **Drew Breunig**, *"Harnesses are Situated Agents"*, dbreunig.com, **2026-08-14**. Raw capture:
`raw/articles/breunig-harnesses-are-situated-agents.md`. Surfaced via
[[simon-willison|Simon Willison's]] 2026-08-23 quotation of its companion piece
([[breunig-fable-and-the-end-of-the-free-lunch]]). A **candidate definitional primary for
[[agent-harness]]**, alongside [[fowler-bockeler-harness-engineering|Böckeler's guides/sensors]] framing.
The cited companion **"Overfitting the Harness" (2026-05-10) is not yet captured.**

## Summary

*"The best way to define a harness is as a 'situated agent.'"* Breunig keeps Harrison Chase's four
elements of an agent — **system prompt, planning tool, file system, subagents** — as **the core loop the
developer controls with the keyboard**, and defines the **harness as everything beyond it: the world the
developer sits within.** He then enumerates that world as **eight layers fanning outward**, ordered by a
single organising rule: *"As we move outward, each layer is used by more people and changed less
often."* The essay closes on a business prediction — harness lock-in will look like SaaS lock-in, not
like model lock-in.

## Key points

- **The eight layers, outward from the agent.** (1) **Session** — the current task and context, "as both
  a trajectory and a durable, branchable log. You can zoom backwards, fork, and replay it." (2)
  **Environment** — the instance: sandbox, terminal, worktree, computer, container. (3) **Repo** — the
  project: code, history, current work, `AGENTS.md`, guides, hooks, versioned in Git. (4) **Memory** —
  "the person's predilections, accrued over time, managing progress and past decisions." (5) **Skills**
  — the domain: reusable workflows or domain knowledge "worth wielding in this situation." (6) **Team**
  — colleagues: shared rooms, shared traces, project tracking, issues, bug reports. (7)
  **Organization** — "the policies and audits, defined by legal, leadership, and procurement." (8)
  **Model** — the LLMs, "the common artifact shared by all. Stochastic blobs we all poke trying to evoke
  positive outcomes. Log or train on their quirks and adjust."
- **What a harness does, in one line.** *"Harnesses account for the above layers, fanning out from the
  agent, to determine what ends up in the context, how the loop runs, and what gets saved."*
- **The Aug-2026 harness census** (worth dating, because it will age): **Omnigent** (Databricks) — a
  *meta-harness* that calls out to Claude Code, Codex, Pi and others; **DeepSeek Harness** (with
  DeepSeek V4-Pro) — "totally modular. Models, tools, skills, sessions, sandboxes, storage, loops,
  scheduling, and the UI are all swappable"; **Buzz** (Block) — "because it's Jack Dorsey it's a Nostr
  social network for agents and humans"; **QM** (Y Combinator) — **org-shaped scoping**, where "each
  employee, Slack room, and project gets its own memory, files, credentials, permissions, schedules, and
  sandboxed execution"; **Flue** (Cloudflare) — a declarative pattern that **"hides the loop from
  users"**; **Muse Code** (Meta) — whose model, Muse Spark 1.2, was **co-trained with the harness
  itself**. Plus OpenClaw, NanoClaw, Hermes, Conductor, Prime Agent.
- **The convergence claim.** *"We've seen enough at this point that the common patterns are starting to
  emerge. Each brings something unique, but **they're more alike than different**."* Innovation is
  happening **per layer**: multiplayer agent environments (Buzz's channels, Claude Tag) at the Team
  layer; Omnigent's **policies** pushing organizational requirements down into what *can* happen in a
  session; Meta training the model to know its harness.
- **Model-harness co-training is more common than the literature shows.** On Muse Spark being co-trained
  with its harness: *"much like others, they just don't write about it…"* — a pointed aside implying the
  practice is widespread and undisclosed. This matters for any benchmark that claims to isolate harness
  quality from model strength.
- **The stickiness thesis, and it is a business argument.** *"The burst of harness innovation, I believe,
  isn't going to slow because managing these layers is **much stickier** than less-situated agents. It's
  trivial to jump from Claude Code to Codex when one tires of Opus's writing, but if the entire org and
  team have already **set up** a system that manages all of the above, it's really hard to shift."* And
  the punchline: *"It's going to be funny if the network effects the AI labs have been searching for end
  up looking just like the network effects of the SaaS era. Coding harnesses, managing the environments
  **around** the agent, look a whole lot like the SaaS platforms of old."* With a nod to Cursor and
  Copilot — "nodding right now, welcoming us all, wondering what took so long."
- **Limits.** A short opinion post (~730 words) with **no measurement**; the eight-layer model is a
  proposed taxonomy, not a validated one, and Breunig offers no test that would distinguish it from
  Chase's four elements plus "everything else." The census is a **list of launch announcements**, mostly
  from vendor blogs, at most weeks old at time of writing — several of these products may not survive,
  and none is evaluated. The stickiness/lock-in claim is a **prediction**, unfalsified. The cited
  companion piece that would support the co-training aside ("Overfitting the Harness," 2026-05-10) is
  **not in `raw/`**, so that claim cannot be followed from this capture. Breunig is an independent writer
  with no product in this space, which is the source's main virtue.

## Connections / contrast

**This is the KB's strongest candidate for restructuring [[agent-harness]]**, which before this source
was one of the thinnest concept pages (a components list plus architecture patterns) and could not carry
this material. Breunig's eight layers subsume the KB's existing primitive list and add three the page has
no place for: **Team**, **Organization**, and **Model**. The **ordering rule** — outward = more people,
less change — is the genuinely new idea, because it converts a flat inventory into a **rate-of-change
gradient**, which is exactly what you need to decide where a policy belongs. Compare
[[langchain-anatomy-of-an-agent-harness]] and [[firecrawl-what-is-an-agent-harness]], both of which stop
at the Repo layer.

**It contests the KB's loop/harness ordering.** [[loop-engineering]] opens on loop engineering sitting
"one floor above the harness" (an ordering it now records as unresolved). Breunig puts the **loop inside**, as the small core the developer drives,
and the harness *around* it — the same inversion [[morris-humans-and-agents-in-software-engineering-loops|Morris]]
makes from the Thoughtworks side. The hardest evidence for that reading in this capture is
**Cloudflare's Flue, which "hides the loop from users."** If the loop can be abstracted away as an
implementation detail of a declarative harness, then "loop engineering" is a claim about *current*
tooling maturity rather than a permanent discipline. See
[[macmanus-schott-react-for-agents-flue-meta-harness]], where Flue's author states the corollary
directly: **"There is no agent without a harness."**

**The Organization layer is the missing rung in the KB's governance thread.** Omnigent's policies —
"manage what *can* happen in a given session, pushing down an organization's requirements" — is
[[agent-governance]] implemented at the harness level rather than as a wrapper, and it is the mechanism
[[deloitte-ai-agents-scaling-faster-than-guardrails]] says is absent. QM's per-employee/per-room/
per-project scoping of memory, credentials, permissions and sandboxes is the same idea applied to
[[prompt-injection]] blast radius, and rhymes with [[prefect-loops-vs-graphs|Lowin's]] per-node
capability scoping and [[addyosmani-human-judgment-relocates|Vercel's]] sandboxes-holding-only-the-
secrets-a-task-needs.

**The Session layer as "a durable, branchable log… zoom backwards, fork, and replay"** is
[[event-sourcing]] described without the word, and lands squarely on the KB's
[[event-sourced-agentic-patterns]] and [[esaa-event-sourcing-for-autonomous-agents]] thread — an
independent, non-event-sourcing author converging on append-only-log-with-replay as the right shape for
agent state.

**Model-harness co-training undercuts a class of measurement.** The KB cites
[[ahe-agentic-harness-engineering|AHE]] (a preprint) for holding the base model frozen while evolving
the harness, and the batch plan flags Evo-Bench as designed to "isolate harness improvements from base
model strength." If frontier models are routinely co-trained with a harness and vendors don't disclose
it, that isolation is harder than those papers assume. Worth carrying as an open question rather than a
refutation — Breunig offers no evidence for the aside.

## Links

[[agent-harness]] · [[harness-engineering]] · [[loop-engineering]] · [[context-engineering]] ·
[[agent-governance]] · [[prompt-injection]] · [[event-sourcing]] · [[event-sourced-agentic-patterns]] ·
[[long-running-agents]] · [[graph-engineering]] · [[multi-agent-orchestration]] ·
[[agent-observability-and-evals]] · [[decision-trace]] · [[simon-willison]] · [[anthropic]] ·
[[langchain]] · [[breunig-fable-and-the-end-of-the-free-lunch]] ·
[[breunig-who-taught-the-models-to-do-that]] ·
[[macmanus-schott-react-for-agents-flue-meta-harness]] ·
[[morris-humans-and-agents-in-software-engineering-loops]] ·
[[voss-what-the-hell-is-a-loop-anyway]] · [[langchain-anatomy-of-an-agent-harness]] ·
[[firecrawl-what-is-an-agent-harness]] · [[fowler-bockeler-harness-engineering]] ·
[[ahe-agentic-harness-engineering]] · [[deloitte-ai-agents-scaling-faster-than-guardrails]]

_Source: [[breunig-harnesses-are-situated-agents]] (raw: `raw/articles/breunig-harnesses-are-situated-agents.md`)._
