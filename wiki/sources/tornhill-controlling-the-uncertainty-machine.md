---
title: "Source: Adam Tornhill — Controlling the Uncertainty Machine: Do You Still Need to Read AI Code?"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [tornhill-controlling-the-uncertainty-machine]
raw_file: [raw/articles/tornhill-controlling-the-uncertainty-machine.md]
tags: [verification-burden, ai-readable-code, agentic-coding, testing, codescene, focus]
---

# Source: Adam Tornhill — Controlling the Uncertainty Machine

Essay by **[[adam-tornhill]]** on his personal Substack *Code for Humans and Machines*
(**2026-08-20**), filed under his AI-READABLE CODE section. Raw capture:
`raw/articles/tornhill-controlling-the-uncertainty-machine.md`. The article the LinkedIn note
[[tornhill-task-uncertainty-decides-what-code-you-read]] announces.

Standfirst: **"Human attention should follow uncertainty. We don't need to read all AI-generated code.
But we need to make the code we do read count."**

## Summary

Tornhill accepts the accountability and rejects the method: "As developers, we're used to being
accountable for all code we write. Coding agents do not change that. But we need to use our time
effectively, and I simply found that trying to grasp all code in detail is no longer efficient." Read
agent output the way you read your own and "we'll spend the majority of our time trying to deconstruct
meaning from code. **We'd effectively turn ourselves into legacy code maintainers.**"

His answer is a **triage rule plus a substitution**.

**The triage rule — attention follows task uncertainty.** "A question like 'do we still need to read
all AI generated code' is pointless in isolation. The answer depends on the task, and more
specifically on the uncertainty inherent in each type of task. That is, how much of the intended
solution's behavior and structure is already understood and represented in the existing system." That
uncertainty sets *both* the autonomy he grants the agent *and* his review effort. A **bug fix** is
naturally constrained — "usually enough to inspect the evidence for the fix. Reproduce the problem,
fix it, and have the new tests pass." The **first iteration on a new feature** has no architectural
home yet, so he goes deeper — but on "the overall structure and patterns," not the details.

**The substitution — tests as the human/agent abstraction boundary.** After planning, he instructs the
agent to **write the end-to-end tests first**, then reviews and iterates on *those*: "A strong test
suite serves as a boundary between the code I do inspect and the code I give the AI autonomy to
develop." With the e2e tests nailed down, "I typically let the agent proceed and write the code that
makes them pass. I rarely spend much time looking at the actual implementation." Notably he inverts
the usual quality assumption: "AI-generated application code is rarely optimal out of the box. But
it's usually decent. **The test code? Not so much.**" So the human effort goes into test
refactoring — pulling tests toward the domain, hunting gaps and negative cases, adding abstractions
that document intent.

**Review findings become future guards.** He refuses to fix code himself: he instructs the agent to
change it, then instructs the agent to **capture the transformation as a forward-looking SKILL** —
"my review findings turn into future guards and guidance."

**Enforce what you don't inspect.** A "multi-layered safety net": ~six months of accumulated SKILLs
(style, design principles, app-specific architecture rules) plus **deterministic tools** — "some of
these tools are commercial (e.g. vulnerability scanners, and the CodeHealth MCP), others like linters
are free" — plus custom domain-specific checks for architectural rules and "the most common e2e sins."
"The point is that these rules and constraints need to be enforced. Deterministically."

The closing section, *"The hardest thing to refactor is our habits"*: "Given that I had typed out code
by hand for almost 40 years, becoming comfortable with not reading code was a large mental shift…
Almost a year into my agentic journey, I'm now quite confident that I don't need to know every line of
code. I get that confidence by knowing that the system behaves as intended, remains maintainable, and
lives within the established boundaries." And: "Familiarity is a poor argument for resisting change."

## Key points

- **The load-bearing sentence: "I never read all AI-generated code. But, and this is important, make
  the code you do read count."** This is a *triage* position, not an abdication position.
- **Uncertainty is defined operationally**: how much of the intended behaviour and structure is
  *already represented in the existing system*. Low uncertainty (bug fix) → verify the evidence; high
  uncertainty (novel feature, no architectural home) → inspect structure and patterns, still not
  details.
- **The verification instrument is the test, reviewed by a human**; the implementation is delegated.
  The e2e suite is deliberately designed "to optimize for ease of inspection" — the artifact is
  engineered for the human, not the machine.
- **AI didn't remove the need for maintainability, it raised the bar**: "as our research discovered, a
  coding agent is even more picky about code quality than we humans" — the claim already held in the
  KB via [[tornhill-codescene-unhealthy-code-agentic-token-cost]] and
  [[borg-tornhill-code-for-machines-not-just-humans]].
- **Successful features attract change**, so uninspected code must still be cheap to change — which is
  why his triage argument needs [[ai-readable-code]] to hold it up. The two threads are one argument.

## Limits

- **VENDOR SELF-REPORT on the prescribed remedy.** Tornhill is founder/CTO of **CodeScene**, and the
  "multi-layered safety net" he prescribes includes **CodeScene's own CodeHealth MCP** by name. His
  diagnosis can stand on its own; his remedy is not disinterested, and the marker travels with it onto
  every page that cites the deterministic-enforcement prescription.
- **IMPRESSION NOT MEASUREMENT throughout.** Everything about the method's payoff is personal
  adaptation reported after "almost 40 years" of hand-coding and "almost a year" agentic: no defect
  rates, no escaped-bug counts, no before/after, no comparison against reading the code. "I'm now
  quite confident" is a confidence report.
- **The unexamined risk is exactly what tests cannot see.** He offers no account of failures that e2e
  tests plus linters plus code-health rules would miss — security logic, concurrency, resource
  lifetimes, cross-cutting design mistakes that are individually legal. (Cf. Brewster's `AddRef()` bug,
  which a rendering-level e2e test would very plausibly pass.)
- **Single-practitioner workflow**, solo or small-team shaped: nothing addresses knowledge transfer,
  juniors, or collective ownership — the functions [[laycock-maybe-we-shouldnt-be-reviewing-all-this-code|
  Laycock]] insists must be relocated rather than dropped. His SKILLs are the closest thing to an
  answer, and they transfer *rules*, not judgement.
- "As our research discovered" refers to CodeScene research, not to work presented in this article.

## Connections / contrast

- **[[verification-burden]]** — the *triage* position, and the most operational of the four: a stated
  decision rule (uncertainty), a named boundary artifact (the e2e suite), and a named enforcement
  layer (deterministic tools + SKILLs).
- **Converges with [[willison-more-than-just-code-review|Willison]]**, independently and within two
  days: "eyeballing every line of code has never been the most effective way to validate a change."
  Willison states the principle; Tornhill supplies the machinery. This is the batch's clearest
  agreement, from two unrelated practitioners.
- **Against [[willison-brewster-cannot-review-180000-lines|Brewster]]**: same premise (you cannot read
  it all), opposite conclusion — Brewster has no substitute instrument, Tornhill's whole argument *is*
  the substitute instrument. The pair is the best illustration on [[verification-burden]] of why
  "don't read every line" and "trust me bro" are not the same position.
- **Partly against, partly with [[laycock-maybe-we-shouldnt-be-reviewing-all-this-code|Laycock]]**:
  they agree that line-by-line inspection is finished and that deterministic checks should be
  automated — and his tools are *deterministic*, not an LLM playing reviewer, so he is not the target
  of her "automating the ceremony" charge (Osmani is). They disagree about where the human-understanding
  function lives: her answer is people, earlier; his is artifacts (tests, SKILLs, rules).
- **[[ai-readable-code]] / [[agent-legibility]]** — "enforce what you don't inspect" is the enforcement
  arm of [[tornhill-clear-design-principles-agentic-age|CLEAR]]; the accompanying
  [[tornhill-beyond-lambdas-raising-the-abstraction-level|Beyond Lambdas]] piece is the code-level
  move that makes the reading he *does* do cheaper.
- **[[tornhill-cannot-trust-agent-codescene-mcp]]** is the missing premise: an LLM cannot reliably
  self-assess code health, which is why the safety net has to be deterministic rather than another
  agent. Read the two together.
- **[[fitness-functions]]** — his custom architectural checks are fitness functions by another name,
  and land in the same place as [[nick-tune-enforced-application-architecture-agents-humans|Tune's
  Rivière]] (make the violation fail the build).
- **[[given-when-then]] / [[adaptech-given-when-then-executable-tests-before-implementation]]** — the
  Event-Modeling seam: "generate the e2e tests first, review those, let the agent make them pass" is
  GWT-before-implementation reached from the code-health side. Also
  [[bockeler-tdd-inside-the-agent-loop]] and [[dilger-lights-off-software-factory-dead-end]]'s
  layers-of-trust ladder recorded on [[software-factory]], which this closely resembles.
- **[[autonomy-ladder]]** — uncertainty-driven autonomy *plus* uncertainty-driven review effort is a
  two-dial version of that page's single dial.

## Links

Entities: [[adam-tornhill]] · [[simon-willison]] · [[rachel-laycock]]. Concepts:
[[verification-burden]] · [[ai-readable-code]] · [[agent-legibility]] · [[fitness-functions]] ·
[[autonomy-ladder]] · [[given-when-then]] · [[comprehension-debt]] · [[attention-bottleneck]].
Related sources: [[tornhill-task-uncertainty-decides-what-code-you-read]] ·
[[tornhill-compressed-cognition-cost-of-faster-coding]] ·
[[tornhill-beyond-lambdas-raising-the-abstraction-level]] ·
[[tornhill-cannot-trust-agent-codescene-mcp]] · [[tornhill-ai-induced-code-smells-codehealth-mcp]] ·
[[willison-more-than-just-code-review]] · [[laycock-maybe-we-shouldnt-be-reviewing-all-this-code]].

_Raw source: `raw/articles/tornhill-controlling-the-uncertainty-machine.md`._
