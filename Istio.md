# Istio Fundamentals
- **Service Mesh**: Infrastructure layer for managing service-to-service communication.
- **Data Plane**: Envoy proxies handling traffic (sidecar containers).
- **Control Plane**: Manages proxies (Pilot, Citadel, Galley).
- **Sidecar Injection**: Automatic or manual addition of Envoy containers to pods.

# Core Components
- **Envoy Proxy**: High-performance data plane (L7/L4).
- **Pilot**: Service discovery and traffic management.
- **Citadel**: Certificate authority for mTLS.
- **Galley**: Configuration validation and distribution.
- **Mixer**: (Deprecated in 1.5+) Policy enforcement and telemetry.

# Architecture
- **Sidecar Pattern**: Proxy runs alongside each service instance.
- **Ingress Gateway**: Entry point for external traffic.
- **Egress Gateway**: Exit point for external traffic.
- **xDS API**: Dynamic configuration protocol for Envoy.

# Traffic Management
- **VirtualService**: Defines routing rules for services.
- **DestinationRule**: Policies for traffic after routing (load balancing, subsets).
- **Gateway**: Configures L4-L6 load balancer for ingress/egress.
- **ServiceEntry**: Adds external services to mesh registry.

# Security Features
- **mTLS**: Automatic mutual TLS between services.
- **RBAC**: Service-level and namespace-level access control.
- **AuthorizationPolicy**: Fine-grained access control (JWT claims, paths).
- **PeerAuthentication**: Defines mTLS mode (strict/permissive/disabled).
- **RequestAuthentication**: Validates JWT tokens.

# Observability
- **Metrics**: Prometheus collects service metrics.
- **Logs**: Access logs for all requests.
- **Distributed Tracing**: Integrated with Jaeger/Zipkin.
- **Kiali**: Service mesh visualization dashboard.
- **Grafana**: Preconfigured dashboards for monitoring.

# Key Concepts
- **Canary Deployments**: Traffic splitting between versions.
- **Circuit Breaking**: Outlier detection for unhealthy services.
- **Fault Injection**: Test resilience with delays/aborts.
- **Mirroring**: Shadow traffic to test new versions.
- **Retries**: Automatic retry of failed requests.

# Installation Modes
- **istioctl**: CLI-based installation.
- **Helm**: Package manager for Istio components.
- **Operator**: Kubernetes operator for lifecycle management.
- **Multi-Cluster**: Mesh spanning multiple clusters.

# Common Commands
- `istioctl analyze`: Validate configuration.
- `istioctl proxy-status`: View sync status of sidecars.
- `istioctl dashboard`: Access web UIs (kiali, grafana, prometheus).
- `istioctl inject`: Manual sidecar injection.
- `istioctl install`: Install control plane.

# Best Practices
- **Gradual Adoption**: Start with permissive mTLS mode.
- **Label Namespaces**: `istio-injection=enabled` for auto-injection.
- **Resource Limits**: Configure sidecar CPU/memory requests.
- **Version Drift**: Keep control plane and sidecars in sync.
- **Minimal APIs**: Use only required Istio CRDs.

# Performance Considerations
- **Latency Overhead**: ~10ms per hop for mTLS.
- **Sidecar Resources**: ~50MB memory per pod baseline.
- **Connection Limits**: Adjust envoy connection pools.
- **Telemetry Sampling**: Reduce tracing overhead.

# Troubleshooting
- **Proxy Logs**: `kubectl logs <pod> -c istio-proxy`.
- **Config Dump**: `istioctl proxy-config all <pod>`.
- **Network Issues**: Verify mTLS and RBAC settings.
- **Version Mismatch**: Check `istioctl version` vs sidecar versions.

# Integration
- **Kubernetes**: Native K8s service discovery.
- **Consul**: Alternative service registry.
- **VM Workloads**: Extend mesh to non-K8s workloads.
- **Knative**: Serverless workloads on Istio.

# Alternatives
- **Linkerd**: Lightweight service mesh.
- **Consul Connect**: HashiCorp service mesh.
- **AWS App Mesh**: Managed service mesh for ECS/EKS.
