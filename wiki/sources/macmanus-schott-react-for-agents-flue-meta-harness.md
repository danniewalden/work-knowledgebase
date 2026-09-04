---
title: "Source: MacManus & Schott — React for Agents: Hooks in the Flue Meta-Harness"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [macmanus-schott-react-for-agents-flue-meta-harness]
raw_file: [raw/articles/macmanus-schott-react-for-agents-flue-meta-harness.md]
tags: [agent-harness, harness-engineering, agent-frameworks, loop-engineering, focus]
---

# Source: MacManus & Schott — React for Agents: Astro Creator Brings Hooks to his Meta-Harness, Flue

Source: **Richard MacManus** interviewing **Fred Schott** (creator of Astro; Cloudflare since the
January 2026 acquisition), *"React for Agents: Astro Creator Brings Hooks to his Meta-Harness, Flue"*,
**Latent.Space**, **2026-08-15**. Raw capture:
`raw/articles/macmanus-schott-react-for-agents-flue-meta-harness.md`. Companion to
[[macmanus-prs-not-welcome-software-factories]] (where Flue's PR policy appears) and the applied form of
[[breunig-harnesses-are-situated-agents|Breunig's]] harness thesis.

**VENDOR interview.** Every claim about Flue is its creator's, about his own framework, on a product
launch; Schott is a Cloudflare employee and Flue is built on Cloudflare infrastructure. No independent
evaluation exists in this capture.

## Summary

Flue 2 — the framework's first stable release — is built on **React-style "Agent Hooks."** In Flue *"an
agent is represented by a JavaScript function"* that **"re-renders on every turn,"** i.e. before every
model call. The quotable positioning: *"I originally tweeted that we were building the Astro for agents
or the Next.js for agents. But then I realized: maybe no one has even built the **React** for agents."*
The load-bearing claim for the KB is architectural, not framework-specific: **"Our early bet was that the
harness is actually not a feature, but it's fundamental to what you think an agent is. There is no agent
without a harness."**

## Key points

- **"There is no agent without a harness."** The strongest statement of harness-primacy in the KB, from
  someone who bet a product on it. Its corollary, in Schott's words: *"Instead of you and your code
  driving the LLM and telling it what to do with scripts, **you're putting the agent into this harness,
  and it is able to drive itself and work through problems**."*
- **Hooks exist because agents cannot be fully configured in advance.** 16 built-in hooks including
  `useSkill()`, `useTool()`, `useSubagent()`, plus custom hooks, authored in TypeScript. Per the launch
  post they *"let you build dynamic agents that can manage their own state, listen to agent lifecycle
  events, and even **attach different resources and capabilities dynamically to enhance themselves at
  runtime**."* Schott's motivating case: *"real support bots, real triage bots"* can't be static —
  *"a support agent might bring in an account management tool **after first verifying a user**."*
- **"File based magic is an antipattern"** (his section heading) — a design lesson learned by shipping the wrong thing. Flue 1
  naively ported file-based routing from web frameworks: *"I'll put your five agents in these five files,
  and that'll be the five routes that they expose. But for a lot of people building with Flue, especially
  the bigger customers, **their whole company is one agent**. They don't care about routing. There's one
  agent."* Hence the pivot from Astro/Next.js concepts to React's: *"less about routing and these website
  concepts and more about, at its base level, **how do you compose an agent on many different
  things?**"*
- **The layering: Flue is an opinionated take on Pi.** Flue is built on **Pi, an open source minimal
  harness**, in the same relation Vite has to Astro: *"I think Pi can serve that role, where it's the
  right abstraction — it doesn't do too much, but it gives the right APIs that then we can go and say,
  well, let's have an opinionated take on this that does more."* Hosted Flue 2 agents are built with
  Vite.
- **Two generations of agent framework, distinguished by whether the harness was designed in.** The
  **"OG agent frameworks"** — Vercel's AI SDK, Cloudflare's own Agents SDK, Mastra — *"came before Flue
  and so weren't created with a harness as the central concept"*; they are all adding harnesses now, but
  Schott counts that as **an added feature** rather than a foundation. Flue and **Vercel's eve** both
  have built-in harnesses; *"Eve, I think, is the most directly competitive… It came around at the same
  time, so it had that same take that a harness is built-in."*
- **"Meta-harness" is not yet a defined term, per someone selling in the category.** Asked where Flue
  sits versus Databricks' Omnigent or the self-improving Exo harness, *"Schott rightly noted that there's
  confusion about what the term meta-harness even means at this early stage."* He declines the
  one-API-across-all-harnesses idea because *"the framework [Flue] and the harness are very
  intertwined"* — Flue specifically defines how skills and subagents work — and calls Exo *"a different
  interest scenario that isn't really related to hosted agents."*
- **Provenance: Flue began as Astro's issue-triage system.** *"At first, it was an LLM-driven script or
  workflow reviewing issues. But then… it gained the ability to take actions in the repo. It started to
  transition from just automation in a repo to wanting to take the Claude Code experience, **make it
  headless, make it hostable and run it in the cloud**."* His v1 description: *"like Claude Code, but 100%
  headless and programmable."* **The framework is a generalisation of one project's triage loop** — which
  is exactly the arc [[macmanus-prs-not-welcome-software-factories]] documents from the governance side.
- **The framework is designed to be built *by* coding agents.** *"We very much are building for them…
  Our whole onboarding flow is that, you know, pass this prompt to your agent, it's gonna guide you
  through it. **All of our docs have markdown support.**"* The interviewer set up his first Flue agent
  using Claude Code. An explicit instance of designing artifacts for an agent audience.
- **Host portability as a stated principle.** *"The best tools are the ones that float above the host…
  That opens the door for the most developer adoption and the most innovation"* — positioned against
  eve, which *"can also be self-hosted [but] is optimized to take advantage of Vercel's many features…
  a known playbook of Vercel, which does the same thing with Next.js."*
- **Where the industry thinks it is, per an editor's note.** Bret Taylor (Sierra CEO, OpenAI chairman),
  quoted from an earlier Latent.Space conversation: *"We're still trying to figure out who the reactive
  agents are and the jury is still out… **We're sort of in the jQuery era of agents, not the react
  era**."*
- **Limits.** A **vendor launch interview** — no benchmark, no adoption figures, no independent user
  reports, and no numbers at all beyond "16 built-in hooks." Every design claim is the author's about his
  own framework; the "OG frameworks bolted the harness on later" characterisation is a **competitive
  claim about competitors**, not an audited one. The customer evidence is anecdotal and unnamed
  ("especially the bigger customers"). Flue 2 is *"its first stable release"* at capture time, so
  durability is unknown; the whole framework census (Flue, eve, Pi, AI SDK, Agents SDK, Mastra, Omnigent,
  Exo) is **date-bound to Aug 2026**. The capture was fetched from a logged-in browser session; a diagram
  and an embedded tweet are noted inline rather than transcribed.

## Connections / contrast

**"There is no agent without a harness" is the sharpest available support for [[agent-harness]]'s
existence as a concept — and it cuts against the KB's loop/harness ordering.** The
[[loop-engineering]] page opens on loop engineering sitting "one floor above the harness" (an ordering
it now records as unresolved). Schott says
the harness is not a floor at all but the *definition* of the thing;
[[breunig-harnesses-are-situated-agents|Breunig]] independently reports that **Flue "hides the loop from
users"** via its declarative pattern. Put together: the framework whose creator says a harness is
constitutive is also the framework that makes the loop invisible. That is the strongest concrete evidence
in this batch that "loop engineering" names a **current tooling gap** rather than a permanent layer —
and it sits alongside [[morris-humans-and-agents-in-software-engineering-loops|Morris's]] inversion
(the harness controls the loops) rather than
[[wong-loop-engineering-teaching-ai-agents-how-to-think|Wong's]] ladder.

**Hooks are a real answer to a problem the KB has only stated abstractly.** [[context-engineering]] and
[[agent-harness]] both note that an agent's tools and context must vary with the situation; nobody in the
KB shows a *mechanism* for it. `useSkill()` / `useTool()` / `useSubagent()` re-evaluated **before every
model call** is a mechanism — "attach capabilities dynamically at runtime" — and the support-bot example
(bring in the account-management tool only **after** verifying the user) is **capability scoping by
lifecycle stage.** That is [[prefect-loops-vs-graphs|Lowin's]] per-node capability scoping ("don't hand
your agent a bazooka"; grant the refund tool only past a control-return) implemented inside a single
agent instead of across graph nodes. Two vendors, two architectures, same security insight — worth
recording on [[graph-engineering]] and [[agent-governance]] as convergence.

**The "File based magic is an antipattern" lesson generalises past Flue.** Porting a web-framework
concept into agent tooling failed because the unit turned out to be different: *"their whole company is
one agent."* That is a caution for every borrowed abstraction in this space — including React's, which
Schott is now borrowing. Compare [[prefect-loops-vs-graphs|Lowin's]] warning that the agent world risks
"rediscovering graph theory from scratch," and
[[wong-graph-engineering-wiring-agents-into-an-organization|LangChain's]] prior-art rebuttal on graphs:
three instances of an old abstraction being re-imported, with mixed results.

**"We build for coding agents; all our docs have markdown support"** is
[[agent-readable-model-artifacts]] and [[borg-tornhill-code-for-machines-not-just-humans|"code for
machines, not just humans"]] applied to *documentation and onboarding* — the audience for a framework's
docs is now partly the agent that will scaffold with it. Same instinct as
[[miller-jasperfx-ai-skills-agent-skills|JasperFx's vendor-maintained skills]] keeping agents off stale
training data.

**Provenance note worth keeping in the KB's factory story:** Astro's triage bot → Flue the framework →
Flue's closed-PR policy is a single causal chain in which **a loop built to manage community
contributions became a product that then changed how community contributions are accepted.** Few KB
sources show a factory reshaping the institution around it.

## Links

[[agent-harness]] · [[harness-engineering]] · [[loop-engineering]] · [[context-engineering]] ·
[[graph-engineering]] · [[agent-governance]] · [[software-factory]] · [[agent-vs-workflow]] ·
[[agent-readable-model-artifacts]] · [[claude-agent-sdk]] · [[model-context-protocol]] ·
[[multi-agent-orchestration]] · [[breunig-harnesses-are-situated-agents]] ·
[[macmanus-prs-not-welcome-software-factories]] · [[macmanus-pocock-wayfinder-skill-fog-of-war]] ·
[[morris-humans-and-agents-in-software-engineering-loops]] ·
[[wong-loop-engineering-teaching-ai-agents-how-to-think]] ·
[[wong-graph-engineering-wiring-agents-into-an-organization]] · [[prefect-loops-vs-graphs]] ·
[[langchain-anatomy-of-an-agent-harness]] · [[firecrawl-what-is-an-agent-harness]] ·
[[borg-tornhill-code-for-machines-not-just-humans]] · [[miller-jasperfx-ai-skills-agent-skills]]

_Source: [[macmanus-schott-react-for-agents-flue-meta-harness]] (raw: `raw/articles/macmanus-schott-react-for-agents-flue-meta-harness.md`)._
