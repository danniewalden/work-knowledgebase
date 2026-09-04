---
title: "Source: MacManus & Pocock — The /wayfinder Skill and the Fog of War"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [macmanus-pocock-wayfinder-skill-fog-of-war]
raw_file: [raw/articles/macmanus-pocock-wayfinder-skill-fog-of-war.md]
tags: [loop-engineering, skills, context-engineering, ubiquitous-language, spec-driven-development, focus]
---

# Source: MacManus & Pocock — The /wayfinder Skill: Navigating the "Fog of War" of Planning

Source: **Richard MacManus** interviewing **Matt Pocock**, *"The /wayfinder Skill: Navigating the 'Fog of
War' of Planning"*, **Latent.Space**, **2026-08-20**. Raw capture:
`raw/articles/macmanus-pocock-wayfinder-skill-fog-of-war.md`. First entry in Latent.Space's new skills
series. Pocock's "AI Skills for Real Engineers" project is cited at 220,000+ GitHub stars and his YouTube
channel at 347,000 subscribers — **audience size, not evidence of efficacy.**

## Summary

`/wayfinder` is an **orchestrator layer for the planning stage**, built because planning — not execution
— had become the bottleneck for away-from-keyboard agent work. Pocock: *"I was finding the planning stage
really onerous, because I would have to be constantly thinking about my session management. Like, how
many tokens am I into my context window? How deep am I going here?… **I wanted an orchestrator layer
that would basically say, okay, whatever you want to plan, I'm going to handle the planning sessions for
you.**"* The skill splits planning across threads (prototyping, research), pulls it back together into a
central document, and is organised around two deliberately chosen words: **the map** and **the ticket**.
Its named problem is the **"fog of war"** — *"you can't quite decide everything right at the start."*

## Key points

- **The design derivation is the most instructive part, because it starts from information flow.**
  *"Whenever you're thinking about context management — **because that's really what a skill is, you're
  managing the context of the agent you're working in** — you need to think about the information flow.
  So what I wanted to think about is, what if a grilling session could manage other grilling sessions?…
  the first step to that is, **what does the child need in that situation?** The child probably needs to
  understand a vague overview of what else is happening, and they need their specific task."* From that
  question, two artifacts fall out: **the map** (everything else — all the decisions already made) and
  **the ticket** (the specific task that goes into the session).
- **Naming is treated as load-bearing engineering, not flavour.** *"Once you've got the kernel of an
  idea, you then need to come up with the words for that idea. Because once you've figured out the words,
  then those entities can be really clearly mapped out by the agent. **Because if you just call
  everything a ticket, or if you just refer to it in different ways in different places, then it's going
  to be really confused and you're going to get strange behavior.** Whereas if you use these very
  specific, what I call **leading words**, to lead the agent to understand exactly what each part is, and
  you've understood what the information flow is, then you've got your skill."*
- **He built a dictionary and made all his skills conform to it.** *"For the last few months, I've been
  pretty obsessed with terminology… I've put together… an **AI coding dictionary** — of basically all the
  terms in AI coding. It's in this beautiful graph that you can explore and understand exactly what an
  agent is, exactly what a harness is, exactly what a model is… I've redone all my courses to use that
  dictionary… And then all of my skills use a consistent dictionary as well. So they're all working off
  the same assumptions, the same leading words."* **Not yet released** at capture time.
- **The explicit framing: a ubiquitous language between human and agent.** *"I realized that I needed a
  **ubiquitous language between me and the agent**. Between me and the agent, there is a communication
  barrier. And that's what I'm trying to do with my skills all the time, is **try to find the right
  words**."* And a striking aside: *"agents are really good at showing you the opportunities for
  different wording — **really good at domain modeling, actually**."*
- **The fog-of-war concept, and why the metaphor was chosen.** *"You can make certain decisions, and
  those certain decisions sort of lead you there and push further out into the fog of war — kind of like
  Warcraft III style, exploring the map. And once I had the idea of 'fog of war' and 'map', I realized
  those two terms actually work really nicely together, and **it really leads the agent into the right
  idea**."* The metaphor was selected for its effect on the agent, not for the reader.
- **Four ticket types, generalising beyond code.** **Grilling** tickets (an adversarial Q&A session),
  **prototype** tickets, **research** tickets, and **task** tickets — *"which are really broad… basically,
  just anything the human needs to do that the agent can't do."* That last category is notable: **the
  plan has first-class slots for human work.** He uses the skill for course planning and non-engineering
  work too.
- **A clean selection rule between two skills.** *"Use 'grill me' in cases where you feel like you can
  plan the whole thing in a single session, and you need to align before you go. So most small features
  will fit into this. Most stuff where you can see the path ahead of you, but you just want to make sure
  the agent is on board… For stuff where you don't know the path ahead, for stuff where you can feel the
  fog of war in front of you, use wayfinder."* **Session-sized uncertainty vs. multi-session
  uncertainty.**
- **The purpose of it all is to feed AFK agents better specs.** *"I didn't want to feel constrained in
  the planning stage anymore… And then your specs can be even more detailed, and you can just whack off
  an AFK agent to go and do tons more work."*
- **Limits.** A short interview (~1,450 words), *"slightly condensed for readability"*, promoting the
  author's own skill on the week of its release: **no measurement, no comparison, no outcome data** — not
  even a self-reported before/after on planning time. The only quantities are **audience metrics**
  (220,000 stars, 347,000 subscribers) and the capture's engagement footnote (73 likes, 2 restacks);
  neither says anything about whether `/wayfinder` works. The AI coding dictionary that underpins the
  terminology claim is **unreleased and unexaminable**. All five of the interview's illustrations are images
  (skill documentation, the author's test project) and are **noted inline rather than transcribed**, so
  the skill's actual contents are not in this capture. The claim that agents are *"really good at domain
  modeling"* is an unevidenced aside — but see below, because it is the most consequential sentence in
  the piece for this KB.

## Connections / contrast

**This instantiates the abstract "Skills" primitive that [[loop-engineering]] describes and never
shows.** That page lists skills as primitive #3 — *"project knowledge written down once (`SKILL.md`) so
the loop doesn't re-derive your project from zero every cycle"* — and cites
[[jwilger-agent-skills-event-modeling]], [[khononov-modularity-claude-code-plugin]] and
[[miller-jasperfx-ai-skills-agent-skills]] as instances. `/wayfinder` is a different *kind* of skill from
all three: those encode **domain or library knowledge**; this encodes **a process for producing plans**,
including its own session-splitting and handoff discipline. A skill that manages other sessions is
closer to [[miracle-my-loop-engineering-workflow|Miracle's]] orchestrator mode than to a knowledge file.

**"That's really what a skill is — you're managing the context of the agent you're working in"** is the
best one-line definition of a skill in the KB and belongs on [[context-engineering]]. It reframes skills
as a *context-engineering* artifact rather than a *knowledge* artifact — the distinction being that a
knowledge file is about the domain, while a skill is about what enters the window and when.

**The naming argument is a genuine, if accidental, argument for [[domain-driven-design]]'s ubiquitous
language — and Pocock uses that exact term.** *"I needed a ubiquitous language between me and the
agent"*, plus *"if you just refer to it in different ways in different places… you're going to get
strange behavior"*, is Evans's argument with a new second party. For this KB's focus that is directly
load-bearing: [[event-modeling]]'s whole value proposition is a shared vocabulary and an explicit model,
and Pocock arrives at the need for one **from pure agent-mechanics reasoning**, with no DDD framing and
apparently no awareness of the lineage. Add his aside — **agents are "really good at domain
modeling"** — and this is an independent practitioner reinventing the front half of the KB's core thread.
It sits alongside [[dymitruk-ai-melts-barrier-event-modeling-is-the-map|Dymitruk's "the model is the
map"]] (note the shared metaphor, independently chosen) and
[[dilger-markdown-is-a-suggestion-dressed-as-a-spec|Dilger's]] insistence that loose prose is not a spec.
**Caution: it is an aside in an interview, with no evidence — treat it as convergent framing, not as
support for any claim about agents doing domain modelling well.**

**The map/ticket split is a parent-child context contract.** *"The child probably needs to understand a
vague overview of what else is happening, and they need their specific task"* is the same two-part
handoff as [[addyosmani-code-agent-orchestra|Osmani's]] subagent briefs (`DATA.md` + `LOGIC.md` read
before starting), [[miracle-my-loop-engineering-workflow|Miracle's]] commission-plus-contract-document
(*"It is the contract; do not re-derive what it settles"*), and
[[wong-graph-engineering-wiring-agents-into-an-organization|Wong's]] authoritative-state-vs-convenience-
summary distinction. Four sources independently converge on: **a child agent needs exactly one
authoritative shared artifact plus one scoped assignment** — arguably the most robust practitioner
consensus in this batch, and worth stating as such on [[context-engineering]].

**The fog of war is the honest counterpart to [[spec-driven-development]].** SDD assumes a spec can be
written first; [[ng-spec-driven-development-is-waterfall-in-markdown|Ng]] objects that this is waterfall
in markdown. Pocock's answer is neither: **plan iteratively, but keep a durable map of what has been
decided** — so the artifact grows as the fog lifts. That is close to
[[dilger-spec-driven-development-needs-four-phases|Dilger's four phases]] and to
[[domain-discovery]] as a staged activity, and it is a better fit for greenfield work than either
"write the spec" or "just prompt."

## Links

[[loop-engineering]] · [[context-engineering]] · [[spec-driven-development]] · [[domain-driven-design]] ·
[[domain-discovery]] · [[event-modeling]] · [[harness-engineering]] · [[agent-harness]] ·
[[multi-agent-orchestration]] · [[unattended-coding-agents]] · [[token-budget-quality-cliff]] ·
[[context-rot]] · [[agent-readable-model-artifacts]] ·
[[macmanus-schott-react-for-agents-flue-meta-harness]] ·
[[macmanus-prs-not-welcome-software-factories]] · [[miracle-my-loop-engineering-workflow]] ·
[[addyosmani-code-agent-orchestra]] ·
[[wong-graph-engineering-wiring-agents-into-an-organization]] ·
[[jwilger-agent-skills-event-modeling]] · [[khononov-modularity-claude-code-plugin]] ·
[[miller-jasperfx-ai-skills-agent-skills]] · [[dymitruk-ai-melts-barrier-event-modeling-is-the-map]] ·
[[dilger-markdown-is-a-suggestion-dressed-as-a-spec]] ·
[[dilger-spec-driven-development-needs-four-phases]] ·
[[ng-spec-driven-development-is-waterfall-in-markdown]]

_Source: [[macmanus-pocock-wayfinder-skill-fog-of-war]] (raw: `raw/articles/macmanus-pocock-wayfinder-skill-fog-of-war.md`)._
