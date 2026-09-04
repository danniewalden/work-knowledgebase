---
source_url: https://www.linkedin.com/in/ricofritzsche/recent-activity/all/
title: "An atomic append isn't enough — Command Context Consistency needs a protected write order"
author: Rico Fritzsche
publication: LinkedIn (post)
published: 2026-06-23
retrieved: 2026-06-29
type: note
---

(Verbatim capture of a Rico Fritzsche LinkedIn post, ~6d old when retrieved on
2026-06-29, pulled via logged-in Chrome. Author notes a fuller article is
linked in the first comment — NOT captured here. Hashtags #EventSourcing
#SoftwareArchitecture #PostgreSQL #SystemDesign.)

An atomic append can still allow two incompatible decisions to pass through.

When two commands evaluate the same Event Query almost simultaneously, they can observe the same command context and context version, reach identical decisions, and call the conditional append with that same expected version.

Using a PostgreSQL CTE that combines the Event Query check with the insert ensures that each append is atomic. However, under READ COMMITTED, it does not establish any order between those concurrent executions. As a result, both statements can evaluate against the same committed history before either transaction commits, leading to both checks passing and both events being recorded.

To achieve Command Context Consistency, more than atomic statements are necessary; a protected write order is essential. Only after establishing that order can the event store re-evaluate the same Event Query, compare the current context version against the expected one, and decide whether to record the events or reject the command.

A straightforward approach in PostgreSQL is to lock a single metadata row at the beginning of each append transaction. This method serializes the physical writes globally, while the actual conflict decision remains local to the command context.

For example, registrations for "alice" and "bob" can both succeed after waiting, but two concurrent registrations for "alice" cannot.

The lock itself is merely an implementation detail; the critical aspect is the contract that the event store provides. Atomicity safeguards one append, while serialization prevents two decisions made from the same observed command context from being accepted.

Link to my full article in the first comment.

How have you managed concurrent commands that rely on the same command context in your systems?

#EventSourcing #SoftwareArchitecture #PostgreSQL #SystemDesign
