---
source_url: https://www.linkedin.com/posts/goeleven_today-id-like-to-explain-my-default-approach-activity-7096075346311016448-g2BW
title: "Default approach to designing interaction between capabilities (Aggregate, Outbox, Projection)"
author: Yves Goeleven
publication: LinkedIn
published: 2023-08-15
retrieved: 2026-06-14
type: article
---

# My default approach to designing the interaction between capabilities

**Yves Goeleven** — *LinkedIn post (2023), part of his "fantastic 9" patterns series on implementing
event-sourced capabilities (MessageHandler infrastructure). Captured via logged-in Chrome.*

---

Today I'd like to explain my default approach to designing the interaction between capabilities that
are further apart in a value stream (where eventual consistency is not a problem). Over the past few
days I already talked about keeping write operations atomic, and treating events as business
decisions. Combining these concepts together with two of my fantastic 9, results in the interaction
design for many of these capabilities.

**Event Sourced Aggregate Root** — The first of my fantastic 9. It has the responsibility to decide
how the system should respond to a command requested by a user. This command is often exposed as an
HTTP API (consumed by the UI components of the capability). The decisions taken by the Aggregate Root
are captured as events, and written to an Azure Storage Table. This is done in a single operation,
even when multiple events are emitted, using a so called entity group transaction.

**Outbox** — As an extension to the event store, there is a message pump, called the outbox. This pump
reads the events from the store and forwards them in a single operation (called batch) to, e.g. an
Azure Service Bus topic, which in turn is responsible to distribute the events across the system. This
pump does need to remember the position read from the event store, and as a consequence has to perform
a second write operation. Should either the first or second write operation fail, then the outbox will
retry the send operation at a later point, ensuring at least once delivery of the messages.

**Atomic message processing** — Next to Event Sourcing, my infrastructure (called MessageHandler) also
comes with an atomic processing engine, which takes care of performing receive and send operations in
an atomic fashion. Within its processing scope, represented by a handler, there is room to perform
exactly one more write operation. Should this operation fail, e.g. a transient exception is thrown,
then the received message will be abandoned and retried.

**Projection** — The second fantastic 9 pattern in this design. It's one of the most common operations
performed in the scope of a handler. It has the responsibility to roll up one or more events from the
event store and turn them into a single state object. This state object can then be stored in a
database of choice in a single operation without the need for transactions on the target data store.
This approach has the added benefit that you can use any database, storage, cache, big data or
cognitive service available in azure. And you don't have to limit yourselves to one either. When using
an azure service bus topic, or event hub, you can attach multiple projections in parallel, and as such
achieve polyglot persistence in your system.

---

*Notable comment exchange — Dragan Stepanović: "Events produced in a bounded context most often should
not be modelled as integration events between bounded contexts. Otherwise, semantical level of coupling
between bounded contexts is the same as if they were accessing the same database." Yves Goeleven: "This
is 100% true. A contract between the capabilities is required... It's the same when you choose a data
store or a UI component as an integration point." (On projections composing events across aggregates,
Yves: "when using events it is typically the consumer [who owns the relationship], but when using state
it might be the producers.")*
