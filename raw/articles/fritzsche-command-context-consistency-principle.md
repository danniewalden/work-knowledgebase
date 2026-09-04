---
source_url: https://ricofritzsche.me/the-command-context-consistency-principle/
title: The Command Context Consistency Principle
author: Rico Fritzsche
publication: ricofritzsche.me ("Thinking in Events")
published: 2026-07-26
retrieved: 2026-08-03
type: article
---

# The Command Context Consistency Principle

*How Event Stores and Relational Databases Guard Business Decisions*

*(Image licensed under the Unsplash+ License.)*

A few years ago I set out to build systems as self-contained feature slices: each slice owning one behavior, end to end. I built them the common way, as Vertical Slice Architecture, and what I got was handlers around a central data model. Every handler loaded mutable entities from that model and saved them back.

The cause was the entity-centric thinking we were taught for many years. Domain-Driven Design made it precise: find the aggregate, load it, call a method, save it. The aggregate holds the invariants, and it holds the transaction: one aggregate per transaction, one consistency boundary, fixed at design time.

The move that changed my systems was dropping the aggregate as the consistency boundary. A command reads facts to decide, and those facts have to still hold when the outcome commits. Nothing about that requires an aggregate.

Dropping it led me to Aggregateless Event Sourcing: no stream per aggregate, an append guarded by the facts the decision was based on instead of by a stream version. It worked, and it still works.

It took me longer to see that the principle does not need the event store either. A relational database enforces it with locks and constraints; an event store enforces it with a conditional append. Event sourcing remains a great option. The principle does not require it. Its name is Command Context Consistency: record the outcome of a command processing only while the facts the decision is based on still hold.

The aggregate is the wrong unit for consistency. The boundary belongs to the facts a command's decision is based on, and that set changes from one command to the next.

## The Aggregate Is a Static Consistency Boundary

Domain-Driven Design gave the aggregate a specific job. Eric Evans defined it as a cluster of objects with a boundary and a root, and made that boundary the unit of consistency for changes. Vaughn Vernon sharpened it into a transactional consistency boundary, with his rule of thumb that a system "modifies only one aggregate instance per transaction", a strong default he allows breaking for good reason. When the transaction commits, the state inside the boundary is consistent, and anything outside it is left to eventual consistency.

The boundary is fixed once, per aggregate, and the store enforces it as a single unit. In a relational model the aggregate root carries a version, and any change to any part of the aggregate turns on that one version. In event sourcing the aggregate is one stream, and an append is accepted only at the expected sequence number for the whole stream. Either way the check covers the whole object, one boundary for every command that touches the aggregate, whatever facts a given command actually reads. A command that reads three facts and a command that reads fifteen are validated against the same aggregate version.

*(One stream per aggregate: One version check covers every event on the stream, relevant to the command or not.)*

One boundary cannot fit every command. Take two commands on one reservation. One changes the guest count, one changes the check-in date. Both load the Reservation aggregate, and the aggregate is one concurrency unit: its version covers every part of it, so the second write fails the version check. They changed different values, and neither change touched a fact the other read, and the boundary still counted them as a conflict. It is too large: it guards the whole reservation where the two commands worked on separate parts of it.

Now take the rule that a listing night is booked once. Two guests request the same night. Each request creates its own Reservation, a separate aggregate instance; each transaction modifies one aggregate, exactly as the rule prescribes, and both commit. The invariant that should stop the second booking is not inside either reservation. It holds across every reservation for that listing and night. The boundary is too small: the fact that needs protecting sits outside the aggregate the command changes.

The usual answers are known. Doctrine says to remodel until the invariant lives inside one aggregate, as Vernon's aggregate-design series prescribes: introduce a ListingAvailability aggregate that owns the booked nights of one listing and route every booking through it. The rule holds again, every booking for that listing now serializes through one object, the object grows night by night, and it exists to hold a lock.

*(ListingAvailability aggregate owns the invariant: every booking for the listing serializes through this one object, and it grows night by night.)*

The second answer is eventual consistency between aggregates: both reservations commit, and a process manager detects the collision afterwards and cancels the later booking, a confirmation followed by a cancellation.

*(Eventual consistency between aggregates: guest B gets a confirmation, then a cancellation.)*

Practitioners know a third answer and file it as an exception: put a unique constraint on the nights and let the database refuse the second insert. The first two answers relocate the boundary and keep its nature, a single fixed boundary rather than the facts any one command needs. The third abandons the aggregate and guards the actual fact. It is worth taking seriously.

The consistency a command needs is the set of facts its decision is based on. It rarely matches the outline of an aggregate, and one fixed boundary cannot fit a set that changes with the command.

## The Command Shapes Its Context

A command expresses an intention, for instance "book this stay" or "cancel this reservation". To decide whether to accept it, the application reads the relevant facts from the Application State. Those facts form an immutable data structure: the command's context.

A fact is a true statement about state and causality, bound to the moment it is about: this guest is eligible, this night is occupied. A fact cannot change; a later commit supersedes it with a new fact about the new state. A context fact holds while no commit has superseded it. A fact belongs in the context when a rule evaluates it. Anything that does not affect the result is excluded, no matter how close it is in the data.

The intent shapes the context. Which facts matter follows from what the command is trying to do. Booking a stay has to establish that the guest may book, that the listing permits the stay, and that the requested nights are free; its context holds those facts and nothing else. The capability defines which kinds of facts its rules read, and the command's values (this guest, this listing, these nights) select the concrete facts for one execution. The same facts matter whatever store holds them.

The context is read once. What the decide function receives is a snapshot of that moment, not a live view of the store. Other commands may commit while the decide function runs; the context does not change. Deciding uses only the command and the snapshot. If a rule needs the time, the time is one of those facts, read with the rest. The same command over the same facts gives the same outcome, every time.

A decision is valid for exactly the facts it was made from. Between the read and the commit, another command may supersede one of them. Then the outcome was decided on facts that no longer hold, and it must not be recorded: in an event store the event records are not appended, and in any store the Application State does not change on a stale basis.

So processing a command has a fixed shape:

*(The fixed shape: read, decide, record.)*

The record step carries the condition: an outcome is recorded only while its context holds. That is the whole principle.

## Command Context Consistency

Ralf Westphal coined the name Command Context Consistency, and he described it against an event store: the context is "all the events relevant for a command during consistency check", and the events a command produces are recorded only after the same query confirms that no new context events arrived. I had set out the same rule in Aggregateless Event Sourcing: a decision's context is the set of facts read for it, held unchanged from the read to the write.

Dropping the aggregate has its own history in the event-sourcing community. Sara Pellegrini argued for killing the aggregate and named the alternative the Dynamic Consistency Boundary: read the events needed for the decision through a query, and append the result only if that selection is unchanged at the moment of the append. She calls it "a form of optimistic lock specific for event sourcing based systems".

All three texts speak event-store language. The principle does not. A command's outcome is recorded only while the facts the decision is based on still hold. That sentence mentions no store. It fixes what has to be true at the moment of commit and says nothing about how to check it. An event store checks with a conditional append, a relational database with locks and constraints. Only the mechanism differs.

The boundary of consistency is the context, one command at a time. A command needs to be re-validated when another commit supersedes a fact its decision is based on; commands do not conflict merely because they touch the same aggregate. Change the guest count and the check-in date of one reservation, and neither change touches a fact the other read, so both commit. Book the same night twice, and each claims the night the other read, so the second is re-validated against the new facts and refused. The boundary follows the facts each command reads.

*(The boundary follows the facts each command reads.)*

A failed guard means one thing: the decision was based on stale context. The store reports it in whatever way its mechanism has: zero rows updated, a failed append condition, a uniqueness violation, a serialization failure. What happens next belongs to the capability. Its Request Processing Unit (RPU), the code that carries it, can roll back, reload the context, and run the same decide function again; that second decision may refuse the booking, and it may accept it when the context moved in a favorable direction. It can also map the conflict directly to a business rejection, the way a night claimed by another booking becomes ListingUnavailable. Either way the answer comes from current facts: the conflict is a business situation to resolve, not a technical error to raise. A rejection that changes no state need not be recorded; recording rejections for audit writes a separate record, on purpose.

Command Context Consistency replaces the aggregate with a boundary the command draws for itself. What remains is to enforce it, in whatever store you have.

## Guarding the Whole Context

The principle has stayed logical: record an outcome only while the facts the decision is based on still hold. A store enforces it with something physical, and the two are easy to run together. The logical context is the set of facts decide read that another commit can supersede. The physical guard is what the store actually holds still: a row, a version, a predicate, a unique constraint, a set of tags, a stream position. Correctness needs the guard to cover the context and never less. A guard narrower than the context lets a fact change unseen, and a wrong outcome commits. A guard wider than the context stays correct, but it blocks commands that changed a fact the decision never read, and contention and false rejection return under another name. Equality is the ideal, and no store hands it over for free. Only mutable facts whose continued validity matters belong in the guard; a captured request time, a generated identifier, or a provider's result is an input to the decision, not something the store can hold unchanged. The criticism of the aggregate returns here in its sharpest form: an aggregate version is a physical guard far wider than most command contexts.

Take the two commands on one reservation to a relational store: PostgreSQL at its default READ COMMITTED, each command in one transaction. Changing the guest count reads the reservation's current count and its status, and writes the new count. The guard is those two facts, and a conditional update names them.

    UPDATE reservations
    SET guest_count = $1
    WHERE id = $2
      AND guest_count = $3
      AND status = $4
    RETURNING id;

The WHERE is the guard, and READ COMMITTED does not hold the row still on its own; the guard does. The update commits only while the count and the status still hold the values the decision was based on. A concurrent command changing the check-in date on the same row makes this statement wait, because a row lock in PostgreSQL holds the whole row, not a column. When that command commits, PostgreSQL re-evaluates the WHERE against the updated row before applying the update. The check-in date is not in the guard, so the row still matches, and the guest-count update proceeds. An empty RETURNING is the only rejection, and it comes only when the count or the status actually changed.

A command-specific guard does not remove database serialization. Two writes to one row still take turns. What it removes is the needless rejection, the guest-count command refused because an unrelated column moved. The two commands are ordered, and both succeed.

A decision that reads more than one fact guards each of them, in the same transaction. Whether a booking is allowed reads the guest's eligibility, the listing's rules, and the nights already taken. A free night is the absence of a row, which a row lock cannot protect, so a unique constraint guards it at commit: the command inserts one row per night, and the constraint rejects a night another booking already claimed.

    INSERT INTO occupied_nights (listing_id, night) VALUES ($1, $2);
    -- UNIQUE (listing_id, night)

The guest's eligibility and the listing's rules are rows read for the decision but never changed. A shared lock holds them to the commit, acquired in a fixed order across commands so two bookings cannot deadlock.

    SELECT booking_eligibility FROM guests WHERE id = $1 FOR SHARE;
    SELECT status, max_guests, min_nights FROM listings WHERE id = $1 FOR SHARE;

FOR SHARE is a wider guard than the columns read, because it holds the whole row: an update to any column of that listing waits, not only a change to a rule the decision is based on. It is the practical guard when a decision is based on most of a row, and a conditional predicate is the tighter one when it does not. Read under the guards, decide, and write in one transaction. If any guarded fact gave way, the transaction does not commit.

On an event store, event records carry the facts and the guard is a query. The context query selects the events that describe the guest, the listing, and the nights. Reading it returns the context and its version: the highest sequence number among the records the query matches, absent while the context is empty: no matching event exists yet, so the first one to arrive is itself the change. Decide, then commit with a conditional append: the store recomputes the context version at the append, and the new events commit only while the actual version still equals the expected one.

*(On an event store: query, decide, append_if.)*

A new matching event raises the actual version above the expected one, and the append is rejected as a conflict; events that do not match the query change nothing about it. The query is the physical guard: it selects by event types and by predicates on the recorded payload, so it holds the events the decision is based on rather than the whole stream.

Back to the two commands on one reservation, now as events. Each capability declares the facts its decision is based on as a context query:

    // ChangeGuestCount: the confirmed reservation and later count changes
    public static EventQuery For(Request request) => new([
      new EventFilter(
        ["ReservationConfirmed", "GuestCountChanged"],
        [SerializeToElement(new { reservation_id = request.ReservationId })])
    ]);

    // ChangeCheckIn: the same shape, with "CheckInChanged" instead of "GuestCountChanged"

    // processing, the fixed shape from above:
    var contextQuery = Query.For(request);
    var read = await eventStore.Query(contextQuery);
    var result = Decide.Execute(request, Context.Fold(request, read.Records));
    await eventStore.AppendIf(result.NewEvents, contextQuery, read.ContextVersion ?? 0);

A committed CheckInChanged does not match the guest-count query, so it does not move that context's version, and both appends commit side by side. Book the same night twice, and both context queries select the events occupying that night: the first append moves the version, the second conflicts and is decided again on the new facts.

The Dynamic Consistency Boundary is the same guard in tag-based form. Same principle, two stores. The relational one guards with a conditional update, a shared lock, and a unique constraint; the event store with a conditional append. Neither reaches for an aggregate. The guard is the context the command read, held still to the moment the outcome is recorded.

## Conclusion

Go back to the two commands on one reservation. The guest count and the check-in date commit side by side now, because neither change lands in the other's context. The two bookings for the same night still collide, because each changes the night the other read, and one is refused. The false conflict is gone, the real one stays, and no aggregate decided either.

The consistency boundary belongs to the command: the facts it read, checked when the outcome is recorded. Command Context Consistency states it as a principle. An event store enforces it with a conditional append over a query, a relational database with locks and constraints.

The aggregate can retire from this job. A Domain Capability is the ability to process a domain request, one that changes the Application State or projects it: in the first case the Application State is the sink, in the second it is the source. The capability defines the facts needed to decide, and the RPU carries that context into the commit condition. Consistency follows the command instead of a static object model. The event-store contract is written down in the Command Context Consistency specification.

Cheers!

### Sources
- Ralf Westphal: Command Context Consistency — https://ralfwestphal.substack.com/p/command-context-consistency
- Sara Pellegrini: The Dynamic Consistency Boundary — https://sara.event-thinking.io/2023/05/dynamic-consistency-boundary.html
- Eric Evans: Domain-Driven Design (2003) — the Aggregate pattern.
- Vaughn Vernon: Effective Aggregate Design (2011) — https://www.dddcommunity.org/library/vernon_2011/
- Rico Fritzsche: Aggregateless Event Sourcing — https://ricofritzsche.me/aggregateless-event-sourcing/
- Dynamic Consistency Boundary specification — https://dcb.events/specification/
- Rico Fritzsche: Command Context Consistency, concept page — https://architecture.ricofritzsche.me/concepts/command-context-consistency/
- Rico Fritzsche: Command Context Consistency specification — https://architecture.ricofritzsche.me/specifications/command-context-consistency/
