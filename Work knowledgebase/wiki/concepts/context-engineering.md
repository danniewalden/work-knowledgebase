---
title: Context Engineering
type: concept
created: 2026-06-11
updated: 2026-06-11
sources: [fowler-bockeler-harness-engineering, langchain-anatomy-of-an-agent-harness, firecrawl-what-is-an-agent-harness]
tags: [context-engineering, harness-engineering, agent-engineering]
---

# Context Engineering

The practice of deciding **what information enters the model's context window at each step** —
and what to compress, retrieve, or leave out. It optimises the *input* to the model.

Techniques drawn from the sources: **compaction** (summarise older history when the window fills),
**tool-call offloading** (keep head/tail tokens, write the full output to the filesystem),
**retrieval** ([[retrieval-augmented-generation]]) of only the relevant docs per step, **Skills /
progressive disclosure** to avoid loading everything up front, and positioning the most important
content at prompt boundaries to counter "Lost in the Middle." All are responses to [[context-rot]].

## Relationship to harness engineering

The two are distinct but nested:

- **Context engineering** controls *what the model sees*.
- **[[harness-engineering]]** controls *the environment the agent operates in* — what it can
  access, what gets verified, what forces a retry.

Per [[fowler-bockeler-harness-engineering]], context engineering supplies the *means* to make
guides and sensors available to the agent, so engineering a coding-agent user harness is "a
specific form of context engineering." [[langchain-anatomy-of-an-agent-harness]] frames harnesses
as "largely delivery mechanisms for good context engineering." Both sit inside [[agent-engineering]].

_Sources: [[fowler-bockeler-harness-engineering]] · [[langchain-anatomy-of-an-agent-harness]] · [[firecrawl-what-is-an-agent-harness]]._
