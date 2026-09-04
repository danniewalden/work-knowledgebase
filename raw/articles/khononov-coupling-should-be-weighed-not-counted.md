---
source_url: https://vladikk.com/2026/02/26/coupling-weighed/
title: "Coupling Should Be Weighed, Not Counted"
author: Vlad Khononov
publication: Rants on Software Design (vladikk.com)
published: 2026-02-26
retrieved: 2026-09-04
type: article
capture_note: Out-of-window backfill (2026-02) filed on the 2026-09-04 sweep — a
  recency-bounded watch cannot reach it. Retrieved via WebFetch and transcribed verbatim;
  site nav, sidebar, footer, share widgets and the related-posts list stripped, the lead
  image noted inline as [image: ...]. Full body present from title through the closing "P.S.";
  no portion missing or truncated. The "Posted on February 26, 2026 | 4 min (748 words)"
  line is the page's own byline block. source_url observed on the site's Coupling category
  index, not reconstructed.
  NOT INDEPENDENT: Khononov is the author of the Balanced Coupling model and of
  "Balancing Coupling in Software Design", and runs coupling.dev — this is the model's own
  author arguing for it, not external corroboration that Integration Strength beats
  Ca/Ce/instability metrics.
  IMPRESSION NOT MEASUREMENT: "in my experience, chasing those metrics never really made the
  design more modular" is a practitioner self-report, and the 1-outgoing/100-incoming
  component is a constructed illustration, not a measured case. The post presents no data.
---

# Coupling Should Be Weighed, Not Counted

Posted on February 26, 2026 | 4 min (748 words)

[image: A balance scale where a single heavy weight outweighs many smaller pieces — illustrating that one heavy dependency can matter more than many lightweight ones.]

> "Words should be weighed, not counted." — A Yiddish Saying

Static code analysis tools count dependencies, calculate ratios, and assign neat scores. Yet in my experience, chasing those metrics never really made the design more modular. It's so easy to game the scores without any improvement to the design itself. Let's see why, and what you can do instead.

## The Counting Approach

Most static analysis tools evaluate coupling by counting dependencies. Afferent coupling (Ca) counts how many components depend on yours. Efferent coupling (Ce) counts how many components yours depends on. A popular instability metric combines them into a neat formula:

```
I = Ce / (Ce + Ca)
```

The higher the ratio of outgoing to total dependencies, the more "unstable" a component is considered. Simple. Automatable. And deeply misleading.

## The Blind Spot

Consider a component with just one outgoing dependency and 100 incoming dependencies. Its instability score is roughly 0.01. According to the metric, this is textbook stability. The kind you'd showcase in architecture reviews.

But what if that single outgoing dependency introduces a dependency on another component's implementation details? For example, its private interfaces, internal data structures, or undocumented behaviors. At the same time, all of the 100 incoming dependencies go through well-defined and stable API contracts.

That one outgoing dependency means any internal change in the other component can break yours. Say you have a microservice that uses another microservice's database directly. Any schema change, any column rename, any table restructuring can break your service. Meanwhile, those 100 contract-based dependencies shield you from internal changes through stable integration contracts.

The metric says: rock-solid stability. Reality says: ticking time bomb.

## Weighing Dependencies

Rather than counting dependencies, the Balanced Coupling model focuses on what matters: the practical implications of a dependency. What kinds of shared reasons for change does it introduce? The model defines the Integration Strength scale: four fundamental types of knowledge that can be shared across component boundaries. Each type results in considerably more cascading changes than the one below it:

**Intrusive coupling** is the heaviest. Components integrate through implementation details: direct database access, private object manipulation, undocumented internal APIs. At this level, you have to assume that *all* knowledge is shared. Any internal change, for any reason, can trigger a cascading change. The reasons for cascading changes are essentially unbounded.

**Functional coupling** switches from "how?" to "what": components implement closely related or identical business requirements. If a business rule changes, all components implementing that rule must change together. Think of the same validation logic duplicated in frontend and backend. A specification change that isn't reflected in both simultaneously leads to inconsistent behavior of the system.

**Model coupling** shifts from logic to structure: components share a domain model, but not the logic that implements it. Think entities, relationships, and concepts that describe the business. When the team's understanding of the domain evolves (new insights, restructured entities, refined concepts), all components sharing that model must adapt.

**Contract coupling** is the lightest. Components share only an integration contract: an API specification, an event contract, a data transfer object. The contract encapsulates everything behind it, making the public interface far more stable than the implementation. Restructure your internals? Rewrite your business logic? Evolve your domain model? No cascading changes. Only modifications to the contract itself propagate across boundaries.

That's the Integration Strength scale. Each level down removes an *entire category* of shared reasons for change. That's why a single intrusive dependency can cause more cascading changes than a hundred contract-based ones.

## Weigh, Don't Count

Back to the proverb. Counting dependencies tells you how many connections exist. Weighing them tells you how much knowledge flows through each one. And it's the knowledge, not the count, that determines whether a change in one component will cascade across your system.

Static analysis tools count because counting is easy to automate. But easy to automate and useful are not the same thing. A metric that treats use of reflection to modify a private field and an API call as equivalent is likely to point you in the wrong direction. Dependencies, like words, should be weighed, not counted.

## P.S.

Found this useful? Share it. Too many teams are still optimizing for the wrong numbers.
