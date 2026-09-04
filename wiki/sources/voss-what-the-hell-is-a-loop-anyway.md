---
title: "Source: Voss — What the Hell Is a Loop, Anyway?"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [voss-what-the-hell-is-a-loop-anyway]
raw_file: [raw/articles/voss-what-the-hell-is-a-loop-anyway.md]
tags: [loop-engineering, vocabulary, disambiguation, software-factory, agentic-coding, focus]
---

# Source: Voss — What the Hell Is a Loop, Anyway?

Source: **Laurie Voss**, *"What the Hell Is a Loop, Anyway?"*, O'Reilly Radar (originally LinkedIn,
republished with permission), **2026-07-29**. Raw capture:
`raw/articles/voss-what-the-hell-is-a-loop-anyway.md`. The KB's first **disambiguation** primary for
[[loop-engineering]] — written specifically because "the people talking about loops aren't all
discussing the same thing."

## Summary

Voss maps **at least four distinct architectures hiding behind the single word "loop,"** and argues
they differ on the three things that matter: **what they iterate on, what ends them, and where the
human sits.** He then names a fifth, the **oversight loop**, which swyx's own diagram left labelled
"???? loop." His organising claim is not that loops are hype but that the word is overloaded: *"A loop
without feedback is just a `for` statement."* Written explicitly from "the peak of the hype cycle," in
the week the term dominated the AI Engineer World's Fair main stage.

## Key points

- **Execution loop** — the agent's own act-observe-decide cycle. Iterates on **steps within one task**;
  ends on **environment feedback** (test output, API response, file contents) *or* whenever the agent
  decides it's done, "whether or not it actually is." Humans appear at the boundaries. This is the
  innermost loop you can engineer; swyx's token loop below it is "just part of the model" —
  **nobody designs the token loop.**
- **Task loop** — Geoffrey Huntley's [[ralph-loop|Ralph loop]]: restart the agent against the same
  spec, **fresh context window every iteration, one task per loop.** Iterates on **a single artifact**;
  ends on **spec compliance + passing tests**. "The apparent waste is the point" — refeeding the spec
  prevents the [[context-rot]] and compaction that degrade long sessions. Human writes the spec, judges
  doneness, and — Huntley's own framing — **watches for failure patterns and fixes them so they never
  recur** ("a locomotive engineer, someone whose whole job is keeping the train on the rails").
- **Product loop — the [[software-factory]].** Iterates on **a codebase and its backlog, continuously**;
  its stop signals come from **outside the codebase entirely** (new issues, production logs, user
  feedback, review outcomes). Tereza Tizkova (Factory): a software factory is "the whole loop, the whole
  lifecycle of developing software with autonomy." Zach Lloyd (Warp) enumerates that lifecycle: **triage,
  specification, implementation, review, verification, shipping, monitoring** — "software engineering
  becomes factory engineering." **The human role becomes configurable**: you choose which lifecycle
  stages to automate and where humans get pulled in.
- **System loop — "autoresearch"** (Roland Gavrilescu, Introspection). The inner loop does user-facing
  work; **the outer loop studies and maintains the primary system**, iterating on prompts, harnesses,
  model choices, **and the evals themselves**. "The loop is the product." Its stop signal is the most
  demanding of the four — evals, judges, filtered product feedback, plus an explicit **ask-a-human
  tool** through which the agent accrues tacit knowledge "the way a new employee does." This is the same
  rung the KB files as the **hill-climbing loop**.
- **The oversight loop — the ring Voss names.** In swyx's diagram the outermost ring is literally
  "???? loop," verbs *set goals, allocate, cull*, exit condition *none*. Voss names it the **oversight
  loop** and says it is "the one ring where a human should live." Quoting Osmani from the AIEWF stage:
  **"That inner loop is capability. The outer loop is agency."**
- **What is deliberately excluded.** Cognition's **Devin Security Swarm** ("Agentic MapReduce" —
  fan parallel bounded agents across a repo, aggregate findings) is *not* a loop: "dispatch, gather,
  validate is a pipeline: nothing feeds back into a next cycle, and a loop without feedback is just a
  `for` statement." **Fan-out is a topology you can deploy inside any of the four loops.** This is the
  sharpest available criterion for what makes something a loop at all.
- **Autonomy is a dial that exists separately on every loop.** "You can run a fully autonomous execution
  loop inside a heavily supervised product loop. You can hand the system loop to agents while keeping
  goal-setting entirely human." So the real engineering question is not which camp wins but *"what
  information do you need to set each dial correctly?"*
- **The disagreements are all about who runs the top ring.** Turn-it-up camp: Lloyd and Gavrilescu
  (ratchet autonomy as trust accrues; Gavrilescu's memorable distinction — **"build orchestras before
  factories,"** an orchestra being a system that keeps a human conductor). Hard-stop camp: Geoffrey Litt
  (Notion) called factories "a depressing vision" and argues **"those who delegate understanding get
  replaced by the agent"**; Paul Bakaus — **"There is no auto, and there will be no auto,"** an
  *ownership* argument, not only a quality one. [[dex-horthy|Dex Horthy]] (HumanLayer) takes a third
  position: not anti-loop (**"Kubernetes is built on control loops, but deterministic ones"**), rather
  that enthusiasm has outrun the engineering — his advice was **step *down* an abstraction level, not up.**
- **Numbers appearing here are relayed vendor self-reports, not measurements.** Warp "ratcheting the
  automatic PR merge rate upward from 20 percent toward 60"; Anthropic saying **65% of its product
  team's code** is created by its internal Claude Tag. Both are **VENDOR SELF-REPORT**, reported
  second-hand; neither is audited or independently replicated, and the Warp figure is a stated *target
  path*, not an achieved result.
- **The most honest datapoint in the piece is a negative one.** Mike Krieger (Anthropic) reports that
  even inside Anthropic **the Claude Tag team is bottlenecked on reviews and on human ability to
  conceptualize what the system is doing.** Voss: "The checkpoint humans kept for themselves is now the
  constraint." **IMPRESSION NOT MEASUREMENT**, but it is a vendor conceding against interest.
- **Limits.** An opinion/mapping essay by a single author, built from conference talks, podcast
  interviews and X posts rather than study data — the taxonomy is a proposal, not a measured
  classification, and Voss says so ("this post is an attempt to map out what everyone means"). The two
  key diagrams and **the four-loops comparison table are images on the original page and were not
  transcribed into the capture**, so the table's cell-level content is unavailable here and is
  reconstructed above only from the surrounding prose. The closing paragraph is a **vendor plug for
  Arize AX** (the author's sponsor/employer context) — the "sweep traces and cluster failures
  continuously" prescription arrives attached to a product. Every named figure is second-hand.

## Connections / contrast

**This is the source that shows [[loop-engineering]] does not yet have one taxonomy — it has three
incompatible ones.** The KB page carries LangChain's four-loop stack (agent / verification /
event-driven / hill-climbing) and had cross-mapped Anthropic's four loop *types* (turn-based /
goal-based / time-based / proactive) onto it as "near-exact." Voss's four (execution / task / product / system, plus
oversight) **do not line up with either**: his *task loop* (Ralph) has no LangChain counterpart;
LangChain's *verification loop* is not one of his four at all (for Voss verification is an *exit
condition* of every loop, not a loop of its own); and he classifies the [[software-factory]] **as a
loop** (the product loop) where the KB files it as the rung *above* loops. Three fourfold taxonomies
that disagree about the members is the KB's clearest evidence that the vocabulary is unsettled —
see the deltas proposal for a side-by-side section rather than a merged "consensus."

**The feedback criterion is a genuine contribution.** "A loop without feedback is just a `for`
statement" gives the KB a test it lacked, and Voss applies it to exclude a famous pattern
(Agentic MapReduce). It is the same test [[miracle-my-loop-engineering-workflow|Miracle]] states from
the other end — "feedback that doesn't refine the next objective is just logging… that is what makes it
a loop and not a pipeline" — two independent authors converging on *refinement of the next iteration*
as the defining property. Useful against [[agentic-workflow-patterns]], where several patterns are
pipelines.

**Against [[wong-loop-engineering-teaching-ai-agents-how-to-think|Wong]]:** Wong defines a loop as
**"a task plus a check"** — one agent's campaign toward one goal, one rung in a
context→harness→loop→graph ladder. Voss's unit is an *architecture class*, and he explicitly denies
there is one loop to engineer. They are not reconcilable as stated.

**Against [[breunig-harnesses-are-situated-agents|Breunig]]:** Breunig makes the loop the *small* thing
(the four Chase elements the developer drives from the keyboard) and the harness the interesting one
(eight surrounding layers) — and notes Cloudflare's Flue **hides the loop from users entirely.** If the
loop can be hidden, "loop engineering" as *the* discipline is a claim about tooling maturity, not a
permanent layer.

**Confirms and dates existing KB claims.** The June-2026 provenance the [[loop-engineering]] page
already carries (Steinberger 2026-06-07, Cherny, Osmani 2026-06-07, swyx's Loopcraft 2026-06-12,
LangChain 2026-06-16) is corroborated here by an outside observer with dates, and extended: the AI
Engineer World's Fair closed **2026-07-02** with an hour-long debate on whether loop hype has outrun
practice. Voss's oversight loop is the same boundary [[addyosmani-own-the-outer-loop|Osmani's outer
loop]] and [[willison-directly-responsible-individuals|Willison's DRI]] argument stake out; Litt's
"delegate understanding and get replaced" is [[comprehension-debt]] stated as a career risk. Horthy's
"step down an abstraction level" is the strongest counterweight in the batch to
[[khononov-microservices-hype-to-ai-sloop|Khononov's]] hype-cycle read — same skepticism, opposite
prescription.

## Links

[[loop-engineering]] · [[ralph-loop]] · [[software-factory]] · [[graph-engineering]] ·
[[agent-harness]] · [[harness-engineering]] · [[context-rot]] · [[comprehension-debt]] ·
[[unattended-coding-agents]] · [[long-running-agents]] · [[agent-observability-and-evals]] ·
[[agentic-workflow-patterns]] · [[autonomy-ladder]] · [[swyx]] · [[addy-osmani]] · [[dex-horthy]] ·
[[anthropic]] · [[addyosmani-own-the-outer-loop]] · [[swyx-loopcraft-art-of-stacking-loops]] ·
[[langchain-the-art-of-loop-engineering]] · [[anthropic-getting-started-with-loops]] ·
[[khononov-microservices-hype-to-ai-sloop]] · [[wong-loop-engineering-teaching-ai-agents-how-to-think]] ·
[[miracle-my-loop-engineering-workflow]] · [[breunig-harnesses-are-situated-agents]]

_Source: [[voss-what-the-hell-is-a-loop-anyway]] (raw: `raw/articles/voss-what-the-hell-is-a-loop-anyway.md`)._
