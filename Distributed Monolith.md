# Distributed Monolith: The Anti-Pattern Between Monolith and Microservices

*With Practical Insights from Sam Newman’s “Building Microservices”*

***

## Introduction

As Java backend developers—and indeed, any engineers embarking on a microservices transition—one of the most insidious architectural traps you can fall into is the **distributed monolith**. It’s a system masquerading as microservices but retaining all the rigidity of its monolithic roots. Drawing from Sam Newman’s "Building Microservices," let’s explore what a distributed monolith is, how it emerges, what makes it so problematic, and how to break free.

***

## What Is a Distributed Monolith?

A **distributed monolith** is a system broken into multiple deployable services that are, in reality, still tightly coupled. While you gain the operational complexity of a distributed system, you forfeit the key advantages of microservices: autonomy, speed, and resilience. Sam Newman highlights this anti-pattern as a common outcome when teams try to “service-ify” monoliths without addressing internal dependencies and boundaries.[^1][^2]

> “A distributed monolith has many services, but everything has to be deployed at the same time, and requires lots of coordination between teams to get anything done.”
> — Sam Newman

***

## Core Characteristics

- **Tight Coupling:** Even though code is separated, services are interdependent—with changes in one cascaring into others.
- **Synchronous Calls:** Services often rely on synchronous communication, making them fragile and slow.
- **Shared Database:** Multiple services write to a common database (or schema), leading to entangled data logic.
- **Coordinated Deployments:** All services must be released together, destroying deployment autonomy.
- **Blurred Boundaries:** Domain lines are poorly defined, so "independent" services still cross responsibilities at runtime or in data models.[^2][^3][^4][^1]

***

## Why Do Distributed Monoliths Happen?

- **Superficial Decomposition:** Teams simply split code into different repositories/processes without changing the deeper design.
- **No Clear Domain Ownership:** The lack of domain-driven boundaries (as explained by Newman) means teams frequently trip over each other’s logic and data.
- **Shared State:** The same database or service state is referenced everywhere, maintaining a monolithic “single source of truth”.
- **Premature Microservices:** Adopting microservices before clarifying what really needs to be autonomous, frequently just to scale a small portion of functionality.[^3][^4][^1]

***

## Diagram: Distributed Monolith in Practice

Here’s a typical representation of a distributed monolith:

<img width="250" height="300" alt="image" src="https://github.com/user-attachments/assets/b2b636af-4f49-47c9-b190-2c42d7e5a6c3" />


**Features:**

- Each “service” is independently deployed but tightly coupled through synchronous APIs and a shared database.
- Deployment or schema changes require system-wide updates.

***

## Problems With Distributed Monoliths

- **No Real Independence:** Services can’t be developed or deployed alone—losing microservices’ core promise.
- **Operational Overhead:** As services multiply, supporting them (DevOps, monitoring, configs) gets harder, not easier.
- **Reduced Resilience:** A single service’s downtime can bring down the whole system thanks to synchronous dependencies.
- **Difficult Testing:** Integration testing is as challenging as with a classic monolith.[^4][^1][^2][^3]

***

## Getting Out (and Avoiding the Anti-Pattern)

Sam Newman’s books and talks offer proven strategies:

1. **Loosen Coupling:**
    - Every service should own its own datastore.
    - Questions and updates should flow through asynchronous events, not direct database access.
2. **Domain-Driven Boundaries:**
    - Use DDD to define clear domain ownership and responsibilities.
    - Each service should have a tight, focused business reason to exist.
3. **Incremental Transition:**
    - Don’t break up everything at once. Use patterns like the *strangler fig* to peel off independent functionality service by service.
4. **Autonomy as a Guiding Principle:**
    - Don’t aim for microservices. Aim for deployment, testing, and scaling independence.
    - When one service can be updated and deployed on its own, you’re on the right path.[^2][^4]

***

## Conclusion

A distributed monolith leaves you with high complexity and little flexibility—the very opposite of what microservices promise. As Sam Newman repeatedly asserts, it’s not the number of deployables that defines a microservice, but the autonomy, separation, and clarity of boundaries. Start with solid domains, ensure true independence, and split your monolith incrementally and intentionally.

If you see deployment coordination and shared databases pervading your “services,” stop: you’re seeing classic symptoms of a distributed monolith! Refactor towards autonomy, and you’ll gain the true benefits of a next-generation architecture.

***

*Inspired by Sam Newman’s “Building Microservices” and “Monolith to Microservices.”*


[^1]: https://codesmells.substack.com/p/conjoined-triplets-anti-pattern-design

[^2]: https://www.infoq.com/news/2020/05/monolith-decomposition-newman/

[^3]: https://danlebrero.com/2022/02/09/monolith-to-microservices-summary/

[^4]: https://www.graphapp.ai/blog/distributed-monolith-vs-microservices-a-comprehensive-comparison
