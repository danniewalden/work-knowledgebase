---
source_url: https://ricofritzsche.me/who-owns-a-rule-shared-across-domain-capabilities/
title: Who Owns a Rule Shared Across Domain Capabilities?
author: Rico Fritzsche
publication: ricofritzsche.me ("Thinking in Events")
published: 2026-07-30
retrieved: 2026-08-03
type: article
---

# Who Owns a Rule Shared Across Domain Capabilities?

*How Autonomous Domain Capabilities Protect Shared Rules While Business Decisions Stay Local*

*(Photo by Mark Fletcher-Brown on Unsplash)*

After publishing *Why the Domain Is Defined by Domain Capabilities, Not Object Models*, I received this comment on Medium:

> Capability ownership is compelling because it aligns code with change, but shared invariants can still cut across capabilities. How do you prevent a localized RPU from duplicating or drifting on rules such as identity, money, or compliance without rebuilding a central service layer?

I took the question seriously because it tests the boundary of capability ownership. Every Request Processing Unit owns its complete decision path. A system can still contain knowledge with one authority across several capabilities. Poor handling produces inconsistent decisions or a shared service that gradually collects business behavior again.

The examples in the question also need more precise terms. Identity, money, and compliance describe different kinds of knowledge. Treating all three as shared invariants hides the design decision we need to make.

## An invariant is a property of state

An invariant has a strict meaning. Leslie Lamport defines it as an assertion that is true in every reachable state. For this discussion, the relevant states are committed states of the application.

For Application State (S), an invariant (I), and an accepted state transition (T), the obligation is:

I(S) and T(S) = S' => I(S')

Every accepted command must preserve the invariant.

Some business rules govern only a decision. "The guest must be at least 18" can be an eligibility rule for one booking capability. It becomes an invariant when the domain promises that every committed reservation has an adult guest.

This distinction fits the definitions in my Architecture Knowledge Base. A Domain Capability owns one business responsibility, its rules, and its possible outcomes. An RPU implements exactly one capability. Application State holds the authoritative facts used by all capabilities. Command Context Consistency requires that a command's outcome is recorded only while the facts the decision is based on still hold.

The examples from the comment now separate into distinct responsibilities:

| KIND OF KNOWLEDGE | EXAMPLE | ARCHITECTURAL HOME |
| --- | --- | --- |
| State invariant | A listing night can belong to at most one active reservation | Application State, enforced at commit |
| External fact | A subject authenticated at a stated assurance level | Provider, optionally recorded as a fact |
| Stable semantics | Money has an amount and a currency | Small pure type or generated local code |
| Shared policy | AML-42 release 2026-07 applies in one jurisdiction | Versioned policy authority; applied by the RPU |
| Capability decision | Release or reject this payout | Owning RPU |

A Reactor coordinates an interaction when several capabilities or external operations must participate. It stays outside these ownership decisions.

## Shared code and shared knowledge are different

Identical conditions in two RPUs can express separate knowledge.

The DRY chapter in The Pragmatic Programmer makes this point with two validators that happen to contain identical code. One validates age and the other validates order quantity. Their current implementation is the same. Each rule belongs to a different source of knowledge and can change for a different reason.

The same applies to RPUs. A deposit amount and a refund amount may both have to be greater than zero today. The deposit capability could later permit corrective entries. The refund capability could add a minimum processing amount. Sharing one PositiveAmountRule would couple two responsibilities that happen to agree at the moment.

Capability-local duplication is reasonable when the rules have different owners or reasons to change. The code remains close to the decision it explains.

The situation changes when several implementations claim to apply one regulation, one contractual policy, or one standard with the same authority and effective date. That is duplicated knowledge. It needs one authoritative representation and a way to prove that every evaluator applies it correctly.

That representation can be a database constraint, a versioned policy artifact, a standards dataset, generated code, or a conformance specification. A synchronous service is only one implementation choice.

## Hard invariants are enforced at commit

Consider BookStay and ChangeReservationDates. Both capabilities can occupy nights for a listing. The relevant invariant is:

A listing night can belong to at most one active reservation.

Both RPUs could call the same is_night_available() function and still violate that invariant. Two commands run at the same time. Both read the night as available before either has recorded anything. Both decide functions produce an accepted outcome, and both RPUs attempt to record it.

The storage mechanism must reject the second commit. In PostgreSQL, this could use a unique or exclusion constraint over the occupied nights. With an event store, the append must be conditional on the relevant context remaining unchanged. The PostgreSQL constraint documentation makes the same distinction between preliminary checks and integrity that the database maintains.

Each RPU still owns the domain response. BookStay may return StayUnavailable. ChangeReservationDates may return RequestedDatesUnavailable. The storage mechanism protects the state, and the capability gives the conflict its business meaning.

A shared helper can keep implementations textually consistent. Concurrent write safety comes from the commit mechanism. Research on invariant confluence reaches the same result formally: independent execution is safe only when independently valid results remain valid after they are combined. Some invariants require coordination.

An invariant can also require one atomic change across two capabilities. The commit point is then the coordination boundary for that invariant. Either one capability owns the whole transition, or the storage mechanism enforces the invariant atomically at commit. A Reactor cannot take this role. It sequences calls to RPUs after each of them has decided and committed its own outcome. It has no atomic commit authority, and it holds no domain decision.

## Identity has several owners

Identity can refer to domain identity, identifier integrity, identity proofing, authentication, or authorization. Each has a different responsibility.

Domain identity concerns continuity and sameness over time. The domain must say when two representations describe the same customer, reservation, or parcel. An identifier represents that decision; its format alone cannot define it.

Identifier uniqueness is a state concern. A rule such as "one account per issuer and subject" can be enforced through a unique constraint over the canonical identity key.

Identity proofing and authentication commonly belong to an external identity provider. The current NIST Digital Identity Guidelines separate identity proofing, authentication, and federation. The relying application then uses the resulting identity and assurance information for its authorization decisions.

In an RPU architecture, a Provider validates the external assertion and supplies explicit facts such as the subject, issuer, authentication time, and assurance level. The RPU decides whether that evidence is sufficient for its capability. Releasing a payout may require stronger assurance than reading a reservation.

A generic IdentityService.isAllowed() mixes authentication with domain authorization and hides the facts that explain its answer.

## Money carries stable semantics

Martin Fowler's Money pattern defines a monetary value through an amount and a currency. It also addresses two common errors: combining different currencies and applying implicit rounding.

A small immutable Money type can own those semantics. It can reject mixed-currency addition, use an exact numeric representation, and require an explicit rounding operation. ISO 4217 supplies standard currency codes and their minor-unit relationships.

Pricing, tax, refunds, deposits, and settlement still have their own business rules. Cancellation-fee rounding and exchange-rate selection belong to the relevant capabilities.

A balanced journal entry is a state invariant. The ledger's commit boundary must reject an unbalanced posting.

A pure Money type is a small shared dependency whose responsibility ends with monetary representation and arithmetic. Business operations and transaction coordination stay in the RPUs. Another option is to generate capability-local types from one specification and verify them with the same conformance tests.

## Compliance needs explicit policies

"Compliance" covers many kinds of obligation. ISO 37301 treats compliance as an ongoing management responsibility that includes implementation, evaluation, maintenance, and improvement.

Inside software, one obligation may prohibit a payout to a sanctioned party. Another may require identity evidence. Privacy law can require a lawful basis, a retention period, or deletion. Some cases need human judgment and recorded approval.

Using a general ComplianceService.isAllowed(command) removes the information needed to understand the result. Which policy applied? Which jurisdiction? Which release? Which facts were considered? Which obligation caused the rejection?

A policy assessment needs an explicit shape:

    PolicyAssessment {
      policy_id: "AML-42",
      release_id: "2026-07-15",
      jurisdiction: "EU",
      effective_from: ...,
      result: prohibited,
      reason_codes: ["SANCTIONS_MATCH"],
      observed_at: ...,
      valid_until: ...
    }

The RPU loads that assessment into its command context, and its decide function produces the capability outcome. A payout RPU may record PayoutRejected with the assessment reference and its own reason.

Current information such as sanctions, revoked credentials, or account freezes may require an external Provider call in the Imperative Shell. An assessment with explicit observation and expiry times can be recorded as a fact and consumed by later RPUs. In both cases, the Functional Core receives explicit data and produces the final decision.

## One policy can have many local evaluators

A shared policy can have one authority and many local evaluators.

The policy authority publishes an immutable release containing its identifier, content digest, jurisdiction, effective period, and source references. Each RPU can evaluate that release through generated code, a pure package, or a locally distributed policy bundle.

Activation needs its own authoritative fact. An ActivatePolicyRelease capability can record the active release in the Application State after the required evaluators have received and verified it. Each affected RPU loads that fact into its command context. If the active release changes before the outcome commits, the conditional commit fails, and the RPU decides again on the facts that now hold. The recorded outcome retains the policy release and reason codes used for the decision.

The effective-time rule determines which release applies. Historical review uses the release recorded for the original decision.

Every release should include a conformance suite with accepted cases, rejected cases, boundary values, missing facts, expired evidence, and jurisdiction-specific examples. The same cases run against every evaluator and RPU integration. The result is semantic consistency with local execution.

Deployment needs the same precision. New evaluators must understand a release before it becomes active. An instance that cannot evaluate the active compliance policy should reject the command explicitly. Silent use of an older release produces decisions that can no longer be explained.

Open Policy Agent bundles show one technical form of this approach: policies and data are authored centrally and distributed to local evaluators. The documentation also states that distribution is eventually consistent. A hard legal cutoff therefore needs a controlled activation process that verifies evaluator readiness.

## Clarifying what capabilities share

My current Application State documentation calls it "the only thing" capabilities share. Its scope is domain ownership. RPUs share no mutable domain model, internal decision functions, or calls to other RPUs.

A Money type, identifier primitive, generated currency catalogue, or policy evaluator is a different kind of dependency. A more precise formulation is:

Each capability retains ownership of its business decisions. Shared semantic primitives and authoritative policy artifacts stay small, pure, explicit, and versioned.

Teams that want absolute code independence can keep the implementations local and use generation plus conformance tests. Teams that share stable semantic primitives must acknowledge the coupling. Both choices are coherent when the boundary stays explicit.

## Ownership follows the decision

Capability autonomy gives every command-to-outcome decision one owner. Currency codes, authenticated identities, policy releases, and state integrity still have their own authorities.

The RPU owns the command-to-outcome decision. The Application State holds persistent invariants, and its storage mechanism enforces them at commit. Providers supply external facts. A policy authority publishes one identifiable release. Local evaluators and shared conformance cases keep its interpretation consistent.

Fowler's Service Layer defines an application boundary through its available operations and coordinates the application's response. Here, each RPU is the complete processing boundary for one capability. Shared components stop at semantic representation, fact supply, policy publication, or commit integrity.

A rule can have one authority and many local evaluators. Capability autonomy depends on keeping the final decision with the capability that owns it.

Cheers!

### Sources
- Leslie Lamport, Inductive Invariants
- David Thomas and Andrew Hunt, The Pragmatic Programmer, 20th Anniversary Edition, DRY chapter excerpt
- PostgreSQL documentation, Constraints
- Peter Bailis et al., Coordination Avoidance in Database Systems
- NIST SP 800-63-4, Digital Identity Guidelines
- Martin Fowler, Money, Patterns of Enterprise Application Architecture catalog
- ISO 4217, Currency codes
- ISO 37301, Compliance management systems
- Open Policy Agent documentation, Bundles
- Martin Fowler, Service Layer, Patterns of Enterprise Application Architecture catalog
