---
source_url: https://ricofritzsche.me/why-your-software-cannot-explain-its-business-decisions/
title: Why Your Software Cannot Explain Its Business Decisions
author: Rico Fritzsche
publication: ricofritzsche.me ("Thinking in Events") — originally on Medium
published: 2026-07-23
retrieved: 2026-08-03
type: article
---

# Why Your Software Cannot Explain Its Business Decisions

*Make the path from command to outcome explicit in the architecture. How you store state, relational or event-sourced, is a separate decision.*

*(Image licensed under the Unsplash+ License)*

A guest asks to cancel a reservation. The application accepts the command, releases the dates, and records the reservation as cancelled. Later, someone challenges the decision, claiming that the cancellation period had already ended. Explaining the outcome now requires more than reading the current state. We need to know which context was considered, which rule applied, and whether that context was still valid when the outcome was recorded.

After more than 30 years of building and changing production systems, I have learned to distrust architectures that make the resulting state easier to find than the decision that produced it. The weakness becomes visible when a rule changes, concurrent requests interact, or someone must explain an outcome long after the code was written.

The objective is practical. A developer should be able to follow one business decision without reconstructing the entire application.

Application architecture must keep a business decision explicit from the command that expresses an intention to the outcome recorded in Application State. Application State is the data the application persists as its authoritative record.

An explicit processing path makes a decision structurally traceable. Explaining one specific past decision additionally requires retaining the decision evidence that mattered at the time.

This thesis applies whether the system stores current state, an event history, or a combination of both. Storage is an explicit implementation decision, made deliberately, not implied by the architecture. A database may protect the Application State, but it must not invent its business meaning.

## A Command Preserves the Intention

The command tells us what someone asked the application to decide. In this case, the command is "Cancel Reservation". A representation could look like this:

    {
      "reservationId": "reservation_555",
      "requestedBy": "guest_456",
      "reason": "change_of_plans"
    }

The command expresses one concrete intention toward the capability "Cancel a reservation". The guest wants the application to cancel a specific reservation. Whether that request can be accepted depends on the relevant context and the business rules.

    COMMAND               DOMAIN CAPABILITY        OUTCOME
    CancelReservation(...) ─▶ Cancel a reservation ─┬─▶ ReservationCancelled
                                                    └─▶ CancellationRejected

A Domain Capability is a capability the domain offers. It defines the business responsibility, the rules behind it, and the possible outcomes. The command is one concrete request toward that capability, tied to a specific reservation and requester.

A Domain Capability is not the delivery mechanism. The same intention can reach the application over HTTP, a message queue, or a command-line tool. The delivery explains how the request arrives. CancelReservation explains what the caller wants to achieve. The capability stays the same no matter which channel carries the command.

The application may accept the command:

    { "outcome": "reservation_cancelled", "reservationId": "reservation_555" }

It may also reject it for a business reason:

    { "outcome": "cancellation_rejected", "reason": "cancellation_period_expired" }

The rejection is a valid business outcome. The application understood the intention, evaluated the request, and determined that the current situation did not permit the cancellation.

The command and the outcome preserve both ends of the decision: what was requested and what followed. Explaining why requires the relevant context and the rules applied to it. That is the missing information in systems that can show their current state but cannot explain the business decision behind it.

## The Outcome Alone Cannot Explain the Decision

After the cancellation, a query may return this representation:

    { "reservationId": "reservation_555", "status": "cancelled" }

The representation tells us the current situation. It cannot tell us why the application accepted the command. Was the requester allowed to cancel? Was the cancellation period still open? Had another operation already changed the reservation?

A domain event gives the outcome a domain specific meaning:

    {
      "type": "ReservationCancelled",
      "reservationId": "reservation_555",
      "cancelledBy": "guest_456",
      "occurredAt": "2026-08-08T10:30:00Z"
    }

ReservationCancelled clearly describes what happened in the domain. In contrast, a generic ReservationUpdated would retain the technical change while discarding its business meaning.

Thinking in events gives us this language before any storage decision is made. Modeling the domain through events is not the same as Event Sourcing. An event history can retain the sequence of facts, and Event Sourcing is one possible way to store Application State. It is not a requirement of this approach, and it does not automatically explain the decisions behind the facts it stores. The event shown tells us what happened. An event may retain additional decision evidence, such as the reason or the applicable policy version, but it does not do so by default. The explanation also depends on the command and the context used to decide it.

For the cancellation, that context may look like this:

    {
      "reservationStatus": "confirmed",
      "guestId": "guest_456",
      "cancellationAllowedUntil": "2026-08-10T15:00:00Z",
      "evaluatedAt": "2026-08-08T10:30:00Z"
    }

The context contains the guest who holds the reservation. The decide function compares it with the requester carried by the command: only that guest may cancel. evaluatedAt comes from a trusted server-side clock at the moment the request is evaluated. The capability defines which moment counts for the deadline; here it is the evaluation time, retained in the context. The cancellation context contains the information capable of changing the outcome. Property photos, the guest's profile, and the full payment history have no place in this decision unless a cancellation rule depends on them.

The same command can produce a different result depending on the context at the time of the request:

    requestedAt: 2026-08-08 ──▶ ReservationCancelled
    requestedAt: 2026-08-11 ──▶ CancellationRejected: cancellation_period_expired

The intention remained the same. The second request relied on a different business situation and was rejected because the cancellation period had expired.

This gives us a requirement for an explainable decision: the capability must make its relevant context visible. A generic Reservation object containing everything associated with the reservation obscures that dependency. The CancellationContext states exactly which information the cancellation decision uses.

It also exposes a consistency problem. The application may load a valid context, make the decision, and then commit the outcome after one of the relevant conditions has changed.

A decision is valid only for the context on which it relied. Command Context Consistency, as described by Ralf Westphal and me, expresses that requirement directly:

> A command is accepted only when the context it relied on for its decision is still valid at the moment the result is committed.

This requirement applies regardless of how the Application State is actually stored. The implementation may use constraints, versions, locks, or context checks. The architectural obligation remains the same: the outcome must not be recorded after the basis for the decision has become invalid.

## A Business Decision Needs a Visible Processing Path

The application can execute a cancellation correctly and still leave its decision hard to explain. This happens when the command, the relevant context, the rule evaluation, the consistency protection, and the resulting outcome exist in code without forming one visible processing path.

Consider an implementation where CancelReservation enters through a controller, a shared service loads the reservation object using a generic repository, a policy object contains part of the rules, and an ORM decides whether the update succeeds. None of these structures owns the cancellation decision. The service loads reservations for every use case, the policy object is reused across features, and the ORM applies a generic update strategy. The capability that belongs together from a domain perspective is distributed across code that was organized for reuse, not for the decision. Every required step may be present. Explaining why the cancellation was accepted still requires reconstructing the decision across those structures.

A Request Processing Unit (RPU) gives that processing a concrete boundary and clear ownership. It implements one request toward a Domain Capability, starting with the command and ending with an accepted or rejected outcome. For our example, the Domain Capability is "Cancel a reservation". The RPU processes one concrete CancelReservation command:

    CancelReservation
      │
      ▼
    process_cancel_reservation
      ├── obtain CancellationContext
      ├── invoke the decide function
      ├── protect the context during the commit
      ├── record the accepted outcome
      ├── coordinate required effects
      └── return CancellationOutcome

The capability defines the responsibility, the rules, and the possible outcomes. The decision is made per command, by applying those rules to the relevant context. The RPU makes the complete processing of that decision visible in the application.

A simplified implementation could read like this:

    let context = load_cancellation_context(&command).await?;
    let decision = decide_cancellation(&command, &context);

    let outcome = match decision {
      Accepted(result) => {
        commit_if_context_is_valid(result, &context).await?
      }
      Rejected(reason) => {
        CancellationRejected(reason)
      }
    };
    Ok(outcome)

decide_cancellation is a function and the decision is its result. The function evaluates the command against the supplied context and proposes acceptance or rejection. A proposed acceptance becomes final only when the context is confirmed to be still valid and the result is committed. When the context has changed in the meantime, the conflict is not a technical failure; the RPU maps it to the appropriate business outcome. The concurrent booking example in the database section shows one way this looks in practice.

The RPU records accepted outcomes and returns rejected ones. Where audit or regulatory requirements demand it, rejected decisions and their relevant context can be retained as well.

The RPU coordinates the effects its capability requires to fulfill the task, after the outcome is committed. Independent follow-up processes, such as initiating the refund, react to the recorded outcome outside the RPU. A failure in follow-up work must not make the committed outcome appear unsuccessful.

This gives a developer somewhere concrete to begin when a decision must be explained. Starting with process_cancel_reservation, they can follow the same path the application followed. There is no need to infer the explanation from unrelated technical structures anymore.

Functional Core / Imperative Shell is one useful way to construct such an RPU. The Imperative Shell obtains the context and handles the commit and external effects. The Functional Core is the decide function evaluating the command against that context. This separation is an implementation choice. The RPU is defined by the complete processing path it implements.

Your software cannot explain its business decisions when that path exists only implicitly. It may show the command, the current state, or the recorded outcome. The RPU connects them through the processing that produced the decision.

## The Database Protects Application State, Not Its Meaning

A cancellation decision is valid for the context on which it was made. Another command may change that context before the outcome is recorded.

In this relational implementation, the RPU uses one transaction together with locks and constraints. The transaction makes the change atomic; the locks and constraints protect the decision-relevant context until commit. Loading the context, making the decision, and recording the outcome operate on the same protected state.

The lock is taken when the context is loaded:

    SELECT status, guest_id, cancellation_allowed_until
    FROM reservations
    WHERE id = $1
    FOR UPDATE;

FOR UPDATE holds the reservation row until the transaction ends. No concurrent transaction can update or delete that locked row before the current transaction commits. Rows the decision reads without modifying can be held with FOR SHARE instead. The protection applies to the rows the decision actually locks: every mutable fact the decision relies on must be locked, constrained, or revalidated during the commit.

After the commit, the resulting row may look like this:

    reservation_id    status     cancelled_at
    reservation_555   cancelled  2026-08-08 10:30:00 +00:00

It tells us that the reservation is now cancelled and that a guarded state transition succeeded. It cannot tell us why the application accepted the command. The business meaning came from the capability. status = 'cancelled' is one possible representation of that outcome in Application State. The full table retains more than the status. In the companion example, a reservation keeps confirmed_at, cancelled_at, and a constraint that permits cancelled_at only on a cancelled reservation. What a table retains is part of the storage decision, and retaining such facts supports later explanation. The columns still do not define the rules behind cancellation, the authority of the requester, or the possible reasons for rejection.

The lock protected this cancellation because the relevant condition lives in an existing row. Not every condition does. Row locks cannot protect the absence of a row; such conditions are protected by the schema itself. In the companion booking capability (github.com/ricofritzsche/booking-a-stay-example), a confirmed reservation inserts one row per night into listing_unavailable_nights, whose primary key is (listing_id, night). When two commands book an overlapping night, the second insert violates that key:

    PRIMARY KEY (listing_id, night)
    concurrent BookStay, same night ──▶ unique violation on insert ──▶ BookingRejected: listing_unavailable

The violation is not treated as a technical error. The RPU rolls back and returns the business rejection: the listing is unavailable. The basis for the decision changed between loading the context and recording the outcome. Command Context Consistency requires that this stale acceptance is not committed; returning the business rejection is this capability's response to the conflict.

This is where the database has authority. Transactions, row locks, and constraints protect the integrity of Application State under concurrent access. They prevent an outcome from being committed against conditions that no longer hold.

An event-sourced implementation has the same responsibility. It may append ReservationCancelled only while the event context used by the command remains valid. Command Context Consistency describes this requirement without making a predefined aggregate the universal consistency boundary. (Relational state: transaction, row locks, constraints. Event history: conditional append. Same requirement: protect the context used by the decision.)

Application State can show what the application recorded. The visible processing path connects that outcome to the command, the relevant context, and the decision that produced it.

## Make the Decision Path Explicit

A business decision becomes explainable when the application makes its processing path explicit. The command expresses the intention. The Domain Capability defines the responsibility, the rules, and the possible outcomes. The RPU obtains the relevant context, invokes the decide function, protects that context during the commit, and records the accepted outcome or returns the rejection.

Storage remains an explicit implementation decision. Relational transactions and constraints or a conditional append on an event store fulfill the same obligation: the outcome must not be recorded after the basis for the decision has become invalid. Event Sourcing is one way to meet that obligation, not a prerequisite for this architecture.

Explaining one specific decision months later may require more than a visible path. The application may need to retain the outcome, the applicable policy version, and enough of the relevant context to show why the result was valid at that moment. How much to retain depends on business, legal, and operational requirements. The RPU gives that information a clear place.

A system that retains only the latest values and no decision evidence discards the information its decisions relied on. An event history retains the outcomes in their recorded sequence and derives state from them; a relational model can retain decision-relevant facts in columns or dedicated decision records, while constraints protect the validity of the resulting state. Both are storage decisions. What makes a decision explainable is the explicit path from intention to outcome and what the application deliberately retains along it. A system built this way can answer the question every challenged decision raises: why.

Cheers!

*This article was originally published on my Medium Blog.*
