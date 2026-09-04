---
title: "Source: Addy Osmani — An agentic code-review skill on five axes"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [osmani-agentic-code-review-skill-five-axes]
raw_file: [raw/notes/osmani-agentic-code-review-skill-five-axes.md]
tags: [verification-burden, agentic-coding, skills, code-review, self-report, focus]
---

# Source: Addy Osmani — An agentic code-review skill on five axes

LinkedIn post by **[[addy-osmani]]** (**2026-08-28**, resurfaced by his own repost ~09-02), captured
verbatim at `raw/notes/osmani-agentic-code-review-skill-five-axes.md` via logged-in Chrome. Announces
the `code-review-and-quality` skill in his public **`addyosmani/agent-skills`** pack
(`npx skills add addyosmani/agent-skills --skill code-review-and-quality`).

## Summary

He describes a skill that "transforms the /review process by doing four specific things," and the four
are the interesting part because each targets a known failure of automated review:

1. **Reviews on five quality axes** — *correctness, readability, architecture, security, performance*.
   His reason: "Most automated reviews collapse to 'do the tests pass?' Tests are necessary, but **they
   don't catch a leaking module boundary.**"
2. **Labels every finding by severity** — "Critical" blocks the merge, no prefix means required, "Nit"
   and "FYI" are optional. Purpose: "This stops authors from treating every comment as mandatory and
   burning an afternoon on formatting preferences."
3. **Leads with leverage** — "If there is one structural problem and ten nits, the structural problem
   *is* the review. Findings are ordered by what actually changes the outcome."
4. **Proposes the move** — "Saying 'This is complex' leaves the author guessing. Saying 'Replace this
   conditional chain with a dispatcher' is a review they can act on."

His framing sentence is the one that puts him in this batch: **"The review is your quality gate. It is
worth telling your agent what a good one looks like. Run /review before you merge."** He closes
generously — "If you don't end up using it or there's another code-review skill out there you like
better, that's totally cool."

## Key points

- **This is the *automate the review* position** — the fourth distinct answer to the verification
  burden, and the only one in the batch that keeps the gate exactly where it is and puts an agent in
  the reviewer's chair.
- **"Tests are necessary, but they don't catch a leaking module boundary"** is a direct, unintended
  rebuttal to
  [[tornhill-controlling-the-uncertainty-machine|Tornhill's]] e2e-suite-as-abstraction-boundary
  method: an inspection instrument aimed at exactly the class of defect a passing test suite is blind
  to. Whether an *LLM* reliably detects that class is untested here — and
  [[tornhill-cannot-trust-agent-codescene-mcp]] argues on separate evidence that it does not.
- **The three ergonomics moves are the transferable content**, independent of the skill: severity
  labels that make optional findings optional, ordering by leverage, and proposing the fix. All three
  attack *review-output overload* — the reviewer-side analogue of
  [[tornhill-compressed-cognition-cost-of-faster-coding|decision density]].
- **Skills-as-distribution.** Another instance of the KB's pattern of practice shipped as an installable
  skill pack rather than written up as an article — cf. [[khononov-modularity-claude-code-plugin]] and
  [[tornhill-controlling-the-uncertainty-machine|Tornhill's review findings captured as SKILLs]].

## Limits

- **AUTHOR'S OWN TOOL.** Everything here is self-report about an artefact he publishes: **no
  evaluation, no benchmark, no comparison against other review skills, and no before/after** on
  defects caught or missed. "Transforms the /review process" is a product claim.
- **THIN CAPTURE** — a LinkedIn announcement post, not a design document or an article. The skill's
  actual prompt content is not in `raw/`; the repo is the ground truth and is not captured.
- **The premise is asserted, not defended.** "The review is your quality gate" is precisely the
  premise [[laycock-maybe-we-shouldnt-be-reviewing-all-this-code|Laycock]] rejects five days later; he
  offers no argument for keeping the gate, only for making it better.
- No position on volume: nothing addresses whether an agent-reviewed merge gate keeps up when the code
  is [[willison-brewster-cannot-review-180000-lines|180,000 lines]], nor who reads the review.
- LinkedIn-derived date; the "1w" age stamp belongs to the original post, not the repost.

## Connections / contrast

- **[[verification-burden]]** — the **automate-the-gate** position. Set beside it Laycock's charge, made
  independently and without naming him: *"I don't think the answer is an AI agent pretending to be the
  human reviewer so we can preserve exactly the same process at higher speed. That's automating the
  ceremony rather than questioning why the ceremony exists."* This is the batch's most direct
  head-to-head, and the KB's job is to show both.
- **Also opposed by [[willison-more-than-just-code-review|Willison]]**: "eyeballing every line of code
  has never been the most effective way to validate a change" — an argument against the instrument
  itself, whoever holds it.
- **Yet partly vindicated by Anthropic's own practice** recorded on [[loop-engineering]] via
  [[willison-fireside-chat-claude-code-team]]: code review moved off humans by finding files where
  automated review "catches 100% of the issues," with an eval set added after each incident. That is
  the automate-the-gate position *with* a measured trust ladder — the thing this post lacks. The pairing
  is the fairest way to hold Osmani's claim.
- **[[addyosmani-agentic-code-quality]] / [[comprehension-debt]]** — from the author who coined
  comprehension debt, this is the tooling answer to it. Worth noting the tension with his own
  [[addyosmani-own-the-outer-loop|Answerability]] argument: an agent may produce the review, but the
  human still owns the merge, and the post's "run /review before you merge" leaves who-decides
  unstated. Also [[willison-directly-responsible-individuals]].
- **[[ai-readable-code]]** — the five axes are a quality vocabulary; "architecture" and "readability"
  are what CLEAR ([[tornhill-clear-design-principles-agentic-age]]) and
  [[tornhill-beyond-lambdas-raising-the-abstraction-level|Beyond Lambdas]] make precise.
- **[[fitness-functions]]** — the deterministic alternative: what Osmani asks an LLM to judge on the
  architecture axis, Tune's Rivière ([[nick-tune-enforced-application-architecture-agents-humans]])
  makes fail the build. Read as competing bets on judgement vs. enforcement.
- Also: [[guardian-agents]], [[agent-observability-and-evals]] (what would be needed to substantiate
  the claim), [[loop-engineering]].

## Links

Entities: [[addy-osmani]] · [[rachel-laycock]] · [[simon-willison]] · [[adam-tornhill]] ·
[[anthropic]]. Concepts: [[verification-burden]] · [[comprehension-debt]] · [[fitness-functions]] ·
[[ai-readable-code]] · [[guardian-agents]] · [[loop-engineering]] ·
[[agent-observability-and-evals]]. Related sources:
[[laycock-maybe-we-shouldnt-be-reviewing-all-this-code]] · [[willison-more-than-just-code-review]] ·
[[tornhill-cannot-trust-agent-codescene-mcp]] · [[addyosmani-agentic-code-quality]] ·
[[willison-fireside-chat-claude-code-team]] · [[khononov-modularity-claude-code-plugin]].

_Raw source: `raw/notes/osmani-agentic-code-review-skill-five-axes.md`._
