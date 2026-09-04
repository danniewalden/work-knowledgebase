---
title: Rachel Laycock
type: entity
created: 2026-09-02
updated: 2026-09-04
sources: [laycock-citizens-build-agents-execute-experts-govern, laycock-maybe-we-shouldnt-be-reviewing-all-this-code, laycock-the-conductor-developer]
tags: [person, thoughtworks, agent-governance, organization, verification-burden, focus]
---

# Rachel Laycock

**CTO of [[thoughtworks]]**, publishing at martinfowler.com under "Rachel's Ramblings." In this KB she
is the **organisational-governance voice** on agentic software delivery — the rung above the
practitioner and code-level material the wiki mostly holds.

Her contribution here is the framing **"Citizens build. Agents execute. Experts govern."**
([[laycock-citizens-build-agents-execute-experts-govern]], 2026-08-19) — which she explicitly says is
*not* a statement about roles but about **where value is moving**. The argument underneath it:
organisations spent decades optimising around the scarcity of people who could write code, and the real
scarcity now is **engineering judgement** — knowing what good looks like and when something that works
is safe to trust in production. Experienced engineers therefore become *"dramatically more leveraged,"*
shifting from building features to building the environment (guardrails, platforms, practices, feedback
loops) in which others and agents can work safely. Her summary line: *"Organisations don't run on code.
They run on trust."*

She is a **not-independent** source for Thoughtworks-originated concepts — see the marker on her source
page and the concentration problem documented on [[thoughtworks]]. Her material is framing rather than
evidence: tentative by her own description, with no data and one anonymised team.

## Two further essays, and a tension she leaves open (ingested 2026-09-04)

**[[laycock-the-conductor-developer|The Conductor Developer]]** (2026-07-31) is the individual-role view
beside the organisational one, and it opens with a **prediction she records as failed**: she expected
the bottleneck to march down the lifecycle (coding → design → architecture → verification) and reports
*"I was wrong."* Instead: **"AI didn't change what great software looks like. It changed what's scarce.
Human attention is now the bottleneck."** The developer becomes a conductor — *"someone has to hold the
whole system in their head"* — and the analogy's constraint is that a conductor is first a musician.
Its real payload is a career claim: eight parallel work streams "sounded like my job," what she had to
learn as CTO was **energy management, not time management**, and *"we're redesigning the tools, but we
haven't started redesigning the job."* Her 8 / 10 / 12 parallel-agent figures are **hearsay** (one
unnamed engineer, plus "similar numbers from others") and must not be cited as a capacity finding. See
[[attention-bottleneck]], where her "widen the span" answer sits against
[[adam-tornhill|Tornhill's]] flat refusal of human-side parallelism.

**[[laycock-maybe-we-shouldnt-be-reviewing-all-this-code|Maybe We Shouldn't Be Reviewing All This Code]]**
(2026-09-02) is her sharpest and most consequential piece here — a named position in the KB's
[[verification-burden]] dispute, written as a response to Brian Houck (DX) after they disagreed on a
panel. She grants that AI outpaces review and that review carries knowledge transfer, mentoring,
ownership and architectural understanding — then asks *"why are we waiting until code review to do all
of those things?"* Each function moves earlier (pairing, mob programming, team design sessions,
[[fitness-functions]] for architectural constraints, automation for anything deterministic), leaving
**review by exception**. Two lines to keep: *"I don't think the answer is an AI agent pretending to be
the human reviewer so we can preserve exactly the same process at higher speed. That's automating the
ceremony rather than questioning why the ceremony exists"* — which lands squarely on
[[osmani-agentic-code-review-skill-five-axes|Osmani's shipped review skill]] and on Anthropic's own
practice recorded in [[loop-engineering]] — and **"We need engineers to understand systems, not
diffs."**

**The tension between her own two essays is unresolved and worth holding:** attention is the scarce
resource (July), and the remedy is pairing, mobbing and team design sessions (September) — practices
that spend *more* human attention per unit of code. She never addresses it. Her two relayed figures
(Meta LOC per human-landed diff **+106%**; median PR size **+64%**) come via **Houck at DX, a vendor
selling developer-productivity measurement**, the first double-relayed and hedged "reportedly" by her;
neither is a KB-grade number, and Houck's own piece is not in `raw/` — the KB holds one side of that
exchange. Her "ten times the code" is rhetorical, not a figure.

**All three captures are on martinfowler.com** — [[thoughtworks]]' own channel, and she is its CTO.
**NOT INDEPENDENT**, and this ingest makes the concentration worse rather than better: see the
concentration section on [[thoughtworks]].

## Related

[[thoughtworks]] · [[martin-fowler]] · [[birgitta-bockeler]] · [[agent-governance]] ·
[[business-capabilities]] · [[software-factory]] · [[unattended-coding-agents]] ·
[[verification-burden]] · [[attention-bottleneck]] · [[fitness-functions]] · [[comprehension-debt]]

_Source pages: [[laycock-citizens-build-agents-execute-experts-govern]] ·
[[laycock-the-conductor-developer]] · [[laycock-maybe-we-shouldnt-be-reviewing-all-this-code]]._
