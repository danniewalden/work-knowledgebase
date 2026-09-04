---
source_url: https://ricofritzsche.me/thinking-in-events/
title: Thinking in Events
author: Rico Fritzsche
publication: ricofritzsche.me (Thinking in Events / Software Architecture)
published: 2026-07-03
retrieved: 2026-08-07
type: article
---

# Thinking in Events

Separating the Modeling of What Happened from the Decision of How to Store It

BY RICO FRITZSCHE IN SOFTWARE ARCHITECTURE — 03 JUL 2026

Most software projects do not struggle because a team cannot persist data, expose an endpoint, or build a form. They struggle when a business situation is translated into technical structure too early.

A booking system is a good example. From the outside, it looks simple: someone finds a place, reserves it, pays for it, and arrives. But the simplicity disappears as soon as the real rules enter the conversation. Availability changes while people are searching. Prices depend on dates, policies, fees, and conditions. A reservation can be canceled, modified, rejected, confirmed, expired, or disputed. Each of these situations has a different meaning for the business.

The problem is not complexity alone. The problem is losing the language that explains the complexity. A conversation about reservations, availability, guests, hosts, payments, stays, and cancellations slowly turns into records, fields, flags, status columns, handlers, and database operations. Step by step, it becomes increasingly difficult to understand the intent behind the data.

This is where architecture discussions can drift from the actual problem. We talk about layers, ports, adapters, repositories, entities, services, messages, and storage patterns. Yet none of these fix a weak understanding of the domain. They only give shape to whatever understanding already exists.

Event Modeling is interesting because it starts from a different place. It helps a team describe an information system through business events, decisions, user intentions, and views over time. It keeps the conversation closer to the people who understand the domain before the implementation starts to dominate the language.

But Event Modeling is also easy to misunderstand. Thinking in events does not automatically mean that the system must be implemented with Event Sourcing. One is a modeling discipline. The other is an implementation choice. Confusing both turns a useful way of thinking into another technical prescription.

This article is about that distinction. It is about Event Modeling as a way to move from technical data operations to business behavior, and about why that shift is valuable even when the final implementation is not Event Sourcing.

## What Event Modeling Is

Event Modeling describes an information system by following how business facts unfold over time. It does not start with the internal shape of the software. It starts with examples of the business in motion and asks which facts become true as the system is used.

Adam Dymitruk describes this with a hotel booking example: imagine the system already exists and ask which facts would have been captured as time moves forward. The model then adds what users see along the way, so the discussion stays connected to the actual use of the system instead of disappearing too early into internal structure.

A reservation does not simply get updated; different business facts can happen after it is confirmed.

The timeline is not an implementation flow. It is a way to keep order and meaning visible. A reservation is confirmed before it can be changed. A reservation can be canceled by a guest, host, or platform. A no-show is not the same situation as a cancellation. These distinctions matter because they carry different rules, authority, timing, and consequences.

Events in Event Modeling are facts, not technical messages by default. ReservationUpdated is weak because it says that something changed, but not why it changed. It hides the difference between a guest changing dates, a host canceling a reservation, support correcting a mistake, or the platform marking a guest as a no-show. These situations may affect similar stored data, but they do not describe the same business fact.

This is the deeper problem with generic update language. It preserves the mutation and loses the reason. The model no longer shows which situation occurred, which rule made it valid, and which later behavior depends on it. ReservationCanceled, CheckInDateChanged, or ReservationMarkedAsNoShow keep the domain distinction visible.

The building blocks of Event Modeling are deliberately simple: events, views, commands, automations, and external systems. Their value is not in the notation itself. Their value is that they connect user-visible information, intent, fact, and consequence in one shared description. Adam's process makes this order clear: first collect business events, arrange them on a timeline, then add what users see, what they do, and which information supports those steps.

Event Modeling is related to Event Storming, but it serves a different purpose. Event Storming is mainly used to explore the problem space. Event Modeling takes the discovered behavior and describes how the system should work over time. The distinction matters because discovery and system description are related, but they are not the same activity.

## Business Language Comes Before Technical Structure

A software model is already a translation. The question is where that translation starts. If it starts with tables, endpoints, DTOs, entities, or generic operations, the business language is already being compressed into technical structure. That structure may be necessary later, but it is a poor starting point for understanding the domain.

Domain experts do not only provide requirements. They provide the vocabulary that makes the requirements precise. In a booking domain, words such as reservation, guest, host, property, listing, availability, check-in, check-out, cancellation, no-show, refund, and stay are not labels added for nicer screens. They separate situations that have different rules and consequences. Booking.com distinguishes reservation changes, cancellations, no-shows, guests, properties, check-in and check-out. Airbnb's help material uses reservation, host, guest, listing, stay, cancellation, refund, and check-in in the same business area.

This is close to the idea behind Ubiquitous Language in Domain-Driven Design. As Martin Fowler has summarized it, the goal is building a "common, rigorous language" between developers and users. The word rigorous is important. Shared language is not a soft communication exercise. Software does not handle ambiguity well, and business ambiguity does not disappear because the code compiles.

A generic word like update damages that rigor. It says that stored data changed, but it does not say which business situation occurred. A guest changing the check-in date, a host canceling a reservation, a property marking a guest as a no-show, and support correcting a wrong detail can all touch reservation data. Treating these cases as one update makes the model easier to implement too early and harder to understand afterwards.

Generic update language preserves the data change but loses the business reason.

Business language also protects the boundary of a decision. A cancellation is not just a different value in a status column. It may depend on who cancels, when the cancellation happens, which policy applies, whether payment has been captured, and whether a refund is due. A no-show has another meaning. A date change has another meaning again. These differences are not implementation details. They are the reason the system exists.

Technical structure should support that language instead of replacing it. Once the team understands the business situations clearly, it can still choose tables, documents, messages, projections, workflows, or an event store. But the choice then follows from the behavior that needs to be supported. It is no longer the vocabulary that defines the domain.

## How Event Modeling Changes the Conversation

The practical value of Event Modeling is not that a team writes events on a wall. Its value is that the conversation changes before the technical design hardens.

Instead of starting with the shape of the data, the team follows a concrete scenario through time. Which information does the guest see before making a reservation? Which rule decides whether the reservation can be accepted? Which fact becomes true after the decision? Which view changes afterwards? Which person or external system has to react?

This exposes gaps that a technical model can hide for a long time. A table can contain a status column without explaining who is allowed to change the status, when the change is valid, or which consequence follows. A generic handler can accept a request without making the business difference visible. An Event Model is less forgiving because every fact has to stand in the timeline and explain its place.

A cancellation is a good example. Once the model names the fact, the next questions become concrete. Who canceled the reservation? Was it the guest, the host, or the platform? Did it happen before or after the free cancellation period? Does the property become available again? Is a refund due? Does anyone need to be notified? These questions are not technical details. They are the behavior of the system.

The same applies to a no-show, a date change, a payment failure, or a reservation that cannot be honored by the property. Each situation creates a different path through the business. Event Modeling helps the team see these paths before they are compressed into fields, flags, and handlers.

This also makes the conversation easier for domain experts. They do not need to understand the internal structure of the software to challenge the model. They can look at the timeline and say whether the sequence is correct, whether a rule is missing, or whether a situation has been described with the wrong word.

Technical design is still needed. Event Modeling does not remove database schemas, APIs, transactions, workflows, or storage choices. It gives those decisions better input. Once the behavior is visible, the team can decide how to implement it without pretending that the implementation structure is the domain.

## Thinking in Events Does Not Require Event Sourcing

Event Modeling and Event Sourcing fit well together, but they are not the same thing. Event Modeling describes behavior. Event Sourcing decides how state is persisted.

Event Modeling names the facts; Event Sourcing makes the fact history authoritative.

This distinction is easy to lose because both use events. In an Event Model, an event is a business fact used to describe the system. In Event Sourcing, events become the stored history from which application state is derived. Fowler's definition is strict: Event Sourcing means that all changes to application state are stored as a sequence of events, and that this sequence can be used to reconstruct past states.

That is a persistence decision with consequences. The event store becomes the authoritative record of state. Event Sourcing means storing the full series of actions in an append-only store instead of storing only current state in a relational database. The store acts as the system of record.

Event Modeling does not require that decision. A model may contain facts such as ReservationConfirmed, CheckInDateChanged, or ReservationCanceled, while the implementation still writes current reservation state to relational tables. The model can guide the naming of operations, the boundaries of decisions, the views users need, and the consequences that follow. None of that forces events to become the source of truth.

Adam Dymitruk makes this separation directly in his work on traditional systems:

"Events happen - whether we store them or not is our choice."

That sentence is the clean boundary. The business may contain meaningful facts even when the system does not persist those facts as an event log. Adam's article shows Event Modeling applied with table storage and explicitly separates the modeling approach from the event-sourced implementation style.

A booking example makes the difference concrete. If a guest cancels a reservation, the model can name the fact as ReservationCanceled. One implementation may append that event to an event store and derive the current reservation view from it. Another implementation may update a reservation row, store cancellation details, release availability, and record an audit entry. The model is still useful in both cases because it keeps the business fact visible.

The decisive question is where authority lives. If the event history is the authoritative application state, the system is using Event Sourcing. If the current tables are authoritative and events only appear in the model, logs, messages, audit trails, or integration notifications, the system may be event-aware or event-driven, but it is not Event Sourcing.

This distinction keeps Event Modeling useful outside the Event Sourcing community. A team can use events to understand the domain without accepting the operational and design trade-offs of an event-sourced system. Event Sourcing may still be the best implementation in some cases, especially when history, auditability, temporal reasoning, and derived views are central. But it should be chosen because the system benefits from events as the source of truth, not because the team used events to understand the business.

Event Sourcing becomes especially compelling when the team needs strong auditability, the ability to reconstruct past states, or independent read models that can evolve separately from the write path.

## Conclusion

Event Modeling should improve the storage decision, not replace it. Once the team has described the business facts, decisions, views, and consequences, it can choose how state should be persisted. That choice may be Event Sourcing. It may also be relational tables, document storage, projections, workflow state, or a combination.

A booking system can expose explicit behavior such as canceling a reservation, changing the check-in date, confirming payment, or marking a guest as a no-show, while still storing current reservation state in relational tables. The model remains valuable because it keeps the behavior visible. The implementation only becomes a problem when these behaviors collapse back into one generic update operation.

The reverse is also true. An event store does not guarantee a good model. If the stored events are named ReservationUpdated, GuestUpdated, or PropertyChanged, the system may technically use Event Sourcing while still preserving a CRUD-shaped understanding of the domain. Storing vague events only preserves the vagueness permanently.

Event Sourcing becomes a serious option when the factual history is valuable as the authoritative application state: for auditability, temporal reasoning, reconstruction of past state, independent read models, or a clear record of why state changed. These benefits come with costs. Events are long-lived facts. Projections, queries, concurrency, and versioning need explicit design.

The storage decision should follow from those needs. Event Modeling helps reveal them, but it should not smuggle in the answer. Its first job is to make the behavior clear. The implementation should preserve that clarity instead of turning the model back into anonymous data mutations.

Cheers!

## Sources
- Adam Dymitruk: Event Modeling: What is it?
- Adam Dymitruk: Event Modeling Traditional Systems
- Event Modeling: About Event Modeling
- Martin Fowler: Ubiquitous Language
- Martin Fowler: Event Sourcing
- Microsoft Azure Architecture Center: Event Sourcing pattern
- Software Engineering Radio: Martin Dilger on Understanding Event Sourcing
- Booking.com Partner Help: Handling cancellations and guest requests
- Booking.com Partner Help: Marking guest no-shows at your property
- Airbnb Help Center: Cancel your home reservation as a guest
- Airbnb Help Center: Rebooking and refund policy for homes
- Airbnb Help Center: If your host cancels your home reservation
