---
title: Jeremiah Lowin
type: entity
created: 2026-07-31
updated: 2026-07-31
sources: [prefect-loops-vs-graphs]
tags: [person, orchestration, agentic-ai, graph-engineering, prefect]
---

# Jeremiah Lowin

Founder and **CEO of [[prefect]]** — the workflow-orchestration company behind the open-source Prefect
engine and FastMCP, which acquired **Dagster** (2026). In this KB he is the **authored primary for the
loops-vs-graphs framing**: he coined **"directed agentic graph"** (a deliberate rebrand of the
decades-old *directed acyclic graph* — dropping "acyclic," keeping "directed," making each node a full
agentic invocation whose tools/skills/model/access are set per-node), introduced it at a **PyData London
keynote** ~6 weeks before the topic went viral, and made it a Prefect product imperative since April 2026.

His argument, from [[prefect-loops-vs-graphs]] (FastMCP podcast ep. 3): **loops are one agent's internal
micro behaviour; directed agentic graphs are macro orchestration across many agents.** A graph gives
businesses the reproducibility, auditability, and control-vs-autonomy modulation a bare
[[loop-engineering|loop]] can't — plus **capability scoping per node** (the "don't hand your agent a
bazooka" security case: do diligence in a node with no dangerous tool, issue the refund only in a later,
narrowly-scoped node past a programmatic control-return). He explicitly distinguishes his **macro** level
from **LangGraph / Pydantic AI**, which graph an *individual agent's internals* (micro). He is
positioned as the "calm down, here's the boring orchestration way that works" voice, warning the agent
world not to "rediscover graph theory from scratch" and repeat the orchestration field's old mistakes —
naming Peter Steinberger's viral tweet as the spark that surfaced the conversation.

In the KB he sits on the [[graph-engineering]] and [[multi-agent-orchestration]] threads, adjacent to
[[nick-tune]]'s graph-substrate argument and [[addy-osmani]]'s "loops vs graphs" aside in
[[addyosmani-software-factories-light-and-dark]]. Not an [[event-modeling]] voice.

_Source pages: [[prefect-loops-vs-graphs]]._
