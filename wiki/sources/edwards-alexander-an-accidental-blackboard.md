---
title: "Source: Edwards-Alexander — An Accidental Blackboard"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [edwards-alexander-an-accidental-blackboard]
raw_file: [raw/articles/edwards-alexander-an-accidental-blackboard.md]
tags: [multi-agent-orchestration, blackboard-system, loop-engineering, harness-engineering, thoughtworks, focus]
---

# Source: Edwards-Alexander — An Accidental Blackboard

Source: **Giles Edwards-Alexander** (CTO for Europe, Middle East and India, **Thoughtworks**),
*"An Accidental Blackboard"*, martinfowler.com — **"Exploring Gen AI"** series, **2026-09-02**. Raw
capture: `raw/articles/edwards-alexander-an-accidental-blackboard.md`.

**NOT INDEPENDENT.** Thoughtworks reporting on a Thoughtworks internal exercise, published on
Thoughtworks' own channel in Thoughtworks' own series — the same provenance as
[[morris-humans-and-agents-in-software-engineering-loops]] and
[[bockeler-tdd-inside-the-agent-loop]]. It is not external corroboration for anything the KB files
under [[harness-engineering]] (a Thoughtworks-coined term).

**Read the two caveats before the finding.** The author says he is *"not convinced I would be able to
reliably prompt our agents into doing it again,"* and the frequent-push discipline that produced the
effect **had to be backed off because it overloaded CI — which killed the effect.** A page that reports
the blackboard emergence without both of those is reporting the wrong thing.

## Summary

Ten Thoughtworks engineers, one room in Barcelona, four days, one monorepo, a goal they call
**"hyper-agentic"**: build an airline **IROps** system (the flight-control-centre system that decides
which flights to cancel, which aircraft to swap, which passengers get offloaded — "hundreds of aircraft,
hundreds of thousands of passengers"). They built one in four days, *"but this post isn't about how we
did that."* It is about what happened by accident: **a build-hygiene rule plus in-repo plans caused the
agents to start coordinating through the repository — reproducing, unintentionally, the classic
blackboard system** (Hearsay-II, 1980; formalised as tuple spaces by Gelernter et al., 1986).

## Key points

- **The mechanism, precisely.** With many agents in one repo, build pipelines suffered. The fix was a
  discipline: **agents must continually commit and rebase from main** — initially *rebase after commit,
  then push, with all build checks in place*. Independently, agents had been directed to **plan, scope
  work to numbered sections of the shared spec, and store those plans in the repo**, updating them with
  progress as they worked. The commit discipline swept those plan updates along with everything else.
  **Result: agents could see other agents' progress.** Nobody designed this.
- **What coordination actually looked like.** One agent on the **evaluator** (does a proposed recovery
  plan break hard or soft constraints?), another on the **search algorithm** that looks for plans —
  search depends on evaluator, via a shared interface. Both plans recorded the integration point: one
  said *"at this point I'm going to need to update the callers to call the real verifier"*; the other
  *"at this point I need to insert the call to the real verifier when it arrives."* Then: *"One agent
  would mark a line of the plan as in progress, the other agent would see that and not work on that
  line. When the first agent finished, the other agent would see not only that the work was complete and
  thus it was released to proceed, but would also be directly delivered **notes on how the line had been
  implemented**."* Claim/release **and** knowledge transfer, through commits.
- **They then exploited it deliberately.** *"We'd kick off a session and direct it to work on a
  particular journey… Knowing that someone else had been working on the cost model and pushing commits
  continually, we directed the agent working on the verifier to look at plans and source, monitor the
  repo, and **when the work for the cost model lands start to integrate it. And it did.**"*
- **The pattern has a name, and a 1980s lineage.** A **blackboard / tuple space** is *"a shared memory
  that autonomous agents can read and write from independently. They read and write tuples with a
  certain minimum structure, and then as many extra fields as you want: **no schema.**"* Effective for
  *"coordinating autonomous problem solvers towards a single goal. They can each solve a decomposed part
  of the problem, drop their solution into the shared space, **label it**, and other autonomous searchers
  will find it, pick it up, and use it as part of their work."* The author's own university thesis used
  the pattern for directing agent behaviour with hierarchical sensors.
- **CAVEAT 1 — reproducibility is unestablished, by the author.** *"But it was an accident. It wasn't an
  intentional act. It wasn't fully structured. **It was missing some of the key parts of how blackboards
  operate.** And because it was accidental, **I'm not convinced I would be able to reliably prompt our
  agents into doing it again.** I've got a pretty good idea what we did, because we did some analysis and
  identified the single prompt that caused this cascade to start happening. **But it was an emergent
  behaviour. It wasn't a directed behaviour.**"*
- **CAVEAT 2 — the mechanism was withdrawn, and the effect died with it.** *"While we created it by
  directing a frequent push cycle, **we backed-off from that. The frequent commits were overloading our
  CI pipeline.** We switched to only push when a more coherent chunk of change was complete. **This
  deprived the agents of the continuous flow of updates on progress.**"* The coordination substrate and
  the CI budget are in direct conflict, and CI won. This is the most useful engineering fact in the
  piece.
- **His own conclusion is that the channel must not be source control.** *"As well as creating this
  intentionally, rather than accidentally, **I believe you want this communication channel to be sitting
  independently of source control.**"* He is building **Talwrn** (Welsh for a threshing pit — "an area or
  space where arguments and conflict get worked out"), aimed at being *"a blackboard for agentic
  engineering… a very simple to use tool that drops straight into your project."* First milestone:
  Talwrn supporting its own development. **Nothing about Talwrn is evidence yet.**
- **Limits.** n=1, four days, a **practice exercise with a specification and a *simulated* airline**, not
  a client system — so nothing here speaks to production constraints, real data, or maintenance. Ten
  engineers in one room means the human coordination channel was also wide open; no attempt is made to
  separate agent coordination from engineers-talking-to-each-other. **No measurement of any kind**: no
  throughput figure, no defect count, no comparison against a non-blackboard arm, no count of how often
  the claim/release behaviour actually fired versus collided. "We managed to build one in four days" is
  the only outcome claim and is explicitly not the subject of the post. The "single prompt that caused
  the cascade" was identified but **is not published**. Plus both caveats above, and
  **NOT INDEPENDENT**.

## Connections / contrast

**A coordination substrate the KB's [[multi-agent-orchestration]] page does not have.** That page
carries protocol- and topology-level material ([[agent2agent-protocol]], orchestrator/worker patterns,
[[devadoss-cead-capability-aligned-agent-design|capability-aligned decomposition]]) and
[[graph-engineering|graphs]] as explicit control flow. A **blackboard is neither** — it is
*schema-less shared memory with labelled deposits and no routing at all*, where coordination is an
emergent consequence of everyone reading the same space. That is a third structural option, with a
1980-1986 literature behind it (Hearsay-II; Gelernter's tuple spaces), and it is the option the KB was
missing. It is also the direct answer to
[[wong-graph-engineering-wiring-agents-into-an-organization|Wong's]] shared-state failure mode
("everyone re-derives the same context… nodes drift apart"): make the artifact itself authoritative and
there is nothing to drift from.

**The strongest rhyme in the KB is with [[event-sourcing]], and it is worth stating carefully.** Git
history *is* an append-only log; the plans are projections over it; agents subscribe by reading. That is
the shape [[esaa-event-sourcing-for-autonomous-agents|ESAA]] argues for deliberately (append-only
intentions + deterministic projections) and [[akka-event-sourcing-backbone-agentic-ai]] and
[[event-sourced-agentic-patterns]] file as the reliable substrate for nondeterministic agents. **The
difference is decisive, though:** ESAA's log is *designed* — total ordering, contracts, hash-verified
projections — and this one was an accident whose author says it was *"missing some of the key parts of
how blackboards operate."* Edwards-Alexander's conclusion that the channel should live **outside source
control** is, in KB terms, an argument for a purpose-built event store instead of a repo — which is
exactly what the event-sourcing thread has been claiming. Treat this as a **naive-implementation
datapoint that motivates the designed version**, not as corroboration that repos are good event stores.

**The CI-overload finding is the transferable one.** [[tornhill-merge-conflicts-agentic-bottleneck]]
already establishes integration as the agentic bottleneck; this adds that **the fix for integration
(commit early and often) is itself capacity-bounded**, and that the capacity that binds is CI, not the
repo. Any KB claim that "frequent integration solves multi-agent collision" now has a named cost. It
also gives [[addyosmani-code-agent-orchestra|Osmani's]] "one file, one owner" rule a competitor:
ownership-by-partition avoids the CI load that ownership-by-continuous-integration incurs.

**It is a case of [[breunig-who-taught-the-models-to-do-that|designed capability showing through]], not
of spontaneous invention.** Breunig's argument — labs deliberately trained models to persist, write
plans down, and coordinate — predicts that a repo full of in-progress plans is the obvious surface for
those trained behaviours to land on. Read together, the two sources reframe the finding: the
*capability* was engineered by the labs; what was accidental was the **affordance** Thoughtworks
happened to build for it. That reading also makes the reproducibility caveat a **harness problem** —
which is the author's own conclusion.

**Contrast with [[dilger-highlighting-markers-give-context-to-agents]] and
[[dilger-planning-like-excel-legible-to-human-and-ai]]:** Dilger's thread argues for *deliberately
legible in-repo artifacts* as the agent's coordination and context surface. This is that thesis
arriving by accident, at a different firm, with the numbered spec sections doing the addressing work —
and then failing for an operational reason Dilger's material doesn't cover.

## Links

[[multi-agent-orchestration]] · [[loop-engineering]] · [[harness-engineering]] · [[graph-engineering]] ·
[[event-sourcing]] · [[event-sourced-agentic-patterns]] · [[agent-readable-model-artifacts]] ·
[[agent-legibility]] · [[locality-of-reference]] · [[software-factory]] · [[llm-wiki]] ·
[[spec-driven-development]] · [[agent2agent-protocol]] · [[thoughtworks]] · [[martin-fowler]] ·
[[morris-humans-and-agents-in-software-engineering-loops]] · [[bockeler-tdd-inside-the-agent-loop]] ·
[[wong-graph-engineering-wiring-agents-into-an-organization]] ·
[[breunig-who-taught-the-models-to-do-that]] · [[esaa-event-sourcing-for-autonomous-agents]] ·
[[akka-event-sourcing-backbone-agentic-ai]] · [[tornhill-merge-conflicts-agentic-bottleneck]] ·
[[dilger-highlighting-markers-give-context-to-agents]] ·
[[dilger-planning-like-excel-legible-to-human-and-ai]] · [[addyosmani-code-agent-orchestra]]

_Source: [[edwards-alexander-an-accidental-blackboard]] (raw: `raw/articles/edwards-alexander-an-accidental-blackboard.md`)._
