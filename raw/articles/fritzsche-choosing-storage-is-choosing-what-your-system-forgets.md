---
source_url: https://ricofritzsche.me/choosing-storage-is-choosing-what-your-system-forgets/
title: Choosing Storage Is Choosing What Your System Forgets
author: Rico Fritzsche
publication: ricofritzsche.me ("Thinking in Events")
published: 2026-07-29
retrieved: 2026-08-03
type: article
---

# Choosing Storage Is Choosing What Your System Forgets

*State, fact, event, record, and what an event store keeps that a current-state database forgets.*

*(Image licensed under the Unsplash+ License)*

In 1998, Hugh Darwen wrote that a database is best thought of as "a repository not just for data, but rather for facts", for true propositions. In 2012, Rich Hickey said about facts: "You cannot update a fact, because you can't change the past." I agree with both sentences. Every relational database ships with UPDATE, and an UPDATE changes rows. If rows hold facts, and facts cannot change, what does an UPDATE change?

Answering takes four words, held apart: state, fact, event, and record. Each gets a definition that stands on its own, and an example after it. The examples support the definitions; they are no part of them.

Note: The examples use a platform for booking stays, in the style of Airbnb or Booking.com. Hosts publish listings: a place to stay, with a nightly price, a maximum number of guests, and a calendar of nights. Guests reserve nights. A reservation gets confirmed, and it is sometimes cancelled later. Hosts can also block nights in their own calendar, for repairs or private use. That is all the domain knowledge this text needs.

## State

State is what holds at a moment.

The state of a domain does not depend on anyone describing it. It is as it is. A query can read it, a sentence can describe it, and it holds either way. What state does is change: after every happening, a different state holds. One thing state cannot do: a state holds, it never happens. Gilbert Ryle and Zeno Vendler drew this line in their analyses of verbs and time: a state is homogeneous and may extend over time; an event occurs and can culminate. In short form: a state s; after a happening, a later state s′.

An example: On July 28 at noon, one listing is in this condition: the nights of August 10 to 14 are free, the nightly price is 120 euros, the guest maximum is 4. That is state. It holds at noon whether anyone looks at it. When a guest books those nights an hour later, a different state holds: the same listing, the nights now taken.

## Event

An event is something that happened: a change of state at one moment.

Where a state holds, an event occurs, and it occurs once. Georg Henrik von Wright described a change as an ordered pair of states, the one before and the one after: c = (s, s′). The pair leaves a gap, and the gap is the important part: two different happenings can produce the same pair. The states before and after a change do not say which happening lies between them. That meaning belongs to the event: its type says which happening changed the state. The event e is the happening between the two states; its type carries what the pair lacks. What happened must be stated somewhere, or it is lost the moment the new state holds.

*(Two happenings, one pair of states.)*

An example: On July 28 at 14:03, a guest books the nights of August 10 to 14. That is an event. At 14:02 the nights were free; at 14:04 they are taken. The same difference has a second possible cause: the host blocks the same nights for repairs. Free before, unavailable after, in both cases: the calendar's state is the same. Anyone who sees only the calendar cannot tell the booking from the blocked nights. The happening needs its own statement.

## Fact

A fact is a true statement about state and/or causality, bound to the moment it is about.

A fact states one of two things: what held at that moment, or what changed and why. Rich Hickey's definition covers both sides: "an event or thing known to have happened or existed". The event or thing is what the fact speaks about; the knowing is the statement. And every fact carries its time. The word itself began there: factum, Latin, a thing done. In form, a fact is a claim: that a state s held, or that (s, e, s′) is true, the state before, the event, the state after. A claim can be true or false. A fact is a claim that is true.

Because a fact speaks about one moment, it cannot change. Later change makes no statement about a past moment false. Hickey again: "You cannot update a fact, because you can't change the past." New knowledge arrives as a new fact that supersedes the old one, and the old one stays true about its own moment.

An example: "On July 28 at noon, the nights of August 10 to 14 were free" states what held. The booking at 14:03 does not touch this sentence; it speaks about noon, and at noon the nights were free. "On July 28 at 14:03, the reservation for August 10 to 14 was confirmed" states what happened. A cancellation in September will not make it false. The price shows superseding. On August 1, the host raises the nightly price from 120 to 135 euros. "The nightly price is 135 euros, as of August 1" supersedes "the nightly price is 120 euros, as of July 28". Both stay true, each about its own time.

## Record

A record is a fact written into a store: the value a system keeps.

The record is not the fact. The fact is the statement; the record preserves it. The container can be anything that holds records: a ledger book, a current-state database, or an event store. The store decides what may happen to a record. One store appends records and never touches them again. Another overwrites records in place. Overwriting changes no fact, because no operation on a record can reach into a past moment. It destroys the record of a fact, and with it the system's only access to that fact.

*(Overwriting keeps state; appending keeps facts.)*

An example: A confirmed reservation stored as a row in a reservations table is a record. An appended entry ReservationConfirmed with the same content is a record too. The price shows what overwriting costs. On August 1, the price column changes in place from 120 to 135. The fact that 120 euros held through July is untouched; the record of it is gone. In October, a guest who booked in July disputes the charge, and the store cannot show the price that held when the booking happened.

## Three layers

The four words sort into three layers. State and events are in the world: what holds, and what happens. Facts are statements about both, each bound to its moment. Records are what a system keeps. Everything a system knows about state and events, it knows through records. This is why storage deserves its own examination: the store is where facts survive, or where they end. In short form: a state s and a later state s′; a change c = (s, s′); an event e, the happening between them; a fact, the claim that s held or that (s, e, s′) is true. Records fix the facts in a container.

*(State and events are in the world, facts state them, records keep them.)*

## What an event store keeps

An event store appends records and never changes them. The discipline of the record matches the immutability of the fact: written once and true about its moment; later records supersede it.

Each record preserves a fact about one event, and the record carries a type named in the domain's language: ReservationConfirmed, ReservationCancelled, NightsBlocked. The type holds what the state difference loses. A booking and a blocked calendar leave the same difference behind; ReservationConfirmed and NightsBlocked are different records, and the distinction survives. Martin Fowler's domain event "captures the memory of something interesting which affects the domain", and it carries two times: the moment the happening occurred and the moment the system learned of it. The two can differ, and both belong to the fact.

Current state is derived. Greg Young: "Current State is a Left Fold of previous behaviours." Start from nothing, apply every recorded event in order, and the result is the state as it stands. Event Sourcing names the decision to make event records the authoritative record and to treat every current value as derivable from them. It is a storage decision. Thinking in events does not depend on it.

One neighbor clarifies the boundary. Datomic appends records of facts without domain types. Its documentation calls each record, the datom, an "immutable atomic fact": an entity, an attribute, a value, a transaction. A store of this kind is a fact store. The domain-named type is what turns a fact store into an event store. The type adds the meaning: which happening changed the state.

## What a current-state database keeps

Hugh Darwen, writing in the relational tradition with C.J. Date, describes a database as "a set of propositions (assumed to be true ones)". A table heading is a predicate; each row fills in the blanks and makes one statement. Read this way, every row of a current-state database states what holds now. The price is 135 euros. The night of August 12 is unavailable.

That is state, stored directly, and here the opening question resolves. An UPDATE changes a record and nothing else. The fact that held before still holds about its moment; its record is destroyed. The happening that caused the change is never written down at all: the calendar says unavailable and stays silent on whether a guest booked or the host blocked. Rich Hickey calls the habit behind this place-oriented programming, "new information replaces old", and traces it to a time when memory was scarce and overwriting was how systems coped.

A current-state database answers one question: what holds now. What held on July 28 left with its records. What happened at 14:03 was never written down.

The dividing line runs through the discipline of the record, and nowhere else. A relational table written append-only keeps facts. Accountants have run their books this way for centuries: one entry per change, corrections as new entries, totals derived. An event log that someone edits in place keeps state under a misleading name. Overwritten records keep state. Appended records keep facts.

## Why hold the words apart

The questions a business asks later are questions about facts and events. Why is this night unavailable? What price did the guest agree to at booking time? Who cancelled the reservation, and when? A store can answer them only while the records that carry the answers exist.

Choosing storage is choosing what the system may forget. A current-state database forgets superseded facts and all happenings; for values whose history nobody will ask about, that is a fair trade. An event store forgets nothing it recorded, and the cost is derivation: current values must be computed from the records. Both choices are legitimate. With the four words held apart, the choice is made knowingly, and the debate about it gets shorter.

Cheers!

### Sources
- Rich Hickey, The Value of Values (talk, GOTO Copenhagen 2012).
- Hugh Darwen, What a Database Really Is: Predicates and Propositions, 1998; the repository sentence quoted in the opening is from C.J. Date's preface.
- Martin Fowler, Domain Event.
- Greg Young, Functional Domain Models and Event Sourcing, 2012.
- Stanford Encyclopedia of Philosophy, Events; the state/event classification traces to Gilbert Ryle (The Concept of Mind, 1949) and Zeno Vendler (Verbs and Times, 1957).
- Datomic Documentation, Data Model.
- Online Etymology Dictionary, fact.
- Ralf Westphal, When to record an Event
