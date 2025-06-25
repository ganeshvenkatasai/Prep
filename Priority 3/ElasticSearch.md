# Elasticsearch Fundamentals
- **Elasticsearch**: Distributed, RESTful search and analytics engine built on Apache Lucene.
- **Document**: Basic unit of information (JSON format) stored in Elasticsearch.
- **Index**: Collection of documents with similar characteristics (analogous to a database).
- **Shard**: Horizontal partition of an index (primary/replica for scalability and redundancy).
- **Node**: Single server instance that stores data and participates in cluster.
- **Cluster**: Collection of connected nodes that hold entire data and provide federated indexing.

# Core Concepts
- **Inverted Index**: Data structure that maps terms to documents for fast full-text search.
- **Analyzer**: Converts text into tokens/terms (character filters, tokenizer, token filters).
- **Mapping**: Defines how documents and fields are stored and indexed (schema-like).
- **Relevance Scoring**: BM25 algorithm calculates how well documents match queries.
- **Near Real-Time (NRT)**: Documents become searchable within 1 second (refresh interval).

# CRUD Operations
- **Index API**: `PUT /index/_doc/1` - Creates or updates a document.
- **Get API**: `GET /index/_doc/1` - Retrieves a document by ID.
- **Delete API**: `DELETE /index/_doc/1` - Removes a document.
- **Update API**: `POST /index/_update/1` - Partially updates a document.
- **Bulk API**: `POST _bulk` - Performs multiple operations in single request.

# Search Operations
- **Query DSL**: JSON-based language for complex searches (match, term, range queries).
- **Full-Text Search**: `match` query analyzes search terms before matching.
- **Term-Level Search**: `term` query searches exact values without analysis.
- **Bool Query**: Combines multiple queries with `must`, `should`, `must_not`, `filter`.
- **Aggregations**: Analytics (metrics, bucketing, pipeline) on search results.
- **Highlighting**: Shows matched fragments in results with custom formatting.
- **Pagination**: `from` and `size` parameters control result window.

# Performance Optimization
- **Shard Strategy**: Optimal shard size 10-50GB, avoid over-sharding.
- **Refresh Interval**: Increase beyond 1s for heavy indexing workloads.
- **Bulk Requests**: Preferred over single-document operations for indexing.
- **Doc Values**: Columnar storage for efficient sorting/aggregations.
- **Fielddata**: In-memory data structure for text field aggregations (use cautiously).
- **Index Templates**: Define default mappings/settings for new indices.
- **Aliases**: Logical names that can point to one or more indices.

# Cluster Management
- **Master Node**: Controls cluster state and operations (minimum 3 for HA).
- **Data Node**: Stores data and executes data-related operations.
- **Ingest Node**: Pre-processes documents before indexing.
- **Coordinating Node**: Routes requests (default role for all nodes).
- **Discovery**: Zen2 protocol handles node communication and cluster formation.
- **Split Brain**: Prevented by setting `discovery.zen.minimum_master_nodes` (quorum).

# Monitoring & Maintenance
- **Cat API**: Compact and aligned text views (`/_cat/indices?v`).
- **Cluster Health**: `GET _cluster/health` shows status (green/yellow/red).
- **Index Management**: Rollover, shrink, forcemerge optimize indices.
- **Snapshot/Restore**: Backup to shared filesystem/S3/HDFS.
- **Hot-Warm Architecture**: Separate hardware profiles for recent vs older data.

# Security Features
- **Authentication**: Username/password, LDAP, PKI, SAML.
- **Role-Based Access**: Control cluster/index/field-level permissions.
- **Document Security**: Shield field- and document-level security.
- **Audit Logging**: Tracks access attempts and operations.
- **TLS/SSL**: Encrypts inter-node and client-node communication.

# Common Use Cases
- **Application Search**: Website/product search with relevance ranking.
- **Log Analytics**: ELK Stack (Elasticsearch, Logstash, Kibana) for log analysis.
- **Metrics Analysis**: Time-series data with metric aggregations.
- **Security Analytics**: SIEM solutions for threat detection.
- **Geospatial Analysis**: Location-based queries and aggregations.

# Best Practices
- **Index per Time Period**: `logs-2023-01-01` for time-series data.
- **Avoid Wildcards**: Specific index names perform better than `log*`.
- **Mapping Explosion**: Limit dynamic mapping for high-cardinality fields.
- **Query Optimization**: Use filters for yes/no conditions (cached results).
- **Circuit Breakers**: Prevent out of memory errors during aggregations.
- **Disable Unused Features**: Turn off `_all` field if not needed.
- **Monitoring**: Track JVM heap, disk usage, query latency.

# Important APIs
- `_search`: Execute search queries.
- `_msearch`: Multiple search in one request.
- `_count`: Count matching documents.
- `_explain`: Shows score calculation details.
- `_validate`: Validate queries without execution.
- `_reindex`: Copy documents between indices.
- `_update_by_query`: Update documents matching query.
- `_cluster/settings`: Modify cluster settings.
