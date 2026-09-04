---
title: "Source: Rachel Laycock — Maybe We Shouldn't Be Reviewing All This Code"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [laycock-maybe-we-shouldnt-be-reviewing-all-this-code]
raw_file: [raw/articles/laycock-maybe-we-shouldnt-be-reviewing-all-this-code.md]
tags: [verification-burden, agent-governance, fitness-functions, thoughtworks, code-review, focus]
---

# Source: Rachel Laycock — Maybe We Shouldn't Be Reviewing All This Code

Essay by **[[rachel-laycock]]**, CTO of [[thoughtworks]], on martinfowler.com ("Rachel's Ramblings"),
**2026-09-02**. Raw capture: `raw/articles/laycock-maybe-we-shouldnt-be-reviewing-all-this-code.md`.
Written explicitly as a **response** to Brian Houck (DX), *"What are code reviews even for?"*, after
they disagreed on a panel at Code Remix hosted by Moderne. Houck's piece is **not** in `raw/`, so this
KB holds only one side of the exchange in the author's own words.

## Summary

Her thesis is in the subtitle: *"perhaps the problem isn't that AI has broken code review, maybe it's
that we've been using code review to solve the wrong problems."* She grants Houck's diagnosis
entirely — AI produces more code than humans can review, and code review carries far more than bug
detection (knowledge sharing, teaching juniors, collective ownership, architectural understanding) —
and then attacks the *placement*: **"why are we waiting until code review to do all of those things?"**

The move is Thoughtworks-classic **shift left**: "If feedback is valuable, don't remove it. Move it
closer to the decision it is informing." So she reassigns each function of review to an earlier
practice — explore alternatives *before* implementing one; knowledge transfer by **pairing**; juniors
learning by working with seniors *while they are thinking*; collective ownership by organising teams
to build and operate together (pairing, mobbing, whiteboard design sessions); architectural alignment
by designing together and then **encoding the constraints as [[fitness-functions]]**; and everything
deterministic (formatting, linting, known security problems) automated — "we really shouldn't still be
arguing about whitespace in 2026."

What remains is **review by exception**: a fundamental architectural change, a sensitive security
boundary, "a change with a huge blast radius, an unfamiliar part of a critical system or simply
something where the team says, 'I'm not confident about this.'" That, she argues, is "very different
from requiring a human to inspect every change because that's the ceremony we've historically used to
create confidence."

Her sharpest line is aimed at the remedy everyone else is building: **"I don't think the answer is an
AI agent pretending to be the human reviewer so we can preserve exactly the same process at higher
speed. That's automating the ceremony rather than questioning why the ceremony exists."**

She concedes the one thing she cannot dispose of: Houck's **"cognitive and intent debt"** — "software
grows while the humans responsible for it understand less and less about why it works the way it does.
I think that's a very real problem. I just don't think mandatory pull requests are a particularly
strong defence against it." Her answer is deliberateness — "collaborative design, pairing, good
boundaries, executable architecture, shared operational responsibility and probably some practices we
haven't invented yet" — closing on **"We need engineers to understand systems, not diffs."**

## Key points

- **Review is over-loaded, and that is the actual finding.** "We've spent years loading an
  extraordinary number of responsibilities onto the humble code review: quality gate, security check,
  architecture review, mentoring mechanism, knowledge-sharing system, ownership model. It worked, sort
  of, while humans could only produce code so quickly. That constraint is disappearing."
- **The bottleneck argument, stated conditionally:** *"If an agent can produce ten times the code but
  every line eventually queues up waiting for a senior engineer to inspect it, we haven't created a
  ten-times engineering organisation, we've created a big backlog and a new bottleneck."* The "ten
  times" is **rhetorical, not measured** — a conditional, not a datum.
- **She dislikes PRs independently of AI**: "I've never particularly liked pull requests as the centre
  of the software development process… build something, finish it, package it up, throw it over to
  somebody else and *then* have the important conversation about whether we built the right thing in
  the right way." (Plus merge conflicts — cf. [[tornhill-merge-conflicts-agentic-bottleneck]].)
- **Agents are welcome in the earlier loops, not as the reviewer**: "agents can participate in those
  loops too, challenging designs, testing assumptions and continuously verifying what is being built,
  but the real thinking is coming from experienced humans."
- **Two relayed figures — do not promote either.** "at Meta, significant lines of code per
  human-landed diff **reportedly increased 106%** in a year, while DX's own data shows **median pull
  request size increasing 64%**." Both reach her via Houck at **DX, a vendor selling
  developer-productivity measurement** — so the 64% is a **VENDOR SELF-REPORT** on the market DX
  sells into, and the 106% is **double-relayed** (Meta → Houck → Laycock) and hedged as "reportedly"
  by Laycock herself. Neither is a KB-grade number; both markers travel with the figures onto any
  page that cites them.

## Limits

- **NOT INDEPENDENT.** Laycock is [[thoughtworks]]' CTO publishing on **martinfowler.com, Thoughtworks'
  own channel**. Every remedy she prescribes — pairing, trunk-based development, [[fitness-functions]],
  "shift left", evolutionary architecture — is a **Thoughtworks-originated or Thoughtworks-promoted
  practice**, so this page is not external corroboration for any of them. The marker travels with the
  claim.
- **No evidence of her own.** Zero data, no case, no team, no before/after. The two numbers in the
  piece are someone else's, and the rest is argument from principle plus personal preference ("I've
  always struggled with the idea…"). She frames the whole ramble as an opinion in a disagreement, and
  it should be read as a well-positioned framing, not as evidence.
- **One side of a two-sided exchange.** Houck's *"What are code reviews even for?"* is not captured, so
  the KB has her characterisation of his argument only — a gap worth closing.
- **Cost of the alternative unpriced.** Pairing and mob programming spend *more* human attention per
  unit of code, which is the exact resource her own [[laycock-the-conductor-developer|conductor piece]]
  calls the new scarcity, and the exact resource [[tornhill-compressed-cognition-cost-of-faster-coding|
  Tornhill's compressed-cognition argument]] says agents are already draining. She does not address
  that tension.
- Assumes a team. Nothing in the prescription is available to a solo maintainer — see
  [[willison-brewster-cannot-review-180000-lines]].

## Connections / contrast

- **The three-way (four-way) dispute.** This is the *restructure* position on
  [[verification-burden]]: don't scale review, **relocate what review is for** and review by
  exception. Set against [[willison-brewster-cannot-review-180000-lines|Brewster]] (review is
  impossible; accept the debt), [[tornhill-controlling-the-uncertainty-machine|Tornhill]] (triage by
  task uncertainty, substitute tests + deterministic enforcement),
  [[tune-no-rapport-with-a-model-you-didnt-code|Tune]] (the loss is upstream, in the domain model, and
  may be unrecoverable), and [[osmani-agentic-code-review-skill-five-axes|Osmani]] — whose shipped
  agentic review skill ("the review is your quality gate… run /review before you merge") is **the
  precise thing she calls automating the ceremony**. Same few weeks, no cross-citation.
- **She and Tornhill agree more than the framing suggests**: both reject line-by-line reading of
  agent output, both push the deterministic checks into automation. They differ on *what carries the
  human-understanding function* — she says humans together, earlier; he says tests, SKILLs and
  deterministic tools. Hers is an organisational answer, his a solo/small-team one.
- **Direct tension with an existing KB page.** [[loop-engineering]] records Anthropic's own practice
  of **moving code review off humans** by finding files where automated review "catches 100% of the
  issues" ([[willison-fireside-chat-claude-code-team]]). That is a vendor-team instance of exactly the
  automated-reviewer path Laycock rejects on principle. Both belong on the page; the KB should not
  pick.
- **[[fitness-functions]]** gets its clearest *purpose* statement here — the mechanism that carries
  architectural alignment once nobody reads every diff — which is also the seam
  [[nick-tune-enforced-application-architecture-agents-humans|Tune's Rivière]] builds machinery for.
- **[[comprehension-debt]]**: she accepts the debt is real and denies that mandatory PRs pay it down;
  "understand systems, not diffs" is the sharpest one-line restatement of that page's thesis in the
  KB. Note the vocabulary datum: Houck's terms are "cognitive and intent debt", arrived at
  independently of Osmani's coinage.
- **[[agent-governance]] / [[laycock-citizens-build-agents-execute-experts-govern]]**: consistent with
  her own earlier argument that the expert's leverage is *the environment* (guardrails, platforms,
  feedback loops), not the review gate. This piece is that thesis applied to one specific gate.
- Also: [[given-when-then]] and [[slice]] — the Event-Modeling seam where an executable spec is the
  "other way" of verifying; [[spec-driven-development]]; [[agent-legibility]].

## Links

Entities: [[rachel-laycock]] · [[thoughtworks]] · [[martin-fowler]] · [[dora]]. Concepts:
[[verification-burden]] · [[fitness-functions]] · [[comprehension-debt]] · [[agent-governance]] ·
[[attention-bottleneck]] · [[agentic-coding]] · [[team-topologies]]. Related sources:
[[laycock-citizens-build-agents-execute-experts-govern]] · [[laycock-the-conductor-developer]] ·
[[willison-brewster-cannot-review-180000-lines]] · [[tornhill-controlling-the-uncertainty-machine]] ·
[[osmani-agentic-code-review-skill-five-axes]] · [[willison-more-than-just-code-review]].

_Raw source: `raw/articles/laycock-maybe-we-shouldnt-be-reviewing-all-this-code.md`._
