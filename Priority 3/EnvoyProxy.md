# Envoy Proxy Fundamentals
- **Envoy**: High-performance L7/L4 proxy and communication bus designed for cloud-native applications.
- **Listener**: Network interface that accepts connections (IP/port/protocol configuration).
- **Filter**: Processing unit that transforms requests/responses (network or HTTP level).
- **Cluster**: Group of logically similar upstream hosts (services/envoy instances).
- **Endpoint**: Individual instance in a cluster (IP/port of actual service).
- **Route**: Rules for forwarding requests to clusters based on request characteristics.

# Core Components
- **xDS API**: Dynamic configuration protocol (CDS/EDS/LDS/RDS/VHDS/SDS).
- **Discovery Service**: Source of truth for dynamic configuration (file/GRPC/REST).
- **HCM (HTTP Connection Manager)**: Main HTTP filter that handles L7 processing.
- **TLS Context**: SSL/TLS termination and origination configuration.
- **Access Logs**: Detailed request/response logging (files/GRPC).
- **Stats**: Metrics collection with tags (counters/gauges/histograms).

# Common Use Cases
- **Edge Proxy**: Ingress controller for Kubernetes (Istio Ingress).
- **Service Mesh Sidecar**: Per-pod proxy in Istio/Linkerd service meshes.
- **API Gateway**: Route, transform, and secure API traffic.
- **Load Balancer**: Distribute traffic across backend services.
- **Protocol Translator**: Convert between gRPC/HTTP/WebSocket etc.

# Key Features
- **Dynamic Configuration**: Hot-reload without restart via xDS API.
- **Load Balancing**: Round robin/least request/ring hash/maglev algorithms.
- **Circuit Breaking**: Outlier detection and ejection of unhealthy hosts.
- **Retries**: Configurable retry policies with budget limits.
- **Timeouts**: Global and per-route timeout controls.
- **Shadowing**: Mirror traffic to another cluster for testing.
- **Rate Limiting**: Integrates with external rate limit service.
- **Tracing**: Distributed tracing support (Zipkin/Jaeger).
- **WASM Extensibility**: WebAssembly-based filter extensions.

# Configuration Types
- **Static**: Bootstrap config loaded at startup (YAML/JSON).
- **Dynamic**: Runtime updates via xDS management servers.
- **File-based**: Watch directory for config updates (--config-yaml flag).
- **Admin Interface**: `/stats`, `/config_dump`, `/logging` endpoints.

# Protocols Supported
- **HTTP/1.1**: Full proxy support with keepalive.
- **HTTP/2**: End-to-end and HTTP/1.1 upgrade.
- **gRPC**: Native support including bidirectional streams.
- **WebSocket**: Full proxy with protocol upgrade.
- **MongoDB**: L7 filtering and metrics.
- **Redis**: Protocol-aware traffic splitting.
- **MySQL**: L7 traffic inspection.
- **Raw TCP**: L4 passthrough with metrics.

# Performance Characteristics
- **C++ Implementation**: High performance with low latency.
- **Non-Blocking I/O**: Event-driven architecture (libevent).
- **Zero Downtime**: Hot restart for config updates.
- **L7 Processing**: ~10K RPS per core for complex HTTP routing.
- **Memory Footprint**: ~50MB baseline, grows with config complexity.

# Observability Features
- **Metrics**: StatsD/sinks for Prometheus/Datadog etc.
- **Tracing**: Support for context propagation headers.
- **Access Logs**: Customizable request/response logging.
- **Admin Interface**: Real-time monitoring endpoints.
- **Tap Filter**: Record full request/response flows.

# Security Features
- **TLS Termination**: Full certificate management.
- **JWT Validation**: Verify and extract claims from JWTs.
- **RBAC**: Network and HTTP-level access control.
- **External Auth**: Integrate with auth services.
- **SDS (Secret Discovery)**: Dynamic certificate rotation.

# Service Mesh Integration
- **Istio**: Default data plane proxy.
- **Consul Connect**: Native integration option.
- **Linkerd**: Alternative lightweight proxy.
- **xDS Standard**: Common config API for mesh interoperability.

# Deployment Patterns
- **Sidecar**: Co-located with application container.
- **Edge Proxy**: Cluster ingress point.
- **Middleware**: Dedicated proxy tier between services.
- **Lambda/Serverless**: Event-driven deployments.

# Common Filters
- **Router**: Main HTTP request routing logic.
- **CORS**: Cross-origin resource sharing.
- **Fault Injection**: Delay/abort requests for testing.
- **Health Check**: Active upstream monitoring.
- **Compression**: Gzip/Brotli response compression.
- **External Processing**: Call out to ext_proc services.
- **WASM**: Custom WebAssembly extensions.

# Best Practices
- **Circuit Breakers**: Essential for resilient upstream calls.
- **Resource Limits**: Set connection/timeout/retry budgets.
- **Observability**: Enable stats/tracing/logging by default.
- **Canary Deployments**: Use weighted clusters for safe rollouts.
- **Zero-Trust**: Default-deny with explicit RBAC policies.
- **Config Versioning**: Track envoy configs in source control.
