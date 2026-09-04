---
source_url: https://ricofritzsche.me/how-event-sourcing-grows-with-the-business/
title: How Event Sourcing Grows With the Business
author: Rico Fritzsche
publication: Rico Fritzsche (ricofritzsche.me)
published: 2026-08-30
retrieved: 2026-09-02
type: article
---

# How Event Sourcing Grows With the Business

Immutable Data, Domain Capabilities, and an Additive Schema

By Rico Fritzsche in Software Engineering — 30 Aug 2026

*[Image: title image — "How Event Sourcing Grows With the Business", licensed under the Unsplash+ License]*

The database schema is the answer to a question that usually cannot be answered at the start of development. Tables that were originally intended to store only data records often end up with additional status, audit, and date columns over time. This is the typical outcome when modeling begins with an entity-centric approach and it is gradually realized that the business has a process.

[In my last article,](https://ricofritzsche.me/why-the-entity-model-is-an-illusion/) I wrote about how much entity-centric thinking has shaped software development over the past few decades. This approach contrasts with process-oriented approaches, which focus on business events. In the entity-centric approach, more or less rigid data structures define the business. In many cases, this leads to thinking in terms of typical database operations—Create, Read, Update, and Delete (CRUD)—because the behavior is tied to a data structure that must be kept up-to-date and consistent. As a result, the focus quickly shifts away from business processes and the domain language.

I will continue to use the example from the car rental industry that I discussed in my last article. Upon closer, process-oriented examination, the typical, general, database-oriented requirement “Create something” broke down into four steps:

```
Acquire → Receive → Infleet → Release
```

This article adds a step after the system is already up and running:

```
Acquire → Receive → Inspect → Infleet → Release
```

That shows how systems in the real world emerge and grow, and it lets you count what has to change and what does not.

## The Problem of Mutable Data

In many applications, the database schema takes center stage. At this point, I no longer distinguish between the data model in the database and the so-called domain model in the code. They are two representations of the same thing. As soon as an ORM maps the object to a row, both have the same operations, and both are based on the idea of adding, updating, or deleting data.

Systems built this way rely on redundancy—duplicating the same schema and, for every operation, loading data into memory, mutating it, and then writing it back to the physical data storage. This raises the legitimate question: Why not just do this directly in the database? Rules alone do not justify an application around a few tables; modern databases can enforce constraints too, and a thin CRUD app can expose the tables over HTTP. The only question is whether the business consists of such operations. The vehicle from the last article initially looked like that.

CRUD is based on the principle of maintaining the most recent state. This most recent state must fit completely within the schema at all times. As a result, the schema must be constantly modified. I know we have good tools to manage this. But it introduces technical dependencies into development that we actually wouldn’t need at all if data were fundamentally immutable.

A table, such as “Vehicle” from my last article, with columns—including a status column—encodes, in one place, the possible states and the data associated with a vehicle. Pat Helland explained in 2015 why this is necessary: Normalization exists to prevent update anomalies. A schema designed to handle updates must therefore be complete before the first record is written. This is not necessary for immutable data.

## Too Late for the Schema

The problem is that development almost always begins with assumptions. As I pointed out in my last article, one might well think that a new vehicle simply needs to be created as a data record in the system. But that’s not how it works. Three decades of experience have shown this time and again. Even if the expert thinks we just need to create the vehicle record and doesn’t mention status transitions, these eventually come to light because it becomes clear that the process wasn’t mapped at all. What happens then? You start adding columns to the table—such as date columns showing when the vehicle was ordered, when it was delivered, and so on.

Some people will surely say: So what? That’s simple. Just business as usual, so to speak. Technically speaking, I agree. But the process isn’t visible. No one can tell from the schema in what order the date columns are filled or which ones are allowed to remain empty. That’s specified in the code, scattered across all the places where the table is written. Every new step is a change to a shared structure, because the database represents a global, shared, mutable state.

*[Image: Figure 1: Table versus event types over three revisions.]*

Martin Kleppmann made this point back in 2014: developers have long since done away with global variables, but the database is one giant global variable. The typical discovery made when dealing with a business comes too late for the centralized schema. Always!

## Event Modeling

The solution is to take a truly iterative approach: talk to the domain experts about their business in their language, identify and model domain events, and implement them in small, manageable units. Event modeling offers the right approach here. Adam Dymitruk described the method in 2019. You create a timeline and use the domain language to document what happens in the process: a vehicle was procured, it was delivered, it was added to the fleet, it was made available for rental. Only then does the question arise as to which action triggers an event and who wants to see what information afterward. Every action that leads to an event is a domain capability. *ReceiveVehicle* is one; *InfleetVehicle* is another.

The names come in pairs. For example, the capability *InfleetVehicle* produces the *VehicleInfleeted* event, and the *InspectVehicle* capability produces the *VehicleInspected* event.

*[Image: Figure 2: The names come in pairs.]*

A domain capability is one ability a domain provides. This capability is implemented as a Request Processing Unit (RPU). In this article I stay with *capability*, because the point here is what the domain can do and what data it keeps, not how the unit is built.

These can be implemented without everything having to be known in advance. *AcquireVehicle* can be built and delivered before anyone knows what the release for rental will look like later. The data structures then each refer to a capability and are immutable.

## The Fold

Each domain capability comes with its own command context. The context defines the scope and what is needed to process a request. To get the relevant context from the Application State (the immutable chronologically ordered sequence of events), the capability has to query a relevant list of events and derive the state from it. This functional operation is called a fold: the chronological list of events is gradually reduced to a single, current state.

Greg Young wrote in 2012: *"Current State is a Left Fold of previous behaviours."*

```csharp
var state = events.Aggregate(InfleetState.Empty, (s, e) => e switch
{
    VehicleReceived r => s with { Received = true, Vin = r.Vin },
    VehicleInfleeted  => s with { Infleeted = true },
    _                 => s
});
```

For *InfleetVehicle*, the only relevant information is whether the vehicle has been delivered and whether it is already in the fleet. The derived state does not need to know anything else in this context, because that information is not required to process the command. Events that the rules do not read are not taken into account. The state exists for as long as the command is being processed: it is created, the rules are applied to it, and the result is one or more new events.

For *ReleaseVehicleForRental*, different information is required in the state, which means the fold is based on different event records, even though both could, in principle, read the same events. There is no shared vehicle object that both would need to share.

## The Fifth Step

For events, the schema consists of a set of event types, and that set only grows. A new process step represents an addition; existing facts do not need to be reinterpreted. Adding *VehicleInspected* involves defining an event type, implementing a new specific function, and modifying existing functions only if the information is relevant to the context. This could be *InfleetVehicle*, for example.

```csharp
// fold in InfleetVehicle
    VehicleReceived r => s with { Received = true, Vin = r.Vin },
    VehicleInspected  => s with { Inspected = true },              // new
    VehicleInfleeted  => s with { Infleeted = true },

// rule in InfleetVehicle
if (!state.Received)  return Rejected("vehicle_not_received");
if (!state.Inspected) return Rejected("vehicle_not_inspected");  // new
```

To integrate the event into an existing capability, you simply need to adjust the fold so that the state contains this new information, allowing the processing to work with it. *AcquireVehicle* and *ReceiveVehicle*, on the other hand, remain unchanged, since they do not require the information from the new event type.

*[Image: Figure 3: The timeline with the inserted step.]*

Event records are persistent and accumulative, not subject to deletion or overwriting. Rich Hickey put it this way in 2012, referring to accounting, court records, and any other record that is meant to be trusted. This is the mechanism on which growing systems should be based.

Extending a domain to include additional capabilities does not alter existing event records. They do not become invalid as a result. In the case of our “Vehicles” domain, this means that vehicles already in the fleet simply do not have a *VehicleInspected* event. The “Fold” function must, if necessary, account for this omission in the function where this information is required. For vehicles already added to the fleet, however, this information is no longer relevant because the *InfleetVehicle* process step has already been completed. New vehicles that have been delivered but not yet added to the fleet must now wait for inspection, which was the intent of this process step.

This eliminates the need for data migration, since there is nothing to correct. By that I mean the stored data; it is not necessary to rewrite events or enter them retroactively. A projection for displaying the inspection, on the other hand, is new code with its own rebuild, and the functions do not depend on it. For a status column, however, you must specify which of the new values should be assigned to the individual old rows.

The reason why extending an application with new process steps is so simple is easy to see: each function derives its own state from the events. The autonomy of the functions and the immutability of the events are two sides of the same coin: events are additive, since no reader needs to know the big picture. Functions, on the other hand, remain small because they derive their specific perspective precisely from the events.

## History Is a Consequence, Not a Cause

In my experience, the use of event sourcing is often justified on the grounds that it provides a complete history. Conversely, it is argued that event sourcing would not be necessary if a history were not needed. I consider this to be fundamentally wrong. Why? Because the fact that the history is preserved is a consequence of that very property, but it is not the reason for it. Anyone who views event sourcing as an audit function has misunderstood its purpose.

For me, the real motivation is to provide domain capabilities that are independent of one another and not tied to a central, shared data structure. At the same time, this avoids entity-oriented thinking. By using events, the domain language is brought to the forefront, and the actual processes become apparent.

In the example, we saw that adding a new domain capability—via a new command, a new event type, and new logic—is done autonomously and with minimal risk, without having to modify existing functionality. This is only necessary if the new event is required within an existing capability to extend the context-bound state. This intervention is minimal. Extensions are therefore additive. Schema migrations, as we know them from centralized, entity-based systems, are not required. It was therefore not necessary to modify existing data in order to introduce a new capability.

*Cheers*!

Sources and Links:

- Pat Helland, [Immutability Changes Everything](https://queue.acm.org/detail.cfm?id=2884038) (CIDR 2015, reprinted in ACM Queue)
- Martin Kleppmann, [Turning the database inside-out](https://martin.kleppmann.com/2015/03/04/turning-the-database-inside-out.html) (transcript of the 2014 Strange Loop talk)
- Rich Hickey, [The Value of Values](https://www.infoq.com/presentations/Value-Values/) (GOTO Copenhagen 2012, InfoQ recording)
- Adam Dymitruk, [Event Modeling: What is it?](https://eventmodeling.org/posts/what-is-event-modeling/) (June 2019)
- Greg Young, [Functional Domain Models and Event Sourcing (October 2012)](https://gregfyoung.wordpress.com/2012/10/01/functional-domain-models-and-event-sourcing/)
