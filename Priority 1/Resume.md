# TCS

```
Justification:
Legacy systems often have scalability and real-time processing issues.

Kafka enables asynchronous, fault-tolerant event processing, improving reliability and decoupling components.

Possible Questions & Answers:
Q: Why did you choose Kafka over other messaging systems (RabbitMQ, SQS)?
A: Kafka was ideal due to its high throughput, fault tolerance, and ability to handle real-time event streams. Unlike RabbitMQ (better for task queues), Kafka’s distributed log architecture ensures no data loss and supports replayability, which was critical for insurance claims tracking.

Q: What challenges did you face while migrating from legacy to event-driven?
A: Challenges included ensuring zero downtime during migration, handling legacy data formats, and training teams on event-driven concepts. We mitigated risks with a phased rollout, CDC (Change Data Capture), and extensive testing.

2. Built a high-throughput Spring Boot service handling 1.4M+ notifications with 99.98% availability, reducing P99 latency by 38% (420ms → 260ms) via Kubernetes autoscaling and Redis optimization, while cutting cloud costs by 22%.
Justification:
Kubernetes autoscaling ensured resources matched demand, avoiding over-provisioning.

Redis caching reduced database load for frequent queries.

Cost savings came from right-sizing pods and optimizing cache TTLs.

Possible Questions & Answers:
Q: How did you measure and achieve 99.98% availability?
*A: We used Prometheus/Grafana for SLO tracking, implemented circuit breakers (Resilience4j), and designed multi-AZ deployments. Failover testing and chaos engineering (e.g., killing pods) validated resilience.*

Q: How did Redis optimization contribute to latency reduction?
*A: We cached high-read/low-write data (e.g., policyholder details) with smart TTLs and Lua scripts for atomic updates. This cut DB roundtrips, directly improving P99 latency.*

Q: How did you reduce cloud costs?
A: By analyzing metrics, we rightsized Kubernetes requests/limits, switched to spot instances for non-critical workloads, and optimized Redis memory usage (ziplists for small hashes).

3. Enhanced database scalability by writing PL/SQL queries with bind variables and materialized views, supporting concurrent users while maintaining 200ms response times.
Justification:
Bind variables prevented SQL injection and improved query reuse.

Materialized views pre-computed complex joins, reducing runtime overhead.

Possible Questions & Answers:
Q: Why use materialized views instead of indexing?
A: For reports with complex aggregations (e.g., monthly claims summaries), materialized views eliminated repetitive full-table scans. Indexes alone couldn’t optimize multi-table joins efficiently.

Q: How did you handle database contention under high concurrency?
*A: We used:

Optimistic locking for write conflicts.

Partitioning to distribute I/O.

Connection pooling (HikariCP) to avoid thread starvation.*

General Experience Questions:
Q: What was your role in the team?
*A: I owned the end-to-end redesign of the claims notification system—from architecture (Kafka topic design) to implementation (Spring Boot services) and ops (K8s monitoring).*

Q: What would you improve if you had more time?
A: I’d explore serverless (e.g., AWS Lambda) for low-volume workflows to further reduce costs and implement deeper distributed tracing (e.g., OpenTelemetry).

Key Takeaways for Interview:
Focus on metrics (latency, cost, availability) to show impact.

Explain trade-offs (e.g., Kafka vs. RabbitMQ, materialized views vs. indexing).

Highlight collaboration (e.g., working with DBAs for query tuning).

Would you like to refine any specific part further?

if they ask about architecture what can i say
If the interviewer asks about the architecture of the system you worked on, structure your answer to cover:

High-level design (components & flow)

Key technologies & why they were chosen

Scalability, fault tolerance, and performance considerations

Trade-offs and lessons learned

Sample Answer (Structured Approach)
Interviewer: "Can you walk us through the architecture of the claims notification system you redesigned?"

You:
"Certainly! The system was redesigned as an event-driven microservices architecture to replace a monolithic legacy system. Here’s the breakdown:

1. High-Level Flow
Event Producers:

Legacy systems (policy updates, claims submissions) published events to Apache Kafka via CDC (Change Data Capture) or REST APIs.

Example: A new claim submission triggered a claim.created event.

Kafka Topics:

Topics were partitioned by claim_id for parallel processing.

Used idempotent producers and exactly-once semantics to avoid duplicates.

Spring Boot Services:

Notification Service: Subscribed to Kafka, enriched data (e.g., fetching user details from DB), and sent emails/SMS.

Audit Service: Logged all events for compliance (stored in PostgreSQL).

Database Layer:

Redis: Cached frequently accessed policyholder data (reducing DB load by ~40%).

Oracle: Used materialized views for aggregated reports (e.g., daily claim stats).

Infrastructure:

Kubernetes: Auto-scaled pods based on Kafka lag metrics.

Prometheus/Grafana: Monitored P99 latency and system health.

2. Key Technology Choices
Why Kafka? Needed high throughput (1.4M+ events/day) and replayability for audits.

Why Redis? Low-latency (~1ms) reads for user data, reducing DB calls.

Why K8s Autoscaling? Spikes in claims (e.g., holidays) required dynamic resource allocation.

3. Scalability & Fault Tolerance
Kafka: Replicated topics across 3 brokers to prevent data loss.

Retry/Circuit Breakers: Used Resilience4j to handle third-party API failures.

Database: Read replicas for analytics; connection pooling to avoid bottlenecks.

4. Trade-offs & Lessons
Trade-off: Event-driven added complexity (e.g., eventual consistency) but improved scalability.

Lesson: Over-partitioning Kafka topics initially caused uneven consumer loads. We fixed it by tuning partition keys.

Future improvements could include dead-letter queues for failed events and serverless (AWS Lambda) for low-volume workflows."

Follow-up Architecture Questions & Answers
Q: How did you ensure data consistency between services?
A: We used:

Saga pattern for cross-service transactions (e.g., claim approval → notification → audit).

Eventual consistency for non-critical paths (e.g., analytics updates).

Q: How would you scale this to 10x the traffic?
A: I’d:

Add Kafka consumers with higher parallelism (more partitions).

Shard the database (e.g., by region).

Use edge caching (CDN) for static data.

Q: How did you secure the system?
A: TLS for in-transit data, Vault for secrets, and Kafka ACLs to restrict topic access.

Key Tips
Visualize: Draw a quick diagram if allowed (even on paper).

Metrics: Reinforce with numbers (*"Kafka handled 1.4M events/day with <100ms latency"*).

Be honest about gaps: "We initially underestimated the monitoring needs but added Prometheus later."

```



# ZopSmart

```
1. Designed and optimized Golang microservices to handle 50K+ RPS with <0.1% error rate, achieving >99.5% uptime through scalable concurrency patterns (goroutines, worker pools) and efficient connection pooling.
Justification:
Golang’s lightweight goroutines and worker pools enabled efficient parallel processing.

Connection pooling reduced overhead from repeated TCP handshakes.

Possible Questions & Answers:
Q: Why did you choose Golang over other languages (Java/Python) for high throughput?
A: Golang’s native concurrency model (goroutines/channels) and low GC overhead made it ideal for high RPS. Unlike Python (GIL limitations) or Java (higher memory footprint), Go provided predictable latency under load.

Q: How did you ensure <0.1% error rate under 50K RPS?
A: We:

Used rate limiting (e.g., token buckets) to prevent overload.

Implemented retries with exponential backoff for transient failures.

Benchmarked with load testing (Locust/Gatling) to identify bottlenecks.

Q: How did worker pools improve performance?
A: Instead of spawning unlimited goroutines (risking resource exhaustion), worker pools recycled a fixed set of goroutines. This reduced memory spikes and improved throughput by 30% in our tests.

2. Built a low-latency analytics pipeline using gRPC, Redis Streams, and Apache Kafka, reducing end-to-end processing time by 40% (from 500ms to 300ms) serving 1M+ users.
Justification:
gRPC (HTTP/2 + Protobuf) minimized serialization overhead.

Redis Streams enabled real-time aggregation before batch DB writes.

Possible Questions & Answers:
Q: Why use both Kafka and Redis Streams? Didn’t that add complexity?
*A: Kafka acted as the durable event log for replayability, while Redis Streams handled real-time windowed aggregations (e.g., “top trending products in last 5 mins”). This hybrid approach balanced durability and speed.*

Q: How did you optimize gRPC performance?
A: We:

Used Protobuf for compact serialization (50% smaller than JSON).

Enabled gRPC connection reuse (avoided per-call handshakes).

Tuned max concurrent streams and keepalive pings.

Q: What metrics did you track for latency reduction?
A: Focused on:

P99 latency (via Prometheus).

Redis Streams consumer lag.

gRPC error rates (retries/cancellations).

3. Cut deployment times by 65% (from 15 mins to <5 mins) by migrating to Kubernetes with Helm, implementing CI/CD pipelines with Jenkins, and automating rollback strategies.
Justification:
Helm standardized templating (avoided manual YAML edits).

Automated rollbacks reduced mean time to recovery (MTTR).

Possible Questions & Answers:
Q: What challenges did you face migrating to Kubernetes?
A: Initially, misconfigured resource limits caused pod evictions. We fixed it by:

Using Vertical Pod Autoscaler (VPA) for memory/CPU recommendations.

Adding liveness/readiness probes to avoid traffic to unhealthy pods.

Q: How did your rollback strategy work?
A: We used:

Helm hooks to run pre/post-deployment checks.

Automated rollback on CI/CD failure (e.g., Jenkins pipeline would revert to last stable Helm release if smoke tests failed).

Q: Why Jenkins over GitLab CI or GitHub Actions?
A: The team already had Jenkins expertise, and its plugin ecosystem (e.g., Kubernetes Blue Ocean) simplified K8s integrations. We later added Argo CD for GitOps.

General Internship Questions:
Q: What was your biggest technical contribution?
*A: Designing the analytics pipeline—it required balancing real-time needs (Redis Streams) with durability (Kafka), while hitting strict latency SLAs. My gRPC optimizations alone saved ~200ms per request.*

Q: What would you do differently?
A: I’d introduce feature flags earlier to decouple deployments from releases, allowing safer canary rollouts.

Key Takeaways for Interview:
Emphasize scale: “50K RPS”, *“1M+ users”* show impact.

Explain trade-offs: E.g., “Kafka for durability, Redis for speed”.

Show ownership: “I migrated…” vs. “We migrated…”.

```
