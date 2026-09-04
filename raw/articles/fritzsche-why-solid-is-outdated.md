---
source_url: https://ricofritzsche.me/why-solid-is-outdated/
title: Why SOLID Is Outdated
author: Rico Fritzsche
publication: ricofritzsche.me ("Thinking in Events")
published: 2026-08-01
retrieved: 2026-08-03
type: article
---

# Why SOLID Is Outdated

*Enterprise development still treats twenty-year-old design rules as current best practice.*

*(Image licensed under the Unsplash+ License.)*

I recommended SOLID for years. I was wrong.

The principles were priced for a world of hour-long compiles and risky releases. That world ended many years ago; the rules stayed. Enterprise software development has treated these five letters as settled truth for twenty years: they shape code reviews, job interviews, and training material in C#, Java, and TypeScript alike. In my own use, AI coding agents reproduce the same structures unless the repository gives them a different design policy. A beginner sees IRepository and learns that an interface proves good design. A reviewer sees a changed switch and asks for a strategy hierarchy. The abstractions arrive before the code contains a boundary worth protecting.

The precise claim:

SOLID is wrong as a general design doctrine and as a default checklist.

The tooling argument names the smaller problem. The deeper defect was present from the beginning: the principles never contained the facts required to decide where an abstraction pays for itself. Several ideas may remain useful under very specific constraints, and I no longer accept a bare principle as a review argument. I make the case in C#, where I know the habits best; the argument does not depend on the language.

## Five Letters from Different Eras

SOLID combines ideas written at different times for different problems. Barbara Liskov described the rule for behavioral sub-typing now called the Liskov Substitution Principle (LSP) in 1987, later developed with Jeannette Wing. Bertrand Meyer named the Open/Closed Principle (OCP) in the 1988 first edition of Object-Oriented Software Construction. Robert C. Martin collected OCP and LSP together with his own Dependency Inversion Principle (DIP) and Interface Segregation Principle (ISP) in his 2000 paper Design Principles and Design Patterns, and gave the Single Responsibility Principle (SRP), which he had named in the late 1990s, its own chapter in his 2002 book Agile Software Development, Principles, Patterns, and Practices. Martin later recalled that Michael Feathers pointed out the SOLID ordering in an email around 2004.

The acronym puts a sub-type contract, a cohesion rule, an extension policy, an interface technique, and a dependency rule at the same level. They address different problems and need different preconditions.

Four of the five share a second defect: no failure signal. A team applying SRP, OCP, ISP, or DIP to the letter gets no indication when the rule is damaging the design; every split, every extension point, and every interface counts as compliance. A rule that calls every outcome compliance guides nothing. LSP is the exception. A broken sub-type contract produces wrong behavior a test can catch.

Martin argued in 2020 that SOLID remains current because software still consists of sequence, selection, and iteration. That defense covers what programs are made of. The original case for the principles rested on what change cost, and that cost depends on the surrounding tool chain. A language-aware rename can update statically known symbol references within a solution; modern version control makes small edits recoverable; CI can build and run dotnet test on every pull request. Configuration strings, reflection, generated code, and external consumers still need separate checks. These tools shorten feedback on revised source. Tests report only the behavior they exercise.

## Open/Closed Is a Bet on Prediction

Martin's 2000 paper uses a slow compile and a source-control check-in taking hours as examples of what it calls environment viscosity. It also presents OCP as the most important object-oriented design principle: change what a module does by adding code while leaving its existing source alone.

Dan North connects OCP directly to that economics. In the 1990s, large C++ builds were expensive, automated refactoring was uncommon outside Smalltalk, and file-based version control made renames painful. Preserving working source was a sensible risk policy.

The prescription built on that policy was weaker from the start. Closing a module requires knowing where change will arrive, and Martin's 1996 article concedes the point: closure "must be strategic", and choosing what to close against "takes a certain amount of prescience derived from experience". Prescience is a guess with no test. An extension point built for a variation that never came was dead structure in 1996 exactly as it is today; the era's economics only decided which mistake cost more.

Modern tooling has reduced the cost of changing team-owned source. A published NuGet API, a plug-in contract, an event schema, or a service consumed by another team can still be expensive to change because its callers cannot move with it. Those boundaries justify versions and extension points.

Martin made a similar qualification in 2013: get the code into a position where behavior changing in expected ways does not force sweeping changes across the system's modules. He pointed back to his 1996 article, which describes strategic closure against certain kinds of change. The design questions are concrete: can the module and all its callers ship together? Must several behaviors coexist at runtime? How often has this variation occurred?

One yes is enough to justify the contract; otherwise direct change is cheaper.

Inside one application, speculative closure has a recurring cost. A second discount type is predicted, so IDiscountRule, a selector, registrations, implementations, and mock-based tests appear around one calculation. The predicted variation may never arrive. A later rounding change edits the implementation anyway. The wrong guess stays in the code-base, together with every concept it brought. North calls this the "Cruft Accretion Principle". I change the local code first and introduce an extension point when callers change independently, several behaviors must coexist, or the same variation returns often enough to establish a stable contract.

## "One Reason to Change" Decides Nothing

SRP says that a module should have "one and only one reason to change". Apply that sentence to invoice code and count the reasons: tax rules change, the PDF layout changes, the database that stores the invoices changes, finance requests one adjustment and compliance requests another. A team can split the code by technical concern, stakeholder, business capability, or deployment ownership and claim SRP each time. The sentence permits all of these boundaries.

Each boundary satisfies "one reason to change"; the sentence does not choose between them.

In common .NET code bases and tutorials, the typical approach is (and always has been): one class per technical concern; for example, a calculator class, a validator class, a mapper class, a formatter class and a repository class. One product change then crossed all five classes. The code had many responsibilities according to the folder structure and one responsibility according to the business request. The rule approved that structure. A sentence that accepts every boundary cannot reject a harmful one.

Martin's 2014 explanation makes the stakeholder interpretation explicit: "This principle is about people." A module should answer to one tightly coupled group that requests changes. That is more specific than the slogan, and it still leaves a choice when one product team owns pricing, presentation, and storage together.

David Parnas gave a concrete decomposition criterion in 1972. Start with the difficult design decisions and the decisions likely to change. Give each module one of those decisions to hide. For the invoice example, "how we calculate the amount owed" is such a decision. Its inputs, rules, and outcome belong together even when the implementation needs more than one small class.

John Ousterhout adds a useful test: a good module hides substantial complexity behind a simple interface. Every class and method introduces another interface for a reader to learn. Splitting code improves the design when the new module hides knowledge; splitting related knowledge across shallow classes increases navigation.

## Every Interface Needs a Reason

Martin's 2000 statement of DIP says dependencies should point toward abstractions. The paper then calls a literal ban on concrete dependencies "draconian" and allows stable concrete modules as a mitigating case. The nuance often disappears in .NET teaching. "Depend on abstractions" becomes "prefix every service with I".

.NET's built-in container accepts concrete registration directly:

    services.AddScoped<InvoiceCalculator>();

The interface mapping is justified when it enforces an architectural dependency direction, narrows the exposed contract, or supports an alternative implementation, proxy, decorator, or independently built consumer:

    services.AddScoped<IInvoiceCalculator, InvoiceCalculator>();

A local pair with the same owner, lifecycle, and dependency direction adds a type, a name, usually a file, a registration mapping, and another navigation step. A mock often makes tests assert calls on that duplicated shape. The production code still contains one behavior.

Local decision logic can be tested through its result:

    public enum CustomerTier
    {
      Standard,
      Preferred
    }

    public sealed record Invoice(decimal Subtotal, CustomerTier Tier);

    public static class InvoicePricing
    {
      public static decimal Total(Invoice invoice)
      {
        var discount = invoice.Tier == CustomerTier.Preferred
          ? 0.10m
          : 0m;

        return decimal.Round(
          invoice.Subtotal * (1m - discount),
          2,
          MidpointRounding.ToEven);
      }
    }

The input is an immutable value. The calculation has no I/O, and a test compares the returned decimal. A remote tax provider changes independently, so an interface can isolate its API. The pricing calculation remains a direct call.

Each extra type adds another name and navigation step.

Microsoft's current C# guidance describes an interface as a contract that multiple types can implement, including unrelated types. Before adding an interface, I ask two questions: Which code will depend on it? What should be able to change without changing that code?

## LSP and ISP Have Bounded Scope

LSP is the most precise member of the set. Liskov and Wing define behavioral sub-typing so that properties established for a super-type continue to hold for its sub-types. A C# implementation must honor the contract its consumer expects. This remains a sound correctness condition wherever genuine sub-type relationships exist. Its scope ends at the sub-type contract; invoice module boundaries remain a separate decision. It is also a different kind of statement: a correctness condition from type theory, standing in a list of heuristics and lending them a rigor they did not earn. Its scope ends at the sub-type contract; invoice module boundaries remain a separate decision.

ISP addresses clients forced to depend on interface members they do not use. That matters for a large public interface, separately compiled consumers, or an existing class used by different client roles. A sole consumer can still have an ISP problem when the interface it depends on contains members it never calls. A consumer that uses the whole small contract gains nothing from a further split; the split adds names without reducing the dependency surface.

A 2024 controlled experiment ran three independent trials with 100 data scientists. Groups reading SOLID-restructured industrial machine-learning code rated it easier to understand than groups reading the original code, with statistically significant results in aggregate. The comprehension measures were self-ratings on questionnaires, results for individual principles varied across the trials, and the authors call for replications. The study measured short-term comprehension of selected ML code; its scope excluded long-term maintenance and interface-heavy enterprise applications.

## Start the Review with the Change

I now start a design review with the change itself. Which business decision is changing? Who requests it? Can the module and its callers ship together? Which dependency has its own lifecycle or more than one current implementation? The answers determine whether a boundary is justified.

For decision code, I prefer immutable inputs and a function whose result states the outcome. I keep the facts and rules for one decision in the same module. The module exposes one small operation and keeps those rules together. I add an abstraction for a published contract, an independently changing effect, or multiple runtime behaviors.

North's CUPID proposal from 2022 replaces the five principles with five properties: composable, following the Unix philosophy, predictable, idiomatic, and domain-based. A property holds by degree, so a team can assess one in context and improve it without creating another type.

SOLID addressed real costs. A compile could run for hours, a check-in could take longer, and every modification risked a shipped binary. Under those conditions, leaving working code alone was rational risk management. Predicting the right extension points was a gamble even then. The costs that excused wrong guesses fell, the rules stayed, and a rule that outlives its cost turns into ritual.

The correction costs one question per abstraction: which concrete change does this boundary make cheaper, and who asks for that change? A contract another team builds against answers it. A tax service that releases on its own schedule answers it. An interface with one implementation, one owner, and one caller has no answer, and every reader pays for it on every navigation until someone deletes it.

If a tutorial today still teaches the five letters SOLID as current best practice, the tutorial is outdated. Same for the training deck, the interview question, and the code review comment.

Cheers!

### Sources
- Robert C. Martin: Design Principles and Design Patterns (2000)
- Bertrand Meyer: Object-Oriented Software Construction, second edition
- Barbara H. Liskov: Data Abstraction and Hierarchy (1987)
- Robert C. Martin: The Open-Closed Principle (1996)
- Robert C. Martin: Clean Architecture (2017)
- Robert C. Martin: An Open and Closed Case (2013)
- Robert C. Martin: The Single Responsibility Principle (2014)
- Robert C. Martin: Solid Relevance (2020)
- Dan North: CUPID: the back story (2021)
- Dan North: CUPID: for joyful coding (2022)
- David L. Parnas: On the Criteria To Be Used in Decomposing Systems into Modules (1972)
- Barbara H. Liskov and Jeannette M. Wing: A Behavioral Notion of Subtyping (1994)
- John Ousterhout: Modular Design, Stanford CS 190 lecture notes (2018)
- Microsoft: Service registration in .NET dependency injection and C# interface guidance
- Microsoft: Rename and move refactorings and test validation with GitHub Actions
- Raphael Cabral et al.: Investigating the Impact of SOLID Design Principles on Machine Learning Code Understanding (2024)
