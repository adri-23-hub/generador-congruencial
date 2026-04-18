# Software Architect — Technical Reference

## Glossary

| Term | Definition |
|------|-----------|
| **ADR** | Architecture Decision Record — a document that captures an important architectural decision |
| **Bounded Context** | DDD concept: a logical boundary within which a domain model is consistent |
| **CQRS** | Command Query Responsibility Segregation — separates read and write models |
| **Event Sourcing** | Storing state as a sequence of events rather than current snapshots |
| **SLA** | Service Level Agreement — externally committed availability/performance target |
| **SLO** | Service Level Objective — internal target (e.g., 99.9% uptime) |
| **SLI** | Service Level Indicator — measurement used to evaluate SLO |
| **RTO** | Recovery Time Objective — max acceptable downtime after a failure |
| **RPO** | Recovery Point Objective — max acceptable data loss measured in time |
| **NFR** | Non-Functional Requirement — quality attributes (performance, security, reliability) |
| **CAP Theorem** | A distributed system can guarantee at most 2 of: Consistency, Availability, Partition Tolerance |
| **Saga** | Pattern for managing distributed transactions via a sequence of local transactions |
| **Strangler Fig** | Migration pattern: incrementally replace a legacy system by routing traffic to new services |
| **Hexagonal Architecture** | Ports & Adapters — isolates core logic from external concerns |
| **DDD** | Domain-Driven Design — aligns software model with business domain |

---

## Availability math reference

| Availability | Downtime/year | Downtime/month |
|-------------|--------------|----------------|
| 99% ("two nines") | ~87.6 h | ~7.3 h |
| 99.9% ("three nines") | ~8.76 h | ~43.8 min |
| 99.95% | ~4.38 h | ~21.9 min |
| 99.99% ("four nines") | ~52.6 min | ~4.4 min |
| 99.999% ("five nines") | ~5.26 min | ~26.3 s |

---

## Cloud provider service mapping

| Category | AWS | GCP | Azure |
|----------|-----|-----|-------|
| Container orchestration | EKS | GKE | AKS |
| Serverless functions | Lambda | Cloud Functions | Azure Functions |
| Managed queues | SQS / SNS | Pub/Sub | Service Bus |
| Managed databases (relational) | RDS / Aurora | Cloud SQL | Azure SQL |
| Object storage | S3 | Cloud Storage | Blob Storage |
| API Gateway | API Gateway | Apigee / Cloud Endpoints | API Management |
| Secrets management | Secrets Manager | Secret Manager | Key Vault |
| Distributed cache | ElastiCache | Memorystore | Azure Cache for Redis |
| CDN | CloudFront | Cloud CDN | Azure CDN |
| Service mesh | App Mesh | Traffic Director | (Istio on AKS) |

---

## Key RFC and standards references

- **REST** — Roy Fielding's dissertation (2000): [ics.uci.edu/~fielding/pubs/dissertation](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm)
- **OpenAPI 3.x** — [spec.openapis.org](https://spec.openapis.org/oas/latest.html)
- **AsyncAPI 2.x** — [asyncapi.com/docs/reference/specification](https://www.asyncapi.com/docs/reference/specification/v2.6.0)
- **gRPC / Protocol Buffers** — [protobuf.dev](https://protobuf.dev/)
- **CloudEvents** — [cloudevents.io](https://cloudevents.io/)
- **12-Factor App** — [12factor.net](https://12factor.net/)
- **C4 Model** — [c4model.com](https://c4model.com/)

---

## Common architectural anti-patterns to flag

| Anti-pattern | Symptom | Remedy |
|---|---|---|
| **Big Ball of Mud** | No clear structure, everything depends on everything | Introduce bounded contexts & modular decomposition |
| **Distributed Monolith** | Microservices with shared databases or tight coupling | Define service contracts; separate data stores |
| **Chatty Services** | Excessive inter-service calls per user request | Aggregate via BFF or redesign service boundaries |
| **Shared Database** | Multiple services reading the same DB tables | Database per service; use events for sync |
| **God Service** | One service doing everything | Apply Single Responsibility; decompose |
| **Leaky Abstractions** | Internal implementation details exposed in APIs | Design APIs around capabilities, not internals |
| **Missing Idempotency** | Non-idempotent mutation endpoints cause data duplication on retry | Add idempotency keys to all write operations |

---

## Decision heuristics — quick reference

### Team size → architecture style

```
1–3 devs   → Monolith or Modular Monolith
4–8 devs   → Modular Monolith or 2–3 well-defined services
9+ devs    → Microservices (with mature DevOps)
```

### Consistency requirements

```
Strong consistency required?   → Avoid event sourcing alone; use 2PC or Saga with compensation
Eventual consistency OK?       → Event-driven / Outbox pattern
Read-heavy workload?           → CQRS with dedicated read model
Write-heavy workload?          → Sharding, write-optimized storage
```

### When to use a message broker

Use a broker (Kafka, RabbitMQ, SQS) when:
- Producers and consumers must be decoupled in time
- You need at-least-once delivery guarantees
- You need replay capability (event log)
- Fan-out to multiple consumers is required

---

## Security checklist for architects

- [ ] Authentication: OAuth 2.0 + OIDC for user-facing APIs
- [ ] Authorization: enforce at the API gateway AND at the service level (defense-in-depth)
- [ ] Secrets: never in code; use a secrets manager
- [ ] Network: mTLS between internal services; private subnets for databases
- [ ] Input validation: at every boundary (API, queue consumer, file upload)
- [ ] Audit logging: log who did what and when for sensitive operations
- [ ] Dependency scanning: automated SCA (Software Composition Analysis) in CI
- [ ] Data classification: know where PII/sensitive data lives and apply encryption at rest + in transit

---

## Observability — three pillars

| Pillar | What to capture | Recommended tools |
|---|---|---|
| **Logs** | Structured JSON logs with trace-id, user-id, severity | ELK Stack, Loki, CloudWatch |
| **Metrics** | RED (Rate, Errors, Duration) + USE (Utilization, Saturation, Errors) | Prometheus + Grafana, Datadog |
| **Traces** | Distributed traces across service calls | Jaeger, Zipkin, AWS X-Ray, OpenTelemetry |
