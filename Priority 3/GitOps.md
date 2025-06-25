# GitOps Fundamentals
- **GitOps**: DevOps methodology using Git as single source of truth for infrastructure and apps.
- **Declarative**: Define desired state in Git, let tools reconcile actual state.
- **Pull-based**: Agents in cluster pull changes (vs push-based CI/CD).
- **Reconciliation**: Continuous process to align cluster state with Git state.
- **Immutable Infrastructure**: Changes require new Git commit (no direct cluster modifications).

# Core Principles
- **Git as Source**: All manifests, configs, and policies versioned in Git.
- **Automated Sync**: Tools automatically apply Git changes to clusters.
- **Observable**: System state always verifiable against Git history.
- **Closed Loop**: Changes only via Git, alerts on drift detection.

# ArgoCD Overview
- **ArgoCD**: Declarative GitOps continuous delivery tool for Kubernetes.
- **Kubernetes-Native**: Runs as controller inside your cluster.
- **Web UI**: Dashboard for visualizing applications and sync status.
- **CLI**: `argocd` command-line tool for management.
- **SSO Integration**: Supports OAuth2, LDAP, SAML authentication.

# Key Components
- **Application**: Custom resource defining source repo and destination cluster.
- **Project**: Logical grouping of applications with RBAC controls.
- **Repository**: Git repo containing Kubernetes manifests (Helm/Kustomize/plain YAML).
- **Cluster**: Target Kubernetes cluster where apps are deployed.
- **Sync Policy**: Automated or manual update strategy.

# Core Features
- **Multi-Cluster**: Manage deployments across multiple Kubernetes clusters.
- **Multi-Tenancy**: Isolate teams/projects using namespaces and RBAC.
- **Health Status**: Built-in checks for Deployment, Service, Ingress etc.
- **Sync Waves**: Order resource creation (e.g., CRDs before controllers).
- **Hooks**: Pre/Post sync operations (e.g., database migrations).
- **Rollback**: Revert to any previous Git commit version.
- **Diff View**: Compare live state vs desired state in Git.

# Sync Strategies
- **Automated**: Immediate sync on Git commit (with pruning).
- **Manual**: Require user approval for sync operations.
- **Sync Options**: Skip dry-run, apply only, force replace.
- **Prune**: Automatically remove resources deleted from Git.
- **Self-Heal**: Automatically revert manual cluster changes.

# Application Sources
- **Helm**: Deploy Helm charts (values in Git or override in UI).
- **Kustomize**: Support for kustomization.yaml overlays.
- **Plain YAML**: Raw Kubernetes manifests directory.
- **Jsonnet**: Templating support for complex configurations.
- **Plugin**: Custom config management tools via plugins.

# Advanced Features
- **ApplicationSets**: Generate apps dynamically from generators (Git directories, clusters).
- **Secrets Management**: Integrates with Vault, SealedSecrets, SOPS.
- **Metrics**: Prometheus metrics for monitoring.
- **Notifications**: Webhook alerts for sync status changes.
- **RBAC**: Fine-grained permissions for teams/applications.

# Common Patterns
- **App-of-Apps**: Parent app manages other apps (hierarchical).
- **Blue-Green**: Manage traffic switching between versions.
- **Canary**: Gradually shift traffic to new version.
- **Git Repo per Env**: Separate branches/folders for dev/stage/prod.
- **Monorepo**: Single repo with multiple app manifests.

# Best Practices
- **Immutable Tags**: Use commit SHAs instead of mutable tags (latest).
- **Small Frequent Commits**: Easier rollback and audit trail.
- **Git Signing**: Sign commits for auditability.
- **Read-Only Prod**: Require PRs for production changes.
- **Secrets in Git**: Encrypt secrets using SOPS/Mozilla Vault.
- **Sync Windows**: Restrict when syncs can occur in production.

# Troubleshooting
- **Sync Status**: Check conditions in Application CR.
- **Resource Health**: Verify custom health checks for CRDs.
- **Sync Logs**: View detailed reconciliation logs.
- **Diff Debugging**: Compare live vs desired state.
- **Finalizers**: Handle stuck deletions properly.

# Alternatives
- **FluxCD**: CNCF GitOps operator (push-based notifications).
- **Jenkins X**: CI/CD with GitOps principles.
- **Tekton**: Kubernetes-native pipeline with GitOps potential.
