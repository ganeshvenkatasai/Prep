# gRPC Fundamentals
- **gRPC**: Modern RPC framework using HTTP/2 and Protocol Buffers.
- **Protocol Buffers**: Interface Definition Language (IDL) for service contracts.
- **HTTP/2**: Underlying transport protocol enabling multiplexing and streaming.
- **Language Agnostic**: Supports multiple languages (C++, Java, Python, Go, etc.).
- **Four Communication Patterns**: Unary, Server Streaming, Client Streaming, Bidirectional Streaming.

# Core Concepts
- **Service Definition**: Defined in .proto files using Protocol Buffer syntax.
- **Code Generation**: protoc compiler generates client/server code.
- **Stub**: Client-side proxy that abstracts remote calls.
- **Channel**: Virtual connection to gRPC service endpoint.
- **Deadlines/Timeouts**: Client-specified time limits for RPC completion.

# Protocol Buffers
- **Message**: Data structure definition (like class without methods).
- **Scalar Types**: int32, double, bool, string, bytes.
- **Repeated Fields**: Arrays/lists (marked with `repeated` keyword).
- **Enums**: Named integer constants for better readability.
- **Nested Types**: Messages can contain other messages.
- **Oneof**: Fields where only one can be set at a time.
- **Maps**: Key-value pairs (map<key_type, value_type>).

# Service Definition
- **rpc Keyword**: Defines remote methods in service.
- **Returns**: Always returns single message (streaming returns stream).
- **Package**: Namespace to prevent naming conflicts.
- **Import**: Reuse definitions from other .proto files.

# Communication Patterns
1. **Unary RPC**: Single request → single response (traditional RPC).
2. **Server Streaming RPC**: Single request → stream of responses.
3. **Client Streaming RPC**: Stream of requests → single response.
4. **Bidirectional Streaming**: Both sides send message streams independently.

# Advanced Features
- **Interceptors**: Middleware for auth/logging (client/server-side).
- **Metadata**: Header-like key-value pairs (like HTTP headers).
- **Error Handling**: Rich error codes and status details.
- **Load Balancing**: Client-side or through proxies like Envoy.
- **Health Checking**: Standard health check protocol.

# Performance
- **Binary Protocol**: Smaller payloads vs JSON/XML.
- **Multiplexing**: Multiple streams over single TCP connection.
- **Header Compression**: HPACK reduces overhead.
- **Pipelining**: Send multiple requests without waiting for responses.

# Security
- **TLS Encryption**: Required for production deployments.
- **Auth Mechanisms**: SSL/TLS, Google token-based, custom auth.
- **Channel Credentials**: Configure at channel creation.
- **Call Credentials**: Per-call authentication (e.g., OAuth2 tokens).

# Best Practices
- **Proto Stability**: Never change field numbers after deployment.
- **Package Naming**: Reverse domain name notation (com.example.service).
- **Versioning**: Add new fields rather than modifying existing ones.
- **Streaming**: Use for large datasets or real-time updates.
- **Deadlines**: Always set reasonable client deadlines.

# Tools & Ecosystem
- **grpcurl**: Like cURL but for gRPC (requires server reflection).
- **grpc-gateway**: Generate RESTful JSON API from proto.
- **protoc-gen-doc**: Generate documentation from proto files.
- **Envoy Proxy**: Advanced gRPC load balancing and observability.

# Common Use Cases
- **Microservices**: Efficient service-to-service communication.
- **Mobile Apps**: Minimize bandwidth and battery usage.
- **IoT Devices**: Handle intermittent connectivity.
- **Real-Time Systems**: Streaming stock prices, game states.
- **Cloud Native**: Kubernetes-native service mesh integration.

# Comparison
- **vs REST**: Binary vs text, streaming vs request-response, HTTP/2 vs HTTP/1.1.
- **vs GraphQL**: Strong typing vs flexible queries, binary vs JSON.
- **vs WebSockets**: Structured vs raw messaging, multiplexing.

# Troubleshooting
- **grpc_cli**: Command-line tool for debugging.
- **Server Reflection**: Enables tools to inspect services at runtime.
- **Logging**: Enable verbose logging for debugging.
- **Channel States**: IDLE, CONNECTING, READY, TRANSIENT_FAILURE, SHUTDOWN.
