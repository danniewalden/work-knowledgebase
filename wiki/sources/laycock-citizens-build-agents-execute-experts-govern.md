---
title: "Rachel Laycock — Citizens Build, Agents Execute, Experts Govern"
type: source
created: 2026-09-02
updated: 2026-09-02
sources: [laycock-citizens-build-agents-execute-experts-govern]
raw_file: [raw/articles/laycock-citizens-build-agents-execute-experts-govern.md]
tags: [agent-governance, business-capabilities, software-engineering, organization, thoughtworks, focus]
---

# Rachel Laycock — Citizens Build, Agents Execute, Experts Govern

Essay by **[[rachel-laycock]]**, CTO of [[thoughtworks]], on martinfowler.com ("Rachel's Ramblings"),
**2026-08-19**. Raw capture: `raw/articles/laycock-citizens-build-agents-execute-experts-govern.md`.
Subtitled *"Why building an app over the weekend isn't the same as building enterprise software."*

## Summary

The essay opens on a recurring conversation: a non-technical executive has built something real over a
weekend — a chatbot, an internal workflow, sometimes a polished app solving an actual business problem —
and asks *"If AI can do this now, why aren't our engineering teams delivering ten times faster?"*

Laycock takes the question seriously and locates the fault on her own side of the table: *"we did this to
ourselves. We've spent so many years banging on about how to write good software that everyone has
assumed writing software is the same as software engineering."* She is careful not to diminish the
weekend app — one of the most exciting things AI has done is increase the number of people who can turn
ideas into working software, and she connects it to her own first "hello world."

What changes is not the artifact but the moment a business depends on it, and the change is a set of
questions that never come up in a demo: is customer data protected, what happens when a dependency
fails, can someone else understand this in two years, will it survive an audit, can it cope with a
thousand times more users — *"Those questions don't show up in a demo or in the build phase at all
unless an experienced engineer is in the room. I certainly wasn't asking them when I was building my
first apps. I only cared about features!"*

**The scarcity argument** is the load-bearing move. We spent decades optimising around people who could
write code, because they were scarce and expensive — *"I'm not convinced that was ever the real
scarcity."* What is scarce now is **good engineering judgement**: knowing what good looks like,
understanding the risks, and knowing when something that works is safe to trust in production. Hence:
*"Organisations don't run on code. They run on trust."*

**The slogan, and her own correction to it.** She first said *"Citizens build. Agents execute. Experts
govern."* almost without thinking, wrote it down because it sounded good, then left it alone — and on
reflection decided it is **not about roles**: *"At first I thought I was talking about roles… But I
don't actually think that's what I meant. I think I was talking about where value is moving."* AI gives
everyone a new way to express ideas; execution shifts to agents; neither reduces the need for expertise.
Experienced engineers become *"dramatically more leveraged"* — their job shifts from building every
feature to *"creating the environment in which thousands of features can be built safely by other
people and by agents"*: guardrails, platforms, practices, feedback loops.

She names one antipattern explicitly and defers it: *"I do not mean people build stuff and throw it to
engineers to fix, that is a total antipattern for another ramble."*

**The FOSE observation.** At an event she refers to only as **FOSE** — the raw links it to
martinfowler.com's *FutureOfSoftwareDevelopment* bliki page and does not expand the acronym or say whose
event it is — they spent little time on coding and most on design, architecture, governance, learning
and judgement. One team described
designing a specification during the day, letting agents work overnight, and reviewing in the morning —
and her interest is pointedly *not* the pipeline: *"The interesting bit for me wasn't the overnight
pipeline, cool as that was. It was what the humans were doing: deciding what good looked like, making
trade-offs and judging whether what came back was actually what they wanted."* Her stated conclusion
from the room: when agents can generate lots of code quickly, **good design matters more, not less**.

She closes on why executives and engineers sound like they are describing different futures: the
executive sees that anyone can build software, the engineer sees that somebody still has to live with
it — *"Both are right."*

## Interested-party note

**Not independent.** Laycock is [[thoughtworks]]' CTO publishing on martinfowler.com, and the evidence
she offers is *"senior engineers at Thoughtworks"* she tested the idea on, plus one anonymised team at
an event. (The capture does **not** say FOSE is a Thoughtworks event; that it is one is outside
knowledge, so the engineers line is the part of the non-independence case this source actually carries.)
Per this wiki's vendor-claim convention this is **not** external corroboration for Thoughtworks-originated
framings — including the capability model in
[[sadalage-chandrasekaran-making-data-ready-for-agentic-ai]] — and the marker travels with any claim
quoted onto another page. It is also worth naming what kind of source this is: an explicitly tentative
essay ("I don't know whether I believe something until I've let it bounce around in my head"), with no
data, no case detail, and one anonymised team. Read as a well-positioned practitioner's framing, not as
evidence.

## In the KB

- **The org rung of [[business-capabilities]].** That page holds the capability idea at the data-
  architecture level (Sadalage/Chandrasekaran) and, via [[autonomous-domain-capabilities]], at the code
  level. Laycock supplies the organisational one — who is permitted to build what, and who carries the
  judgement — without using the word "capability" at all.
- **A governance claim that inverts the usual direction.** [[agent-governance]] holds
  [[devadoss-cead-capability-aligned-agent-design|CEAD's]] finding that governance cannot substitute for
  design. Laycock arrives at the same place from the people side: the expert's leverage *is* the
  environment — guardrails, platforms, feedback loops — not the review gate.
- **A description of the overnight-agent loop from the enterprise-governance side**, where
  [[unattended-coding-agents]] and [[spec-driven-development]] mostly hold practitioner accounts — and
  notable for treating the human judgement, not the pipeline, as the interesting part. (Not
  *independent* in this wiki's sense — see the marker above.)
- **"Judgement is the scarcity" belongs next to the verification tax.** [[agent-governance]] carries
  DORA's finding that cost has shifted to governance and verification; this is the same claim in labour
  terms. The un-ingested Osmani capture
  (`raw/articles/addyosmani-human-judgment-relocates.md`, "human judgment doesn't leave the software
  factory, it relocates") is the closest thing in `raw/` to a second voice on it — worth reading
  together, and flagged here so the pairing is not lost.
- **[[software-factory]] gets an owner for the guardrails.** That page describes the factory; this
  supplies the role that builds and vouches for it.

## Links

Entities: [[rachel-laycock]] · [[thoughtworks]] · [[martin-fowler]]. Concepts: [[agent-governance]] ·
[[business-capabilities]] · [[software-factory]] · [[unattended-coding-agents]] · [[autonomy-ladder]] ·
[[agentic-coding]] · [[comprehension-debt]] · [[conways-law]] · [[team-topologies]]. Related:
[[sadalage-chandrasekaran-making-data-ready-for-agentic-ai]] ·
[[devadoss-cead-capability-aligned-agent-design]] · [[fowler-agentic-programming]].
