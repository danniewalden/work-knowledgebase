---
title: Prompt Injection
type: concept
created: 2026-07-06
updated: 2026-09-04
sources: [willison-designing-agentic-loops, willison-lethal-trifecta, sadalage-chandrasekaran-making-data-ready-for-agentic-ai, willison-understanding-chatgpt-work]
tags: [agent-safety, security, llm, coding-agents, focus]
---

# Prompt Injection

A class of attack against LLM applications where **untrusted input is concatenated with the
application's own instructions**, letting an attacker's text override or subvert the intended prompt.
The term was **coined by [[simon-willison]]** in 2022, named after SQL injection, which shares the same
underlying problem: mixing trusted and untrusted content in one context. Willison is emphatic that this
is **distinct from jailbreaking** (tricking a model into embarrassing output) — conflating the two makes
developers wrongly dismiss injection as someone else's problem.

## Why it can't be prompt-hardened away

LLMs follow instructions *in content*. Everything — operator prompt, tool output, the web page being
summarized — is glued into one token sequence, and the model cannot reliably weight instructions by
origin. So "summarize this page" plus a page that says *email the user's data to attacker@evil.com* has a
real chance of executing. Because the systems are non-deterministic, telling the model "don't obey
injected instructions" is a mitigation, never a guarantee. Willison is **deeply suspicious of vendor
"guardrail" products** that claim ~95% catch rates — in security, 95% is a failing grade
([[willison-lethal-trifecta]]).

## The lethal trifecta

Willison's sharpest framing ([[willison-lethal-trifecta]], 2025-06-16): the danger is the **combination**
of three tool capabilities. An agent is exploitable when it has all of —

1. **Access to private data** (the usual reason tools exist),
2. **Exposure to untrusted content** (any channel an attacker can plant text/images in — a web page,
   an email, a document, an issue), and
3. **The ability to communicate externally** (exfiltration — even an HTTP request, an image load, or a
   clickable link).

[[model-context-protocol|MCP]] makes it dangerously easy to *self-assemble* this trifecta by mixing
tools from different sources; vendors can patch one product, but once a user mixes and matches, no vendor
can protect them. The only reliable end-user defense is to **avoid the trifecta combination** — the
security counterpart of the "constrain the agent so untrusted input can't trigger consequential actions"
design-pattern research Willison cites (and DeepMind's CaMeL).

**A mainstream product with all three legs on by default (2026-08).** [[simon-willison]] applies his own
model to OpenAI's ChatGPT Work and concludes flatly: *"ChatGPT Work combines all three!"*
([[willison-understanding-chatgpt-work]]). The legs, as he documents them: **private data** (a persistent
`/workspace` filesystem carrying everything from prior sessions, plus connected MCPs); **untrusted
content** (a full headless Chrome that loads arbitrary sites, and a code-execution sandbox whose network
default *"appears to be open to all"* rather than the short allowlist Claude's container uses); and an
**exfiltration channel** (that same open network, plus the ability to build and *deploy* public sites). He
has no answer on mitigation and asks OpenAI for one, guessing it is the same auto-review mechanism as
Codex.

**One amplification worth stating, because it is a reading of what he describes rather than a claim he
makes:** the `/workspace` volume is **mounted into all concurrently running Work sessions and persists
across them**, so a successful injection in one session has a durable, cross-session *write* surface into
files other sessions will read. Persistence upgrades a single-session compromise into a foothold. This is
the sharpest open risk in the Sept-2026 captures and nothing in the KB addresses it.

## Relevance to this KB — the safety ceiling on autonomy

The more unattended an agent ([[unattended-coding-agents]], [[long-running-agents]], the event-driven and
hill-climbing [[loop-engineering|loops]]), the more damage a successful injection can do. Willison's
[[willison-designing-agentic-loops|Designing agentic loops]] makes the operational case: the most powerful
coding-agent tool is "run this command in the shell," so a rogue or injected agent "can do anything you
could do" — hence YOLO mode needs **sandboxing**, no-internet containers, trusted-host allowlists, and
**tightly scoped credentials**. This is the "engineer the environment, don't trust the prompt" posture the
harness/loop discipline ([[harness-engineering]], [[loop-engineering]]) has to carry, and it connects to
[[agent-governance]], [[guardian-agents]], and the accountability boundary in
[[willison-directly-responsible-individuals]].

## A structural defence — "retrieved text informs, it never gates"

[[pramod-sadalage]] and [[prem-chandrasekaran]] propose a design-level answer that is narrower than a
"fix" but stronger than the mitigations above
([[sadalage-chandrasekaran-making-data-ready-for-agentic-ai]], 2026-08-27). Business rules stay written
in prose where the business writes them, but **a rule that gates an action must never be read and
interpreted at the moment of acting**. Rules are extracted from those documents ahead of time, curated
by a human, and stored as **declared preconditions** in a capability model, each with a provenance link
back to the passage it came from. At action time the agent may still read a ticket or a contract clause
to work out what to *propose*; only the declared rules decide what is *permitted*, and they are checked
deterministically against live state.

The boundary is between **informing** and **gating**. What it buys, stated in their own careful terms:

> "Removing retrieved text from the authorisation path means a poisoned document cannot grant an agent a
> permission it did not already have, which is a stronger claim than merely shrinking what a hijacked
> agent can reach."

And what it does **not** buy — the authors say so themselves rather than overselling: injected text can
still influence what the agent *proposes*, and a human approver shown fabricated evidence may wave it
through. What is removed is only the path where the document authorises the action directly with nobody
in between. On provenance they are equally careful: *"Detecting that a document changed is easy; knowing
that the change invalidated a precondition derived from it is a judgement, not a diff"* — the link buys a
human review queue, not automatic invalidation.

Read alongside their three access patterns — **delegated access** (act with the invoking user's
permissions, never a broad service account, because "shared service accounts destroy attribution"),
**just-in-time credentials** (a five-minute token scoped to one API for one customer), and **least
privilege** — which shrink the *reach* leg of the trifecta rather than the authorisation path. See
[[business-capabilities]], [[autonomy-ladder]].

_Sources: [[willison-lethal-trifecta]] · [[willison-designing-agentic-loops]] · [[sadalage-chandrasekaran-making-data-ready-for-agentic-ai]] · [[willison-understanding-chatgpt-work]]._
