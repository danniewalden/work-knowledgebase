---
source_url: https://spin.atomicobject.com/cqrs-event-sourcing-typescript/
title: "CQRS and Event Sourcing in TypeScript: A Production Walkthrough"
author: Vlad Surganov
publication: Atomic Spin (Atomic Object)
published: 2026-06-04
retrieved: 2026-06-17
type: article
---

*Below, you'll find a tour of CQRS, Event Sourcing, and Projections as they actually appear in a real production NestJS + KurrentDB + PostgreSQL + Drizzle codebase. It's roughly a 15-minute read. The goal is not just to discuss what these patterns are, but why they are shaped the way they are, and where they earn their keep.*

Most CQRS explainers reach for a bank account aggregate. If you have read one more bank account example in your life, you are owed a refund.

This post uses an actual production system — the kind with a dozen-plus event types per aggregate, schema evolution, and side effects that cannot be allowed to block the UI — as its running example. No toy code.

## A Motivating Puzzle

Here is a question worth holding onto for the whole post.

You ship a feature that lets an administrator approve a pending organization. The implementation is the natural one: `UPDATE organizations SET status = 'active' WHERE id = ?`.

Two weeks later, your product manager asks you a perfectly reasonable question: *"Who approved this organization, and when, and why did we reject that other one last month — can you pull up the reasoning?"*

You cannot. The row tells you *what state we are in*. It says nothing about *how we arrived there*. You saved the destination and bulldozed the road behind you.

That puzzle — and the fact that you cannot solve it by adding a few audit columns without making your life worse — is the itch that Event Sourcing was invented to scratch.

Pair it with CQRS, then sprinkle projections on top, and a number of other problems you did not realize were problems begin dissolving: temporal queries, retroactive bug fixes, new read models added years after the fact.

I am not here to sell you anything. These patterns have real costs, which we will discuss honestly. But when the fit is right, the fit is glorious.

## The Production Stack

Our example system's stack, for the record: **NestJS** as the framework, **@nestjs/cqrs** for command-handler plumbing, **KurrentDB** (the database formerly known as EventStoreDB) as the event log, **PostgreSQL** with **Drizzle ORM** on the read side, and a small fleet of **projections** that translate between the two.

This is for teams whose domain has a memory: approvals, rejections, assignments, migrations, corrections, compliance questions, and a business habit of asking *why* something is in its current state.

If your application is mostly simple profile edits and preference toggles, the honest recommendation is to enjoy your `UPDATE` statements and spend the complexity budget somewhere else.

## The Thesis, in One Paragraph

It's worth memorizing, because we will come back to it:

**CQRS** observes that reading data and writing data are different problems, and it is a form of violence to force one model to do both. **Event Sourcing** proposes that we store not the current state, but the sequence of facts that produced it. **Projections** are the bridge: they translate that stream of facts into whatever shapes the read side wants.

That is the entire idea. Everything else we do today is plumbing, and plumbing, as any homeowner will tell you, is where the interesting failures live.

## Commands Describe Intent, not Data

On the write side of a CQRS system, the API does not accept "please make this row look like that." It accepts **commands** — named, intentful requests like `ApproveOrganization` or `RejectOrganization`.

A command is a verb. It is a thing someone, or something, is trying to do.

In our codebase, every command extends a common base class carrying three fields: the **entity ID** it targets, the **issuer** (a user? the system? a migration?), and a **timestamp**. Specific subclasses add the rest:

```typescript
export class CreateOrganizationCommand extends Command {
  constructor(
    id: string,
    issuer: Issuer,
    public readonly fields: OrganizationData,
  ) {
    super(id, issuer);
  }
}

export class RejectOrganizationCommand extends Command {
  constructor(
    id: string,
    issuer: Issuer,
    public readonly rejectReason: OrganizationRejectReason,
  ) {
    super(id, issuer);
  }
}
```

Notice what is present and what is absent. There is no `status: 'approved'` parameter anywhere. The command does not tell the system what the new row should look like.

Instead, it tells the system what the user is *trying to accomplish*. The system then decides whether that is a legal thing to do, and what state changes it implies.

This distinction is more important than it appears. When your write API speaks in verbs — *approve*, *reject*, *invite* — instead of nouns-with-mutations — *PATCH the status field to "approved"* — the code begins to speak the same dialect as the business.

Your product manager can read your command names. That is not cosmetic. It is a substantial reduction in translation cost between the people who decide what the software should do and the people who make it do it.

A well-named command set is, in effect, an executable glossary of your domain. If a business analyst cannot read your commands, your commands are poorly named.

## The Aggregate is a State Machine

A command bus routes each command to a **command handler**. The handler's job is to load the right **aggregate** — a domain entity with its full history rehydrated into memory — and hand the command to it.

In our system, the aggregate extends a class called `PersistentEntity`. It is, at heart, a state machine with one responsibility: given its current state and an incoming command, decide what events should fire.

```typescript
export class Organization extends PersistentEntity<
  OrganizationCommand,
  OrganizationData,
  OrganizationEvent
> {
  static readonly eventMap = {
    [OrganizationCreatedEvent.TYPE]: OrganizationCreatedEvent,
    [OrganizationUpdatedEvent.TYPE]: OrganizationUpdatedEvent,
    [OrganizationApprovedEvent.TYPE]: OrganizationApprovedEvent,
    [OrganizationRejectedEvent.TYPE]: OrganizationRejectedEvent,
    [OrganizationDocumentAddedEvent.TYPE]: OrganizationDocumentAddedEvent,
    // ...more domain events
  } satisfies EventMapFor<OrganizationEvent>;

  static readonly stateMap = {
    [UninitializedOrganizationState.STATE_NAME]: UninitializedOrganizationState,
    [PendingOrganizationState.STATE_NAME]:       PendingOrganizationState,
    [ActiveOrganizationState.STATE_NAME]:        ActiveOrganizationState,
    [RejectedOrganizationState.STATE_NAME]:      RejectedOrganizationState,
    [InactiveOrganizationState.STATE_NAME]:      InactiveOrganizationState,
    [ClosedOrganizationState.STATE_NAME]:        ClosedOrganizationState,
  } satisfies StateMapFor<OrganizationState>;

  constructor() {
    super(new UninitializedOrganizationState());
  }
}
```

### States are real objects.

An organization in *Pending* state is a genuinely different thing from one in *Active* state, and it accepts different commands. You cannot approve an already-approved organization. You cannot update a rejected one.

That rule does not live in an `if` statement buried in a service. It lives in the state class, where it cannot be forgotten. Invalid transitions become impossible, not merely improbable.

### Exhaustiveness is enforced by TypeScript.

The phrase `satisfies EventMapFor<OrganizationEvent>` instructs TypeScript: "this object must cover every event type in the `OrganizationEvent` union." Add another event to the union and forget to register it here? The compiler refuses to build.

This is our first encounter with a recurring theme: *exhaustiveness checking*. In an event-sourced system, the type system is the first, last, and best line of defense.

The pattern to internalize: use your language's type system to make impossible states impossible. "Approve a rejected organization" should not be a bug you catch in code review. It should be a bug the compiler already caught while you were off doing something else.

## Events are What Actually Get Saved

Here is where we diverge most sharply from the world of CRUD. The aggregate does not persist itself. It emits **events**, and the events are appended to a stream.

The aggregate's in-memory state is merely a cached fold over the event history.

```typescript
export class OrganizationApprovedEvent extends EntityEvent {
  static readonly TYPE = 'OrganizationApprovedEvent' as const;
  readonly type = OrganizationApprovedEvent.TYPE;

  constructor(
    entityId: string,
    issuer: Issuer,
    timestamp: Date = new Date(),
  ) {
    super(entityId, issuer, timestamp);
  }
}
```

An event is a **fact about the past**. It is immutable. It carries the minimum information needed to describe what happened — not a full snapshot of the world, just a delta.

`OrganizationApprovedEvent` does not serialize the entire organization. It says: *this ID was approved, by this issuer, at the event timestamp.*

When a command arrives, the aggregate validates it, constructs the appropriate events, and applies them to its own state. The framework then appends those events to the entity's stream in KurrentDB with **optimistic concurrency control**.

In plain English: "I expect this stream to be at revision 42 when I write. If someone else got there first, fail loudly."

```typescript
async writeEvent<E>(
  streamName: string,
  eventType: string,
  eventData: E,
  expectedVersion?: number,
): Promise<void> {
  const event = jsonEvent({ id: uuid(), type: eventType, data: eventData as JSONType });

  expectedVersion !== undefined
    ? await this.client.appendToStream(streamName, event, { streamState: BigInt(expectedVersion) })
    : await this.client.appendToStream(streamName, event, { streamState: ANY });
}
```

Streams are named by entity: `Organization-{uuid}`, `User-{uuid}`, and so on. KurrentDB also provides virtual category streams.

For example, `$ce-Organization` contains every organization event across every organization, which is precisely what projections will want to subscribe to in a moment.

A reflective pause. The first time it lands that your database contains no rows describing organizations — only an append-only log of things that have happened to organizations — produces a mild vertigo.

You have written code that has never, not once in its life, issued an `UPDATE`. The word "update" does not appear in your write path. You may want to sit down.

## Reconstructing the Present from the Past

How, then, does the aggregate know its current state when the next command arrives? By rereading its history.

When a command targets organization `abc-123`, the framework loads stream `Organization-abc-123`, instantiates a fresh `Organization` aggregate, and feeds every event through `apply()` in order.

After the final event, the aggregate's state reflects the current state of the organization. *Only then* is the new command dispatched.

### Snapshots keep replay cheap.

The natural objection: "You replay the entire history for every command? Every time?"

Yes. For a while, that is fine. Events are small, streams are short, and event stores are astoundingly fast at reading them.

Eventually, though, an aggregate gets chatty. An organization with 40,000 document-added events will let you know. The answer is **snapshots**.

A snapshot is a serialized copy of an aggregate's state at a particular event revision. In our system, snapshots live in a PostgreSQL `snapshots` table, not in KurrentDB itself. That keeps the write path clean.

Every hundred events, the framework persists a snapshot; we retain the last five per entity. On rehydration we load the most recent snapshot and replay only the events *after* that revision. Two hundred thousand events collapse to forty.

Here is the subtle, critical point: snapshots are a **performance optimization, not a source of truth**. If a snapshot is corrupt, outdated, or written under an older schema, you discard it and replay from the events.

The log is always authoritative. This is one of Event Sourcing's quiet superpowers: *your caches are permitted to lie*, because you always have something to fall back on.

## Making Events Queryable

The question that always arises at this point: the UI needs to show a list of organizations, sorted by name, filtered by status, paginated. You cannot possibly be replaying every event on every page load.

So how does anyone actually query this thing?

Correct. We do not. Meet the **projection**.

A projection is a long-running subscriber that reads events off a category stream — for us, `$ce-Organization` — and translates them into whatever read model the UI needs.

Most of ours write to PostgreSQL via Drizzle. The read side of the system is, by design, a completely boring, indexed, joinable relational database. It is exactly the shape your frontend wants, because your frontend was born wanting rows.

```typescript
export const organizations = pgTable(
  'organizations',
  {
    id: uuid('id').primaryKey(),
    subscriptionType: text('subscription_type').notNull(),
    name: text('name').notNull(),
    addressLine1: text('address_line_1').notNull(),
    // ...more
    status: text('status').notNull().default(OrganizationStatus.Pending),
    rejectReason: jsonb('reject_reason'),
    approvedAt: timestamp('approved_at', { withTimezone: true }),
    rejectedAt: timestamp('rejected_at', { withTimezone: true }),
    createdAt: timestamp('created_at', { withTimezone: true }).notNull(),
    updatedAt: timestamp('updated_at', { withTimezone: true }).notNull(),
  },
  (table) => ({ idIdx: index('id_idx').on(table.id) }),
);
```

This table is not where the organization's data lives. This table is where a *read-shaped reflection* of that data lives, maintained by a projection that listens for organization events and keeps everything in sync.

### A projection is a translator.

And the projection itself:

```typescript
@Injectable()
export class OrganizationDbProjection
  extends AbstractDbProjection<OrganizationEventEnvelope> {

  protected readonly entityClass = Organization;
  protected readonly config: PersistentSubscriptionConfig = { startFrom: 'start' };

  protected async handleEvent(event: OrganizationEventEnvelope): Promise<void> {
    await match(event)
      .with({ type: OrganizationCreatedEvent.TYPE },  (e) => this.handleOrganizationCreated(e))
      .with({ type: OrganizationUpdatedEvent.TYPE },  (e) => this.handleOrganizationUpdated(e))
      .with({ type: OrganizationApprovedEvent.TYPE }, (e) => this.handleOrganizationApproved(e))
      // ...more
      .exhaustive();
  }
}
```

Four things to notice here, each worth sitting with for a moment.

- **This is just pattern matching.** We use `ts-pattern`'s `.exhaustive()`. Add a new event type to the union, forget to handle it here, and the build fails. Same exhaustiveness trick as in the aggregate.
- **Each handler is a small SQL writer.** `handleOrganizationApproved` sets `status = 'approved'` and `approved_at = event.timestamp`. That is all. There is no domain logic here; all of that already ran on the write side.
- **`startFrom: 'start'` is a superpower.** If we want to change the read model — add a column, split a table, index differently, *add a completely new read model* — we can replay every event from the beginning of time.
- **The offset update is atomic with the write.** The abstract base class wraps `handleEvent()` and the offset bookkeeping in a single PostgreSQL transaction. Either both succeed or both roll back.

### Read models are rebuildable.

This is worth saying plainly: *the read side is rebuildable*. That changes the risk profile of database migrations more than any sentence of mine will convince you of until you experience it.

You cannot end up in a state where the event was projected but the offset was not saved. You also cannot advance the offset without applying the projection. This sounds obvious. It is not obvious. People get this wrong all the time, and then they wonder why production is weird.

## The Read Side is Mercifully Boring

A small epiphany waits here. Once you have a projection maintaining a relational read model, the read side of your CQRS application stops being exotic.

Controllers inject an `OrganizationRepository`, the repository issues a Drizzle query, JSON comes out. There's no `QueryBus`. No query handlers. No ceremony.

Some CQRS purists will insist that reads, too, should go through a query bus. I have built it both ways. A bus on the read side adds indirection without adding much value when your reads are mostly "give me the thing."

A bus on the write side earns its keep, because commands have *behavior*: validation, state transitions, event emission. You want one place where all of that lives.

Asymmetry in architecture is a feature, not a bug. Do not make your system more symmetrical than your requirements.

## Production Details that Tutorials Skip

Everything up to this point is standard CQRS and Event Sourcing — the stuff the textbooks describe. What follows is the set of pieces that tutorials gloss over.

In my experience, these are the difference between a proof-of-concept and something you can run a business on.

### KurrentDB offers optimistic concurrency, plus a belt.

KurrentDB offers optimistic concurrency on writes: "I expect this stream to be at revision N." If it is not, you receive a `WrongExpectedVersionError`, reload, and retry.

In practice, if two commands for the same entity arrive simultaneously, both threads load the aggregate, both build events at revision N+1, one wins, the other retries, reloads, and tries again. Under load, this gets ugly in a hurry.

So, for each entity, we acquire a **PostgreSQL advisory lock** keyed on the entity ID before executing the command. It is a FIFO serialization for that entity; other entities proceed in parallel, unaffected.

```typescript
return this.lockService.withEntityLock(entityId, async (_tx: DrizzleTransaction) => {
  const entity = new entityClass();
  entity.receiveCommand(command);
  // ...persist events
});
```

This is cheap, database-local, and already installed. No Redis, no ZooKeeper, no distributed-lock fairy dust.

Entity-level serialization turns out to be a pleasant sweet spot: commands for the same entity queue up; commands for different entities run concurrently. Write throughput scales with entity count, which is almost always what you actually want.

### Events evolve; upcasters help you survive.

Your events live forever. Your code does not. Eventually, you will need to add a field to an event, rename one, or quietly concede that the original shape was a mistake.

You cannot `UPDATE` the event log. That would defeat the entire point of the log.

The answer is the **upcaster**: a small function that reads an older event version, transforms it to the current shape, and passes it up the stack.

Each event class carries a `SCHEMA_VERSION`. When the stored version is less than the current one, the upcasters run in order until the payload is current.

```typescript
export function upcastUserCreatedEventV1(data: Record<string, unknown>) {
  // v2 added a required `status` field; default old events to 'active'
  if ((data.schemaVersion ?? 1) >= 2) return data;
  return { ...data, status: 'active', schemaVersion: 2 };
}
```

This is a lightweight pattern, but one you must build in *on day one*. Retrofitting versioning onto a log of a million events is not a sprint you want on your calendar.

Put the ceremony in place before you need it. The first upcaster can simply return its input. The skeleton is what matters.

### Idempotency is not optional

KurrentDB's persistent subscriptions deliver events **at least once**. On a crash, redeploy, or deliberate retry, the same event can arrive twice. Your projection must not care.

We achieve this with a per-projection offset stored in PostgreSQL and an in-memory LRU cache of recently-processed event IDs. The cache catches the hot path at about a 99% hit rate when the projection is caught up; the offset table catches the cold path.

In either case, applying an event twice is a no-op. *Assume duplicates. Design for duplicates. Duplicates are not an edge case; they are Tuesday.*

The failure mode is painfully ordinary. A projection handles `OrganizationApprovedEvent`, updates the read model, and the process dies before the offset is committed.

On restart, the subscription redelivers the same event. If the projection increments counters, sends emails, or inserts child rows without an idempotency guard, congratulations: one approval just became two side effects.

This is why the offset write and read-model write share a transaction, and why side-effect projections need their own deduplication story.

### There are two flavors of projection.

Some projections are the *read model*. They must be consistent enough that the UI can show the right thing after a write. Those run transactionally, as described above.

Many things, however, are not read model updates. Sending a welcome email. Auto-assigning a default profile when a user joins. Posting to a webhook. Notifying Slack.

These are **side effects**, and they should not share a transaction with your read model. If your email provider is having a day, your UI should not suffer.

So we run a second kind of projection: an **async projection**. It subscribes to the same category stream independently and handles side effects.

It can fail, retry, lag, and restart without touching the write side or the read model. Same machinery — a persistent subscriber with idempotency — different responsibilities.

This pattern is worth dwelling on, because it is the one newcomers to CQRS tend to underestimate. Once your side effects are modeled as projections over the event log, they stop being tangled into command handlers.

Adding a new one stops feeling dangerous. Want to notify Slack when an organization is approved? Write a projection. The rest of the system does not change. Nothing is refactored. Nothing is threaded.

You add new behaviors without modifying existing ones, which, as a gentleman named Meyer observed, is the whole ballgame.

### Correlation IDs give you an audit trail.

When a command fires, we stamp a correlation ID onto the logging context. That ID rides along into every event the command produces.

Which means: when you are staring at a strange read-model state six months from now, you can find the events that caused it, trace back to the HTTP request that issued the command, and read every log line from that request.

The audit trail was not a feature we built. It fell out of the architecture.

Free features are the best features, and if you architect well, many of the features you pride yourself on shipping were never actually separate features at all.

## An honest Accounting of the Costs

I like this architecture. I use it on real projects. That said, anyone who sells you a pattern without telling you what it costs is trying to sell you something.

### It is more code.

For a trivial CRUD feature — "admins can edit their profile bio" — you do not want a command, an event, a state transition, and a projection handler.

You want a `PUT` endpoint and an `UPDATE`. If the majority of your application is features of that flavor, event sourcing will feel like formalwear at a backyard barbecue.

### Eventual consistency is real.

After a write, the read model takes some milliseconds to catch up. Most of the time the user never sees it.

Sometimes they do, and you must design the UX to handle the gap: optimistic UI, explicit loading states, or, in rare cases, waiting for a projection checkpoint.

Pretending this problem does not exist is how you accumulate angry support tickets that say "I approved it but it still shows as pending."

### Cross-aggregate queries are harder.

"Show me all organizations whose primary contact has not logged in for 90 days" crosses two aggregates.

Projections can answer it — you build a joined read model for precisely that question — but that is another moving piece to design, populate, and maintain.

You trade the freedom of arbitrary joins for the discipline of purposeful read models.

### The onboarding ramp is real.

New engineers need to internalize the write/read split, the immutability of events, the idempotency requirements, and the versioning story.

It is not difficult material, but it is unfamiliar, and unfamiliar costs you calendar days. Budget for them.

### Here's when the cost is worth it.

So when is formalwear the right call? When your domain is genuinely *eventful* — when "why is this thing in this state?" is a question the business asks, not just a question you ask at 2 a.m. during an incident.

Finance. Compliance. Healthcare. Logistics. Anything with a regulator or an auditor in its life.

Also: anywhere you suspect you will need read models you have not yet imagined. The ability to rebuild projections from the complete history is, frankly, a cheat code, and it is worth a lot of architectural weight.

## 7 Things Worth Taking Away

If nothing else from this post sticks, let these:

- **Commands are intents, not payloads.** `ApproveOrganization`, not `UpdateOrganizationStatus`. Your codebase will begin to read like your product spec, and this is a wonderful thing.
- **Keep aggregates small.** An aggregate is a consistency boundary. If a command handler is reaching across to other aggregates, you have drawn the boundary in the wrong place. Solve it with async projections ("when X happens, dispatch Y"), not bigger aggregates.
- **Use the type system for exhaustiveness everywhere.** Event maps, state maps, projection handlers. `satisfies` and `.exhaustive()` are load-bearing. The compiler catching a missed case is worth any ten tests you could write.
- **Install event versioning on day one.** The first upcaster can be a no-op. The machinery is what matters.
- **Treat the event log as sacred.** No deletions. No mutations, outside explicit redaction or privacy-retention policies. Everything else — snapshots, projections, caches — is rebuildable, and therefore disposable.
- **Prefer projections over sagas.** If "when X, do Y" can be a projection subscribing to X's events, make it one. One fewer concept in the codebase. One more boring, idempotent, restartable piece of code.
- **Advisory locks are almost always enough.** You probably do not need a distributed lock service. You almost certainly have PostgreSQL. PostgreSQL already has what you need.

## A Closing Thought

Here is the line I keep returning to: In a CRUD system, your database tells you *what*. In an event-sourced system, your database tells you *what happened*.

The difference sounds academic until the first time a stakeholder walks to your desk and asks why something is the way it is. With an event log, you can produce a perfectly ordered record of every decision, every actor, and every timestamp that conspired to produce this exact present.

That first time resembles magic. Once you have seen it, it becomes difficult to un-see.

CQRS and Event Sourcing are not right for every application. When they fit, though, they fit exactly. The more complex your domain becomes, the more precisely they fit.

If your business has a memory, your database should have one too.

Go read some event logs. Break something. Come back with better questions than the ones you started with.
