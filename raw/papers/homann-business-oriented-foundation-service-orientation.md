---
source_url: https://cdn.ymaws.com/www.businessarchitectureguild.org/resource/resmgr/homann_article_on_capabiliti.pdf
title: "A Business-Oriented Foundation for Service Orientation"
author: Ulrich Homann (Microsoft)
publication: Microsoft (MSDN); republished by the Business Architecture Guild
published: 2006-02
retrieved: 2026-06-14
type: paper
---

# A Business-Oriented Foundation for Service Orientation — Ulrich Homann (Microsoft, Feb 2006)

> **Capture note:** This is a copyrighted Microsoft paper (© 2006 Microsoft). Per copyright limits it
> is **summarized/paraphrased here, not reproduced verbatim**, with only short attributed quotes.
> It is the most-cited foundational reference for *business capability mapping* (cited by the BIZBOK
> Guide). Read the original at the source URL for full text.

## Thesis

Service-orientation is "only the implementation of a particular model" — it is *not* the starting
point. The durable foundation should be a model of **what a business does**, because the stable
elements of a business are its activities (create purchase orders, ship product, pay employees), while
*how* it implements them (people, procedures, technology, and the processes that knit them together)
is far less stable. Process-first modeling fixes the "how" and only optimizes mechanics; capability-
first modeling challenges the "what."

## Key definitions (short quotes)

- **Business capability:** "a particular ability or capacity that a business may possess or exchange
  to achieve a specific purpose or outcome." It describes *what* the business does (outcomes + service
  levels) and **abstracts/encapsulates the people, process, technology, and information** into building
  blocks. A capability is essentially a **"black box"** — external, observable, measurable behavior
  with defined inputs/outputs and a contracted **service-level expectation (SLE)**; *how* it's done
  inside doesn't matter at this level. Examples: "Pay Employees", "Ship Product".
- **Capability connectors:** the links between capabilities. Not just messages — they carry "rich
  semantic information": information exchange (input/output, supporting info) and control/policy
  (regulatory influence). Homann stresses that **discovering the connections may be as valuable as
  defining the capabilities**, because you manage change through the connections while the capability
  black boxes stay stable.
- **Business processes:** describe *how* the business implements/connects capabilities to deliver an
  outcome (end-to-end work, transcending departments — Hammer & Champy lineage).
- **Business capability mapping:** "the definition and clear structural outline of the capabilities and
  their connections." Capabilities are the **building blocks of business architecture** — "thinking of
  capabilities as an architectural blueprint is a good analogy, whereas the process is the
  implementation of that architecture at any given time."

## Why capabilities are the stable layer

Capabilities are "sufficiently descriptive to understand how a function fits in the business … yet
summarize enough to provide … a firm, longer-lasting base." Illustration: a grocery checkout — manual
vs. self-service checkout share the same capabilities (identify customer, scan products, take payment);
self-service merely adds one capability (validity check, via the weight-scale). **The capabilities
remain stable while the processes change.** Another: you manage a phone/energy provider purely by the
capabilities and service levels they deliver, not by knowing *how* they deliver the dial tone — so
providers are interchangeable by service level. Capabilities map cleanly onto service-orientation
because both are **black boxes whose connections matter more than their internals**.

## Capability model structure (taxonomy)

A business capability model is a **nested hierarchy** exposing all capabilities across the ecosystem
(it spans the whole value network, not just one legal company — e.g. UPS, ADP participate in a
collective "business"):

- **Level 1 — Foundation Capabilities:** split into **Operations Capabilities** (inside the business
  boundary: develop products/services, generate demand, produce/deliver, collaborate with partners,
  plan & manage the business) and **Environmental Capabilities** (outside: customers, customer-facing
  channels, logistics providers, infrastructure & compliance, financial providers, suppliers,
  governments/regulators).
- **Level 2 — Capability Groups:** e.g. within "Develop Products/Services" a group "Plan
  Products/Services". Often the first actionable level for analyzing service levels, constraints, and
  organizational ownership/accountability.
- **Level 3…n — Business Capabilities:** the building blocks, decomposable to finer capabilities; not
  all branches need decomposing to the same depth.

## Why it matters (context: connected businesses)

The linear supply chain has become a **value network** of partners (BPO, self-service, regulators), so
modeling must cross corporate boundaries. Any architecture will be in flux; building around the stable
"what" turns architectural investment into "enduring assets" and lets management decide sourcing
(in-source vs outsource) on an equal, service-level basis across capabilities.
