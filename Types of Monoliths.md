# Exploring Different Types of Monoliths: Insights from _Building Microservices_

Monolithic architectures are often the starting point for most backend applications, especially in the Java ecosystem. While the evolution to microservices is a hot topic, understanding the *different kinds of monoliths* and how they function is essential for every developer. Drawing on Sam Newman’s "Building Microservices" and follow-up literature, let’s dive into the variations within monolithic designs and the transition journeys they enable.

***

## What is a Monolith?

A **monolithic application** is constructed as a single, self-contained unit. All the functions—presentation, business logic, and data access—are part of one codebase, compiled and deployed as a single artifact (e.g., WAR or JAR in Java)[^1][^2].

***

## Main Kinds of Monoliths

Sam Newman’s work and subsequent notes identify several distinct categories of monoliths, each with its unique traits and pain points:

### 1. Traditional Layered Monolith

- **Structure**: Follows the classic "n-tier" (controller-service-repository) approach.
- **Deployment**: All code bundled into one deployable package.
- **Pros**: Simple to develop and deploy, efficient local interactions.
- **Cons**: Hard to scale, difficult for team autonomy, tightly coupled codebase[^1][^2].


### 2. Modular Monolith

- **Structure**: Organizes code into *modules* within the monolith, often by business domain (vertical slices).
- **Deployment**: Still packaged as one deployment unit.
- **Pros**: Improved maintainability, easier to understand boundaries, better team autonomy.
- **Cons**: Database and runtime coupling often remain[^1][^3].
- **Use Case**: Can be a stepping stone for moving to microservices.

> “Increase maintainability and team autonomy by modularizing the monolith. Instead of the traditional layered architecture, the subdomains are organized into vertical slices consisting of presentation, business, and persistent logic.” — Microservices.io[^1]

### 3. Distributed Monolith

- **Structure**: Appears like microservices (multiple processes/services), but with tight runtime or deployment coupling.
- **Deployment**: Multiple services must be built, tested, and deployed together.
- **Pros**: Potential for separation, individual scaling.
- **Cons**: Retain monolithic drawbacks—shared database, coordinated releases, fragile interdependencies[^3].


### 4. Third-Party Black-Box Monoliths

- **Structure**: Vendor systems (on-premise or SaaS) with integrated functionality.
- **Deployment**: Managed externally; little developer control.
- **Pros**: Quick deployment, plug-and-play.
- **Cons**: Hard to extend, integrate, or refactor; often acts as a bottleneck for new features[^3].

***

## Monolith Coupling Challenges

Sam Newman discusses several types of coupling seen in monoliths, which developers must recognize when considering a migration:

- **Implementation Coupling**: All changes, even minor, require full redeployment.
- **Temporal Coupling**: Services dependent on synchronous calls.
- **Deployment Coupling**: Release trains where multiple components must ship together.
- **Domain Coupling**: Overlapping responsibilities and unclear boundaries[^3].

***

## When Does a Monolith Make Sense?

| Aspect | Monolith Strength | Monolith Weakness |
| :-- | :-- | :-- |
| Simplicity | Easy to build, test, deploy | Less scalable as codebase grows |
| Team Size | Few developers, simple business | Coordination issues in big teams |
| Fault Tolerance | All or nothing | Entire system can go down |
| Technology Diversity | One stack for everything | Hard to switch technologies |
| Modularity | Possible within modular monolith | Still single deployment |


***

## Final Thoughts

Monoliths come in various forms: simple layered, modular, distributed, or even third-party integrations. Each has tradeoffs, and not all monoliths are equal. Recognizing **which type you’re using** is vital when planning improvements or considering a switch to microservices.

If your codebase is modular but maintains a single deployment artifact and shared database, you might be well-placed to iterate toward a microservices approach—a core theme in Sam Newman's books. Start by analyzing your couplings and modular boundaries; a thoughtful, evolutionary journey will serve your business better than a hasty leap into distributed complexity[^3][^4][^1].

***

> *In your migration journey, keep in mind: modularizing your monolith might be the best first step. Microservices are not the goal; agility, maintainability, and team autonomy are.*

<div style="text-align: center">⁂</div>

[^1]: https://microservices.io/patterns/monolithic.html

[^2]: https://www.clariontech.com/blog/monolithic-vs.-microservices

[^3]: https://danlebrero.com/2022/02/09/monolith-to-microservices-summary/

[^4]: https://www.boxpiper.com/posts/monolith-to-microservices-book-notes-summary-and-top-ideas

[^5]: https://www.bennadel.com/blog/3154-building-microservices-designing-fine-grained-systems-by-sam-newman.htm

[^6]: https://book.northwind.ir/bookfiles/building-microservices/Building.Microservices.pdf

[^7]: https://dl.ebooksworld.ir/books/Monolith.to.Microservices.Sam.Newman.OReilly.9781492047841.EBooksWorld.ir.pdf

[^8]: https://www.infoq.com/articles/github-monolith-microservices/

[^9]: https://samnewman.io/books/building_microservices_2nd_edition/

[^10]: https://alokai.com/blog/monolith-vs-microservices

[^11]: https://camunda.com/blog/2023/08/monolith-vs-microservice-architecture-comparison/
