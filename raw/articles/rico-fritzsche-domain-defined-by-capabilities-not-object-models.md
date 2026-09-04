---
source_url: https://ricofritzsche.me/why-the-domain-is-defined-by-domain-capabilities-not-object-models/
title: Why the Domain Is Defined by Domain Capabilities, Not Object Models
author: Rico Fritzsche
publication: Rico Fritzsche (ricofritzsche.me) — also Level Up Coding / gitconnected
published: 2026-06-17
retrieved: 2026-06-19
type: article
---

# Why the Domain Is Defined by Domain Capabilities, Not Object Models

Additive Domain Evolution Through Autonomous Capabilities

By Rico Fritzsche in Event Sourcing — 17 Jun 2026

*Photo by KeepCoding on Unsplash*

After publishing my last article about Request Processing Units / Reactors, I noticed that some parts were probably harder to understand than I expected. Especially the project structure led some developers to mentally map the approach back to horizontal layered architectures and centralized technical ownership, even though the architectural cut is fundamentally different.

It is important to recognize that layering and Separation of Concerns (SoC) are not the same thing. Layered architectures separate software through centralized technical ownership. One domain capability becomes physically fragmented across controllers, services, repositories, entities, mappers, and persistence models. Understanding what a single capability actually does means traversing multiple technical abstractions spread across the entire system.

The approach I described applies a completely different cut. The domain capability itself becomes the primary ownership boundary. The full processing of one capability lives in one place, including the localized imperative shell around loading and persisting facts as well as the functional core responsible for context interpretation, business decisions, and consequence generation. The technical separation exists locally inside the Request Processing Unit (RPU) itself instead of globally across centralized technical layers.

This distinction sounds subtle at first, but it changes the coupling structure of the entire system. And I increasingly believe this is the actual architectural shift behind the approach, far more than the terminology around RPUs or Reactors themselves.

*This article was originally published here:* https://levelup.gitconnected.com/why-the-domain-is-defined-by-domain-capabilities-not-object-models-8921b454c2cd

### Distributed Technical Ownership

One thing became very obvious while discussing the architecture with others: many developers instinctively equate Separation of Concerns with layering. This is understandable because most software architectures of the last decades taught us exactly that. Controllers handle transport concerns, services contain or coordinate logic, repositories access persistence, entities represent the domain model, and mappers translate between structures. The domain capability itself emerges only as the combined result of all those technical parts.

*In typical layered, object-oriented architectures, one domain capability is processed across multiple technical ownership boundaries. The capability emerges through the cooperation of controllers, services, domain models, repositories, mappings, and persistence structures distributed throughout the system.*

This creates a very specific ownership structure inside the system. The technical layers own different aspects of the capability, which means the capability itself becomes physically fragmented across the architecture. To understand what 'register a tool' actually does, it is necessary to traverse multiple technical ownership boundaries spread across the system.

In other words, layered architectures are systems of distributed technical ownership. The system is organized around technical ownership boundaries instead of autonomous domain capabilities. A single capability therefore does not exist as one coherent ownership boundary but is reconstructed through cooperation between multiple technical structures.

The consequence is not only additional indirection or functional dependencies. The much bigger consequence is coordination pressure. Every new domain capability partially integrates into already existing technical structures, shared abstractions, dependency inversions, entity models, and repositories. Over time these shared ownership centers become bottlenecks because many otherwise independent capabilities continuously depend on the same structures evolving together.

Vertical Slice Architecture already moved software structure significantly toward domain capabilities instead of purely technical layers. But the architectural center frequently remains shared internal ownership structures underneath the slice itself.

The feature or request becomes the organizational boundary of the project structure while the actual processing of the domain capability is still reconstructed through multiple internal coordination boundaries. The capability therefore remains structurally distributed even though the packaging appears vertical.

### Localized Capability Ownership

Autonomous domain capabilities in the form of RPUs apply a fundamentally different ownership model. I also described this shift from another perspective in this article Why I Replaced Enterprise OOP Thinking with Feature-Local Logic. The primary boundary is no longer the technical layer but the domain capability itself. An RPU owns the complete processing of one domain request, including loading relevant facts, building the command context, evaluating business rules, generating consequences, and persisting the resulting facts. The architecture applies a localized Functional Core / Imperative Shell structure inside each capability boundary where pure business decisions and infrastructure concerns remain clearly separated without fragmenting the capability itself across the system.

*The RPU becomes the primary ownership boundary of the domain capability. The Imperative Shell encapsulates infrastructure and IO concerns, while the Functional Core focuses on context interpretation, business rules, and consequence generation. Note: Solid arrows represent the internal data flow of the capability. Dashed arrows represent interaction with external infrastructure such as the Event Store or optional Providers.*

The practical consequence is that understanding one domain capability no longer requires traversing large parts of the system. The complete processing remains localized in one place. To understand how a tool is registered for instance, the developer opens the *register_tool* RPU folder. The structure remains simple because the capability itself is the ownership boundary instead of being reconstructed through multiple technical structures distributed across the system.

*RPU folder structure example*

The important distinction is that Delivery Mechanisms, Reactors, and Providers do not become ownership centers of the domain capability itself. They exist to connect, coordinate, or translate, but they do not absorb the domain decision boundary.

External interactions such as HTTP requests, CLI commands, or incoming messages are translated into internal domain requests and transformed back into client-compatible responses. A Reactor coordinates data flow when one interaction requires several domain capabilities or external systems to participate together. Providers encapsulate access to infrastructure and external resources.

None of these structures define the domain capability itself. The domain remains centered around autonomous capabilities interpreting facts and producing consequences independently within their own decision boundaries.

The domain itself behaves as a functional core. Application state is not stored as mutable object graphs continuously coordinated across the system. Instead, the state is derived from an immutable sequence of recorded facts inside the Event Store.

This changes how the domain evolves over time. New capabilities emerge as independent processing units without continuously restructuring a centralized mutable domain model.

### User Interactions and Domain Capabilities Are Different Things

One of the most important distinctions in the RPU approach is the separation between user interactions and domain capabilities. Both are frequently treated as the same thing in software architecture even though they describe completely different concerns.

A user interaction describes how the outside world engages with the system. It starts with an external trigger such as an HTTP request, a UI action, a CLI command, or an incoming message and ends when the system returns a response. User interactions are shaped by presentation concerns, workflows, client requirements, transport protocols, and user experience.

A domain capability describes something fundamentally different. It defines one autonomous business decision boundary inside the system. A capability owns the complete processing of one specific business responsibility including interpreting relevant facts, evaluating business rules, and producing consequences. In other words, all business rules are encapsulated within the domain as a whole. Not in aggregates, but in the domain. That is precisely where the problem with Domain-Driven Design lies.

Treating user interactions and domain capabilities as the same architectural unit creates large coordination structures almost automatically. One user interaction frequently combines multiple domain capabilities, external systems, validation steps, data loading operations, and response transformations. When all of that becomes one architectural ownership boundary, the result is usually a large handler, application service, workflow object, or aggregate orchestration layer where business meaning slowly accumulates again.

The RPU approach separates those concerns intentionally.

- User interactions remain external interaction boundaries.
- RPUs remain internal business capability boundaries.
- A Reactor may coordinate several capabilities when one interaction requires multiple processing steps, but the participating RPUs still own their business decisions independently.

This distinction is important because user interactions and domain capabilities evolve for fundamentally different reasons. A frontend workflow or external API may change completely while the underlying business capability and decision boundary remain stable. Separating both prevents external interaction structures from becoming the ownership model of the domain itself.

### Why Delivery Mechanisms, Reactors, and Providers Are Not Layers

Delivery Mechanisms, Reactors, and Providers can superficially resemble presentation layers, service layers, and infrastructure layers from traditional architectures. But the ownership model underneath is fundamentally different.

In layered architectures, horizontal structures participate directly in the ownership of every domain capability. Controllers, services, repositories, aggregates, and orchestration structures collectively reconstruct the capability through cooperation across the system. The capability itself therefore does not exist as one autonomous ownership boundary.

Delivery Mechanisms, Reactors, and Providers do not participate in the ownership of the domain capability itself. The capability already exists fully inside the RPU. Fact loading, command-context construction, business rules, consequence generation, consistency evaluation, and persistence flow remain localized inside the capability boundary.

*A Delivery Mechanism translates external requests into internal domain requests and transforms the resulting domain responses back into client-compatible responses. The domain capability itself remains fully owned by the RPU.*

A Delivery Mechanism translates an external interaction into an internal domain request and transforms the result back into a client-compatible response. The interaction boundary itself remains capability-local instead of becoming a shared horizontal structure such as *UserController* or *ToolController*. A *RegisterToolHttpHandler* belongs only to the *register_tool* capability and does not become a shared ownership structure for unrelated capabilities.

Reactors also do not become centralized orchestration layers where displaced domain logic accumulates. A Reactor coordinates already autonomous domain capabilities when one user interaction spans multiple decision boundaries. The participating capabilities continue to own their business decisions independently.

Providers encapsulate infrastructure access without containing knowledge about the domain capability being processed.

Layers participate in the ownership of every capability horizontally across the system, and that is where the difference lies. Delivery Mechanisms, Reactors, and Providers remain peripheral to already complete domain capabilities.

### Conclusion

The important shift behind the RPU approach is not new terminology or another variation of feature-oriented packaging. The deeper shift is the representation of the domain itself.

The domain no longer acts as a shared mutable object model continuously coordinated across repositories, services, aggregates, and orchestration structures. Autonomous domain capabilities interpret immutable facts, evaluate business rules, and produce consequences within localized decision boundaries. The domain therefore behaves as a deterministic functional core instead of a centralized mutable structure.

This changes how systems evolve over time. New capabilities emerge as independent processing units instead of continuously extending shared behavioral centers and coordination structures. The system grows additively through autonomous domain capabilities that remain locally understandable, independently evolvable, and directly aligned with real domain responsibilities.

*Cheers*!
