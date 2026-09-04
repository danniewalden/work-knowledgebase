---
title: "Source: Morris — Humans and Agents in Software Engineering Loops"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [morris-humans-and-agents-in-software-engineering-loops]
raw_file: [raw/articles/morris-humans-and-agents-in-software-engineering-loops.md]
tags: [loop-engineering, harness-engineering, on-the-loop, antecedent, thoughtworks, focus]
---

# Source: Morris — Humans and Agents in Software Engineering Loops

Source: **Kief Morris** (Thoughtworks), *"Humans and Agents in Software Engineering Loops"*,
martinfowler.com — **"Exploring Gen AI"** series, **2026-03-04**. Raw capture:
`raw/articles/morris-humans-and-agents-in-software-engineering-loops.md`.

**Deliberate out-of-window backfill** (published ~5 months before the capture's 14-day lookback), taken
as a gap-filling **antecedent primary**: it names the *out-the-loop / in-the-loop / **on**-the-loop*
taxonomy and **"the agentic flywheel"** four months before
[[addyosmani-own-the-outer-loop|Osmani's "Own the Outer Loop"]] (2026-07) and
[[langchain-the-art-of-loop-engineering|LangChain's hill-climbing loop]] (2026-06), both of which the
wiki already holds. The capture note flags it as an accept/reject call on ingest — **filed, with the
provenance consequence stated below.**

**NOT INDEPENDENT.** Morris is a Thoughtworks employee writing in Thoughtworks' own *Exploring Gen AI*
series on martinfowler.com, and the piece's concluding move is to point at
[[fowler-bockeler-harness-engineering|Harness Engineering]] — a **Thoughtworks-coined concept**, in the
same series. This is not external corroboration for [[harness-engineering]]; it is the same house
arguing for its own term. The same marker applies to the other *Exploring Gen AI* material in this
batch ([[edwards-alexander-an-accidental-blackboard]]) and already in the wiki
([[bockeler-tdd-inside-the-agent-loop]], [[fowler-bockeler-maintainability-sensors]]).

## Summary

Morris splits software work into a **"why loop"** (iterate ideas → working software → outcomes; *"until
the AI uprising comes humans will run this loop because we're the ones who want what it produces"*) and
a **"how loop"** (create, select and use intermediate artefacts — code, tests, tools, infrastructure,
designs, [[adr|ADRs]]). The how loop is itself **multiple nested loops** — outermost specifies and
delivers the software, innermost generates and tests code, middle ones decompose and validate. He then
walks three human positions — **outside**, **in**, and **on** the loop — argues for **on**, and closes
with the **agentic flywheel** (agents improving the harness themselves).

## Key points

- **The three positions, and the single line that distinguishes them.** *"The difference between in the
  loop and on the loop is most visible in what we do when we're not satisfied with what the agent
  produces… The 'in the loop' way is to fix the artefact, whether by directly editing it, or by telling
  the agent to make the correction we want. **The 'on the loop' way is to change the harness that
  produced the artefact so it produces the results we want.**"* This is the cleanest operational test
  for "on the loop" in the KB.
- **Humans outside the loop = the common definition of [[vibe-modeling|vibe coding]]** — and, Morris
  notes pointedly, *"Some interpretations of [[spec-driven-development|Spec Driven Development]] are much
  the same,"* with humans investing effort in writing the desired outcome but not dictating how the LLM
  achieves it. A useful, unflattering adjacency the KB's SDD pages do not make.
- **Why internal quality still matters when no human reads the code.** He grants the strongest form of
  the opposing case (*"It doesn't matter whether a variable name clearly expresses its purpose as long as
  an LLM can figure it out"*), then answers it on **external** grounds: *"a cleanly-designed,
  well-structured codebase has externally important benefits… When LLMs can more quickly understand and
  modify the code they work faster and spiral less. We do care about the time and cost of building the
  systems we need."* Internal quality is instrumental, and the instrument is now the agent — the same
  argument [[borg-tornhill-code-for-machines-not-just-humans]] later measures and
  [[ai-readable-code]] files.
- **Humans in the innermost loop become the bottleneck.** *"Agents can generate code faster than humans
  can manually inspect it. Reports on developer productivity with AI show mixed results, which may be at
  least partly because of humans spending more time specifying and reviewing code than they save by
  getting LLMs to generate it."* Note the hedging — *may be, at least partly* — this is a hypothesis
  about the mixed-results literature, **not a finding**, and no study is named.
- **Shift-left, applied to agents.** The QA-team analogy: as developers writing their own tests beat
  throwing code over the wall, *"Agents produce better code when they can gauge the quality of the code
  they produce themselves rather than relying on us to check it for them."* Note this cuts against the
  batch's dominant maker ≠ checker rule — Morris wants the agent to *have* quality signals, not to *be*
  the arbiter; the harness supplies them.
- **The harness, defined from the loop side.** *"The collection of specifications, quality checks, and
  workflow guidance that control different levels of loops inside the how loop **is** the agent's
  harness. The emerging practice of building and maintaining these harnesses, Harness Engineering, is how
  humans work on the loop."*
- **"On the loop" ≈ "the middle loop."** He notes the same idea was described as the **middle loop** by
  participants of *The Future of Software Development Retreat* — "moving human attention to a
  higher-level loop than the coding loop." A third name for the same relocation.
- **The agentic flywheel.** Humans direct **agents** to manage and improve the harness rather than doing
  it by hand. Build it by feeding the agents signal: start with the tests and evals already in the
  harness; then **pipeline stages that measure performance and validate failure scenarios**; then
  **operational data from production, user journey logs, and commercial results.** For each workflow step
  the agent reviews results and recommends harness improvements — the scope, in his words, *"includes improvements to any of the
  upstream parts of the workflow that could improve those results. What we have now is an agent harness
  that generates recommendations for improving itself."*
- **A staged autonomy path for the flywheel itself** — the KB's earliest statement of it: consider
  recommendations interactively → have agents file recommendations **into the product backlog** to be
  prioritized and picked up → as confidence grows, have agents **score their own recommendations
  including risks, costs and benefits**, and **auto-approve above a score threshold.** That last step is
  exactly the self-modification-with-a-grader problem the KB tracks as the grader leak.
- **He anticipates the objection to his own endpoint.** *"At some point this might look a lot like humans
  out of the loop, old-school vibe coding. I suspect that will be true for standard types of work that
  are done often as the improvement loops reach diminishing returns. But by engineering the harness we
  won't just get one-off, 'good enough' solutions, we'll get robust, maybe even anti-fragile systems that
  continuously improve themselves."* An honest concession that the flywheel's terminus resembles the
  position he argued against.
- **Limits.** An essay with **no data, no case study and no worked example** — five conceptual diagrams
  and an argument. It is a *proposal* for the flywheel, written in the future tense ("we build the
  flywheel by…", "we might then decide that…"), not a report of one running. **NOT INDEPENDENT** (see
  above). The one empirical gesture — mixed AI productivity results possibly explained by review
  overhead — names no study. Its footnote is worth carrying: *"These days 'ralph loop' is often used
  colloquially to mean just firing up a bunch of agents and leaving them to keep looping until
  (hopefully) they finish their task. But as originally described the operator plays an important role
  in steering agents as they ralph"* — a correction to the KB's own [[ralph-loop]] usage.

## Connections / contrast

**This changes the provenance story on two KB pages from "named in July 2026" to "named in March and
independently renamed in July."** [[loop-engineering]] currently dates the inner/outer-loop framing to
[[addyosmani-own-the-outer-loop|Osmani, 2026-07]] and the hill-climbing loop to
[[langchain-the-art-of-loop-engineering|LangChain, 2026-06]]. Morris has **on-the-loop** and the
**agentic flywheel** on **2026-03-04**, with the flywheel's staged-autonomy path spelled out. That is a
materially different claim about how settled this vocabulary is — and it means the June-2026 "coinage"
the page reports is at best the moment the *market* adopted words that already existed. It also
resolves a dangling forward-link from
[[ng-spec-driven-development-is-waterfall-in-markdown]].

**But it contradicts the KB's layering, and that contradiction should stand on the page.** The
[[loop-engineering]] page opens, following Osmani, on *"loop engineering sits one floor above the
harness"* — and now flags that ordering as unresolved. [[wong-loop-engineering-teaching-ai-agents-how-to-think|Wong]] says the same ("a harness
governs one step, a loop governs the campaign"). **Morris inverts it**: the harness is *the thing that
controls the loops*, so harness engineering is not a floor below loop engineering — it **is** the human
work at the loop's boundary. [[breunig-harnesses-are-situated-agents|Breunig]] sits closer to Morris
(the harness is the world; the loop is the small core the developer drives). The five definitional
sources in this batch do not agree: **Morris and Breunig put the harness *above or around* the loop;
Wong puts it below (a rung the loop sits on top of); Voss treats it as an object the system loop
iterates on; and [[miracle-my-loop-engineering-workflow|Miracle]] calls it the *place* the loops run
on.** The KB should record the disagreement rather than pick a winner.

**The flywheel is LangChain's hill-climbing loop and Voss's system loop, four months early.** Compare:
Morris — agent reads results and rewrites the harness, fed by evals then pipeline metrics then
production data; [[langchain-the-art-of-loop-engineering|LangChain]] — analysis agent reads production
traces and rewrites harness config; [[voss-what-the-hell-is-a-loop-anyway|Voss/Gavrilescu]] — outer loop
studies and maintains the primary system, iterating on prompts, harnesses, models *and the evals
themselves*; [[ahe-agentic-harness-engineering|AHE]] — measures it. Morris's contribution to that
lineage is the **signal-enrichment ladder** (evals → pipeline stages → production/commercial data) and
the **auto-approval-above-a-score** step, which is the grader-leak risk stated as a deliberate design
choice rather than a hazard.

**The "how loop / why loop" split maps onto the KB's existing spec thread.** The why loop is
[[addyosmani-human-judgment-relocates|"someone still chooses the problem"]] and the "should this exist"
question; the how loop is where [[spec-driven-development]], [[harness-engineering]] and
[[agentic-coding]] live. His warning that some readings of SDD amount to humans-outside-the-loop is a
direct counterpoint to [[ng-spec-driven-development-is-waterfall-in-markdown|Ng's]] critique from the
other direction, and worth putting next to [[dilger-describing-without-solving-burns-you-out|Dilger's]]
"describing a problem without solving it leaves a hole that keeps growing."

## Links

[[loop-engineering]] · [[harness-engineering]] · [[agent-harness]] · [[software-factory]] ·
[[spec-driven-development]] · [[vibe-modeling]] · [[ralph-loop]] · [[ai-readable-code]] ·
[[comprehension-debt]] · [[agent-observability-and-evals]] · [[feedforward-and-feedback-controls]] ·
[[autonomy-ladder]] · [[adr]] · [[agentic-coding]] · [[thoughtworks]] · [[martin-fowler]] ·
[[fowler-bockeler-harness-engineering]] · [[fowler-bockeler-maintainability-sensors]] ·
[[bockeler-tdd-inside-the-agent-loop]] · [[edwards-alexander-an-accidental-blackboard]] ·
[[addyosmani-own-the-outer-loop]] · [[langchain-the-art-of-loop-engineering]] ·
[[ahe-agentic-harness-engineering]] · [[voss-what-the-hell-is-a-loop-anyway]] ·
[[wong-loop-engineering-teaching-ai-agents-how-to-think]] ·
[[ng-spec-driven-development-is-waterfall-in-markdown]] ·
[[borg-tornhill-code-for-machines-not-just-humans]]

_Source: [[morris-humans-and-agents-in-software-engineering-loops]] (raw: `raw/articles/morris-humans-and-agents-in-software-engineering-loops.md`)._
