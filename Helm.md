# Helm Fundamentals
- **Helm**: Kubernetes package manager for deploying applications ("apt/yum for K8s").
- **Chart**: Helm package containing all K8s resource definitions.
- **Release**: Instance of a chart running in a cluster.
- **Repository**: Collection of published charts (public/private).
- **helm CLI**: Command-line tool for managing charts and releases.

# Core Components
- **Templates**: YAML files with Go templating for dynamic K8s manifests.
- **values.yaml**: Default configuration for charts (customizable during install).
- **Chart.yaml**: Metadata about the chart (name, version, dependencies).
- **_helpers.tpl**: Reusable template snippets.
- **hooks**: Special resources for release lifecycle events.

# Helm Architecture
- **Tiller**: (Deprecated in v3) Server-side component that managed releases.
- **Helm 3**: Client-only architecture using K8s secrets for storage.
- **Release Storage**: Secrets store release metadata (helm ls data).
- **Chart Museum**: Popular chart repository server.

# Basic Commands
- `helm install`: Deploy a chart as new release.
- `helm upgrade`: Update existing release with new config/chart.
- `helm rollback`: Revert to previous release version.
- `helm uninstall`: Remove a release from cluster.
- `helm list`: Show deployed releases.
- `helm status`: Display release status/details.
- `helm pull`: Download chart without installing.
- `helm template`: Render templates locally (dry-run).

# Chart Development
- `helm create`: Scaffold new chart directory structure.
- `helm lint`: Validate chart for possible issues.
- `helm package`: Bundle chart into versioned .tgz file.
- `helm dependency`: Manage sub-chart dependencies.
- `helm test`: Execute test pods defined in chart.

# Templating Features
- **Go Templates**: Control structures (if/else, range, with).
- **Built-in Objects**: Access to Release, Chart, Files, Capabilities.
- **Functions**: 60+ built-in Sprig template functions.
- **Pipelines**: Chain template commands ({{ .Values.foo | quote }}).
- **Named Templates**: Define reusable components in _helpers.tpl.

# Advanced Features
- **Subcharts**: Modular charts that include other charts.
- **Library Charts**: Shared utility charts (no resources).
- **Hooks**: Jobs that run at release lifecycle points (pre-install, post-upgrade).
- **Secrets Management**: Integrate with Vault, SOPS, etc.
- **Schema Validation**: values.schema.json for input validation.

# Best Practices
- **Semantic Versioning**: Follow Chart.yaml version conventions.
- **Immutable Releases**: Never modify deployed resources manually.
- **Value Overrides**: Use --set for ad-hoc changes, -f for files.
- **RBAC**: Include minimal required permissions in templates.
- **Documentation**: Maintain README.md and NOTES.txt.

# Security
- **Content Trust**: Verify chart signatures with helm verify.
- **RBAC**: Configure service account permissions carefully.
- **Tillerless**: Helm 3 removes cluster-side component.
- **Secrets**: Avoid hardcoding sensitive values in charts.

# Ecosystem
- **Artifact Hub**: Discover community charts (formerly Helm Hub).
- **Helmfile**: Declarative spec for managing multiple releases.
- **Chart Releaser**: GitHub Action for automating chart releases.
- **Helm Secrets**: Plugin for encrypting sensitive data.

# Common Use Cases
- **Standardized Deployments**: Consistent app packaging across teams.
- **Environment Differences**: Manage dev/stage/prod variations.
- **CI/CD Integration**: Automated release pipelines.
- **Shared Services**: Deploy common infrastructure (DBs, monitoring).

# Troubleshooting
- `helm get manifest`: View deployed templates.
- `helm get values`: See configured values for release.
- `--dry-run --debug`: Test template rendering.
- `helm history`: View release revisions.
- `helm plugin`: Manage CLI plugins.
