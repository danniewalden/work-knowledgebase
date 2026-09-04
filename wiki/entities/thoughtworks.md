---
title: Thoughtworks
type: entity
created: 2026-06-11
updated: 2026-09-02
sources: [fowler-bockeler-harness-engineering, fowler-bockeler-maintainability-sensors, bockeler-context-engineering-coding-agents, bockeler-tdd-inside-the-agent-loop, martinfowler-prince-building-reliable-agentic-ai-systems, fowler-agentic-programming, sadalage-chandrasekaran-making-data-ready-for-agentic-ai, laycock-citizens-build-agents-execute-experts-govern]
tags: [organization, consultancy, software-engineering, harness-engineering, business-capabilities, focus]
---

# Thoughtworks

Global software consultancy known for thought leadership in software engineering practices
(continuous delivery, microservices, the Technology Radar) and home to [[martin-fowler]]'s widely read
site.

**It is by some distance the most heavily represented organization in this KB** — which is a fact worth
holding onto when reading its material, because it is also the organization that *coined* several of the
concepts the KB tracks and then supplies most of the evidence for them.

## Who and what the KB holds

| Person | Role | Material |
| --- | --- | --- |
| [[birgitta-bockeler]] | Distinguished Engineer, AI-assisted delivery | Named the [[harness-engineering]] mental model ([[fowler-bockeler-harness-engineering]]); [[fowler-bockeler-maintainability-sensors]]; [[bockeler-context-engineering-coding-agents]]; [[bockeler-tdd-inside-the-agent-loop]]. Her SDD/Kiro analysis is captured in `raw/` awaiting ingest — see her page. |
| [[martin-fowler]] | Chief Scientist | [[fowler-agentic-programming]]; martinfowler.com is the **venue** for most of the rest of this table |
| [[pramod-sadalage]] · [[prem-chandrasekaran]] | Distinguished Engineer (data) · Market Tech Director | [[sadalage-chandrasekaran-making-data-ready-for-agentic-ai]] — the capability model, reversibility-as-autonomy-key, "retrieved text informs, it never gates" |
| Sarang Kulkarni et al. | — | [[martinfowler-prince-building-reliable-agentic-ai-systems]] — the Bayer PRINCE production case |
| [[rachel-laycock]] | CTO | [[laycock-citizens-build-agents-execute-experts-govern]] (2026-08-19) — *"Citizens build. Agents execute. Experts govern."*, which she says is about where value is moving, not about roles; judgement, not coding ability, is the scarcity; *"Organisations don't run on code. They run on trust."* One capture still un-ingested: `raw/articles/laycock-the-conductor-developer.md` (2026-07-31) |
| Kief Morris | Cloud technology specialist | `raw/articles/morris-humans-and-agents-in-software-engineering-loops` (Exploring Gen AI, 2026-03-04), **un-ingested** — Batch F, and it names the out/in/**on**-the-loop taxonomy the KB currently lacks |

The **Technology Radar** is a Thoughtworks artifact the KB now cites substantively — the HOLD on naive
API-to-MCP conversion ([[model-context-protocol]]) — and has learned to discount as self-citation when a
Thoughtworks author cites it in support of their own position ([[business-capabilities]]).

## The concentration problem

Three of the KB's threads lean on Thoughtworks material, and in two of them the firm is both the
originator of the idea and the main supplier of evidence for it:

- **[[harness-engineering]]** — Thoughtworks named the concept (Böckeler) *and* provides its flagship
  production case (Bayer PRINCE). The PRINCE source page carries the caveat; the pages that cite it
  mostly do not, and [[agent-explainability]] goes further and calls PRINCE "independent corroboration."
  It is not independent of the concept's author's employer.
- **[[business-capabilities]]** — the Sadalage/Chandrasekaran capability model is a genuinely new
  contribution, but its supporting citations are Radar placements.
- **[[spec-driven-development]]** — Böckeler's taxonomy (spec-first / spec-anchored / spec-as-source) is
  the KB's working vocabulary, mostly used without attribution.

- **[[agent-governance]] / the org thread** — added 2026-09-02 with [[rachel-laycock]]'s ingest. Her
  "citizens build, agents execute, experts govern" framing is offered as observation, and the evidence
  behind it is a Thoughtworks event (FOSE) plus conversations with Thoughtworks senior engineers. It
  converges usefully with [[devadoss-cead-capability-aligned-agent-design|CEAD]] — an outside source —
  but it is not itself outside support for anything on this list.

None of this makes the material wrong; Böckeler in particular publishes negative results about
Thoughtworks-adjacent enthusiasms ([[bockeler-tdd-inside-the-agent-loop]] finds TDD inside the agent loop
buys no quality at 3–8.5× the tokens). The point is that **"a Thoughtworks source agrees" is weaker
corroboration than the KB has sometimes treated it as**, and pages should say which firm they are quoting.

## Related

[[martin-fowler]] · [[birgitta-bockeler]] · [[pramod-sadalage]] · [[prem-chandrasekaran]] ·
[[rachel-laycock]] · [[harness-engineering]] · [[context-engineering]] · [[business-capabilities]] ·
[[agent-explainability]] · [[agent-governance]] · [[spec-driven-development]] ·
[[model-context-protocol]]

_Sources: [[fowler-bockeler-harness-engineering]] · [[fowler-bockeler-maintainability-sensors]] ·
[[bockeler-context-engineering-coding-agents]] · [[bockeler-tdd-inside-the-agent-loop]] ·
[[martinfowler-prince-building-reliable-agentic-ai-systems]] · [[fowler-agentic-programming]] ·
[[sadalage-chandrasekaran-making-data-ready-for-agentic-ai]] ·
[[laycock-citizens-build-agents-execute-experts-govern]]._
