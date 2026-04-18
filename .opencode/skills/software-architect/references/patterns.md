# Architecture Patterns Catalog

## Creational / Structural

### Repository Pattern
**Intent:** Abstract data access behind an interface, decoupling domain logic from persistence.  
**Use when:** You need to swap databases, unit test without a real DB, or support multiple persistence backends.  
**Key rule:** The repository interface lives in the domain layer; implementations live in the infrastructure layer.

---

### Gateway / Anti-Corruption Layer (ACL)
**Intent:** Translate between your domain model and an external system's model.  
**Use when:** Integrating with legacy systems or third-party APIs with incompatible models.

---

### Facade
**Intent:** Provide a simplified interface to a complex subsystem.  
**Use when:** Exposing a coarse-grained API over fine-grained internal services (e.g., BFF — Backend for Frontend).

---

### Strangler Fig
**Intent:** Incrementally migrate a legacy system by routing requests to new services piece by piece.  
**Steps:**
1. Place a proxy in front of the legacy system
2. Implement new functionality in a new service
3. Route specific requests to the new service
4. Repeat until legacy is fully replaced and can be decommissioned

---

## Distributed System Patterns

### Circuit Breaker
**Intent:** Stop cascading failures by failing fast when a dependency is unhealthy.  
**States:** Closed → Open → Half-Open  
**Parameters to configure:** failure threshold, timeout window, recovery probe interval

---

### Retry with Exponential Backoff + Jitter
**Intent:** Automatically retry transient failures without overwhelming the target.  
```
delay = min(cap, base * 2^attempt) + random_jitter
```
**Use when:** Calling remote APIs, queues, or databases that may have transient errors.  
**Avoid:** Retrying non-idempotent operations without idempotency keys.

---

### Bulkhead
**Intent:** Isolate components so that failure in one does not exhaust resources for others.  
**Implementations:** Thread pool isolation, connection pool per downstream, container resource limits.

---

### Sidecar
**Intent:** Deploy a helper process alongside a main service container to handle cross-cutting concerns.  
**Examples:** Envoy proxy (service mesh), log forwarder, secrets injector.

---

### API Gateway
**Intent:** Single entry point for all clients; handles routing, authn/authz, rate limiting, SSL termination.  
**Variants:**
- **Edge Gateway** — internet-facing, handles external clients
- **BFF (Backend for Frontend)** — tailored aggregation per client type (mobile, web, third-party)

---

## Data Patterns

### CQRS (Command Query Responsibility Segregation)
**Intent:** Separate write model (commands) from read model (queries) to optimize each independently.  
**When to use:** Complex query requirements, high read/write ratio imbalance, need for independent scaling.  
**Trade-off:** Eventual consistency between write store and read projections.

---

### Event Sourcing
**Intent:** Store state as an append-only log of events; derive current state by replaying events.  
**Benefits:** Full audit trail, temporal queries, event replay for debugging or projections.  
**Challenges:** Event schema evolution, snapshot strategies for long-lived aggregates.

---

### Outbox Pattern
**Intent:** Guarantee at-least-once event publishing without distributed transactions.  
**Steps:**
1. Write business entity + outbox event in the **same local DB transaction**
2. A separate poller/CDC process reads the outbox table and publishes events to the broker
3. On success, mark events as published

---

### Saga Pattern
**Intent:** Manage long-running distributed transactions through a sequence of local transactions with compensating actions on failure.

**Choreography-based Saga**
- Services react to events; no central coordinator
- Pros: loose coupling | Cons: harder to track overall state

**Orchestration-based Saga**
- A central orchestrator tells each service what to do next
- Pros: clear flow, easier debugging | Cons: single point of coordination

---

### Database per Service
**Intent:** Each microservice owns its data; no shared databases.  
**Why:** Allows independent schema evolution, technology choice per service, and clear ownership.  
**Data sync:** Use events or API calls; never direct cross-service DB queries.

---

## Reliability Patterns

### Health Endpoint
**Intent:** Expose `/health` (liveness) and `/ready` (readiness) endpoints for orchestration platforms.  
- **Liveness:** "Is the process running?" — restart if fails
- **Readiness:** "Is the service ready to receive traffic?" — remove from load balancer if fails

---

### Idempotency Key
**Intent:** Allow safe retries of non-idempotent operations.  
**Implementation:** Client sends a unique `Idempotency-Key` header; server stores result keyed by it and returns cached result on duplicate.

---

### Graceful Degradation
**Intent:** Return partial results or cached data when a dependency fails, rather than propagating errors.  
**Example:** Return cached catalog data if the inventory service is down.

---

### Distributed Tracing
**Intent:** Track a request as it flows through multiple services using a shared trace-id.  
**Standard:** OpenTelemetry (W3C Trace Context)  
**Key concepts:** Trace, Span, Span context propagation via HTTP headers (`traceparent`)

---

## Messaging Patterns

### Publish-Subscribe (Pub/Sub)
**Intent:** Decouple producers from consumers; producers publish to a topic, multiple subscribers receive independently.

### Dead Letter Queue (DLQ)
**Intent:** Route unprocessable messages to a separate queue for inspection and reprocessing.  
**Always configure** a DLQ for production message queues.

### Competing Consumers
**Intent:** Multiple instances of the same consumer pull from a shared queue to scale throughput horizontally.

### Message Deduplication
**Intent:** Ensure idempotent message processing when at-least-once delivery is used.  
**Approaches:** Idempotency key stored in DB, set-based deduplication, conditional writes.
