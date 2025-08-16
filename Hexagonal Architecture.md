# Hexagonal Architecture: The Ports and Adapters Pattern Explained

*Based on Alistair Cockburn’s Writings and Philosophy*

***

## Introduction

Hexagonal Architecture, also called the **Ports and Adapters pattern**, was introduced by Alistair Cockburn to enable truly flexible, technology-independent applications. Its main promise: keep your business logic pure and decoupled, adapting easily to changing frameworks, database solutions, and user interfaces.

***

## Why “Hexagonal”?

Cockburn chose the hexagon shape simply to visualize multiple ways systems interact, not as a technical constraint.
> "The hexagon was chosen so we could illustrate–with at least six sides–an application’s ability to easily connect to different systems or actors." — Alistair Cockburn

***

## Core Principles
<img width="600" height="448" alt="image" src="https://github.com/user-attachments/assets/49812f5a-1880-4547-8b17-7e582b7dab38" />

### 1. Centered Business Logic

At the heart is the “hexagon” — your domain model and business rules. These core rules are not concerned with technology, frameworks, or devices.
**Goal:** The domain logic does not depend on any outside world concerns.

### 2. Ports

Ports are abstract interfaces through which the outside world interacts with your core.

- **Driving ports:** What the application offers, e.g., APIs, UIs.
- **Driven ports:** What the application needs externally, e.g., database or messaging access.


### 3. Adapters

Adapters implement the ports for specific technologies:

- **Driving adapters:** UI controllers, CLI commands, REST endpoints.
- **Driven adapters:** SQL repositories, Kafka consumers, etc.

This way, you can swap a technology, database, or UI without touching the business logic.
> “Adapters let you plug in new devices or systems–without changing the application's internals.”

***

## Actors: Drivers and Devices

Cockburn distinguished:

- **Drivers:** Initiate actions—users, schedulers, external systems.
- **Devices (Driven Actors):** The application triggers actions on—databases, queues, external APIs.

Ports and adapters shape the software’s communication with both categories, ensuring technology changes never affect the core.

***

## A Hexagonal Diagram Explained

Hexagonal architecture showing core business logic, ports, and adapters for external systems.

(see the generated image above)

**Explanation:**

- The business logic sits in the middle (hexagon).
- Outbound and inbound ports defined as interfaces.
- Adapters connect these ports to real technologies, such as HTTP APIs, SQL databases, test doubles, or event buses.

***

## Example: Applying the Pattern

Suppose you’re designing a library system.

- The **domain logic** (hexagon) maintains rules for book lending.
- **Driving ports:** Define how to interact with books (e.g., methods `lendBook()`, `returnBook()`).
- **Driving adapters:** REST API or CLI commands implementing these methods.
- **Driven ports:** Interface for fetching and persisting book data.
- **Driven adapters:** MySQL implementation, MongoDB, in-memory test storage.

If you switch from MySQL to MongoDB, you update only the adapter, never touching your business logic.

***

## Benefits, According to Cockburn

- **Total Decoupling:** Swap UIs, databases, messaging, or even test adapters without impacting the core.
- **Testability:** Easily inject test adapters for both inbound and outbound ports.
- **Extensibility:** Plug in any new technology with minimal refactoring.
- **Clarity:** Everyone sees what is business logic vs. external concern.

> “Hexagonal architecture makes it clear what belongs to the business and what belongs to technology.” — Alistair Cockburn

***

## Conclusion

Alistair Cockburn’s hexagonal architecture is not about shapes, but *boundaries*. Let ports and adapters shield your business rules from change.
Your application becomes truly technology-independent, testable, and evolvable—ready for anything the future brings.

**Put the hex in your next project for long-lasting, maintainable backend code!**

