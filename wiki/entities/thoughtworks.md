---
title: Thoughtworks
type: entity
created: 2026-06-11
updated: 2026-09-04
sources: [fowler-bockeler-harness-engineering, fowler-bockeler-maintainability-sensors, bockeler-context-engineering-coding-agents, bockeler-tdd-inside-the-agent-loop, martinfowler-prince-building-reliable-agentic-ai-systems, fowler-agentic-programming, sadalage-chandrasekaran-making-data-ready-for-agentic-ai, laycock-citizens-build-agents-execute-experts-govern, morris-humans-and-agents-in-software-engineering-loops, edwards-alexander-an-accidental-blackboard, laycock-the-conductor-developer, laycock-maybe-we-shouldnt-be-reviewing-all-this-code, bockeler-understanding-sdd-kiro-speckit-tessl]
tags: [organization, consultancy, software-engineering, harness-engineering, business-capabilities, focus]
---

# Thoughtworks

Global software consultancy known for thought leadership in software engineering practices
(continuous delivery, microservices, the Technology Radar) and home to [[martin-fowler]]'s widely read
site.

**It is by some distance the most heavily represented organization in this KB** — which is a fact worth
holding onto when reading its material, because it is also the organization that *coined* several of the
concepts the KB tracks and then supplies most of the evidence for them.

> ## ⚠ Say this plainly: martinfowler.com is Thoughtworks' own channel
>
> **martinfowler.com is not a third-party venue. It is Thoughtworks' own publishing channel**, run by its
> Chief Scientist, and the *Exploring Gen AI* series on it is Thoughtworks staff writing about
> Thoughtworks practice. It follows that **none of its authors is independent corroboration for a
> Thoughtworks framing** — [[harness-engineering]] above all, which Thoughtworks coined:
>
> - **[[rachel-laycock]] is Thoughtworks' CTO.** Four captures, all on martinfowler.com. **NOT
>   INDEPENDENT.**
> - **[[birgitta-bockeler]] is a Thoughtworks Distinguished Engineer** and the person who *named* the
>   harness-engineering mental model. Five captures. **NOT INDEPENDENT** — she is a primary for her own
>   trials, never external support for her own employer's vocabulary.
> - **Giles Edwards-Alexander**, author of the accidental-blackboard piece, is a Thoughtworks engineer
>   writing up a Thoughtworks engagement. **NOT INDEPENDENT.**
> - **Kief Morris** likewise (Thoughtworks cloud specialist, *Exploring Gen AI*). **NOT INDEPENDENT.**
> - A **Technology Radar** placement cited by a Thoughtworks author is **self-citation**, not external
>   support.
>
> "A Thoughtworks source agrees" is therefore **not** corroboration for anything on the list below. Any
> page that counts one of these authors as independent support for a Thoughtworks-coined concept is
> wrong and should be corrected against this section. The marker belongs inline at each citation, not
> once at the top of a citing page.

## Who and what the KB holds

| Person | Role | Material |
| --- | --- | --- |
| [[birgitta-bockeler]] | Distinguished Engineer, AI-assisted delivery | Named the [[harness-engineering]] mental model ([[fowler-bockeler-harness-engineering]]); [[fowler-bockeler-maintainability-sensors]]; [[bockeler-context-engineering-coding-agents]]; [[bockeler-tdd-inside-the-agent-loop]]; [[bockeler-understanding-sdd-kiro-speckit-tessl]] (2025-10-15, **sole author** — the origin of the spec-first / spec-anchored / spec-as-source ladder). |
| [[martin-fowler]] | Chief Scientist | [[fowler-agentic-programming]]; martinfowler.com is the **venue** for most of the rest of this table |
| [[pramod-sadalage]] · [[prem-chandrasekaran]] | Distinguished Engineer (data) · Market Tech Director | [[sadalage-chandrasekaran-making-data-ready-for-agentic-ai]] — the capability model, reversibility-as-autonomy-key, "retrieved text informs, it never gates" |
| Sarang Kulkarni et al. | — | [[martinfowler-prince-building-reliable-agentic-ai-systems]] — the Bayer PRINCE production case |
| [[rachel-laycock]] | CTO | [[laycock-citizens-build-agents-execute-experts-govern]] (2026-08-19) — *"Citizens build. Agents execute. Experts govern."*, which she says is about where value is moving, not about roles; judgement, not coding ability, is the scarcity; *"Organisations don't run on code. They run on trust."* Plus [[laycock-the-conductor-developer]] (2026-07-31) and [[laycock-maybe-we-shouldnt-be-reviewing-all-this-code]] (2026-09-02) — **all three on martinfowler.com** |
| Kief Morris | Cloud technology specialist | [[morris-humans-and-agents-in-software-engineering-loops]] (Exploring Gen AI, 2026-03-04) — the out-the-loop / in-the-loop / **on-the-loop** taxonomy and the **agentic flywheel**, four months before the KB's other statements of both |
| Giles Edwards-Alexander | Engineer | [[edwards-alexander-an-accidental-blackboard]] (Exploring Gen AI, 2026-09-02) — ten engineers in Barcelona accidentally reproducing the classic blackboard system via commit-and-rebase discipline plus in-repo plans, with two caveats that are the point: the author is *"not convinced I would be able to reliably prompt our agents into doing it again,"* and the frequent-push discipline **had to be backed off because it overloaded CI, which killed the effect** |

The **Technology Radar** is a Thoughtworks artifact the KB now cites substantively — the HOLD on naive
API-to-MCP conversion ([[model-context-protocol]]) — and has learned to discount as self-citation when a
Thoughtworks author cites it in support of their own position ([[business-capabilities]]).

## The concentration problem

Three of the KB's threads lean on Thoughtworks material, and in two of them the firm is both the
originator of the idea and the main supplier of evidence for it:

- **[[harness-engineering]]** — Thoughtworks named the concept (Böckeler) *and* provides its flagship
  production case (Bayer PRINCE). The PRINCE source page carries the caveat; the pages that cite it
  mostly do not, and [[agent-explainability]] goes further and calls PRINCE "independent corroboration."
  It is not independent of the concept's author's employer. **The KB now holds five *Exploring Gen AI*
  primaries on martinfowler.com by Thoughtworks authors** —
  [[fowler-bockeler-harness-engineering]], [[fowler-bockeler-maintainability-sensors]],
  [[bockeler-tdd-inside-the-agent-loop]], [[morris-humans-and-agents-in-software-engineering-loops]],
  [[edwards-alexander-an-accidental-blackboard]] — which is **the same house arguing for its own term**
  and must not be counted as external corroboration for it. Five sources are not five witnesses.
- **[[business-capabilities]]** — the Sadalage/Chandrasekaran capability model is a genuinely new
  contribution, but its supporting citations are Radar placements.
- **[[spec-driven-development]]** — Böckeler's taxonomy (spec-first / spec-anchored / spec-as-source) is
  the KB's working vocabulary, mostly used without attribution.

- **[[agent-governance]] / the org thread** — added 2026-09-02 with [[rachel-laycock]]'s ingest. Her
  "citizens build, agents execute, experts govern" framing is offered as observation, and the evidence
  behind it is a Thoughtworks event (FOSE) plus conversations with Thoughtworks senior engineers. It
  converges usefully with [[devadoss-cead-capability-aligned-agent-design|CEAD]] — an outside source —
  but it is not itself outside support for anything on this list.

- **[[verification-burden]] / [[attention-bottleneck]] — worse as of 2026-09-04.** Two more
  martinfowler.com-published Laycock pieces landed in this ingest
  ([[laycock-the-conductor-developer]], [[laycock-maybe-we-shouldnt-be-reviewing-all-this-code]]), so
  **three of the KB's named positions on review, attention and governance now come from one company's
  channel and its CTO.** Her two essays also disagree with each other and she never addresses it — see
  her page.

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
[[laycock-citizens-build-agents-execute-experts-govern]] ·
[[bockeler-understanding-sdd-kiro-speckit-tessl]] · [[laycock-the-conductor-developer]] ·
[[laycock-maybe-we-shouldnt-be-reviewing-all-this-code]] ·
[[morris-humans-and-agents-in-software-engineering-loops]] ·
[[edwards-alexander-an-accidental-blackboard]]._
