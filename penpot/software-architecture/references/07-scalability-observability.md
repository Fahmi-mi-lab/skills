# Scalability, Failure Mode & Observability

This stage is often skipped even though it's what gets asked about most in architecture reviews ("what happens if X goes down?", "what if traffic grows 10x?"). It doesn't always need a new diagram — it can be annotations on top of the existing deployment diagram.

## Scalability strategy
- **Horizontal vs vertical scaling** — state which components scale which way, and why.
- **Caching** — at which layer (CDN, application-level, database query cache), and what gets cached.
- **Sharding/partitioning** — if data is or will be very large, how it's partitioned (by region, by tenant, by hash).

## Failure mode analysis
- **Single Point of Failure (SPOF)** — identify any component whose failure would take down the whole system. Mark it on the deployment diagram (e.g. a red outline/annotation) to distinguish SPOFs from redundant components.
- **Redundancy** — which components have a backup/replica.
- **Circuit breaker & retry** — for inter-service communication, state the failure-handling strategy (retry with backoff, circuit breaker to prevent cascading failure).
- **Graceful degradation** — what happens to the user experience if one part of the system fails (does the system stay partially usable, or go fully down).

## Observability — three pillars
- **Logging** — what gets logged, where it's stored/aggregated (e.g. centralized logging).
- **Metrics** — key metrics being tracked (latency, error rate, throughput, resource usage), and the tool used.
- **Tracing** — distributed tracing to follow a single request across multiple services (important for microservices architectures).
- **Alerting** — what thresholds trigger an alert, and who receives it.

## Representation in Penpot
Two possible forms:
1. Additional annotations on top of the `06-Deployment-Infrastructure` frame (highlight SPOFs, add monitoring icons at key points), or
2. A separate frame `07-Resilience-Observability` with a checklist/summary table if annotating the deployment diagram directly would make it too cluttered.

Choose based on how complex the system is — small systems are fine with annotations; larger systems are clearer with a separate frame.

## Polish checklist
- [ ] At least one SPOF is explicitly identified (or explicitly stated that there is none, with reasoning)
- [ ] Scaling strategy references a specific component in the deployment diagram, not a generic statement
- [ ] All three observability pillars (logging, metrics, tracing) are addressed, not just one
