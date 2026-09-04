---
source_url: https://nick-tune.me/blog/2026-08-13-enforced-application-architecture-for-agents-and-humans/
title: "Enforced application architecture for agents and humans"
author: Nick Tune
publication: nick-tune.me
published: 2026-08-13
retrieved: 2026-08-17
type: article
---

# Enforced application architecture for agents and humans

*Enforcing application architecture instead of relying on markdown files*

AUGUST 13, 2026 — tags: AI, DDD, ARCHITECTURE, TYPESCRIPT

One of the most frustrating parts of AI-generated code is that it does not follow architectural guidelines that are written in skill files, ADRs, and various other places in the repo. A few months ago, I talked about a deterministic solution I had been working on.

I've been iterating on that approach. I still think it's good and now I have a richer mental model and understand more of the nuances and thought I'd dump a snapshot of my brain into a blog post.

The key things are:

- Different packages require different rules, so classify packages (e.g. domain model vs cli app)
- Strive for broad, generic rules at the layer level (folder A cannot import from folder B etc)
- Use more fine-grained role-based rules as a last resort (e.g. data-access layer can import aggregate from domain but it cannot import domain-service)
- Enforce domain boundaries

## Package classification and enforcement

I'm using NX monorepos for my TypeScript projects and this already provides an example of package classification: `/apps` folder is for runnable apps and `/packages` folder is for others. What I'm doing is making that more granular.

For example, I believe that isolating domain code from all the rest is crucial. The most important parts of how the business works should not be coupled with http controllers, database transactions, and plumbing stuff.

### domain-model

So I have a package type called `/domain-model`. A package that matches `packages/{subdomain}/domain-model` must have, and can only have, one root folder called `/domain` which cannot import from other subdomains' domain models or use-cases packages. My current DSL looks like this:

```
const domainRoles: RoleName[] = [
'aggregate',
'value-object',
'domain-event',
'domain-port',
'domain-service',
'domain-error',
]

export const domainModel = {
locations: locationConfiguration<RoleName>(
location('/domain', domainRoles, {
allowAnySubLocations: true,
importRules: {
allow: { anySubdomain: ['published-language'] },
},
}),
),
}
```

The argument `domainRoles` specifies that only code annotated with `aggregate`, `value-object` (and a few others) can live in this layer. Anything else is a hard fail of the build.

Inside the `/domain` folder, any sub-folders are allowed. I don't want or need restrictions here because domain models should express the business however necessary.

If you're only going to add one convention in your codebase, enforcing domain isolation is probably the best one.

There is one exception here: the package-level rules allow `/domain` to import published languages, which are pure contracts like schemas, and are usually versioned.

In my project the Rivière graph schema is a JSON Schema. The published language is a library that exposes those data structures as typescript objects for convenience (each consumer of the schema could just as easily generate those files for themselves from the schema and not use the library).

### use-cases

A use-cases package orchestrates processes from start to finish like raising an invoice or cancelling an order. Contrary to the domain model, I do want things to be highly standardised and boring. All the plumbing and orchestration should be similar for each use case.

So my configuration here specifies a whitelist of allowed directories (aka sublocations) oriented around features:

- All feature code must live in `/features/{feature}` (i.e. vertical slices)
- No sharing between feature folders (`importRules: { allow: {} }`)

```
location('/features/{feature}', {
commands: {
roles: commandRoles,
importRules: {
allow: {
sibling: ['data-access'],
ownSubdomain: ['domain'],
anySubdomain: ['published-language'],
},
},
},
queries: {
roles: queryRoles,
importRules: {
allow: {
sibling: ['data-access'],
ownSubdomain: ['domain'],
anySubdomain: ['published-language'],
},
},
},
'data-access/{concept}': { roles: dataAccessRoles },
'adapters/{adapter}': { roles: adapterRoles },
importRules: { allow: {} },
})
```

Human-readable version: ADR-002 describes the same architecture for humans. The ADR and executable Rivière configuration are kept aligned.

Each feature folder must provide its own:

- `/commands` => use cases that orchestrate write operations
- `/queries` => use cases that orchestrate query operations
- `/data-access` => aggregate repositories and query-model loaders
- `/adapters` => implementations of domain ports

## Domain boundaries

The configurations above define what is allowed inside each type of package. But there are also rules about packages themselves - where they can live, the dependencies they can have, and more importantly, how they must respect domain boundaries.

Firstly, I make it mandatory for most packages to live inside a subdomain (that contain domain-specific code).

```
export const config = roleEnforcementConfiguration({
configurations: {
'apps/': app,
'packages/{subdomain}/domain-model': domainModel,
'packages/{subdomain}/published-language': publishedLanguage,
'packages/{subdomain}/use-cases': useCases,
},
// ...
})
```

Violations or anything outside the above rules will fail the build. Like if you put a domain-model in the root of packages (no subdomain folder), the build fails.

This allows preventing coupling between subdomains. For example, the commands inside a use-cases in one subdomain, cannot touch the domain-model of a different subdomain. It can only import domain from its `ownSubdomain`:

```
commands: {
roles: commandRoles,
importRules: {
allow: {
sibling: ['data-access'],
ownSubdomain: ['domain'],
anySubdomain: ['published-language'],
},
},
},
```

## Layer-based rules vs role-based rules

Once the package layouts are organised, the next level of the hierarchy is layer-based rules: for any given folder, which others can it import from?

As we discussed, the domain-model should be pure and decoupled as much as possible. It cannot even import anything inside its own subdomain except a published language.

On the contrary, `/commands` and `/queries` can import their own domain model (only in their own subdomain / parent folder). Commands load and orchestrate domain objects needed to achieve their outcome. Queries read persisted state through `/data-access` and may use the domain model for domain-owned query behaviour.

```
queries: {
roles: queryRoles,
importRules: {
allow: {
sibling: ['data-access'],
ownSubdomain: ['domain'],
anySubdomain: ['published-language'],
},
},
},
```

On the other hand, app packages provide an experience to the user which often requires orchestrating or aggregating multiple subdomains (think of a BFF API for example). So it can import use-cases from multiple subdomains.

### role-based rules

Now, layer-based rules are not always enough to ensure that code is properly organised. Finer-grained control is sometimes needed. This is where role-based rules can be extremely useful.

Using ports and adapters as an example, I have an `/adapters` layer. The job of an adapter is to implement an interface defined in `/domain` (a domain-port). The adapter will use an external library or service to implement the logic.

In order to achieve this, the adapter needs to import from `/domain` and `/infra/external-clients` and join the two together. Our bespoke domain model and generic infrastructure code cannot reference each other.

```
import type { ReadWorkflowGitStatus } from '@living-architecture/dev-workflow-v2-domain-model/domain/ports/read-git-status'
import type { GitRepositoryStatus } from '../../../../infra/external-clients/git/git-client'

/** @riviere-role domain-port-adapter */
export function createWorkflowGitStatusReader(
readGitRepositoryStatus: () => GitRepositoryStatus,
): ReadWorkflowGitStatus {
return () => {
const status = readGitRepositoryStatus()
return {
changedFilesVsDefault: status.changedFilesVsDefault,
currentBranch: status.currentBranch,
hasCommitsVsDefault: status.hasCommitsVsDefault,
headCommit: status.headCommit,
workingTreeClean: status.workingTreeClean,
}
}
}
```

But I don't want the adapter to be able to import everything from `/domain` otherwise domain logic can easily end up there. AI does dumb stuff like that all the time even with a million lines of markdown screaming at it not to do that.

To solve that problem, I have a role-based rule that says the adapter layer can only import code with the type `domain-port` from `/domain`. Nothing else, no aggregate or domain-service etc. The rule for that looks like this:

```
'adapters/{adapter}': {
roles: adapterRoles,
importRules: {
allow: {
root: ['infra'],
ownSubdomain: [{ domain: ['domain-port'] }],
},
},
},
```

You might think that AI will just put all the logic in a domain-port but that role is highly constrained so it can't.

A similar example is `/data-access`. This can import from `/domain` because it needs to load an aggregate, but it can only import `aggregate` and `value-object` not `domain-service` because that type of coupling should never happen.

What I'm saying is, even though `/data-access` CAN depend on `/domain` it cannot access EVERY type of code in there, only a subset. I can't achieve this through layers, so I filter on layer + role.

```
'data-access/{concept}': {
roles: dataAccessRoles,
importRules: {
allow: {
sibling: [{ queries: ['query-model'] }],
root: ['infra'],
ownSubdomain: [{ domain: ['aggregate', 'value-object'] }],
anySubdomain: ['published-language'],
},
},
},
```

### role constraints

As I showed in the previous blog post, you can go a level further and constrain the shape of an individual role to enforce consistency in a codebase or to prevent logic being put in the wrong place.

I want all value objects to be consistent and follow certain rules. Even if that means some code is not as elegant as I would like, consistency makes things easier to navigate and, more importantly, enforce. So I optimise for that.

Here my value objects are constrained like this:

```
role('value-object', {
targets: ['class'],
forbiddenCallableDataMembers: true,
forbiddenSupertypes: ['Error'],
requiredPrivateMembers: ['brand'],
requiresPrivateConstructor: true,
requiredStaticMethodNamePrefix: 'parse',
requiresDataMembers: true,
forbiddenDependencies: ['aggregate', 'domain-service'],
})
```

So they all look roughly like this:

```
import { z } from 'zod'

const schema = z.string()

/** @riviere-role value-object */
export class State {
declare private readonly brand: 'State'

private constructor(readonly value: string) {}

static parse(value: string) {
const parsed = schema.safeParse(value)
return parsed.success
? { success: true as const, state: new State(parsed.data) }
: { success: false as const, error: parsed.error }
}
}
```

You could use the type system to define a base class and use a role definition to enforce the base class. Different ways you can achieve a lot of these constraints, it's the concept which is the main thing to focus on.

What is important is what I alluded to above: not only does this make code consistent, but it makes the code highly constrained. AI cannot implement an aggregate inside value-object because an aggregate-repository must return an aggregate. So it wouldn't be able to load it.

## Is all of this worth it?

It's interesting, and I'm still figuring things out. I think at some level yes, it's worth it. How far down the configuration layers you go is the real question.

Package, domain, and layer-based rules are pretty easy to set up and enforce. I find it hard to justify not adding those. If you can't set codebase standards at that level, I don't think you'll get far with agentic AI.

Adding role annotations to all your code, classifying every piece of code, and defining rules at the role-level? Yeah, still playing around with that. Come back in 6 months. I feel confident it's the right approach.

In addition, having this setup in place makes ongoing evolution easier. Every time AI finds a way to write dumb code, I have the ability to add small constraints and prevent it (that is not always as easy as I'm making out, and requires trading off optimal code vs consistent boring code).

Something else interesting, is that when planning new features, we can discuss up front which new roles are needed and where different parts of the solution will be implemented, which helps to get to the right outcome faster. Not big up-front design, but getting the rough shape right and identifying tricky decisions early.

If you want help adding this to your codebase, get in touch.
