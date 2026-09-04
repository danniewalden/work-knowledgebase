---
title: "Source: Zalando — Agentic Engineering at Zalando: a Snapshot"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [zalando-agentic-engineering-snapshot]
raw_file: [raw/articles/zalando-agentic-engineering-snapshot.md]
tags: [agentic-coding, agent-governance, em-standardization-foundation, production-evidence, focus]
---

# Source: Zalando — Agentic Engineering at Zalando: a Snapshot

Source: **Bartosz Ocytko** (Executive Principal Engineer, **Zalando SE**), *"Agentic Engineering at
Zalando: a snapshot"*, Zalando Engineering Blog, **2026-08-14**. Raw capture:
`raw/articles/zalando-agentic-engineering-snapshot.md`. Surfaced via
[[martin-fowler|Martin Fowler's]] *Fragments: August 24*, which flagged it as "detailed and thoughtful."

**Two markers, and they are not in conflict — record both.** The capture note files this as a rare
**non-vendor** account, in the sense that Zalando sells fashion, not agent tooling, and is describing
practice at scale (>250 engineering teams, 2.5 years) rather than pitching a product — the same class of
independent evidence as [[stripe-minions-one-shot-coding-agents]]. That is right and is why the source is
valuable. **But every number in it is Zalando reporting on Zalando's own internal tooling, so
VENDOR SELF-REPORT applies to the figures** (the risk-based-approval percentages in particular). The
useful distinction: *non-vendor about the market, self-reporting about itself.*

## Summary

A 2.5-year retrospective on agentic engineering across **>250 engineering teams**, notable for what it
is *not*: no transformation narrative, no productivity claim, no mandated toolchain. Its recurring theme
is **deliberate non-convergence** — *"With >200 teams innovating and broadly exploring the ecosystem, the
question arises whether and when to converge. **We believe it's way too early for this.**"* The
substance is infrastructure and governance: an **LLM proxy from day one** (LiteLLM, January 2024), vendor
independence as policy, a **risk-based PR approval bot**, a centralized **agent skill collection**, an
internal Tech Radar AI section, and a training/knowledge-sharing apparatus. Its honest headline:
*"AI amplifies the good and bad practices across our organization."*

## Key points

- **The platform decision that made everything else possible: an LLM proxy on day one.** A LiteLLM-based
  API proxy deployed **January 2024** with access to OpenAI, AWS Bedrock and Google Vertex, so
  *"it became easy for our engineers to experiment with different tools and models"* while the platform
  team got *"a single point to measure adoption via: MAU, WAU, model, User-Agent."* Operational detail
  worth keeping: **post-call hooks for anonymized cost tracking**, **pre-call hooks enforcing client
  version upgrades by User-Agent** (*"For self-managed client installations, unfortunately blocking
  access is the only effective measure. Same goes for retiring models. **There is always a long-tail
  group of users who do not adjust their local configurations**"*), **auto-injection of prompt caching
  checkpoints** (*"which reduced costs for custom agents while their authors still learn about prompt
  caching"*), and forced restarts after 20k requests to work around LiteLLM memory leaks — running 2k MAU
  on six small pods.
- **Vendor independence as explicit policy.** *"We have never centrally mandated the use of a single
  tool. Users make choices for tools, based on available models and their own preferences."* The finding
  underneath it is behavioural and contrarian: *"we see users **becoming too attached** to the coding
  agent they had been using for a while… **The hesitance to switch tools on psychological level exists
  despite the rather low switching costs** between the tools as capabilities of the tools are largely
  similar to one another."* And a structural reason to keep the option open: *"moving off closed-weight
  models requires switching to open tools."*
- **Two recurring tooling gaps, reported as vendor-ecosystem failures.** (1) **Generic `User-Agent`
  headers** make client tools unidentifiable at the proxy — for their own applications they include
  *"a name and originating repository and version"*; for others they request changes upstream. (2)
  **No support for custom auth commands**: tools support only static credentials or default to
  subscription offerings, so *"tokens expire and need to be refreshed manually which involves restarting
  the applications."* Their bridge is a local proxy injecting auth headers, which grew a **TUI showing
  per-model costs, gaps in cached-token usage, and per-request metadata.**
- **Risk-based PR approval — the concrete governance mechanism, and the source of the figures.** Every
  PR is evaluated at creation for rollout risk (**low / medium / high**). *"**33% of our PRs are low-risk
  and are auto-approved by the bot.** The author of the PR can thus choose to merge the PR, which in our
  case **reduced PR lead time by 20-40%** (when compared with all PRs)."* The rule set is *"built based
  on analysis of our production incidents and the typical drivers for outages"* and is *"highly specific
  to our tech stack, deployment manifests, configuration files"* — **typos that break configuration are
  high risk** (with a named prior incident it would have caught), **breaking backwards-compatibility is
  medium** and *"requires judgement from another human to double-check the business rationale"*,
  **docs-only changes are low.** The **most interesting reported effect is behavioural**: *"Anecdotal
  evidence shows that the bot affects behavior of engineers to increase the probability of a low-risk PR.
  For example, PRs start to be broken down into those that can be shipped quickly (low risk) with
  backwards compatible-changes and less important medium-risk PRs dropping unused fields that require
  another approval. In the past, we observed such changes to be mixed together, increasing time to market
  and rollout risk."* — the author labels this **anecdotal** himself.
- **Observed effects on the codebase, offered as illustration and not causation.** PR sizes have grown
  for two years, *"with growth in the higher buckets since Sonnet 4 release in Q2/2025, esp. [500,1k) and
  [1k,2k)."* Team responses vary: some set **internal agreements capping PR size** (*"Hard enforcement
  through pre-commit hooks is less popular"*), others lean on **semantic grouping of changes** in the
  review tooling instead of crafted commit sequences. On complexity, they mapped commit-level
  cyclomatic-complexity evolution across **four codebases** (`go-agentic-only` new/full agent adoption
  from day 0 with spec-driven development; `go-reference` 10y+ OSS, agents from commit >3000;
  `java-with-agents` 4y, gradual adoption from commit >1600; `java-reference` 12y+, none) and *"can
  pinpoint inflection points in code complexity at a time when coding agents come into the picture."*
  For the agent-native codebase *"we see complexity to build up very quickly with growth fading out,"*
  and the open question is stated honestly: *"If code complexity is expected to plateau for a well-scoped
  microservice, one would hope this means that the time to build has been drastically reduced. **Time
  will show whether this is the case.**"* Also: *"even commit messages carry the footprint of coding
  agents, typically around the 5k character mark. In one extreme case, we found a commit message to
  include a full log of unit test execution."*
- **Agent skills as an organizational artifact.** A centralized collection grouped into plugins, spanning
  disciplines (data, engineering, frontend, SRE) and languages; **migration skills are the most popular
  type** — *"skills that guide teams in adopting new platform tools or infrastructure practices."*
  Distributed via managed configuration or a CLI installing symlinks (*"opencode does not support plugin
  marketplaces"*). The second-order benefit is the notable one: *"By encouraging broad contribution of
  skills that teams found useful, we got an opportunity to **discover and disseminate best practices
  across the organization**"* — including validating plugin syntax in CI/CD and settling
  **separation of concerns between skills and scripts** (e.g. where OAuth token generation belongs).
- **Governance without convergence.** Their mechanisms are deliberately old and boring: an internal
  **Tech Radar** with a new AI section (*"In the past 10 years, library choices have been offloaded to our
  language communities of practice and out of scope for the Tech Radar. However, the cambrian explosion
  of AI tools… increased the need for clearer guidance on practices that are proven and those that are
  still early stage"* — note they now track **practices**, not just tools), per-use-case legal assessment
  entry points for early-stage projects, and **auto-detection of AI model usage by scanning deployed
  Docker images**, which auto-registers the system in the developer portal and asks owners for
  documentation or legal review. That last one is a genuinely reusable governance primitive.
- **Learning from session data.** *"Looking at session data from coding agents is highly educational.
  Aside from spotting non-essential traffic (e.g. generating plan names, terminal window titles, or
  recaps for idle sessions) that costs tokens, users can learn more about their own prompting patterns."*
  A worked instance: a user with a **<30% cache hit ratio in opencode versus 80%+ expected**, chased down
  with a purpose-written parser and found not to be systematic.
- **Training, and one finding that cuts against the whole trend.** GenAI Labs (~20 people, 1–4h, paired
  exercises, 6 sessions/120–150 participants over 3 days), an **LLM guild** running weekly 1h sessions
  since 2024, and topic-seeded hackathons used to *"explore parallel paths and choose what tools to
  invest in."* The finding: *"One important guidance for training sessions is to **state explicitly when
  manual coding is expected** from attendees… We have observed that the temptation of participants to use
  coding agents as a shortcut to achieve results is high. **Yet, using coding agents usually inhibits
  learning.**"*
- **Balance as an explicit policy.** *"There are things happening in engineering besides AI that deserve
  attention. During our annual Software Engineering Community Conference, we ran the Agentic Engineering
  track on day 1 and **to balance it out an Engineering Fundamentals track on day 2**."*
- **What's next, stated as unsolved problems.** A **repository AI-readiness scanner** *"allowing for
  correlations between delivery posture and codebase health"* — with the candid aside that its side
  effect is promoting best practices *"that otherwise would not be applied due to missing ROI"*; a
  fleet-wide transformation tool now running coding-agent CLIs across repo sets; an agent platform built
  from OSS components (**kagent** on Kubernetes) plus an **Identity Broker** capturing *"delegation chains
  for on-behalf-of flows, brokering between different OAuth2 infrastructures, and implementing a token
  vault"*, designed to sit in the call path between agent and MCP server or between agents. Open
  problems named: managing tooling/config on user devices, local sandboxing, and **auto-routing across
  models including open-weight ones** — *"users rarely switch models unless nudged by hitting a limit or
  error."*
- **A monorepo caveat they raise against their own results.** *"Across industry, many AI wins and
  increases in PR throughput are reported for monorepos where the leverage is high. While we have a few
  monorepos, we largely use separate repositories for our microservices."* An honest statement that
  reported wins elsewhere may not transfer to their topology — and, read the other way, a caution about
  every monorepo-based factory result in this KB.
- **Limits.** **VENDOR SELF-REPORT for all figures** (33% low-risk auto-approved; 20–40% PR lead-time
  reduction) — Zalando's own numbers about its own bot, with no external audit. The lead-time figure in
  particular is stated *"when compared with all PRs"*, which is a **selection-biased comparison**:
  low-risk PRs (docs, config-safe changes) would plausibly merge faster than average with or without a
  bot, so the 20–40% cannot be attributed to the bot from what is published. The complexity analysis is
  **four codebases with no control arm**, and agent adoption is inferred partly from `Co-authored-by`
  markers which the author says are inconsistent (*"esp. OSS… not all authors disclose usage of coding
  agents"*) — treat the inflection points as **illustrative, not causal**, which is how the author
  presents them. The behavioural claim about engineers restructuring PRs is labelled **anecdotal** in the
  text. **All four figures in the piece are images not transcribed in the capture**, so the underlying
  distributions cannot be inspected. Nothing here reports defect rates, incident rates, delivery
  throughput, or cost per merged change; there is **no productivity claim at all** — which is unusual and
  is part of the source's credibility. Published one day outside the capture window's strict lookback and
  filed anyway.

## Connections / contrast

**The KB's second non-vendor, production-scale account of agentic engineering, and the first one that is
about *organization* rather than *tooling*.** [[stripe-minions-one-shot-coding-agents]] reports a
mechanism and a throughput number; this reports **a platform, a governance stack, and a training
apparatus, with almost no throughput claims.** For [[agentic-coding]] and [[agent-governance]] it is the
most grounded evidence the KB has that the hard parts at scale are *identity, auth, cost attribution,
model retirement, config drift on developer machines* — none of which appears in any practitioner-loop
source in this batch. It also directly answers
[[deloitte-ai-agents-scaling-faster-than-guardrails]] with a worked instance of guardrails keeping pace.

**"Deliberate non-convergence" is a real position on [[em-standardization-foundation]] and
[[team-topologies]].** *"We believe it's way too early for this"* — and instead of a mandated stack, they
run **transparency mechanisms** (Tech Radar tracking *practices*, a guild, hackathons, labs). That is the
opposite of the standardization-first instinct the KB records elsewhere, and it is an argument
[[skelton-team-topologies-foundation-ai-roi]] would recognise: platform provides the substrate
(proxy, skills, radar), teams keep the choice. Contrast with
[[laycock-citizens-build-agents-execute-experts-govern|Laycock's]] citizens/agents/experts split — Zalando
has the govern layer but explicitly declines to have the standard.

**Risk-based auto-approval is [[feedforward-and-feedback-controls]] and the [[autonomy-ladder]]
implemented at PR granularity — and it routes by *change class*, derived from incident history.** That
is the same idea as [[borg-tornhill-code-for-machines-not-just-humans|Borg & Tornhill's]] peer-reviewed
recommendation to **route AI work by code health** (low-risk where healthy, human oversight where
unhealthy), but with the routing key being **deployment risk from past outages** instead of code metrics.
Two independent instantiations of "route by measured risk"; Zalando's is running in production at scale
but self-reported, Borg & Tornhill's is peer-reviewed but not deployed. **The KB should hold both and
note that neither validates the other.**

**"Using coding agents usually inhibits learning"** is the batch's only *organizational* observation of
the skill-decay risk [[osmani-ai-wont-teach-you-the-lesson-unless-you-force-it|Osmani asserts]] and
[[macmanus-prs-not-welcome-software-factories|MacManus finds]] at community scale. It is still an
observation, not a study — but it comes from running ~6 sessions for 120–150 people and it produced a
**policy change** (state explicitly when manual coding is expected). That is the closest thing to
evidence the KB has on this, and it is worth carrying on [[comprehension-debt]] with exactly that
weight.

**Their commit-message finding is an underrated agent-legibility datapoint.** *"Even commit messages
carry the footprint of coding agents, typically around the 5k character mark"*, with one containing a
full unit-test log — and their fix is *"a good constraint to add in pre-commit hooks."* Together with
[[breunig-who-taught-the-models-to-do-that|Breunig's]] observation that models will reason **anywhere
that can hold text** (including code comments), this is the same phenomenon showing up in two
independent places: **trained-in write-things-down behaviour spilling into every text field in the
repository.** Neither author connects them; the KB can.

**The AI-readiness scanner is [[ai-readable-code]] as a fleet-wide programme**, and their aside is the
sharp bit: agent readiness brings *"promotion of engineering best practices that otherwise would not be applied due
to missing ROI."* That is [[breunig-fable-and-the-end-of-the-free-lunch|Breunig's]] economics from the
enterprise side — the agent supplies the business case that code quality never could — and it converges
with [[tornhill-codescene-unhealthy-code-agentic-token-cost|Tornhill's]] token-cost argument (a vendor
claim) and [[borg-tornhill-code-for-machines-not-just-humans|its peer-reviewed successor]].

**Also worth filing:** the Identity Broker (delegation chains for on-behalf-of flows, OAuth2 brokering, a
token vault, in the path between agents and [[model-context-protocol|MCP]] servers) is a concrete
answer to the auth problem the KB's MCP pages raise and
[[prompt-injection]]/[[agent-governance]] both require. And their **per-PR live-data preview
deployments** — *"This mechanism enables now not only agents, but also non-engineers who can prompt
changes and easily review the results before asking engineers to take over"* — is a verification
substrate that widens who can check agent output, which is the capacity lever
[[addyosmani-agentic-code-quality|Osmani]] says you must scale.

## Links

[[agentic-coding]] · [[agent-governance]] · [[em-standardization-foundation]] · [[team-topologies]] ·
[[autonomy-ladder]] · [[feedforward-and-feedback-controls]] · [[ai-readable-code]] ·
[[comprehension-debt]] · [[harness-engineering]] · [[model-context-protocol]] · [[prompt-injection]] ·
[[agent-observability-and-evals]] · [[software-factory]] · [[unattended-coding-agents]] ·
[[spec-driven-development]] · [[conways-law]] · [[wardley-mapping]] · [[martin-fowler]] ·
[[matthew-skelton]] · [[adam-tornhill]] · [[stripe-minions-one-shot-coding-agents]] ·
[[skelton-team-topologies-foundation-ai-roi]] ·
[[laycock-citizens-build-agents-execute-experts-govern]] ·
[[deloitte-ai-agents-scaling-faster-than-guardrails]] ·
[[borg-tornhill-code-for-machines-not-just-humans]] ·
[[tornhill-codescene-unhealthy-code-agentic-token-cost]] ·
[[breunig-who-taught-the-models-to-do-that]] · [[breunig-fable-and-the-end-of-the-free-lunch]] ·
[[osmani-ai-wont-teach-you-the-lesson-unless-you-force-it]] ·
[[macmanus-prs-not-welcome-software-factories]] · [[addyosmani-agentic-code-quality]]

_Source: [[zalando-agentic-engineering-snapshot]] (raw: `raw/articles/zalando-agentic-engineering-snapshot.md`)._
