# Kafka

## Core Concepts
```
Broker = Single Kafka server that stores data
Cluster = Group of brokers working together
Topic = Category/feed name for messages
Partition = Ordered subset of a topic's messages
Offset = Unique ID for each message in partition
Producer = App that sends messages to Kafka
Consumer = App that reads messages from Kafka
Consumer Group = Set of consumers sharing workload
Replica = Copy of partition for fault tolerance
Leader = Primary replica handling all requests
Follower = Backup replica syncing with leader
```

## Essential Commands

```
kafka-topics --create --topic my_topic --partitions 3 --replication-factor 2 # Create topic
kafka-topics --list # List all topics
kafka-topics --describe --topic my_topic # Show topic details
kafka-console-producer --topic my_topic # Start producer
kafka-console-consumer --topic my_topic --from-beginning # Start consumer
kafka-consumer-groups --list # List consumer groups
```

## Key Configuration Settings

```
server.properties = Main broker config file
log.dirs = Where Kafka stores data files
zookeeper.connect = Zookeeper connection string
num.partitions = Default partitions per new topic
default.replication.factor = Default replicas per partition
```

## Critical Producer/Consumer Settings
```
acks=all = Wait for all replicas to confirm write
retention.ms = How long to keep messages (default 7 days)
auto.offset.reset = What to do when no offset exists (earliest/latest)
enable.auto.commit = Let consumer commit offsets automatically
```

## Common Patterns
```
Exactly-once = Prevent duplicate message processing
Dead Letter Queue = Handle failed messages pattern
Request-Reply = Two-way communication pattern
Event Sourcing = Store state changes as event stream
CQRS = Separate read and write paths
```

## Monitoring Metrics
```
Consumer lag = Messages not yet processed
Under-replicated = Partitions missing replicas
Active controllers = Broker managing cluster
Offline partitions = Currently unavailable partitions
```

## Ecosystem Tools
```
kcat = CLI producer/consumer (formerly kafkacat)
ksqlDB = SQL interface for stream processing
Kafka Connect = System integration framework
Schema Registry = Central schema management
```

## Production Best Practices
```
Partition count = Max consumer parallelism needed
Replication factor ≥ 2 for production
Always monitor consumer lag
Set appropriate message retention policy
Enable SSL/SASL for security
Test broker failure scenarios
Use compression for large messages
Size brokers for peak load + buffer
```

## Tips
```
More partitions = more parallelism but more overhead
Consumers in same group share topic partitions
Keys determine which partition messages go to
Order is guaranteed only within single partition
Zookeeper needed for older versions (removed in newer)
```



