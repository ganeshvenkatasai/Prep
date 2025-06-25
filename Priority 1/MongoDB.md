# MongoDB Fundamentals
- **NoSQL Database**: Document-oriented, schema-less data store.
- **BSON**: Binary JSON format used for storage (supports more data types than JSON).
- **Collections**: Analogous to tables in RDBMS (contains documents).
- **Documents**: JSON-like records (field-value pairs with flexible schema).
- **_id Field**: Unique primary key (auto-generated ObjectId if not specified).

# CRUD Operations
- **insertOne()**: Add single document to collection.
- **insertMany()**: Add multiple documents at once.
- **find()**: Query documents (empty = all docs).
- **findOne()**: Returns first matching document.
- **updateOne()**: Update first matching document.
- **updateMany()**: Update all matching documents.
- **replaceOne()**: Fully replace first matching document.
- **deleteOne()**: Remove first matching document.
- **deleteMany()**: Remove all matching documents.
- **bulkWrite()**: Perform multiple operations in bulk.

# Query Operators
- **Comparison**: $eq, $ne, $gt, $gte, $lt, $lte, $in, $nin.
- **Logical**: $and, $or, $not, $nor.
- **Element**: $exists, $type.
- **Array**: $all, $elemMatch, $size.
- **Evaluation**: $expr, $jsonSchema, $mod, $regex, $text, $where.

# Update Operators
- **Fields**: $set, $unset, $rename, $inc, $mul, $min, $max.
- **Arrays**: $push, $pop, $pull, $pullAll, $addToSet.
- **Bitwise**: $bit.
- **Array Positional**: $ (update matched array element).
- **Aggregation Pipeline**: Use $[] for all array elements.

# Indexes
- **Single Field**: Index on one field.
- **Compound**: Index on multiple fields.
- **Multikey**: Index on array fields (one entry per array element).
- **Text**: Full-text search index.
- **Geospatial**: 2dsphere for geometric data.
- **Hashed**: For sharding hash-based keys.
- **TTL**: Automatically remove docs after period.
- **Unique**: Enforce field uniqueness.
- **Partial**: Index only docs matching filter.
- **Sparse**: Index only docs with the field.

# Aggregation Framework
- **$match**: Filter documents (like find()).
- **$group**: Group by expression.
- **$project**: Reshape documents (include/exclude fields).
- **$sort**: Order documents.
- **$skip**: Skip N documents.
- **$limit**: Limit result count.
- **$unwind**: Deconstruct array fields.
- **$lookup**: Left outer join with another collection.
- **$facet**: Multiple pipelines in single stage.
- **$bucket**: Categorize docs into groups.

# Performance
- **Explain Plans**: Analyze query performance (db.collection.explain()).
- **Covered Query**: Query satisfied entirely by index.
- **Read Preference**: Control where queries execute (primary/secondary).
- **Write Concern**: Number of nodes that must acknowledge writes.
- **Sharding**: Horizontal partitioning across servers.
- **Replica Sets**: High availability through data replication.

# Data Modeling
- **Embedded**: Related data in single document (1:1, 1:few).
- **Referenced**: Related data in separate collections (1:many, many:many).
- **Atomicity**: Write operations atomic at document level.
- **Schema Validation**: Enforce structure with JSON Schema.

# Transactions
- **Multi-Document ACID**: Supported in replica sets (v4.0+) and sharded clusters (v4.2+).
- **Session**: Context for transaction sequence.
- **Retryable Writes**: Automatically retry certain operations.

# Security
- **Authentication**: SCRAM, x.509, LDAP, Kerberos.
- **Authorization**: Role-based access control (RBAC).
- **Encryption**: TLS/SSL, client-side field-level encryption.
- **Auditing**: Track system activity.

# Tools
- **mongod**: Primary daemon process.
- **mongos**: Router for sharded clusters.
- **mongo**: Interactive shell.
- **Compass**: GUI for MongoDB.
- **Atlas**: Cloud MongoDB service.
- **BI Connector**: SQL interface for analytics.

# Best Practices
- **Index Selectivity**: Create indexes on high-cardinality fields.
- **Projection**: Return only needed fields.
- **Batch Operations**: Use bulk writes for efficiency.
- **Connection Pooling**: Reuse database connections.
- **Monitoring**: Track slow queries, hardware metrics.
- **Backups**: Regular snapshots + oplog for point-in-time recovery.

# Common Use Cases
- **Content Management**: Flexible schema for varied content types.
- **Product Catalogs**: Nested attributes, variants.
- **Real-time Analytics**: Aggregation framework.
- **IoT**: Time-series data, sensor readings.
- **Mobile Apps**: Offline-first sync capability.
