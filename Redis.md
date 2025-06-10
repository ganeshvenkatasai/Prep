# Redis Basics
```
In-Memory Database: Stores data in RAM for ultra-fast read/write operations.
Key-Value Store: Simple data structure where keys map to values (strings, lists, etc.).
NoSQL Database: Schema-less, flexible data storage, unlike traditional SQL databases.
Persistence Options: Supports snapshotting (RDB) and append-only file (AOF) for durability.
Single-Threaded: Handles commands one at a time, ensuring atomicity.
```

# Data Structures
```
Strings: Basic key-value pairs (e.g., SET name "Alice").
Lists: Ordered collections of strings (e.g., LPUSH and RPOP operations).
Sets: Unordered unique elements (e.g., SADD to add, SINTER for intersection).
Sorted Sets: Sets with scores for ordering (e.g., ZADD to rank items).
Hashes: Key-value pairs within a key (e.g., HSET user:1 name "Bob").
Bitmaps & HyperLogLogs: Special types for efficient bit operations and unique counting.
```

# Advanced Features
```
Pub/Sub Messaging: Real-time message broadcasting between clients.
Transactions (MULTI/EXEC): Group commands to execute atomically.
Lua Scripting: Run server-side scripts for complex operations.
TTL (Time-To-Live): Auto-expire keys after a set duration (EXPIRE key 60).
Replication: Master-slave setup for read scalability and backup.
Cluster Mode: Sharding for horizontal scaling across multiple nodes.
Geospatial Indexing: Store and query locations (e.g., GEOADD).
```

# Use Cases
```
Caching: Speed up apps by storing frequently accessed data.
Session Storage: Manage user sessions in web apps.
Leaderboards: Sorted sets for rankings (e.g., gaming scores).
Rate Limiting: Control API request rates.
Real-Time Analytics: Track metrics with fast writes.
```

# Commands Cheatsheet

## Basic Key-Value Operations

```
SET name "Alice"          # Stores key "name" with value "Alice"  
GET name                 # Returns "Alice"  
DEL name                 # Deletes the key "name"  
EXISTS name              # Returns 1 if key exists, else 0  
EXPIRE name 60           # Deletes "name" after 60 seconds  
TTL name                 # Checks remaining time-to-live (in seconds)  
```

## Data Structures

### Strings

```
SET counter 10            # Stores integer 10  
INCR counter             # Increments to 11 (atomic)  
DECR counter             # Decrements to 10  
APPEND name " Smith"     # Appends to value ("Alice Smith")  
```

### Lists (Ordered)

```
LPUSH users "Alice"       # Adds to start of list  
RPUSH users "Bob"        # Adds to end  
LPOP users               # Removes/returns first element  
LRANGE users 0 -1        # Returns all elements  
```


### Sets (Unique)

```
SADD admins "Alice"      # Adds "Alice" to set
SREM admins "Bob"        # Removes "Bob"
SMEMBERS admins          # Lists all members
SISMEMBER admins "Alice" # Returns 1 if member exists
```

### Sorted Sets (Ranked)

```
ZADD leaderboard 100 "Alice"  # Adds with score 100
ZRANGE leaderboard 0 -1       # Returns all (ascending)
ZREVRANGE leaderboard 0 2     # Top 3 (descending)
```

### Hashes (Key-Value Pairs in a Key)

```
HSET user:1 name "Alice" age 30  # Stores nested fields
HGET user:1 name            # Returns "Alice"
HGETALL user:1              # Returns all fields
```

## Advanced Features

### Pub/Sub Messaging

```
SUBSCRIBE news            # Listens to "news" channel
PUBLISH news "Hello!"     # Sends message to subscribers (in another terminal)
```


### Transactions

```
MULTI                     # Starts transaction
SET balance 100
INCRBY balance 50
EXEC                      # Executes all commands atomically
```

### Lua Scripting

```
EVAL "return redis.call('GET', 'name')" 0  # Runs script to fetch "name"
```


### Persistence & Administration

```
SAVE                      # Forces snapshot (blocks Redis)
BGSAVE                    # Saves snapshot in background
CONFIG GET *              # Lists all server configs
FLUSHALL                  # Deletes ALL data (use with caution!)
```


## Real-World Use Cases

### Caching

```
SETEX page:home 3600 "<html>..."  # Caches HTML for 1 hour
```


### Rate Limiting

```
INCR ip:127.0.0.1        # Tracks requests
EXPIRE ip:127.0.0.1 60   # Resets counter after 60s
# (Check if counter > 100 to block)
```


### Session Storage

```
SET session:abc123 "{user_id: 1}"
EXPIRE session:abc123 86400  # Expires in 24h
```



























