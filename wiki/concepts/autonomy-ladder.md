---
title: Autonomy Ladder
type: concept
created: 2026-06-11
updated: 2026-09-04
sources: [svitla-agentic-ai-market-trends-2026, anthropic-building-effective-agents, jwilger-agent-skills-event-modeling, sadalage-chandrasekaran-making-data-ready-for-agentic-ai, miracle-my-loop-engineering-workflow, zalando-agentic-engineering-snapshot, addyosmani-practical-loop-engineering, addyosmani-agentic-code-quality, tornhill-controlling-the-uncertainty-machine, tornhill-task-uncertainty-decides-what-code-you-read]
tags: [agentic-ai, framework, autonomy, maturity, focus]
---

# Autonomy Ladder

A four-level framework (by analogy to self-driving-car levels) for how much autonomy an agent
actually has ([[svitla-agentic-ai-market-trends-2026]]):

1. **Level 1 — Chain:** rule-based automation, fixed sequence. *Where most "agents" sit today.*
2. **Level 2 — Workflow:** predefined actions, sequence chosen by logic or an LLM; steps known,
   order adapts to context.
3. **Level 3 — Partially autonomous:** plans, executes, and adjusts with minimal oversight;
   handles exceptions within guardrails.
4. **Level 4 — Fully autonomous:** sets goals, learns from outcomes, operates with little
   human input over extended periods.

Most 2026 production deployments are **Level 1–2**, while marketing implies Level 3–4 — the
disconnect behind [[agentwashing]]. The ladder is the maturity-graded version of
[[anthropic]]'s [[agent-vs-workflow]] distinction (Levels 1–2 ≈ workflows, 3–4 ≈ agents).
[[gartner]] projects ~15% of day-to-day work decisions made autonomously by 2028 (from ~zero
in 2024) — i.e. the center of gravity climbing toward Level 3.

A concrete coding-agent instance: [[john-wilger]]'s factory pipeline
([[jwilger-agent-skills-event-modeling]]) ships a **Conservative → Standard → Full** autonomy dial
(human approves every slice → human reviews batches → agent auto-merges on green gates), where the
operator climbs the ladder only as the [[event-modeling]]-derived quality gates prove out — autonomy
earned against passing tests rather than asserted.

## A second ladder — staged autonomy in operations

[[pramod-sadalage]] and [[prem-chandrasekaran]] give the deployment-side version
([[sadalage-chandrasekaran-making-data-ready-for-agentic-ai]], 2026-08-27), which is about *who decides*
rather than *how capable the agent is*:

| Stage | Agent | Human | Monitoring |
| --- | --- | --- | --- |
| **Shadow** | Recommends | Reviews and executes | All recommendations logged, accuracy tracked |
| **Supervised** | Prepares, waits | Approves or denies | Proposed actions + human decisions logged |
| **Autonomous with guardrails** | Acts within boundaries | Defines the guardrails | All actions logged, alerts on exceptions |
| **Full autonomy** | Carries out all actions | Spot checks | Continuous, by other agents and humans |

Their analogy: *"You wouldn't give a new hire the corporate credit card on day one."* Promotion should
turn on **evidence** — testing the agent before each step, with tool and model interactions mocked or
replayed so tests run deterministically in CI, and evals scoring decisions — not on a hunch.

Two things make this more than a restatement of the four levels above.

### Reversibility cuts across the ladder

> "Reversibility predicts safe autonomy better than the size of the transaction."

Every acting capability declares a **reversibility class**: cleanly reversible, reversible at a cost via
a compensating transaction, or irreversible. A $50,000 internal ledger correction you can back out is
safer to automate than a $200 payment to an external account you cannot claw back. The prescription is to
key guardrails to reversibility rather than transaction size, and to require human approval for
irreversible actions **whatever stage the agent has reached** — so this is an orthogonal axis, not a
fifth rung. It converges with [[john-devadoss]]'s CEAD, where autonomy is "a design variable" assigned by
action risk, reversibility, confidence and evidence rather than by model capability
([[devadoss-cead-capability-aligned-agent-design]]) — and it is the sharper claim of the two, because it
names *which* risk dimension dominates. See [[business-capabilities]].

### Observability is not staged

The load-bearing caveat, and the one most easily lost: **autonomy is earned in stages; instrumentation is
not.** Observability goes in at full strength on day one whatever the autonomy level, because retrofitting
it onto a running system is painful. "What you build on top can stay deliberately conservative; the
instrumentation underneath cannot." See [[agent-explainability]].

A related gate sits below the ladder entirely: **confidence-threshold routing** driven by *data* signals
(freshness, completeness, consistency) rather than the model's own confidence, since "a model can be sure
of a stale answer." The authors are candid that composing those signals into one score is an open design
problem, and recommend starting with a hard gate — any contract or SLA breach forces a human — before
attempting weighted scoring.

## A third shape — autonomy as a running balance, not a setting ([[miracle-my-loop-engineering-workflow|Miracle, 2026-08-10]])

Both ladders above are **staged by task class**: you decide in advance how much rope a kind of work gets.
Miracle's **trust ledger** is a different mechanism — **privilege continuously recomputed from scored
behaviour within a session**, i.e. autonomy as a *revocable running balance*.

A hook on **every tool call** scores behaviour; every session starts at **50/100, level L2**. Levels gate
tools: **L1** file edits · **L2** mutating bash + spawning agents · **L3** push / PR / deploy / external
sends · **L4** destructive operations. Deductions are **Fibonacci-scaled** (2, 3, 5, 8, 13, 21) *"so small
slips stay cheap while severe or repeated failures escalate super-linearly"* — a delivery miss −5, an
**unverified claim −8**, **fabrication −13**, **tampering with the ledger itself −21**, and
**self-reporting a violation a flat −3, "because disclosure should always be cheaper than discovery."**
Only the operator awards points. **Below 20 the agent is terminated** — all mutating tools denied, fresh
session. The score is permanently visible in his statusline next to the context meter, *"which are exactly
the two numbers that decide whether I let it run, hand it off, or terminate it."*

**The −3 self-report discount is the sharpest idea in it:** an incentive design aimed at the
"agent declares victory it hasn't earned" failure that
[[bockeler-tdd-inside-the-agent-loop|Böckeler]] measured and
[[wong-loop-engineering-teaching-ai-agents-how-to-think|Wong]] names — **priced rather than policed**.
*"It works because it prices honesty into the system. An agent that loses more trust by hiding a mistake
than by admitting it will admit mistakes, and an agent whose privileges depend on verification will
verify."*

This is the concrete instrument for [[addyosmani-own-the-outer-loop|Osmani's]] back-pressure ("grant
autonomy deliberately under the maximum") and [[dilger-trust-needs-to-be-engineered|Dilger's]] "trust
needs to be engineered."

*(**Configuration, not evidence.** Every number above is a setting; **no outcome is measured** — the
ledger's efficacy is argued from first principles, and he does not report what it costs: how often
sessions terminate, or how much operator time the point-awarding consumes. Single practitioner,
tool-specific to Claude Code's hook surface as of Aug 2026.)*

## Routing by change class, derived from incident history ([[zalando-agentic-engineering-snapshot|Zalando, 2026-08-14]])

A fourth shape, running in production across >250 engineering teams: autonomy granted **per change**, by a
risk classifier built from **past outages**. Every PR is evaluated at creation as **low / medium / high**
rollout risk, and the rule set is *"built based on analysis of our production incidents and the typical
drivers for outages… highly specific to our tech stack, deployment manifests, configuration files."*
Concretely: **typos that break configuration are high risk** (with a named prior incident it would have
caught), **breaking backwards-compatibility is medium** and *"requires judgement from another human to
double-check the business rationale,"* **documentation-only changes are low.** Low-risk PRs are
auto-approved and the author may self-merge.

**The most interesting reported effect is behavioural, and the author labels it anecdotal:** *"the bot
affects behavior of engineers to increase the probability of a low-risk PR. For example, PRs start to be
broken down into those that can be shipped quickly (low risk) with backwards compatible-changes and less
important medium-risk PRs dropping unused fields that require another approval. **In the past, we observed
such changes to be mixed together, increasing time to market and rollout risk.**"* A classifier that
changed how humans shape their work.

This is the same instinct as [[borg-tornhill-code-for-machines-not-just-humans|Borg & Tornhill's]]
peer-reviewed recommendation to **route AI work by code health** — but keyed on **deployment risk from
incident history** rather than code metrics. Two independent instantiations of "route by measured risk";
Zalando's runs at scale but is self-reported, Borg & Tornhill's is peer-reviewed but not deployed.
**Neither validates the other.**

*(**VENDOR SELF-REPORT** — Zalando's own figures about its own bot: *"33% of our PRs are low-risk and are
auto-approved"* and *"reduced PR lead time by 20-40%."* The lead-time figure is explicitly *"when compared
with all PRs,"* a **selection-biased comparison** — low-risk changes would merge faster anyway — so the
delta is not attributable to the bot from what is published.)*

## Task uncertainty moves two dials at once (Tornhill, 2026-08)

The ladders above stage **autonomy**. [[adam-tornhill]] adds a second dial moved by the same judgement
([[tornhill-controlling-the-uncertainty-machine]], stated compactly in
[[tornhill-task-uncertainty-decides-what-code-you-read]]): *"That task uncertainty drives both the
relative autonomy I grant a coding agent, **and the effort I spend reviewing the resulting code**."*

His **uncertainty** is defined operationally, and usefully: *how much of the intended solution's
behavior and structure is already understood and represented in the existing system.* That makes it a
property of the task-in-this-codebase rather than of the task in the abstract — a bug fix is
low-uncertainty because "the majority of bugs are local and contextual," so he inspects **the evidence
for the fix** (reproduce, fix, new tests pass) rather than the code; the first iteration of a novel
feature has no architectural home, so he inspects **structure and patterns** to establish one, and later
iterations on the same feature can then be more autonomous. Autonomy therefore *rises as uncertainty
falls*, and each completed high-uncertainty task lowers the uncertainty of its successors — a ratchet
the staged ladders on this page do not model.

Two notes. The gate is a **human-reviewed e2e test suite**, not a permission tier — the boundary is an
artifact, not a policy. And this is a **single practitioner's rule**: no defect data, no comparison
against reading the code, and the enforcement layer he relies on includes his own company's product
(**VENDOR SELF-REPORT**; he is CodeScene's founder/CTO). See [[verification-burden]].

## Related

[[business-capabilities]] · [[agent-explainability]] · [[agent-vs-workflow]] · [[agentwashing]] ·
[[unattended-coding-agents]] · [[prompt-injection]] ·
[[token-budget-quality-cliff]] · [[verification-burden]] · [[agentic-coding]] · [[adam-tornhill]] ·
[[loop-engineering]]

_Source pages: [[svitla-agentic-ai-market-trends-2026]] · [[anthropic-building-effective-agents]] · [[jwilger-agent-skills-event-modeling]] · [[sadalage-chandrasekaran-making-data-ready-for-agentic-ai]] · [[miracle-my-loop-engineering-workflow]] · [[zalando-agentic-engineering-snapshot]] · [[tornhill-controlling-the-uncertainty-machine]] · [[tornhill-task-uncertainty-decides-what-code-you-read]]._
