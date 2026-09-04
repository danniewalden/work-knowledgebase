---
title: "Source: MacManus — PRs NOT Welcome: Open Source Projects Turn to Software Factories"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [macmanus-prs-not-welcome-software-factories]
raw_file: [raw/articles/macmanus-prs-not-welcome-software-factories.md]
tags: [software-factory, provenance-trust, open-source-governance, unattended-coding-agents, focus]
---

# Source: MacManus — PRs NOT Welcome: How Top AI Open Source Projects Are Managing Thousands of Contributors

Source: **Richard MacManus**, *"PRs NOT Welcome: How Top AI Open Source Projects Are Managing Thousands
of Contributors"*, **Latent.Space**, **2026-09-01**. Raw capture:
`raw/articles/macmanus-prs-not-welcome-software-factories.md`.

**All headline percentages here are VENDOR SELF-REPORT, four weeks in, unaudited** (see Limits), and the
two most quotable adoption claims are **IMPRESSION NOT MEASUREMENT**. The interesting claim in this piece
is not a number — it is a **reframing of trust**, described below.

## Summary

*"GitHub invented pull requests, and for 18 years they have been open by default. But now some of the
top AI-native open source projects are shutting PRs off, because they've found a better way."* Four
projects — **Vercel's AI SDK, Astro, Flue and tldraw** — are replacing drive-by community PRs with
maintainer-owned [[software-factory|software factories]]: *"a 'team' of agents triaging a PR, reproducing
the issue (if it's a bug), implementing a fix or a new feature, reviewing it, and then handing it back to
a human to merge it."* Flue and tldraw **automatically close every external PR** and convert it to an
issue or discussion.

## Key points

- **THE CLAIM THAT MATTERS — the stated reason is trust in a *specific optimised agent configuration*,
  which is the maker-checker argument reframed as a PROVENANCE argument.** Vercel engineer Lars Grammel:
  *"If we have a very specific agent with a very specific prompt that we optimized — and we know that,
  over history, it was very successful in fixing a certain category of bugs — then **we develop trust in
  that particular agent configuration**."* And the recommendation that follows: *"For open-source
  projects, it's worth considering having your own agents and your own setup, and **not necessarily
  trusting the community**, because it can actually cut down your time to review."* The trust object is
  neither the code nor the contributor's competence — **it is the pipeline that produced the change, with
  a track record per bug category.** That is a different acceptance criterion from anything else in the
  KB, and it is what makes this source worth a page.
- **The consequence, stated by the participants.** Mitchell Hashimoto: *"the future is that large open
  source projects will close contributions completely."* Steve Ruiz (tldraw): *"It just makes less sense
  to have people contributing code **if the issue is decently well-specified and the code can be written
  by agents**."* Note the conditional — the argument is contingent on spec quality, which links it
  directly to [[spec-driven-development]].
- **Flue's policy mechanics.** *"Every external pull request in the Flue project is automatically closed
  and converted into an issue or discussion"* — bug reports and fix proposals become issues, feature
  requests become discussions. The contributor guide's stated motive: preventing **"Drive-by AI slop
  PRs."** MacManus's framing: *"It's kind of like **treating incoming requests as leads**, rather than as
  a piece of work a maintainer feels obliged to review."* Deciding what to work on next uses the team's
  own expertise plus *"the best available SOTA LLMs that we have access to."* Once decided, agents are
  deployed for *"research, design, implementation, and initial review."*
- **tldraw's stated reasons are broader than quality.** Ruiz announced the auto-close policy in January
  2026 and reiterated it five months later, calling it *"an opinionated decision made in response to
  changes in how we're coding (more discussion, more agents), **the social practices around public
  contribution**, and **the changing landscape around code security**."* Three separate drivers — coding
  practice, social norms, supply-chain risk — only one of which is about agents being good.
- **Astro's auto-triage, and what changed about the work.** *"For five years, we were in this place where
  issues came in faster than we could handle them"* (Fred Schott). Now: triage, reproduction, and
  **getting the user to verify the bot's suggested fix "before we even look at it."** The reported change
  is qualitative and structural: *"Being able to essentially treat issues as a thing that every week, you
  prioritize — no matter what — versus a backlog that you're constantly trimming."* The auto-triage system
  **directly led Schott to build the Flue agent framework** ([[macmanus-schott-react-for-agents-flue-meta-harness]]).
- **The community cost is acknowledged, not solved.** *"Traditionally in open source, pull requests have
  been reviewed by maintainers not only for the code, **but to teach contributors and assess them as
  future maintainers**."* Schott concedes the risk: *"It still leaves this open hole of, well, if you just
  keep narrowing the project, at a certain point, you and I go on vacation — what happens? It doesn't
  really solve every problem."* The partial answer both Flue and tldraw offer is that they **still accept
  issues and discussions** — so trust and assessment move to conversation. Ruiz: *"it's better to limit
  community contribution to the places it still matters: **reporting, discussion, perspective, and
  care**."*
- **Limits — every figure in this piece.** **VENDOR SELF-REPORT, unaudited, four weeks in:** Vercel's
  claim that its factory *"authors between 25 and 35% of PRs we merge and closes 70-80% of issues"* is
  **Vercel's own claim about Vercel's own project**, reported second-hand by Latent.Space, measured
  *"just four weeks after this software factory was implemented"* — a window far too short to say
  anything about durability, regression rate, or whether closed issues stayed closed, and with no stated
  methodology for either percentage. **IMPRESSION NOT MEASUREMENT:** Schott's *"It's totally shifted in
  the last six months"* and *"I've never seen that in my entire decade-plus experience with open source"*
  are practitioner impressions and must never be rendered as a figure. Other numbers in the piece are
  **popularity, not efficacy** (20M+ npm downloads/week for AI SDK; 62,000 GitHub stars for Astro;
  50,000 for tldraw; the pre-factory backlog of *"over 1,000 open issues and almost 800 pull requests"* —
  that last one is at least a stated baseline, but no post-factory count is given). Structurally: this is
  **journalism about four self-selected AI-native projects**, three of which are commercially backed
  (Vercel, Cloudflare via Astro/Flue, tldraw as "source available"); there is no comparison project, no
  counterfactual, and no data on whether the closed-PR policy changed contributor numbers. Latent.Space
  is a paywalled Substack that happened to render in full to an unauthenticated fetch; the linked
  *"Software Factories"* and *"Flue 2"* pieces were not in `raw/` at capture time (the latter now is, as
  [[macmanus-schott-react-for-agents-flue-meta-harness]]).

## Connections / contrast

**Provenance-based trust is a third acceptance mechanism, and the KB should name it.** The KB's
verification vocabulary has two moves: **check the artifact** (tests, sensors, gates —
[[addyosmani-agentic-code-quality]], [[feedforward-and-feedback-controls]]) and **use a different checker
than the maker** ([[loop-engineering]]'s maker ≠ checker,
[[wong-loop-engineering-teaching-ai-agents-how-to-think|Wong]]). Vercel's stated reason is neither: they
accept a change because of **who and what produced it**, on the strength of a per-category track record.
That is maker-checker inverted — trust the maker enough that the checking budget shrinks — and it is the
same logic as a signed build or a trusted CI runner, applied to an agent configuration. It also has an
obvious failure mode nobody in the piece raises: **a trusted configuration's track record is
retrospective**, and the thing being trusted is a prompt that can be edited. Worth adding to
[[software-factory]] and [[unattended-coding-agents]] as a distinct mechanism, with that caveat.

**It supplies the institutional third level of the KB's skill-decay problem.** The mechanism Schott
concedes — PRs were how maintainers were taught and assessed — is
[[osmani-ai-wont-teach-you-the-lesson-unless-you-force-it|Osmani's "you miss the reps"]] operating on a
community rather than a person, and the same worry
[[voss-what-the-hell-is-a-loop-anyway|Voss relays from Geoffrey Litt]] ("those who delegate understanding
get replaced by the agent") at career scale. Individual → career → institution, three sources, **no
evidence at any level.** That triad is the most interesting thing this batch adds to
[[comprehension-debt]].

**"Written policy as an enforceable stopping condition" now has two independent instances.** Astro/Flue
convert PRs by rule, and [[addyosmani-practical-loop-engineering|Osmani]] turns his repo's contribution
guidelines ("we currently don't accept translations") into a `/loop` triage criterion. In both cases a
**human-authored policy document becomes the machine's exit condition** — which is
[[bockeler-tdd-inside-the-agent-loop|Böckeler's]] "Approved Scenarios" idea (a human-frozen spec
*outside* the loop rather than a process inside it) arriving in project governance rather than in
testing.

**Warp's triage-label mechanism is the same pattern, described from the factory side.** In
[[addyosmani-human-judgment-relocates]], Warp's four-state label *"is the queue, the lock and… where a
human can park stuff without saying no permanently."* Astro's and Flue's PR-to-issue conversion is that
parking spot made mandatory. Together they make a concrete claim the [[software-factory]] page can carry:
**the factory's real interface is a mutable label on a work item**, not a prompt.

**Contrast with the KB's existing open-source-adjacent sources.**
[[dudycz-fork-can-you-own-it|Dudycz's]] "LLM as a fork" warns that cheap generation shifts cost from
producing to *owning* code; this is maintainers agreeing and acting on it — declining to own code they
did not generate. And [[mitchell-hashimoto|Hashimoto's]] prediction here (large projects close
contributions completely) is a harder line than anything in
[[hashimoto-my-ai-adoption-journey]], worth noting on his entity page as a position stated in 2026-09.

## Links

[[software-factory]] · [[unattended-coding-agents]] · [[loop-engineering]] · [[agentic-coding]] ·
[[spec-driven-development]] · [[comprehension-debt]] · [[agent-governance]] · [[harness-engineering]] ·
[[agent-harness]] · [[feedforward-and-feedback-controls]] · [[prompt-injection]] ·
[[mitchell-hashimoto]] · [[addy-osmani]] · [[macmanus-schott-react-for-agents-flue-meta-harness]] ·
[[macmanus-pocock-wayfinder-skill-fog-of-war]] · [[addyosmani-human-judgment-relocates]] ·
[[addyosmani-practical-loop-engineering]] · [[addyosmani-agentic-code-quality]] ·
[[osmani-ai-wont-teach-you-the-lesson-unless-you-force-it]] ·
[[voss-what-the-hell-is-a-loop-anyway]] · [[bockeler-tdd-inside-the-agent-loop]] ·
[[dudycz-fork-can-you-own-it]] · [[hashimoto-my-ai-adoption-journey]] ·
[[wong-loop-engineering-teaching-ai-agents-how-to-think]]

_Source: [[macmanus-prs-not-welcome-software-factories]] (raw: `raw/articles/macmanus-prs-not-welcome-software-factories.md`)._
