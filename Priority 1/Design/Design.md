## LLD 

**Steps**

```
1. Requirements Clarification :

Think about possible entities
Write down the responsibilities
Ask if any additional actions to be included
Tell if you can add additional possible actions (keep it minimalistic)

2. Define Key Components :
List out all the important entities based on requirements

3. Class Diagram Design :
Draw a class diagram with entities
Add attributes for it
Write relationships, Enumerations, Multiplicity

4. Design Patterns Consideration :
Creational Patterns : Singleton, Factory Method, Abstract Factory, Builder, Prototype
Structural Patterns : Adapter, Decorator, Facade, Composite, Proxy
Behavioral Patterns : Observer, Strategy, Command, Iterator, State

5. Interface Definitions :
Based on design patterns make interfaces
Use SOLID principles

6. Core Logic Implementation :
add methods for endpoints (CRUD and additional)
Write Pseudocode for helper functions 
Add Exceptions

7. Database Considerations :
Normaliation, Indexing


8. Concurrency Handling :


9. Scalability Discussion :


10. Testing Approach :



```


**Generic things**

```

Payment : Strategy Design Pattern
Payment processing failure scenarios.
Use Enum
Abstract Factory: Vehicle and ParkingSpot hierarchies.
Singleton: ParkingLot (single instance in most implementations)
Lost ticket handling (TicketStatus.LOST).

Blackbox

Pull/ Push Notifications

Soft Delete




```

**Tips**

```

**Requirements is God listen carefully**

Nuv em cheppav ela cheppav ivem kadhu, perfect communication and how deep techinically you are good anthe 

Interface is God

1. Time Management : Keep less time for requirement gathering and keep requirements as minimalistic as possible
After the requirements were given ask some generic questions (very less but impactful questions)

2. Think like you are user 

3. Note down requirements

4. Use simple design patterns which can build quickly (Factory, Singleton, Observer, Startegy)

5. Discuss tradeoffs

6. Use DSA in UML

7. Always practice on white board

```


```
scalability, reliability, availability, latency
CAP Theorem
ACID vs BASE

Design Patterns in HLD:
1. Scalability & Load Handling
Load Balancing (Round Robin, Weighted Round Robin, IP Hash, Least Connections, Least Connections, Weighted Least Connections, Least Response Time, Consistent Hashing, Geographic Load Balancing, )
Sharding (Horizontal Partitioning)
Types of Sharding
Range-Based Sharding : Splits data by value ranges (e.g., IDs 1-1000 → Shard A).
Hash-Based Sharding : Uses a hash function (e.g., hash(key) % N) to distribute data.
Directory-Based Sharding : Uses a lookup table to map keys to shards.
Geo/Region-Based Sharding : Splits data by physical location (e.g., US → Shard 1, EU → Shard 2).
Key-Based (Dynamic) Sharding : Custom logic assigns shards (e.g., user_id % 10).
Vertical Sharding (Column-wise) : Splits tables by columns (e.g., users_profile vs. users_orders).

Caching (Redis, CDN, LRU Eviction)
Types of Caches
1. In-Memory Cache	RAM (Fastest)	Frequent reads	Redis, Memcached
2. CDN Cache	Edge servers (Global)	Static files (images, JS)	Cloudflare, Akamai
3. Database Cache	DB’s built-in cache	Query results	PostgreSQL cache
4. Browser Cache	User’s device	Websites (CSS/JS)	Chrome cache
5. Application Cache	App layer (Custom)	Session data	Django cache

Cache Strategies :

Write-Through
Data is written to cache and DB simultaneously.
Use case: Banking apps (consistency critical).

Write-Behind (Write-Back)
Data goes to cache first → DB later (async).
Use case: High-write systems (e.g., logs).

Cache-Aside (Lazy Loading)
App checks cache first; if missing, fetches from DB.
Use case: Most read-heavy apps (e.g., social media).

Time-to-Live (TTL)
Cache auto-deletes data after X seconds.

When to Use Caching?
✅ Read-heavy apps (e.g., blogs, social media).
✅ Slow backend (DB/API calls > 100ms).
✅ Repetitive data (e.g., user profiles, product listings).

When to Avoid?
❌ Frequently changing data (e.g., real-time sensors).
❌ Critical consistency needed (e.g., payment systems).

Cache Eviction Policies List :

LRU (Least Recently Used) – Removes the least recently accessed item.
LFU (Least Frequently Used) – Removes the least frequently accessed item.
FIFO (First In, First Out) – Removes the oldest item (based on insertion time).
LIFO (Last In, First Out) – Removes the newest item.
Random Replacement (RR) – Randomly selects an item to evict.
TTL (Time-To-Live) – Automatically expires data after a set time.
MRU (Most Recently Used) – Removes the most recently accessed item (rare).

Bonus:
ARC (Adaptive Replacement Cache) – Balances between LRU and LFU.
2Q (Two Queues) – Uses a mix of FIFO and LRU.



Read Replicas (Scale Read Operations)
Definition: Exact, read-only copies of the primary (master) database.

How Read Replicas Work
Primary DB handles all writes (INSERT/UPDATE/DELETE).
Changes are replicated (asynchronously/synchronously) to replicas.
Read queries (SELECT) are directed to replicas.
Read Replica Flow
(Visual: Writes → Primary | Reads → Replicas)

When to Use Read Replicas?
✔ Read-heavy apps (e.g., blogs, analytics dashboards).
✔ Reporting queries (slow, complex SELECTs).
✔ Geographically distributed users (place replicas near users).

When to Avoid?
❌ Write-heavy systems (replicas add replication lag).
❌ Strong consistency needed (replicas may serve stale data).

Key Challenges
⚠ Replication Lag: Replicas may serve stale data (eventual consistency).
⚠ Failover Complexity: Promoting a replica to primary requires care.
Pro Tip
Use connection pools (e.g., PgBouncer) to route reads/writes efficiently.

2. Fault Tolerance & Reliability
Circuit Breaker (Fail Fast, e.g., Hystrix)
A Circuit Breaker is a design pattern used in software development, particularly in distributed systems, to improve fault tolerance and prevent cascading failures. It acts as a safety mechanism to stop calls to a failing service, allowing it time to recover before retrying.

How It Works:
The Circuit Breaker pattern is inspired by electrical circuit breakers. It monitors requests to a service and, if failures reach a threshold, it "trips" and temporarily stops further requests. This prevents overloading a failing service and gives it time to recover.

Circuit Breaker States:
Closed (Normal Operation):
Requests are allowed to pass through.
Failures are counted; if they exceed a threshold, the circuit trips to Open.

Open (Failure Detected):
Requests are immediately rejected (no calls to the failing service).
After a timeout period, the circuit moves to Half-Open.

Half-Open (Testing Recovery):
A limited number of test requests are allowed.
If they succeed, the circuit returns to Closed.
If they fail, it goes back to Open.

Benefits:
Prevents cascading failures by stopping repeated calls to a failing service.
Reduces latency by failing fast instead of waiting for timeouts.
Improves system resilience by allowing services to recover.

Use Cases:
Microservices communication (e.g., when Service A calls Service B).
External API calls (e.g., payment gateways, third-party services).


Leader Election (ZooKeeper, Raft)
Leader Election is a coordination mechanism in distributed systems where multiple nodes (servers/processes) select one node as the "leader" to manage tasks, while others act as followers. This ensures:
Consistency (only one leader makes decisions).
Fault tolerance (if the leader fails, a new one is elected).
Avoiding conflicts (preventing split-brain scenarios).
How Leader Election Works
Nodes Communicate:
Nodes exchange messages (e.g., "I’m alive" or "I want to be leader").
Protocols like Paxos, Raft, or ZooKeeper’s ZAB are often used.
Election Criteria:
Highest ID/node priority (e.g., oldest node).
Randomized backoff (e.g., Bully Algorithm).
Consensus-based voting (e.g., Raft).
Leader Responsibilities:
Coordinates tasks (e.g., scheduling, writes in a database).
Sends heartbeats to followers (to prove it’s alive).
Failure Handling:
If the leader crashes, followers detect missing heartbeats and trigger a new election.

Leader Election Algorithms
Algorithm	Approach	Use Case
Bully	Highest-ID node wins	Small clusters
Raft	Voting + log replication	Distributed databases (etcd)
Paxos	Consensus via proposals	Highly available systems
ZooKeeper	Uses ephemeral nodes + watches	Coordination services


Redundancy (Multi-AZ, Replication)
Redundancy is a key strategy in distributed systems to ensure high availability (HA), fault tolerance, and disaster recovery. It involves duplicating critical components (data, servers, services) so that if one fails, another can take over seamlessly.

1. Types of Redundancy
A. Multi-AZ (Availability Zone) Deployment
Definition: Distributes resources across multiple physically separated data centers (Availability Zones) within a cloud region.
Purpose: Protects against data center failures (power outages, network issues, natural disasters).
How it Works:
A primary instance runs in AZ-1, and a standby replica in AZ-2.
If AZ-1 fails, traffic automatically fails over to AZ-2.
Example: AWS RDS Multi-AZ, Azure Zone-Redundant Storage.

B. Replication (Data Redundancy)
Definition: Copies data across multiple nodes to ensure consistency and availability.
Types:
Synchronous Replication (strong consistency, higher latency):
Data is written to primary + replicas before confirming success (e.g., PostgreSQL with sync replication).
Asynchronous Replication (eventual consistency, lower latency):
Primary writes first, replicas update later (e.g., MySQL async replication).
Multi-Region Replication (global redundancy):
Data is copied across geographically distant regions (e.g., Google Cloud Spanner).

2. Why Use Redundancy?
Benefit	Multi-AZ	Replication
Fault Tolerance	✅	✅
Disaster Recovery	✅	✅
Load Balancing	❌	✅ (read replicas)
Zero Downtime	✅ (auto-failover)	✅ (if synced)
3. Real-World Implementations
A. AWS Multi-AZ (High Availability)
Amazon RDS (Relational DB):
Primary DB in us-east-1a, standby in us-east-1b.
Automatic failover in ~60 seconds.
Elastic Load Balancer (ELB):
Distributes traffic across AZs to prevent single-point failures.
B. Database Replication
MongoDB Replica Set:
One primary node + multiple secondaries.
If primary fails, an election picks a new leader.
Kafka Replication:
Topics are replicated across brokers to prevent data loss.
C. Kubernetes & Multi-AZ
Deploying pods across AZs (using topologySpreadConstraints).
Persistent Volumes (PVs) replicated via storage solutions (e.g., Ceph, Portworx).
4. Challenges & Trade-offs
Challenge	Solution
Higher Costs (more resources)	Use auto-scaling & spot instances
Data Consistency Issues	Choose sync/async wisely
Complex Failover Logic	Use managed services (e.g., AWS RDS, MongoDB Atlas)
5. Key Takeaways
✅ Multi-AZ = Protects against data center failures (best for HA).
✅ Replication = Ensures data durability & read scalability.
✅ Synchronous = Strong consistency (but slower).
✅ Asynchronous = Faster but risk of data loss.

Health Checks & Auto-Healing
1. Health Checks: "Is This Thing Working?"
What it is: A way for a system to check if a server, service, or application is running properly.
How it works:
Sends a small test request (like a "ping").
Expects a response (e.g., HTTP 200 OK or "I'm alive!").
If no response (or errors), marks it as unhealthy.
Examples:
Web Server: Checks if /health returns success.
Database: Tests if queries execute without errors.
Kubernetes: Uses liveness probes to restart failing containers.
2. Auto-Healing: "Fix It Automatically!"
What it is: When a system detects a problem (via health checks) and tries to fix it without human help.
How it works:
Detects failure (e.g., server crash, high CPU, timeout).
Tries to recover (restarts, replaces, or shifts traffic).
Alerts humans if it can’t fix it.
Examples:
Cloud (AWS/Azure): Auto-replaces unhealthy VMs.
Kubernetes: Kills & restarts crashing pods.
Load Balancer: Stops sending traffic to a broken server.
Why This Matters?
✅ Less downtime – Systems recover faster.
✅ Less manual work – No need for 3 AM emergency fixes.
✅ More reliable apps – Bad parts are removed automatically.


3. Data Consistency & Messaging
What it is: Making sure all parts of a system agree on the same data, even when updates happen.
Types of Consistency:
Strong Consistency
Eventual Consistency

Messaging: "Passing Notes in Class"
What it is: Systems communicate by sending messages (events) instead of directly calling each other.

Why?
Avoids bottlenecks (no waiting for replies).
Handles failures gracefully (retry if a service is down).
Tools: Kafka, RabbitMQ, AWS SQS.

Event Sourcing (Append-Only Log)
Like a Diary for Your App
What it is: Storing every change (events) as an append-only log, instead of just the latest state.

Example (Bank Account):
Event	Balance
AccountCreated($100)	$100
Deposited($50)	$150
Withdrew($30)	$120
Why Use It?
✅ Full history – Know exactly what happened (audits, debugging).
✅ Time travel – Rebuild past states by replaying events.
✅ Scalability – Easy to distribute events across systems.
Used in: Banking, e-commerce (order histories), blockchain.


CQRS (Separate Read/Write Paths)
What is CQRS?
CQRS (Command Query Responsibility Segregation) is a design pattern that splits an application into two parts:
Commands (Writes) – Handle updates (create, update, delete).
Queries (Reads) – Handle data retrieval.
Instead of using the same model for both, they are separated, allowing optimization for each task.

Why Use CQRS?
✅ Better Performance – Reads can be optimized (e.g., cached, denormalized).
✅ Scalability – Reads & writes can scale independently.
✅ Flexibility – Different databases for reads (fast queries) and writes (strong consistency).
✅ Simpler Code – No complex "one-size-fits-all" model.

How It Works
1. Commands (Write Path)
Actions: CreateOrder, UpdateUser, DeletePost.
Stored in: A structured, transactional database (e.g., PostgreSQL).
May trigger: Events (for eventual consistency).

2. Queries (Read Path)
Actions: GetUserProfile, ListProducts.
Optimized for: Speed (denormalized data, caching, materialized views).
Stored in: Fast read-optimized stores (e.g., Redis, Elasticsearch).

3. Sync Between Read & Write
Eventual Consistency: Changes in the write DB propagate to the read DB (e.g., via Kafka, change data capture).
Example:
You update a username (Command → Write DB).
Later, the read DB updates (via an event).

Saga Pattern (Distributed Transactions)
Problem:
In microservices, a single business process (e.g., "Place Order") spans multiple services (Order, Payment, Inventory). If one step fails, how do we undo previous steps without a traditional database transaction?

Solution: Sagas
A Saga breaks a transaction into smaller steps, each handled by a different service. If any step fails, compensating actions (rollbacks) are triggered to maintain consistency.

How Sagas Work
1. Two Types of Sagas
Choreography-Based (Decentralized)
Services emit events to trigger the next step.
Example: Order → Payment → Inventory (each reacts to events).
Orchestration-Based (Centralized)
A Saga Orchestrator manages the workflow.
Example: Orchestrator tells Order → Payment → Inventory what to do.

2. Compensating Actions (Rollbacks)
If a step fails, the Saga executes "undo" actions:

Step	Action	Compensating Action
Create Order	✅ Success	(None)
Charge Payment	✅ Success	(None)
Update Inventory	❌ Fails	Refund Payment
Real-World Example: E-Commerce Checkout
Order Service → Creates order (PENDING).
Payment Service → Charges credit card.
Inventory Service → Reserves items.

If inventory fails:
Payment Service issues refund.
Order Service cancels order.

Pros & Cons
✅ Works across microservices	❌ Complex error handling
✅ No distributed locks needed	❌ Temporary inconsistency
✅ Scalable & decoupled	❌ Hard to debug
When to Use Sagas?
✔ Long-running transactions (e.g., travel booking).
✔ Microservices with no shared DB.
❌ Avoid for simple ACID transactions (just use a DB).

Key Takeaways
🔹 Sagas split transactions into steps + rollbacks.
🔹 Choreography (events) vs. Orchestration (central control).
🔹 Eventual consistency (not immediate like ACID).


Publisher-Subscriber (Kafka, RabbitMQ)
What is Pub/Sub?
Pub/Sub is a messaging pattern where:

Publishers send messages without knowing who receives them

Subscribers receive only the messages they're interested in

A message broker (like Kafka or RabbitMQ) acts as the middleman

How It Works (Post Office Analogy)
Publishers = People mailing letters (don't know who will get them)

Message Broker = Post office (receives and routes mail)

Subscribers = People with PO boxes (only get mail addressed to their box)

Key Components
Component	Role	Example
Topic	Category/channel for messages	"orders", "payments"
Publisher	Sends messages to topics	Order service
Subscriber	Listens to specific topics	Inventory service
Broker	Manages message storage and delivery	Kafka, RabbitMQ
Message	Data being sent (usually JSON/protobuf)	{order_id: 123, status: "paid"}
RabbitMQ vs Kafka
Feature	RabbitMQ (Traditional)	Kafka (Modern)
Best For	Simple workflows, RPC	High-throughput, event streaming
Message Life	Deleted after consumption	Stored for set period (days/weeks)
Speed	Fast for simple cases	Extremely fast for big data
Complexity	Easier to set up	More complex but powerful
Real-World Example: Food Delivery App
Order Service (Publisher) → Sends "order_placed" event to "orders" topic

Multiple Subscribers react:

Payment Service: Processes payment

Kitchen Service: Starts preparing food

Notification Service: Sends confirmation SMS

Why Use Pub/Sub?
✅ Loose coupling - Services don't need to know about each other
✅ Scalability - Easily add more subscribers
✅ Reliability - Messages persist if service is down
✅ Flexibility - Different services can process at their own pace

Common Use Cases
Event-driven architectures

Microservices communication

Real-time notifications

Data streaming/analytics

Log aggregation

Potential Challenges
⚠️ Message ordering (Kafka preserves order per partition, RabbitMQ doesn't)
⚠️ Exactly-once delivery is hard (usually "at least once")
⚠️ Backpressure handling when subscribers are slow

4. Performance Optimization
1. Materialized Views (Pre-Computed Queries)
What: Pre-calculated query results stored as physical tables
Why: Avoid expensive real-time computations for frequent queries
How it works:

Database periodically refreshes the view (e.g., hourly/daily)

Queries read from this snapshot instead of raw tables

Example:

sql
Copy
-- Create materialized view for daily sales reports
CREATE MATERIALIZED VIEW daily_sales AS 
SELECT date, SUM(amount) 
FROM orders 
GROUP BY date
REFRESH EVERY 1 HOUR;
Best for: Dashboards, analytics, complex aggregations

2. Lazy Loading (On-Demand Fetch)
What: Load data only when needed
Why: Reduce initial load time and memory usage

Common implementations:

Web: Load images when scrolling into view (loading="lazy")

Databases: JOIN queries executed only when accessing related data

Frontend: React.lazy() for code splitting

3. Batching (Bulk Operations)
What: Group multiple operations into a single request
Why: Reduce network/processing overhead

Examples:

Scenario	Single Request	Batched Request
Database writes	100 INSERT statements	1 BULK INSERT
API calls	50 HTTP requests	1 request with array
Email sending	Send individually	Send as digest


4. Rate Limiting (API Throttling)
What: Control request frequency per user/service
Why: Prevent abuse, ensure fair usage, maintain stability

Common algorithms:

Token bucket: Refilling token pool (e.g., 100 requests/hour)

Leaky bucket: Fixed outflow rate

Fixed window: Counts per time window (e.g., 10 requests/minute)

Implementation Example:

python
Copy
from fastapi import FastAPI, Request
from slowapi import Limiter, _rate_limit_exceeded_handler

app = FastAPI()
limiter = Limiter(key_func=get_ip_address)
app.state.limiter = limiter

@app.get("/api")
@limiter.limit("5/minute")
async def sensitive_endpoint(request: Request):
    return {"data": "protected"}
Best for: Public APIs, payment endpoints, auth services

Performance Optimization Cheat Sheet
Technique	When to Use	Potential Gain
Materialized Views	Frequent complex reads	10-100x faster queries
Lazy Loading	Large payloads with partial usage	2-5x faster load
Batching	High-volume small operations	50-90% fewer requests
Rate Limiting	Public-facing APIs	Prevents 100% outages

5. API & Communication
1. API Gateway (Single Entry Point)
What: A unified entry point that routes requests to backend services
Why:

Simplifies client access (one endpoint)

Handles cross-cutting concerns (auth, logging, rate limiting)

Aggregates responses from multiple services

Features:
✅ Request routing & composition
✅ Authentication/authorization
✅ Load balancing
✅ Caching
✅ Protocol translation (HTTP → gRPC)

Example:

Copy
Client → API Gateway → [UserService | OrderService | PaymentService]
Tools: Kong, AWS API Gateway, Apigee, Nginx

2. Backend for Frontend (BFF)
What: Dedicated API layer per client type
Why:

Customizes data for specific frontend needs

Reduces over-fetching

Isolates client-specific logic

Example:

Copy
Mobile App → Mobile BFF (optimized for small payloads)  
Web App → Web BFF (rich data for desktop)  
IoT Device → IoT BFF (binary protocols)
Key Benefit: Frontends get exactly what they need without backend changes

3. Service Mesh (Istio, Linkerd)
What: Infrastructure layer handling service-to-service communication
Why:

Manages traffic (load balancing, retries)

Observability (metrics, tracing)

Security (mTLS, policies)

How it works:

Sidecar proxies (Envoy) intercept all service traffic

Control plane manages configuration

Features:
🔹 Circuit breaking
🔹 A/B testing
🔹 Automatic retries
🔹 Zero-trust security

Tools: Istio, Linkerd, Consul Connect

4. Polling vs. Webhooks
Polling (Pull)	Webhooks (Push)
Mechanism	Client repeatedly checks for updates	Server pushes data when available
Latency	High (delay between polls)	Low (instant)
Efficiency	Wastes resources when idle	Efficient (only active when needed)
Complexity	Simple to implement	Requires endpoint setup
Use Cases	Status checks, simple clients	Real-time updates (payments, chat)
Example:

javascript
Copy
// Polling (Client-side)
setInterval(() => fetch('/updates'), 5000);

// Webhook (Server-side)
app.post('/webhook', (req) => handleUpdate(req.body));
Hybrid Option: Consider Server-Sent Events (SSE) for real-time streaming

6. Storage & Databases
1. Write-Ahead Log (WAL) – Crash Recovery Mechanism
What:
A transaction log where changes are recorded before they’re applied to the database.

Why Use It?

Guaranteed durability: Survives crashes (e.g., power failure).

Atomicity: Ensures transactions are all-or-nothing.

Performance: Enables batch writes to the main DB.

How It Works:

Log First: Write "Plan to update row X → Y" to WAL.

Apply Later: Update the actual database.

Recovery: After a crash, replay WAL to restore consistency.

Used In:

PostgreSQL, SQLite, Kafka (for replication).

Blockchain (transaction logs).

Example:

plaintext
Copy
WAL Entry: [TxID: 123, Action: UPDATE accounts SET balance=200 WHERE id=1]
2. Time-Series Database (Prometheus, InfluxDB)
What:
Optimized for time-stamped data (metrics, IoT sensors, logs).

Key Features:

Time-centric storage: Data indexed by timestamp.

Efficient compression: Downsamples old data automatically.

Specialized queries: rate(), moving_avg().

VS Traditional DBs:

Query	Time-Series DB	Traditional DB
CPU usage last 5 mins	10 ms (native time filters)	500 ms (full scan)
Tools:

Prometheus: Pull-based metrics + alerting.

InfluxDB: High-throughput writes + SQL-like queries.

TimescaleDB: PostgreSQL extension for time-series.

Example Query (PromQL):

promql
Copy
http_requests_total{status="500"}[1h]  // Count 500 errors in last hour
3. Polyglot Persistence – Mixing SQL + NoSQL
What:
Using different databases for different data needs in one system.

Why?

Right tool for the job:

SQL: Transactions, complex queries.

NoSQL: Scalability, flexible schemas.

Common Combos:

Data Type	Database Choice	Reason
User profiles	PostgreSQL (SQL)	ACID compliance
Product catalog	MongoDB (Document)	Flexible schema
Session data	Redis (Key-Value)	Low-latency reads
Analytics	Cassandra (Wide-Column)	High write throughput
Example Architecture (E-Commerce):

mermaid
Copy
graph LR
  A[Frontend] --> B[SQL: Orders/Users]
  A --> C[NoSQL: Product Catalog]
  A --> D[Redis: Shopping Cart]
Trade-Offs:
✅ Optimized performance per use case.
❌ Complexity: Multiple DBs to manage.

When to Use Each?
Technology	Best For	Avoid When
WAL	Systems needing crash recovery	Simple apps with no transactions
Time-Series DB	Metrics, IoT, monitoring	Relational business data
Polyglot Persistence	Complex systems with diverse data needs	Small projects
Pro Tip:

Use WAL for reliability in transactional systems.
Time-series DBs can reduce storage costs for metrics by 10x vs SQL.
Start monolithic (single DB), then go polyglot only if needed.



1. Microservices vs Monolithic Architecture
Aspect	Monolithic	Microservices
Structure	Single codebase	Decoupled services (1 service = 1 function)
Deployment	Deploy entire app	Deploy services independently
Scalability	Scale vertically (bigger server)	Scale horizontally (add more instances)
Complexity	Simpler debugging	Harder to trace (needs observability tools)
Best For	Small apps, startups	Complex systems, large teams
Example	WordPress	Netflix, Uber
Trade-Off:

Microservices add overhead (network calls, service discovery) but enable agility.

Monoliths are simpler but hard to scale beyond a point.

2. Load Balancing Algorithms
Algorithm	How It Works	Use Case
Round Robin	Rotates requests evenly	Simple stateless apps
Least Connections	Sends to least busy server	Long-lived connections (e.g., WebSockets)
Consistent Hashing	Same user → same server (minimizes cache misses)	Distributed caches (Redis)
Tools: NGINX, AWS ALB, HAProxy.

3. Caching Strategies
Strategy	Description	Example
LRU Cache	Evicts least-recently-used items	CPU cache, Redis
CDN	Caches static content globally	Images, JS/CSS (Cloudflare)
Redis	In-memory key-value store (low latency)	Session storage
Memcached	Simple multi-threaded cache	Database query caching
Rule of Thumb:

Cache read-heavy data (e.g., product catalogs).

Invalidate caches on writes.

4. Database Choices
Type	Strengths	Weaknesses	Use Case
SQL	ACID transactions, complex joins	Hard to scale horizontally	Banking, e-commerce
NoSQL	Flexible schema, horizontal scale	No joins, eventual consistency	IoT, real-time analytics
Scaling Techniques:

Sharding: Split data by key (e.g., user ID).

Replication: Slave DBs for read scaling.

5. Message Queues
Tool	Model	Best For	Throughput
Kafka	Pub/Sub + streaming	Event sourcing, logs	1M+ msgs/sec
RabbitMQ	Queue-based	RPC, task queues	50K msgs/sec
Patterns:

Event-driven: Services react to events (e.g., OrderPlaced).

Dead Letter Queue (DLQ): Store failed messages for retry.

6. APIs
Type	Protocol	Performance	Use Case
REST	HTTP/JSON	Moderate	CRUD apps, public APIs
gRPC	HTTP/2 + Protobuf	Very fast	Microservices (internal)
WebSockets	TCP	Real-time	Chat, live updates
gRPC vs REST:

gRPC is 5–10x faster but harder to debug.

7. Scalability Approaches
Type	How	Limits
Vertical	Upgrade CPU/RAM	Single-server ceiling
Horizontal	Add servers + load balancing	Complexity (state management)
Database	Read replicas, partitioning	Eventually consistent reads
Golden Rule:

Scale horizontally first (cloud-friendly).

Use auto-scaling (AWS Auto Scaling, Kubernetes HPA).

8. Performance Optimization
Technique	Impact	Example
CDN	50–90% faster static content	Cloudflare, AWS CloudFront
Database Indexing	100–1000x faster queries	CREATE INDEX idx_name ON users(name)
Denormalization	Faster reads (avoid joins)	Duplicate data in NoSQL
Pro Tip:

Index high-cardinality fields (e.g., user_id).

CDNs reduce TTFB (Time to First Byte).

Key Takeaways
Architecture: Start monolithic → split to microservices only when needed.

Scaling: Prefer horizontal scaling + auto-scaling.

Caching: Cache aggressively but invalidate wisely.

APIs: Use gRPC internally, REST/WebSockets externally.

Performance: Indexes + CDNs = easiest wins.

Famous System Design Problems :
Design Twitter / Facebook Feed
Design Uber / Ola
Design URL Shortener (TinyURL)
Design WhatsApp / Chat System

3. Low-Level Design (LLD) Preparation
Key Concepts
Object-Oriented Design (OOD)

SOLID Principles (Single Responsibility, Open-Closed, Liskov Substitution, Interface Segregation, Dependency Inversion)

Class Diagrams (UML - Inheritance, Composition, Aggregation)

Encapsulation, Abstraction, Polymorphism, Inheritance

Design Patterns (Gang of Four)

Creational (Singleton, Factory, Builder, Prototype)
Structural (Adapter, Decorator, Proxy, Facade)
Behavioral (Observer, Strategy, Command, State)

Database Schema Design

Normalization (1NF, 2NF, 3NF, BCNF) :
Normalization is a crucial concept in database design that helps eliminate redundancy and maintain data integrity. For system design interviews, you'll need to understand the different normal forms and when to apply them. Here's a breakdown of the key normalization forms:

1NF (First Normal Form)
Requirements:

Each table cell should contain a single value (atomic values)

Each record needs to be unique (no duplicate rows)

Values stored in a column should be of the same domain

Example Problem:

Copy
Orders Table:
OrderID | Products
--------|---------
1       | Laptop, Mouse
2       | Monitor
1NF Solution:

Copy
Orders Table:
OrderID | Product
--------|--------
1       | Laptop
1       | Mouse
2       | Monitor
2NF (Second Normal Form)
Requirements:

Must be in 1NF

All non-key attributes must depend on the entire primary key (no partial dependency)

Example Problem (in 1NF but not 2NF):

Copy
OrderDetails:
OrderID | ProductID | ProductName | Quantity
--------|-----------|-------------|---------
1       | 101       | Laptop      | 1
1       | 102       | Mouse       | 2
2       | 101       | Laptop      | 1
2NF Solution:
Split into two tables to remove partial dependency (ProductName only depends on ProductID, not OrderID):

Copy
OrderItems:
OrderID | ProductID | Quantity
--------|-----------|---------
1       | 101       | 1
1       | 102       | 2
2       | 101       | 1

Products:
ProductID | ProductName
----------|------------
101       | Laptop
102       | Mouse
3NF (Third Normal Form)
Requirements:

Must be in 2NF

No transitive dependencies (non-key attributes shouldn't depend on other non-key attributes)

Example Problem (in 2NF but not 3NF):

Copy
Orders:
OrderID | CustomerID | CustomerName | CustomerAddress
--------|------------|--------------|----------------
1       | C001       | John Doe     | 123 Main St
2       | C002       | Jane Smith   | 456 Oak Ave
3NF Solution:
Split into two tables to remove transitive dependency (CustomerName and CustomerAddress depend on CustomerID, not OrderID):

Copy
Orders:
OrderID | CustomerID
--------|------------
1       | C001
2       | C002

Customers:
CustomerID | CustomerName | CustomerAddress
-----------|--------------|----------------
C001       | John Doe     | 123 Main St
C002       | Jane Smith   | 456 Oak Ave
BCNF (Boyce-Codd Normal Form)
Requirements:

Must be in 3NF

For any non-trivial dependency X → Y, X must be a superkey (a set of attributes that can uniquely identify a row)

Example Problem (in 3NF but not BCNF):
Consider a classroom scenario where:

A student can be in multiple classes

A class has multiple students

Each class has one teacher

A teacher can teach multiple classes

For each student, their teacher is determined by their class

Copy
Enrollments:
StudentID | ClassID | TeacherID
----------|---------|----------
S1        | C1      | T1
S1        | C2      | T2
S2        | C1      | T1
Here, the functional dependencies are:

(StudentID, ClassID) → TeacherID

ClassID → TeacherID

BCNF Solution:
Split into two tables to ensure all determinants are superkeys:

Copy
StudentClasses:
StudentID | ClassID
----------|---------
S1        | C1
S1        | C2
S2        | C1

ClassTeachers:
ClassID | TeacherID
--------|----------
C1      | T1
C2      | T2
Interview Tips
When to normalize:
When you need to minimize redundancy
When data integrity is critical
For OLTP systems (transaction-heavy)

When to denormalize:
For read-heavy systems (OLAP)
When performance is more critical than storage
For analytical queries that join many tables

Common interview questions:
"Design a database schema for X system" (then discuss normalization)
"How would you improve this existing schema?"
"What are the tradeoffs between normalization levels?"

Remember that in real-world system design, you often stop at 3NF unless you have very specific requirements that demand BCNF. The tradeoff between normalization and performance is a common discussion point in interviews.


Indexing (B-Tree, Hash Index) :
ndexing is a critical database optimization technique that speeds up data retrieval operations. Understanding different indexing methods is essential for system design interviews.

Why Indexing Matters
Indexes are like the table of contents in a book - they allow the database to find data without scanning every row. Proper indexing can make queries orders of magnitude faster, while poor indexing can slow down write operations unnecessarily.

B-Tree Index (Balanced Tree)
What it is:

The most common index type in relational databases

Self-balancing tree structure that maintains sorted data

Allows searches, sequential access, insertions, and deletions in O(log n) time

Structure:

Copy
       [Root Node: 20, 40]
        /      |       \
[<20]  [20-40]  [>40]
Characteristics:

Each node contains multiple keys and pointers

All leaves are at the same level (balanced)

Data is stored in sorted order

Supports range queries (>, <, BETWEEN) efficiently

Use Cases:

Default index type in most databases (MySQL InnoDB, PostgreSQL)

Columns frequently used in WHERE clauses

Columns used in JOIN, ORDER BY, or GROUP BY operations

Example:

sql
Copy
-- Creating a B-tree index
CREATE INDEX idx_customer_name ON customers(last_name);

-- Query that would use this index
SELECT * FROM customers WHERE last_name = 'Smith';
Hash Index
What it is:

Uses a hash table structure

Maps keys to specific locations via a hash function

Provides O(1) lookup time for exact matches

Structure:

Copy
Hash Buckets:
[0] -> (key1, value1) -> (key4, value4)
[1] -> (key2, value2)
[2] -> (key3, value3)
Characteristics:

Extremely fast for equality comparisons (=)

Doesn't support range queries

Requires exact matches

Performance depends on hash function quality

Use Cases:

In-memory databases (Redis, Memcached)

Exact match lookups (primary key access)

Temporary tables or join operations

Example:

sql
Copy
-- MySQL MEMORY storage engine uses hash indexes by default
CREATE TABLE session_data (
    session_id CHAR(32) PRIMARY KEY,
    user_data TEXT
) ENGINE=MEMORY;

-- Fast lookup by exact session_id
SELECT * FROM session_data WHERE session_id = 'abc123';
Comparison: B-Tree vs. Hash Index
Feature	B-Tree Index	Hash Index
Query Support	Range, equality, sorting	Only equality
Time Complexity	O(log n)	O(1) for perfect hashes
Space Overhead	Moderate	Low to moderate
Update Cost	Moderate	Low
Common Uses	General purpose	Exact match lookups
Database Examples	MySQL InnoDB, PostgreSQL	MySQL MEMORY, Redis
Interview Considerations
When to use which index:

Use B-Tree for most general cases (supports more operations)
Use Hash for exact-match lookups when range queries aren't needed
Tradeoffs to discuss:
Indexes speed up reads but slow down writes (inserts/updates/deletes)
Additional storage space required
Maintenance overhead

Common interview questions:
"How would you optimize this slow query?"
"What columns would you index in this schema?"
"Explain how a database finds records with and without an index"

Advanced topics to know:
Composite indexes (multi-column indexes)
Covering indexes (when the index contains all needed data)
Clustered vs. non-clustered indexes
Index selectivity (how unique values are in an index)

Transactions (ACID Properties) :
Transactions are fundamental to database systems, ensuring data integrity even in cases of system failures or concurrent access. The ACID properties define the key characteristics of reliable transactions.

What is a Transaction?
A transaction is a sequence of operations performed as a single logical unit of work that must either:

Complete entirely (all operations succeed), or

Have no effect at all (as if none of the operations happened)

Example:

sql
Copy
BEGIN TRANSACTION;
  UPDATE accounts SET balance = balance - 100 WHERE account_id = 'A';
  UPDATE accounts SET balance = balance + 100 WHERE account_id = 'B';
COMMIT;
ACID Properties
1. Atomicity
Definition: The transaction is treated as a single "unit" - either all of its operations complete, or none do.

Key Points:

Implemented using transaction logs (undo/redo logs)

If any operation fails, the entire transaction is rolled back

Ensures there are no partial updates

Example: In a funds transfer, if the debit succeeds but the credit fails, the debit is rolled back.

2. Consistency
Definition: A transaction brings the database from one valid state to another, maintaining all defined rules (constraints, cascades, triggers).

Key Points:

Database constraints (PK, FK, unique, checks) must remain valid

Application-level invariants must be preserved

If a transaction would violate consistency, it's aborted

Example: A transaction can't leave a "balance" field negative if there's a CHECK(balance >= 0) constraint.

3. Isolation
Definition: Concurrent transactions execute as if they were serial (one after another), preventing interference.

Key Points:

Implemented via locking or multi-version concurrency control (MVCC)

Isolation levels control the degree of isolation (with performance tradeoffs)

Prevents dirty reads, non-repeatable reads, and phantom reads

Common Isolation Levels:

Read Uncommitted - Lowest isolation, can read uncommitted changes (dirty reads)

Read Committed - Only see committed changes (default in many databases)

Repeatable Read - Same read returns same result within transaction

Serializable - Highest isolation, transactions appear to execute serially

4. Durability
Definition: Once a transaction is committed, its effects persist even in case of system failure.

Key Points:

Achieved through write-ahead logging (WAL)

Committed data is written to persistent storage

Survives power outages, crashes, etc.

Example: After you get a "Transfer Successful" message, the bank can't lose that transaction.

Transaction States
Copy
        Begin
          ↓
      Active
     /      \
  Failed   Committed
    ↓
  Aborted
Interview Considerations
Implementation Questions:

1. Implementing Transactions in Distributed Systems
Approaches:

Two-Phase Commit (2PC):

mermaid
Copy
graph TD
  A[Coordinator] -->|Prepare| B[Participant 1]
  A -->|Prepare| C[Participant 2]
  B -->|Vote| A
  C -->|Vote| A
  A -->|Commit/Rollback| B
  A -->|Commit/Rollback| C
Coordinator first sends "prepare" to all participants

Participants lock resources and vote (Yes/No)

If all vote Yes, coordinator sends "commit"

Saga Pattern (for long-running transactions):

Break transaction into smaller sub-transactions

Each sub-transaction has a compensating action

Example: e-commerce order (reserve inventory → charge card → ship)

Tradeoffs:

2PC provides ACID but blocks during failures

Saga is more scalable but requires compensation logic

2. 2PC vs 2PL
Two-Phase Commit (2PC)	Two-Phase Locking (2PL)
Purpose	Atomic commit across nodes	Concurrency control
Phases	1. Prepare 2. Commit/Rollback	1. Growing (acquire locks) 2. Shrinking (release locks)
Used in	Distributed transactions	Single-node transaction systems
Failure Handling	Blocks if coordinator fails	Deadlocks possible
Example	Updating bank balance across DCs	Preventing dirty reads in MySQL
3. Achieving Durability
Methods:

Write-Ahead Logging (WAL):

All changes logged to disk before applying to data files

Example: PostgreSQL's WAL, MySQL's InnoDB redo log

Shadow Paging:

Maintains two page tables (current and shadow)

Atomic switches between them (used in SQLite)

Replication:

Synchronous replication to multiple nodes

Example: MongoDB's write concern "majority"

Key Techniques:

fsync() calls to force OS buffer flush to disk

Checksums to detect corruption (ZFS, Cassandra)

Battery-backed write cache in enterprise storage

Interview Tip: Mention that durability often involves tradeoffs between write speed and safety (e.g., MongoDB's journaling vs writeConcern settings).

Tradeoffs:

Higher isolation levels reduce concurrency

Strict ACID compliance can limit scalability

NoSQL systems often sacrifice some ACID properties for performance

Real-world Examples:

Banking systems require strong ACID compliance

Shopping cart checkouts need transaction support

Social media feeds might tolerate weaker consistency

CAP Theorem Connection:

ACID databases typically favor CP (Consistency and Partition tolerance)

Discuss when you might relax ACID requirements for availability

Common Interview Questions
"How would you design a payment system that maintains balance consistency?"

"What isolation level would you choose for an e-commerce inventory system?"

"Explain how you'd handle a transaction that fails halfway through."

"How do NoSQL systems handle transactions differently than SQL systems?"



Concurrency & Multithreading :
Concurrency and multithreading are fundamental concepts for building high-performance systems. Here's what you need to know for system design interviews:

Core Concepts
Concurrency - The ability of a system to handle multiple tasks in overlapping time periods (not necessarily simultaneously)

Parallelism - Actually executing multiple tasks simultaneously (requires multiple CPU cores)

Thread - The smallest sequence of programmed instructions that can be managed independently by a scheduler

Key Challenges in Multithreading
Race Conditions

When multiple threads access shared data and try to change it simultaneously

Example: Two threads incrementing the same counter without synchronization

Deadlocks

When two or more threads are blocked forever waiting for each other

Classic example (Four necessary conditions):

Mutual exclusion

Hold and wait

No preemption

Circular wait

Starvation

When a thread is perpetually denied access to resources

Synchronization Mechanisms
1. Locks/Mutexes
python
Copy
lock = threading.Lock()

def thread_safe_function():
    with lock:
        # Critical section
        shared_variable += 1
2. Semaphores
python
Copy
semaphore = threading.Semaphore(3)  # Allow 3 threads at once

def limited_access_function():
    with semaphore:
        # Only 3 threads can execute this at once
3. Monitors
Higher-level synchronization construct that combines mutual exclusion with condition variables

4. Atomic Operations
java
Copy
AtomicInteger counter = new AtomicInteger(0);

void increment() {
    counter.incrementAndGet();  // Thread-safe without explicit locking
}
Common Patterns
1. Producer-Consumer
mermaid
Copy
graph LR
    P[Producer Threads] -->|Put items| B[Blocking Queue]
    B -->|Take items| C[Consumer Threads]
2. Thread Pools
Reuse a fixed number of threads to execute tasks

Avoids thread creation/destruction overhead

3. Read-Write Locks
Multiple readers or single writer

Improves performance for read-heavy workloads

Interview Considerations
Performance vs. Correctness

"How would you optimize this concurrent code?"

"What tradeoffs would you make between throughput and safety?"

System Design Questions

"Design a web server that handles multiple requests"

"How would you implement a rate limiter?"

Troubleshooting

"This code has a race condition - how would you fix it?"

"How would you debug a deadlock?"

Modern Approaches

Async/await (coroutines)

Actor model (Akka, Erlang)

Software Transactional Memory

Example Interview Question
"Design a thread-safe counter that can be incremented by multiple threads"

Solution:

java
Copy
public class ThreadSafeCounter {
    private AtomicInteger count = new AtomicInteger(0);
    
    public void increment() {
        count.incrementAndGet();
    }
    
    public int getCount() {
        return count.get();
    }
}
Key points to discuss:

Why AtomicInteger instead of synchronized?

Tradeoffs of different implementations

Performance implications under high contention

Remember to discuss:

Thread safety guarantees

Memory visibility (volatile, happens-before)

Performance considerations

Alternative approaches


4. Step-by-Step Approach for Solving Design Problems

For HLD
Clarify Requirements (Ask clarifying questions)
Estimate Scale (Traffic, Storage, Bandwidth)
Define APIs (Endpoints, Request/Response)
Database Design (Tables, Indexes, Sharding)
High-Level Architecture (Components, Data Flow)
Deep Dive (Caching, Load Balancing, Fault Tolerance)
Identify Bottlenecks (Optimize where needed)

1. Clarify Requirements
Goal: Understand the problem scope, constraints, and edge cases.
Key Questions:

Functional Requirements:

What are the core features? (e.g., "Is this a read-heavy or write-heavy system?")

What are the input/output expectations? (e.g., "What data does the API need to return?")

Are there any special constraints? (e.g., "Does it need real-time updates?")

Non-Functional Requirements:

What’s the expected availability (99.9% SLA?) and latency (p99 < 200ms)?

How important is consistency vs. availability (CAP tradeoffs)?

Any security or compliance requirements (GDPR, encryption)?

Example:

For a URL shortener:

"Should the short links expire?"

"Do we need analytics for clicks?"

2. Estimate Scale (Traffic, Storage, Bandwidth)
Goal: Calculate rough numbers to guide design decisions.
Key Questions:

Traffic Estimates:

What’s the QPS (Queries Per Second) for reads/writes?

What’s the peak traffic (e.g., 10x average during spikes)?

Storage Estimates:

How much data per entity? (e.g., "Each URL mapping is 500 bytes")

Total storage after 5 years? (Include growth rate.)

Bandwidth:

Data transfer per request/response (e.g., "1 KB per shortened URL request").

Example Calculation:

If you have 1M daily active users (DAU) with 10 requests/user/day:

QPS = (1M × 10) / 86400 ≈ 116 QPS

Storage: 1M new URLs/day × 500 bytes = 500 MB/day → ~180 GB/year.

3. Define APIs
Goal: Specify how clients interact with the system.
Key Questions:

What are the endpoints and their methods (GET/POST/PUT/DELETE)?

What’s the request/response schema? (JSON/Protobuf?)

Are there rate limits or authentication requirements?

Example for a URL Shortener:

rest
Copy
POST /api/shorten  
Request: { "original_url": "https://example.com/very-long-path" }  
Response: { "short_url": "https://short.ly/abc123" }  

GET /abc123  
Response: 302 Redirect to original URL  
4. Database Design
Goal: Choose DB type, schema, and scaling strategy.
Key Questions:

SQL vs. NoSQL? (Need transactions? Flexible schema?)

Tables/Collections: What’s the schema? (e.g., short_urls(id, original_url, user_id, expires_at))

Indexes: What queries need optimization? (e.g., INDEX ON short_code).

Sharding/Partitioning: How to scale? (e.g., shard by short_code hash).

Example:

For a Twitter-like system:

Tweets table (sharded by user_id).

Secondary indexes for trending hashtags.

5. High-Level Architecture (Components, Data Flow)
Goal: Draw the system’s major components and interactions.
Key Questions:

What are the core services? (e.g., API servers, DB, cache, queue).

How do they communicate? (REST/RPC/event-driven?).

Any third-party services? (CDN, Auth, Payment).

Example Diagram:

Copy
Client → Load Balancer → API Servers → Cache (Redis) → Database (PostgreSQL)  
                         ↓  
                     Async Queue (Kafka) → Analytics Service  
6. Deep Dive (Caching, Load Balancing, Fault Tolerance)
Goal: Optimize critical paths and ensure reliability.
Key Questions:

Caching:

What to cache? (e.g., "Top 10% of URLs get 90% traffic").

Cache eviction policy? (LRU/LFU).

Load Balancing:

Round-robin, least connections, or consistent hashing?

Fault Tolerance:

How to handle DB failures? (Read replicas? Multi-region?).

Retry strategies for failed requests?

Example:

Use Redis for caching hot URLs with 5-minute TTL.

Multi-AZ DB deployments with failover.

7. Identify Bottlenecks & Optimize
Goal: Find and resolve scalability limits.
Key Questions:

Where is the slowest part of the system? (DB? Network?).

How to reduce latency? (Edge caching, DB read replicas).

How to handle traffic spikes? (Auto-scaling, throttling).

Example Optimizations:

Database: Add read replicas for heavy read loads.

Network: Use a CDN for static assets.

Cost: Move cold data to S3/archive storage.

Bonus: Questions to Ask the Interviewer
"Are there any specific scalability goals we should prioritize?"

"Should we optimize for consistency or availability in this scenario?"

"Are there legacy systems we need to integrate with?"
 
```
