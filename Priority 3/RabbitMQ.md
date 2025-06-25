# RabbitMQ Fundamentals
- **Message Broker**: Middleware for asynchronous messaging between systems.
- **AMQP Protocol**: Advanced Message Queuing Protocol (RabbitMQ implements 0-9-1).
- **Producer**: Application sending messages.
- **Consumer**: Application receiving messages.
- **Queue**: Buffer storing messages until consumed.
- **Exchange**: Receives messages and routes to queues.
- **Binding**: Link between exchange and queue with routing rules.

# Core Components
- **Virtual Host**: Logical isolation unit (like namespace).
- **Connection**: TCP connection between app and broker.
- **Channel**: Lightweight connection inside a TCP connection.
- **Message**: Data + headers/attributes (persistent or transient).

# Exchange Types
- **Direct**: Routes via exact routing key match.
- **Fanout**: Broadcasts to all bound queues (no routing key).
- **Topic**: Routes via pattern matching (wildcards * and #).
- **Headers**: Routes based on message headers (ignore routing key).
- **Default (Nameless)**: Auto-bound to queues with matching names.

# Message Patterns
- **Work Queues**: Distribute tasks among workers (round-robin).
- **Pub/Sub**: Broadcast messages to multiple consumers.
- **Routing**: Selective message delivery based on keys.
- **Topics**: Complex routing patterns.
- **RPC**: Request-reply pattern (using reply-to and correlation_id).

# Message Properties
- **Persistent**: Survive broker restart (needs durable queue).
- **Delivery Mode**: 1=non-persistent, 2=persistent.
- **TTL**: Message expiration (queue or message level).
- **Priority**: Higher priority messages get processed first.
- **Dead Lettering**: Route failed messages to special exchange.

# Queue Features
- **Durable**: Survives broker restart (messages must also be persistent).
- **Exclusive**: Only one connection can use it (deleted when connection closes).
- **Auto-delete**: Deletes when last consumer unsubscribes.
- **Arguments**: Additional features (x-message-ttl, x-dead-letter-exchange).

# Reliability Features
- **Publisher Confirms**: Broker acknowledges message receipt.
- **Consumer Acknowledgements**: Manual (explicit) or auto (implicit).
- **HA Queues**: Mirrored across cluster nodes for fault tolerance.
- **Transaction**: Batch operations (less performant than confirms).

# Cluster Architecture
- **Nodes**: RabbitMQ instances in cluster (share users/vhosts/queues).
- **Disk Node**: Stores metadata on disk (recommended: 1 per cluster).
- **RAM Node**: Stores metadata in memory (faster but volatile).
- **Queue Mirroring**: Replicate queues across nodes (HA policy).

# Administration
- **Management Plugin**: Web UI for monitoring (port 15672).
- **CLI Tools**: rabbitmqctl, rabbitmqadmin.
- **Policies**: Apply rules to exchanges/queues (HA, TTL, DLX).
- **Shovel Plugin**: Move messages between brokers.
- **Federation Plugin**: Link exchanges/queues across brokers.

# Best Practices
- **Connection Management**: Reuse connections, use multiple channels.
- **Error Handling**: Implement confirms and return listeners.
- **Consumer Prefetch**: Limit unacknowledged messages (QoS).
- **Monitoring**: Track queue lengths, consumer counts.
- **Resource Alarms**: Configure memory/disk thresholds.

# Common Use Cases
- **Background Jobs**: Offload slow processing tasks.
- **Microservices**: Decouple service communication.
- **Event-Driven**: React to system events.
- **Buffer**: Handle traffic spikes gracefully.
- **Work Distribution**: Parallel task processing.

# Troubleshooting
- **Queue Backlog**: Add consumers or increase prefetch.
- **Memory Pressure**: Reduce message TTL or add consumers.
- **Network Partitions**: Configure pause_minority mode.
- **Message Loss**: Enable confirms and persistence.
- **Performance**: Use more channels instead of connections.

# Alternatives
- **Kafka**: Higher throughput but more complex.
- **ActiveMQ**: JMS-compliant alternative.
- **AWS SQS**: Managed queue service.
- **NATS**: Simpler, lightweight broker.
