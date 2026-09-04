---
title: Adam Dymitruk
type: entity
created: 2026-06-11
updated: 2026-09-04
sources: [eventmodeling-what-is-event-modeling, semaphore-dymitruk-event-modeling, dymitruk-event-modeling-future-proof-agents, dymitruk-ai-trained-on-dysfunction-agents-are-a-must, dilger-first-event-modeling-conference-munich-recap, event-modeling-event-sourcing-podcast, adaptech-workflow-not-inside-giant-process-manager, dymitruk-ai-melts-barrier-event-modeling-is-the-map, dilger-podcast-episode-47-agentic-modeling-audit-trails]
tags: [person, event-modeling, event-sourcing, software-design, agentic-ai]
---

# Adam Dymitruk

Software developer; CEO and founder of [[adaptech-group]]. Originator of
**[[event-modeling]]**, the method this KB's event-modeling thread is built on. Co-hosts the weekly
**[[event-modeling-event-sourcing-podcast|Event Modeling and Event Sourcing Podcast]]** with
[[martin-dilger]].

## Contribution

- Coined and developed **[[event-modeling]]** — describing information systems as a
  timeline of events ("a captured screencast of someone using the system you intend to
  build") using 3 building blocks, 4 patterns, and a 7-step workshop.
- Evolved it from Alberto Brandolini's [[event-storming]] (kept the workshop/sticky-note
  format) and built on [[greg-young]]'s CQRS/ES long-running process specifications.
- Strong advocate of [[event-sourcing]] (the append-only "no erasers" ledger) and of
  pairing it with event modeling to give explicit contracts between workflow steps.
- Runs [[adaptech-group]] on **fixed-price** delivery, which he attributes to the
  flat-cost-curve property of event modeling.
- **Standardization JV (2025-10):** gave the Day-1 keynote at the first Event Modeling Conference
  ([[dilger-first-event-modeling-conference-munich-recap]]) and announced a **joint venture with
  [[martin-dilger]]** — a new company focused on **Event Modeling tooling and standardization** — plus
  a planned EM certification program; a governance signal for the method itself.
- **On AI agents (2025):** argues Event Modeling is "future proof" — because automation was built in
  from the start, an agent is just a **user** or a **processor** (Automation pattern), so multi-agent
  systems can be modeled without new notation ([[dymitruk-event-modeling-future-proof-agents]]). See
  [[event-modeled-agent-design]].
- **On why agents are needed (2026-06-15):** "AI was trained on dysfunction," so it won't produce
  best-practice software on its own — but you *can* assemble best-practice systems, so agents are a
  must; he points to [[martin-dilger]] and [[yordis-prieto]] as the way
  ([[dymitruk-ai-trained-on-dysfunction-agents-are-a-must]]). The blunt rationale for the spec-as-
  scaffolding view in [[event-modeled-agent-design]] / [[agentic-coding]].
- **The model is the map; the LLM barely matters (2026-08-09):** code artifacts are "a black box" with
  "no standard way to see what's going on inside," but **[[event-modeling|Event Modeling]] gives you a map**
  that "no AI tooling gives you" — so *which LLM you use* "doesn't matter that much"; "choosing an LLM is
  like picking up pennies in front of a steamroller." The quotable, LLM-agnostic form of the model-as-
  source-of-truth thesis (vs [[yordis-prieto-code-is-the-ultimate-diagram|Prieto's code-first counter]]).
  Companion same-day post: **AI melts the barrier to entry** to non-default good practices (Linux /
  [[event-sourcing|Event Sourcing]] analogy) — accountability-by-default becomes cheap to adopt
  ([[dymitruk-ai-melts-barrier-event-modeling-is-the-map]]).

## Podcast Episode 47 — three positions (date unresolved)

**"Agents need an audit trail, not a snapshot"**
([[dilger-podcast-episode-47-agentic-modeling-audit-trails]], **date unresolved — do not assign one**;
the episode carries no date in HTML, metadata or body, is absent from the RSS feed and from
podcast.eventmodeling.org, and may be a channel prior sweeps never polled): *"Events are the truth, the
full story, not just the current state. Read models are derived and disposable. If an agent goes
sideways, follow the event trail, find the divergence, fix it, replay. No mystery, no data surgery."*
He is **endorsing, not originating** — the hosts are relaying a LinkedIn post by **Svet Angelov** that is
not captured in `raw/`. It is the crispest statement of the KB's [[event-sourced-agentic-patterns]]
thesis as an *agent requirement*.

Same episode, two more positions: **screens are legitimate model content** — *"all the arguments about
not having screens and design sessions is just gatekeeping by architect wannabes"*
([[screens-as-specification]]) — and a caution on agentic modelling: an over-eager agent flooding a
[[given-when-then|GWT]] list with edge cases *"can make a simple slice look far more complex than it
really is, since event modeling is visual"* ([[event-modeling-anti-patterns]]). He also restates
**specification by example** as the method's existing answer to over-specification: *"draw a few
representative example paths and trust the implementer to infer the rest."*

*Marker: show-notes level, not verified against audio, on a podcast he co-hosts with
[[martin-dilger]] about a platform Dilger sells — see the vendor markers on [[eventmodelers-ai]].*

## Where he appears

- [[eventmodeling-what-is-event-modeling]] — his canonical write-up (eventmodeling.org).
- [[semaphore-dymitruk-event-modeling]] — interview on event modeling, DDD, OCP, event sourcing.
- [[dymitruk-event-modeling-future-proof-agents]] — X post applying Event Modeling to AI agents.
- [[dymitruk-ai-trained-on-dysfunction-agents-are-a-must]] — LinkedIn post: agents needed to assemble best-practice systems.
- [[event-modeling-event-sourcing-podcast]] — his weekly podcast with [[martin-dilger]] (46 eps), where the design substrate (aggregate-killing, slices, sagas→to-do lists, GWT, AI/[[agentic-coding]]) gets argued out conversationally.
- [[adaptech-workflow-not-inside-giant-process-manager]] — [[adaptech-group]] design essay he reposted (2026-07-28): replace a giant saga/process manager with a projected to-do list + focused processors; the dedicated primary for the podcast's "sagas → to-do lists" theme ([[process-managers-and-todo-lists]]).
- [[dymitruk-ai-melts-barrier-event-modeling-is-the-map]] — two LinkedIn posts (2026-08-09): the model is the map so the LLM barely matters ("pennies in front of a steamroller"); AI melts the barrier to good defaults.

## Related

[[model-as-code-vs-model-as-language]]

_Source pages: [[eventmodeling-what-is-event-modeling]] · [[semaphore-dymitruk-event-modeling]] · [[dymitruk-event-modeling-future-proof-agents]] · [[dymitruk-ai-trained-on-dysfunction-agents-are-a-must]] · [[event-modeling-event-sourcing-podcast]] · [[adaptech-workflow-not-inside-giant-process-manager]] · [[dymitruk-ai-melts-barrier-event-modeling-is-the-map]] · [[dilger-podcast-episode-47-agentic-modeling-audit-trails]] (**DATE UNRESOLVED**)._
