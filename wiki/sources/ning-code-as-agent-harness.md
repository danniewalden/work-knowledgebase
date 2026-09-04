---
title: "Source: Code as Agent Harness (Ning et al.) — survey, 42 authors"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [ning-code-as-agent-harness]
raw_file: [raw/papers/ning-code-as-agent-harness.md]
tags: [harness-engineering, agent-harness, survey, academic, agentic-coding, focus]
---

# Source: Code as Agent Harness (Ning et al.)

**Ning, Tieu, Fu, Wei, Li … Tong & He — arXiv:2605.18747, submitted 2026-05-18. 42 authors; affiliations listed as University of Illinois Urbana-Champaign, Meta and Stanford University. arXiv PREPRINT — NOT PEER-REVIEWED; arXiv is not peer review, and that caveat travels with every claim below.** Raw capture: `raw/papers/ning-code-as-agent-harness.md`.

**Correction to a standing KB assumption, recorded here because it changes how this paper is cited: this is a SURVEY, not a method paper.** The watch config had it filed as one of three candidate harness-optimisation *methods*. It is not — it is a five-section, ~50-subsection review with two corresponding authors and 42 contributors, whose contribution is a framing plus a map of other people's work.

## Summary

The **earlier of two independent surveys published 27 days apart** organising the harness literature — this one submitted 2026-05-18, [[guo-survey-question-answering-to-task-completion-harness-design|Guo et al. (arXiv:2606.20683)]] on 2026-06-14, no author overlap. Where Guo et al. cut the field by *model-harness coupling*, Ning et al. cut it by **substrate**: their thesis is that **code has stopped being only the agent's output and become the agent's operating medium**. "In emerging agentic systems, code is no longer only a target output. It increasingly serves as an operational substrate for agent reasoning, acting, environment modeling, and execution-based verification." They name the frame **"code as agent harness"** — "a unified view that centers code as the basis for agent infrastructure" — and organise the survey in three layers: the **harness interface** (code for reasoning / acting / environment), **harness mechanisms** (planning, memory, tool use, feedback-driven control and optimisation), and **scaling the harness** from single- to multi-agent settings "where shared code artifacts support multi-agent coordination, review, and verification".

Its closing move is the one that matters most here: it calls explicitly for a **"science of harness engineering"** (§5.2.7), which is a survey with 42 authors declaring the topic underdeveloped-but-real rather than novel.

## Key points

- **The three-layer frame** (from the abstract, verbatim): harness interface → harness mechanisms → scaling the harness. Applications named: "coding assistants, GUI/OS automation, embodied agents, scientific discovery, personalization and recommendation, DevOps, and enterprise workflows" — i.e. the frame is claimed well beyond [[agentic-coding]].
- **Verification is treated as a first-class harness function, and it is executable.** §3.4 is "Harness Control through the Plan, Execute, and Verify Loop", with subsections on **"Planning as Contract Formation"**, **"Sandboxed Execution and Permissioned State Transition"** and **"Verification through Deterministic Sensors"**. That last heading is, near-verbatim, [[birgitta-bockeler|Böckeler]]'s *computational sensor* from [[feedforward-and-feedback-controls]] — arrived at independently by a different community, which is the kind of convergence this KB exists to notice. "Planning as contract formation" likewise rhymes with [[esaa-event-sourcing-for-autonomous-agents|ESAA]]'s boundary contracts.
- **It contains a subsection-level map of the harness-evolution literature.** §3.5 "Agentic Harness Engineering for Adaptive Harness Optimization" breaks into **3.5.1 Deep Telemetry as the Optimization Substrate · 3.5.2 The Evolution Agent · 3.5.3 Governed Harness Mutation** — which is [[ahe-agentic-harness-engineering|AHE]]'s three observability pillars (experience → agent → governed edits) recognised as a named pattern with its own section in a survey. Independent evidence that the pattern is a research programme, not one lab's prototype.
- **Multi-agent coordination is framed as shared *state*, not shared messages.** §4.3 takes an explicit "Position: The Shared Code-Centric Harness Substrate", with "Shared Harness Representation" and "Harness-State Convergence"; §5.2.4 raises **"Transactional Shared Program State and Semantic Conflict Resolution"** as an open problem. Transactional shared state, ordering and conflict resolution across concurrent agents is precisely the ground [[agentic-event-driven-systems]] and [[event-sourcing]] claim to already own — see Connections.
- **Its open problems double as an agenda for this wiki's harness pages** (§5.2, headings verbatim): harness-level evaluation and **oracle adequacy**; semantic verification beyond executable feedback; **self-evolving harnesses without regression**; transactional shared program state; **"Human-in-the-Loop Safety and Accountability as Harness State"**; multimodal code-harness systems; and "Toward a Science of Harness Engineering". The abstract states the same list as "evaluation beyond final task success, verification under incomplete feedback, regression-free harness improvement, consistent shared state across multiple agents, human oversight for safety-critical actions".
- **"Self-evolving harnesses without regression" is named as an open problem by a survey** — which is the field's own acknowledgement, from inside, that the harness-evolution results are not settled. Set beside [[wang-rethinking-evaluation-of-harness-evolution-for-agents|Wang et al.]]'s negative result and [[ahe-agentic-harness-engineering|AHE]]'s measured *regression blindness*, three independent sources agree the regression problem is unsolved.
- **Roadmap claim:** "a unified roadmap toward **executable, verifiable, and stateful** AI agent systems." Those three adjectives are close to the KB's own [[event-sourced-agentic-patterns]] pitch, reached from the code side.

## Limits

- **PREPRINT, NOT PEER-REVIEWED.** arXiv is not peer review, and that applies to the framing, the taxonomy and the open-problem list alike.
- **Survey = secondary evidence.** No experiment, no measurement, no benchmark of its own. It cannot corroborate any number; it can only tell you a literature exists and how it is shaped.
- **The capture is the abstract plus the heading tree — its map, not its content.** NOT captured: the body prose of all five sections, every figure and table, the per-method summary tables, and the references. The PDF is 7,860 KB and was not retrieved. **No claim about *which* methods the survey covers, how it rates them, or what it concludes about any individual system can be sourced from this capture** — only the structure above and the abstract's own words.
- **Affiliations are unmapped.** The capture records three institutions (UIUC, Meta, Stanford) but states explicitly that the HTML gave no per-author marker it could reproduce, so **no author on this page is attributed to a specific institution**. Note that Meta is an industrial co-author on a survey that frames the field — not a product pitch, but not a purely academic author list either.
- 42 authors on a survey is worth reading as a community-organising artifact (a workshop-scale effort) rather than as 42 independent endorsements of each claim.

## Connections / contrast

- **[[guo-survey-question-answering-to-task-completion-harness-design]]** — the sibling survey, **27 days later**. Two surveys inside a single month, **disjoint author sets**, both existing to organise the same literature: a topic does not attract two surveys unless there is a corpus. This pairing is the load-bearing evidence that [[harness-engineering]] is a field.
- **[[agent-harness]] / [[harness-engineering]]** — supplies the substrate claim (code as the harness's medium) and the "science of harness engineering" framing; also the strongest external support for those pages' treatment of verification as harness machinery rather than QA.
- **[[ahe-agentic-harness-engineering]]** — §3.5's three subsections are AHE's pattern named as a category. Useful as *independent recognition of the pattern*, not as corroboration of AHE's numbers.
- **[[wang-rethinking-evaluation-of-harness-evolution-for-agents]]** — agrees with the critique on substance: "self-evolving harnesses without regression" and "harness-level evaluation and oracle adequacy" are the survey's own open problems.
- **[[event-sourcing]] · [[agentic-event-driven-systems]] · [[event-sourced-agentic-patterns]]** — §5.2.4's "transactional shared program state and semantic conflict resolution" is an open problem for this survey and a **solved-shape** for the event-sourcing tradition (total ordering, append-only log, conflict detection before effects apply — cf. [[esaa-event-sourcing-for-autonomous-agents]]). The most direct research-gap-meets-existing-answer seam this batch surfaces.
- **[[feedforward-and-feedback-controls]]** — "Verification through Deterministic Sensors" is the sensor argument reached independently by an academic group.
- **[[multi-agent-orchestration]]** — §4 is a harness-side treatment of the same problem, with "Optimized Workflow Topology for Agentic Coordination" as a heading.
- **[[agent-governance]] · [[decision-trace]]** — "Human-in-the-Loop Safety and Accountability **as Harness State**" is a governance claim in harness vocabulary: accountability is something the harness *stores*, not something a process document asserts.
- **[[agentic-coding]] · [[ai-readable-code]]** — the code-as-substrate thesis is the strongest academic frame yet for why code legibility is an *agent-infrastructure* concern.

_Source page: [[ning-code-as-agent-harness]]._
