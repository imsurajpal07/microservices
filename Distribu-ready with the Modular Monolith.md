## Distribu-ready with the Modular Monolith: Key Insights, Patterns, and Examples

### Introduction: Navigating the Hype Around Microservices

The last decade has brought an explosion of interest in microservices and distributed architectures, often promoted as essential for modern, large-scale systems. However, many teams have encountered the pain of *“Distributed Monoliths”*: projects that fell into a complexity trap by prematurely dividing code into services without genuine need or readiness. The results? Difficulty in development, deployment nightmares, accidental tight coupling, and lost developer productivity.

***

### 1. The Problem: Accidental Complexity \& The “Distributed Monolith”

> “Complexity is your enemy. Any fool can make something complicated. It is hard to keep things simple.” — Sir Richard Branson

#### Why Not Jump Directly to Distributed Systems?

- **Monoliths:** Simple to debug, deploy, and work with locally. Scale is vertical/horizontal. Cons: Can become hard to maintain if not modularized.
- **Microservices:** Fine-grained, independent scaling and deployments. Cons: Orchestration, distributed debugging, local development with containers, network issues, and data consistency make life much harder.
- **Distributed Monoliths:** The worst of both worlds—split code with tight database coupling, creating entangled services that force teams into painful cross-service deployments. No real independence, but with all the infrastructure complexity.

**Golden Rule:** If you cannot definitively say “yes, we truly need microservices,” then you *don’t need* microservices. Most teams overcomplicate their systems by adopting distributed architectures too soon.

***

### 2. The Modular Monolith: Modern Architecture for Simplicity \& Growth

#### What is a Modular Monolith?

A **Modular Monolith** is a single executable where internal domain boundaries and features are implemented as separate, well-encapsulated modules. These modules are highly cohesive (tightly related code grouped together) and loosely coupled (modules interact only via well-defined interfaces).

**Analogy:** The *KitKat Pattern*

- Imagine a KitKat bar: Each “finger” is a module, distinct but part of the bar. You can break one off without disturbing the others (i.e., can be extracted to microservices later!).

***

### 3. Designing the Modular Monolith

#### Step 1: Find Natural Module Boundaries

- Start broad: Group your code around natural business domains—e.g., Orders, Inventory, Notifications, Payments.
- Use *Domain-Driven Design* (DDD) ideas of *high cohesion* (code working on the same concerns) and *loose coupling* (minimal interdependence).
- Start with large chunks; refactor to smaller modules only as needed—avoid going too granular initially.


#### Step 2: Encapsulate Each Module

- Each module should contain everything related to its purpose: APIs, logic, and data access layers.
- In .NET, modules can map to assemblies or projects (class libraries), but the same applies to Java modules/packages.


#### Step 3: Handle the Database

- **Code-first**: Extract code first, then address data separation. Easier for code, trickier for data.
- **Data-first**: Extract and partition your data first, then move code. Often better if data will be tricky to separate.
- **Shared database is okay** if you remain a monolith, but recognize the *technical debt*: if you go distributed, you *must* split the data.


#### Step 4: Make Modules Independently Deconstructible

- No direct cross-module dependencies—use interfaces or contracts.
- Apply macro-level *Single Responsibility Principle*: Every module has one purpose.
- When a module can be carved out cleanly (self-contained with contracts), it can become a standalone service later.

***

### 4. Module Communication Patterns

#### Internal Communication

- Prefer using an abstraction layer (mediator/message broker) instead of direct module-to-module calls. This minimizes future refactoring pain when extracting modules as independent services.
- Example patterns:
    - **Mediator pattern**: Central mediator object manages all inter-module requests.
    - **Messaging/event-driven**: Producers send events to a queue/broker; consumers pick what interests them.


#### External Communication

- All external requests come via a single entry point (e.g., Web API).


#### Sample Implementation (Pseudocode—Java style):

```java
public interface OrdersContract {
    void submitOrder(OrderDto order);
    OrderDetailsDto getOrderDetails(String orderId);
}

public class OrdersModule implements OrdersContract {
    // Internal logic, only exposes contract methods
}
```

- Modules interact *only* via contracts or message interfaces; implementation details are hidden.

***

### 5. When to Carve Out a Module—Satellites and The Distributed-Ready Advantage

- **Satellite Pattern:** A modular monolith can “break off” a module that needs to scale independently (e.g., notification service → serverless function/container) while retaining the rest as a monolith.
- As requirements grow, you carve off more modules as “satellites,” incrementally evolving towards distributed if truly necessary.

***

### 6. Enforcing Architecture: Code, Culture, and Automation

#### Prevent Slipping into a Distributed Monolith

- **Code Review:** Ensure deep knowledge of architecture within the team.
- **Compile-Time Encapsulation:** Use language features (private/internal classes, package visibility) so modules can only interact via contracts/interfaces.
- **Automated Static Analysis:** Set up checkers to enforce module boundaries.
- **Architecture Tests:** Automated tests at the assembly/package level to prove forbidden access is impossible.
- **Style Guide \& Documentation:** Document module boundaries, permitted interactions, and onboarding for newcomers.

***

### 7. Example Flow: Building with the Modular Monolith

1. **Project setup:** Each module as a separate project/package.
2. **Web/API entrypoint:** References modules, but modules don’t reference each other.
3. **Dependency Injection:** Entrypoint injects dependencies into modules.
4. **Service contracts:** Modules implement public contracts/interfaces for communication.
5. **Messaging infrastructure:** Optionally add internal event/messaging system (RabbitMQ, Kafka, or Java equivalents) to decouple further and ease future module extraction.

***

### 8. Sample Modular Monolith Project Structure (Java/Spring Boot Inspired)

```
/myapp
  /orders-module
    - OrderService.java
    - OrdersContract.java
  /inventory-module
    - InventoryService.java
    - InventoryContract.java
  /notifications-module
    - NotificationService.java
    - NotificationsContract.java
  /web-api
    - MainController.java
    (imports all Contracts, injects all modules)
```

- All module dependencies and imports are one way—from API to modules.
- **No module-to-module calls**; always through contract interfaces or messaging.

***

### 9. Final Recommendations

- Be *pragmatic*, not dogmatic: Don’t pursue microservices or modular monoliths out of hype; decide based on the real, current needs of your team and business.
- **Loose coupling, high cohesion**: This principle guides maintainable modularization.
- **Accept technical debt**: Shared database or shortcuts may be necessary—just recognize and document the trade-off for future remediation.

***
### 9.Diagrams:

<img width="3465" height="1337" alt="Modular Monolith_1" src="https://github.com/user-attachments/assets/6ad78106-5647-4a90-9cd1-52fd057b06c8" />


<img width="5042" height="1737" alt="Modular Monolith_2" src="https://github.com/user-attachments/assets/a15048cd-7e57-4187-bcfd-588500de6688" />


<img width="4983" height="1536" alt="Modular Monolith_3" src="https://github.com/user-attachments/assets/df665c3f-ef3c-43a3-84dc-89c54b1a2954" />


<img width="4862" height="1137" alt="Modular Monolith_4" src="https://github.com/user-attachments/assets/c84d35fc-84f4-48c6-8891-b4c3b9ff500f" />


<img width="4862" height="1137" alt="Modular Monolith_5" src="https://github.com/user-attachments/assets/77b20080-4bcc-4afd-99e8-d34696e9e5b7" />


<img width="5339" height="1137" alt="Modular Monolith_6" src="https://github.com/user-attachments/assets/b49ebbe2-cd14-4147-a1b3-2deef2c9b3a0" />


<img width="7742" height="1636" alt="Modular Monolith_7" src="https://github.com/user-attachments/assets/53cc7fd2-9ad1-4ab7-92ef-b7e8d486095a" />


<img width="5285" height="1838" alt="Modular Monolith_8" src="https://github.com/user-attachments/assets/b3842d25-c654-468a-be1c-98b60349baa4" />


<img width="6832" height="2338" alt="Modular Monolith_9" src="https://github.com/user-attachments/assets/75b50025-bf58-4663-9bb8-61c47274f000" />


<img width="3900" height="1537" alt="Modular Monolith_10" src="https://github.com/user-attachments/assets/725fe55e-7601-48b6-a789-1a83e7a6ce86" />


***

## Conclusion: The Modular Monolith as Your Future-Proof Foundation

The modular monolith is a battle-tested architectural approach that sets you up for growth, balances simplicity and extensibility, and allows you to “go distributed” only when truly required. If you’re building with Java or .NET, focus on well-defined contracts, keep your module boundaries strict, and avoid premature microservices migrations.

Move incrementally, automate your architectural rules, and use messaging where appropriate to minimize future friction. **The modular monolith is “distribu-ready”—grow your software right!**

***

### References

This post summarizes and restructures ideas and recommendations presented by Layla Porter at NDC Oslo 2024. For further exploration, see her talks, slides, and associated blog posts or check out the full video for advanced diagrams and coding demos.

<div style="text-align: center">https://www.youtube.com/watch?v=L3r1k8_Bi1M&t=2179s</div>

[^2]: https://www.youtube.com/watch?v=L3r1k8_Bi1M\&ab_channel=NDCConferences

