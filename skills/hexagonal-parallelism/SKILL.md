---
name: hexagonal-parallelism
description: Guides the Architect Agent to apply Hexagonal Architecture (Ports & Adapters) and Dependency Inversion to maximize component decoupling, enabling the highest degree of parallel task execution by AI agents. Use this skill whenever designing the architecture for a new feature or module.
---

# Hexagonal Parallelism

This skill transforms Hexagonal Architecture from a mere "clean code" pattern into an **industrial parallelism strategy** for Agent-Driven Development. The Architect Agent MUST organize every Technical Checklist (`T00X` file) into **three sequential phases** that unlock massive parallel execution by Engineer Agents.

## The Mandatory Rule

> **Every Technical Checklist MUST be structured in 3 Phases. Tasks within a phase are parallel-safe. Phases are sequential.**

```text
Phase 1 → Domain      (parallel tasks, zero dependencies)
Phase 2 → Ports       (parallel tasks, depends on Phase 1)
Phase 3 → Adapters    (parallel tasks, depends on Phase 2) ← MAXIMUM PARALLELISM
```

---

## The Three Phases

### 🔵 Phase 1 — Domain Core

> *"We trigger multiple agents in parallel to implement pure business logic and entities. Zero infrastructure dependencies."*

| Aspect | Rule |
| -------- | ------ |
| **What to build** | Entities, Value Objects, Domain Services, Domain Events, Enums, Custom Exceptions |
| **Framework dependencies** | **NONE.** Zero framework annotations. Zero infrastructure imports. Pure language constructs only |
| **Parallelism** | Leaf entities (no domain composition) are fully parallel. Composite entities must declare `Depends On` for their parts |
| **Testing** | Unit tests with no mocks — pure logic validation |

**The Domain layer has zero FRAMEWORK dependencies.** No `@Entity`, no `@Component`, no `@JsonProperty`, no infrastructure types.

#### ⚠️ Intra-Phase Dependencies (Domain Composition)

Although Phase 1 has zero *framework* dependencies, **domain objects can depend on other domain objects** through composition and aggregation. The Architect Agent MUST identify these relationships and declare them explicitly.

Examples of intra-domain dependencies:

| Entity | Depends On | Reason |
| -------- | ----------- | -------- |
| `Order` | `OrderItem`, `OrderStatus` | Order contains a list of OrderItem and uses OrderStatus |
| `OrderItem` | `Product` | OrderItem references a Product |
| `OrderDomainService` | `Order`, `OrderItem` | Service operates on both entities |
| `OrderStatus` (enum) | — | Leaf node, no domain dependencies |
| `OrderNotFoundException` | — | Leaf node, no domain dependencies |

**Rules for intra-phase dependencies:**

1. **Leaf-first ordering:** Enums, Value Objects, and Exceptions with no domain dependencies are the **first tasks** — they are fully parallel.
2. **Composite entities second:** Entities that reference other domain objects must list them in `Depends On`.
3. **Domain Services last within Phase 1:** They typically depend on multiple entities and value objects.
4. **The Dependency Gate applies.** The Engineer Agent will verify that intra-phase dependencies are met before proceeding — even within the same phase.

#### Task Categories for Phase 1

- `[Domain-Model]` — Entities and Value Objects
- `[Domain-Enum]` — Enumerations and status types
- `[Domain-Service]` — Pure business logic services
- `[Domain-Event]` — Domain events
- `[Domain-Exception]` — Domain-specific exceptions

---

### 🟡 Phase 2 — Ports & Use Cases (The Boundaries)

> *"With the domain ready, agents define the interfaces. The contract is 'signed'."*

| Aspect | Rule |
| -------- | ------ |
| **What to build** | Input Ports (use case interfaces), Output Ports (repository/gateway interfaces), Application Services (use case implementations), DTOs, Commands, Queries |
| **Dependencies** | Depends **only on Phase 1** artifacts. References Port interfaces, never adapters |
| **Parallelism** | Each use case and each port interface is an **independent task** |
| **Testing** | Unit tests with mocked Ports |

**Ports are the signed contracts.** Before Phase 3 begins, every Port interface must define:

- Method signatures using **domain types** (not framework types).
- Javadoc/JSDoc describing the expected behavior and edge cases.
- Error contract: which exceptions/errors can be thrown.

#### Task Categories for Phase 2

- `[Port-In]` — Input Port interfaces (driving/use case interfaces)
- `[Port-Out]` — Output Port interfaces (driven/repository/gateway interfaces)
- `[UseCase]` — Application Service implementations (use case orchestration)
- `[DTO]` — Commands, Queries, and Data Transfer Objects

---

### 🟢 Phase 3 — The Adapter Explosion

> *"Since the ports are already defined, I can deploy an army of agents: one implements persistence (JPA/SQL), another the Web REST layer, and another the messaging consumers. All at the same time."*

| Aspect | Rule |
| -------- | ------ |
| **What to build** | REST Controllers, JPA/Hibernate Repositories, Message Consumers/Producers, External API Clients, Mappers, Database Migrations, Configuration classes |
| **Dependencies** | Depends **only on Phase 2** Port interfaces. **No adapter may reference another adapter** |
| **Parallelism** | **MAXIMUM.** Every adapter is a fully independent task. The JPA agent has zero knowledge of the REST agent |
| **Testing** | Integration tests per adapter in isolation |

**This is where the magic happens.** Because every adapter only depends on a Port interface (defined in Phase 2), they can ALL be built at the same time by different agents.

#### Task Categories for Phase 3

- `[Adapter-Persistence]` — JPA/SQL/Prisma repository implementations + JPA entities + mappers
- `[Adapter-Web]` — REST controllers, request/response objects, API docs
- `[Adapter-Messaging-In]` — Message consumers (Kafka, RabbitMQ, SQS)
- `[Adapter-Messaging-Out]` — Message producers/publishers
- `[Adapter-External]` — External API clients (HTTP, gRPC, SDK wrappers)
- `[Adapter-Infra]` — Database migrations (Flyway/Liquibase), configuration classes

#### The Zero Cross-Reference Rule

> **No adapter may import, reference, or depend on another adapter.**

- ❌ A REST controller directly calling a JPA repository.
- ❌ A message consumer importing a REST DTO.
- ❌ An external API client depending on a database entity.
- ✅ The only legal dependency path: `Adapter → Port ← Application Service → Domain`

---

## How to Structure a Technical Checklist

When generating a `T00X` file, the Architect Agent MUST organize tasks as follows:

### Template

```markdown
#### Technical Checklist (Atomic Tasks)

##### 🔵 Phase 1 — Domain Core (Zero framework dependencies)
###### Leaf nodes (fully parallel — no domain dependencies)
- [ ] Task 001 - [Domain-Enum]: Create `OrderStatus` enum
- [ ] Task 002 - [Domain-Exception]: Create `OrderNotFoundException`
- [ ] Task 003 - [Domain-Model]: Create `Product` value object

###### Composite nodes (parallel within group — depend on leaf nodes above)
- [ ] Task 004 - [Domain-Model]: Create `OrderItem` value object (Depends On: Task 003)
- [ ] Task 005 - [Domain-Model]: Create `Order` entity (Depends On: Task 001, Task 004)

###### Domain services (depend on entities above)
- [ ] Task 006 - [Domain-Service]: Implement `OrderDomainService` (Depends On: Task 005)

##### 🟡 Phase 2 — Ports & Use Cases (All tasks parallel-safe | Depends on Phase 1)
- [ ] Task 007 - [Port-Out]: Define `OrderRepository` output port interface
- [ ] Task 008 - [Port-Out]: Define `PaymentGateway` output port interface
- [ ] Task 009 - [Port-Out]: Define `OrderEventPublisher` output port interface
- [ ] Task 010 - [Port-In]: Define `CreateOrderUseCase` input port interface
- [ ] Task 011 - [Port-In]: Define `CancelOrderUseCase` input port interface
- [ ] Task 012 - [UseCase]: Implement `CreateOrderService` (implements CreateOrderUseCase)
- [ ] Task 013 - [UseCase]: Implement `CancelOrderService` (implements CancelOrderUseCase)

##### 🟢 Phase 3 — Adapters (All tasks parallel-safe | Depends on Phase 2)
- [ ] Task 014 - [Adapter-Persistence]: Implement `JpaOrderRepository`
- [ ] Task 015 - [Adapter-Web]: Implement `OrderController` (REST)
- [ ] Task 016 - [Adapter-External]: Implement `StripePaymentAdapter`
- [ ] Task 017 - [Adapter-Messaging-Out]: Implement `KafkaOrderEventPublisher`
- [ ] Task 018 - [Adapter-Infra]: Create Flyway migration for `orders` table
```

### Task Detail Template

Each task detail MUST include the **Phase**, **Depends On**, and **Parallel With** fields:

```markdown
##### Task 005 - [Domain-Model]: Create Order entity
- **Phase:** 1
- **Depends On:** Task 001 (OrderStatus enum), Task 004 (OrderItem value object)
- **Parallel With:** — (must wait for dependencies)
- **Objective:** Create the Order aggregate root containing a list of OrderItems and an OrderStatus.
- **Files/Path:** `src/main/java/com/app/domain/model/Order.java`
- **Technical Acceptance Criteria:**
  - Pure POJO — zero framework annotations.
  - Contains `List<OrderItem>` and `OrderStatus` fields.
  - Encapsulates business rules (e.g., `addItem()`, `calculateTotal()`).
  - Unit test validates order creation and item management.
```

```markdown
##### Task 014 - [Adapter-Persistence]: Implement JpaOrderRepository
- **Phase:** 3
- **Depends On:** Task 005 (Order entity), Task 007 (OrderRepository port)
- **Parallel With:** Task 015, Task 016, Task 017, Task 018
- **Objective:** Implement the JPA adapter for the OrderRepository port.
- **Files/Path:** `src/main/java/com/app/adapter/out/persistence/`
- **Implements Port:** `OrderRepository` (from `com.app.application.port.out`)
- **Technical Acceptance Criteria:**
  - Implements all methods defined in the `OrderRepository` port.
  - Uses JPA Entity mapping (separate from domain entity).
  - Includes mapper: `JpaOrderEntity ↔ Order (domain)`.
  - Integration test validates CRUD operations against H2/Testcontainers.
```

---

## Dependency Inversion: The Foundation

The Dependency Inversion Principle (DIP) is what makes the 3-phase model possible:

> **High-level modules must not depend on low-level modules. Both must depend on abstractions (interfaces/ports).**

```text
Domain (Phase 1)  ←  depends on NOTHING
     ↑
Application/Ports (Phase 2)  ←  depends only on Domain
     ↑
Adapters (Phase 3)  ←  depends only on Ports (never on other Adapters)
```

This unidirectional dependency flow guarantees that phases can be executed sequentially while tasks within each phase execute in parallel.

---

## Package Structure Reference

### Java (Spring Boot)

```text
com.app
├── domain                         ← Phase 1
│   ├── model                      # Entities, Value Objects, Enums
│   ├── service                    # Domain Services (pure business logic)
│   └── exception                  # Domain-specific exceptions
├── application                    ← Phase 2
│   ├── port
│   │   ├── in                     # Input Ports (Use Case interfaces)
│   │   └── out                    # Output Ports (Repository/Gateway interfaces)
│   ├── service                    # Use Case implementations (Application Services)
│   └── dto                        # Commands, Queries, DTOs
└── adapter                        ← Phase 3
    ├── in
    │   ├── web                    # REST Controllers, Request/Response objects
    │   └── messaging              # Message Consumers (Kafka, RabbitMQ)
    └── out
        ├── persistence            # JPA Repositories, JPA Entities, Mappers
        ├── messaging              # Message Producers
        └── external               # External API Clients (HTTP, gRPC)
```

### TypeScript (Next.js / Node.js)

```text
src/
├── domain                         ← Phase 1
│   ├── model                      # Entities, Value Objects, Enums
│   ├── service                    # Domain Services (pure business logic)
│   └── error                      # Domain-specific error classes
├── application                    ← Phase 2
│   ├── port
│   │   ├── in                     # Input Ports (Use Case interfaces)
│   │   └── out                    # Output Ports (Repository/Gateway interfaces)
│   ├── service                    # Use Case implementations
│   └── dto                        # Commands, Queries, DTOs
└── adapter                        ← Phase 3
    ├── in
    │   ├── web                    # Route handlers, API controllers
    │   └── messaging              # Message consumers
    └── out
        ├── persistence            # Prisma/TypeORM repositories, DB entities
        ├── messaging              # Message producers
        └── external               # External API clients (fetch, axios)
```

---

## Anti-Patterns to Reject

The Architect Agent MUST reject these patterns during planning:

| Anti-Pattern | Why It Breaks Parallelism |
| --- | --- |
| Domain entity with `@Entity` / `@Column` | Couples Phase 1 to Phase 3 — they become entangled and cannot be parallelized |
| Use case directly instantiating a repository | Bypasses Port — adapter cannot be developed independently in Phase 3 |
| Controller calling repository directly | Skips Phase 2 — creates a shortcut that prevents independent testing and parallel execution |
| Shared DTOs between adapters | Creates hidden coupling between Phase 3 adapters, breaking their independence |
| Single "God Service" orchestrating everything | Cannot be split into parallel tasks — becomes a sequential bottleneck |
| Circular dependencies between packages | Destroys the unidirectional `Domain → Ports → Adapters` flow |

---

## Metrics & Validation

After generating a Technical Checklist, the Architect Agent SHOULD evaluate:

- **Parallelism Ratio:** `(tasks executable in parallel) / (total tasks)`. Target: **≥ 70%**.
- **Phase Distribution:** Phase 3 (Adapters) should contain the most tasks — this is where maximum parallelism occurs.
- **Cross-Phase Dependencies:** Each task should depend ONLY on tasks from previous phases, **never from the same phase**.

---

## Summary

> *Hexagonal Architecture in the context of ADD is not about clean code — it's about industrial parallelism. The hexagon is the assembly line, the ports are the signed contracts, and the adapters are the interchangeable workers that can all build at the same time.*

**The formula: 1 Domain → 2 Ports → 3 Adapters = Maximum Parallel Agents.**
