# CI/CD Fundamentals
- **CI (Continuous Integration)**: Automatically build and test code changes when committed to shared repository.
- **CD (Continuous Delivery)**: Automatically deploy all code changes to testing/staging environment after build.
- **CD (Continuous Deployment)**: Automatically deploy to production after passing tests (no manual intervention).
- **Pipeline**: Automated sequence of steps to build, test and deploy software.
- **Build**: Process of converting source code into executable artifacts.
- **Artifact**: Output of build process (JAR, WAR, Docker image etc).
- **Release**: Versioned package of artifacts ready for deployment.

# Key Components
- **Version Control**: Git (GitHub, GitLab, Bitbucket) stores source code.
- **Build Tools**: Maven, Gradle, NPM, Make compile source code.
- **CI Server**: Jenkins, CircleCI, GitHub Actions orchestrate pipelines.
- **Test Frameworks**: JUnit, Selenium, Jest run automated tests.
- **Containerization**: Docker packages apps with dependencies.
- **Orchestration**: Kubernetes manages container deployment.
- **Configuration Management**: Ansible, Chef, Puppet manage infra.
- **Monitoring**: Prometheus, ELK track deployments.

# CI/CD Pipeline Stages
1. **Code Commit**: Developer pushes changes to version control.
2. **Build**: Compile code and create executable artifacts.
3. **Unit Testing**: Run small, fast tests on individual components.
4. **Integration Testing**: Verify components work together.
5. **Code Quality**: Static analysis (SonarQube, ESLint).
6. **Security Scan**: Check for vulnerabilities (OWASP, Snyk).
7. **Artifact Storage**: Save outputs (Nexus, Artifactory).
8. **Deployment**: Release to staging/production environments.
9. **E2E Testing**: Validate entire system (Selenium, Cypress).
10. **Monitoring**: Track performance in production.

# Popular Tools
- **Jenkins**: Open-source automation server with plugins.
- **GitHub Actions**: Native CI/CD within GitHub repositories.
- **GitLab CI/CD**: Built-in pipelines in GitLab.
- **CircleCI**: Cloud-based CI/CD platform.
- **Travis CI**: Hosted CI service for GitHub projects.
- **Azure DevOps**: Microsoft's CI/CD suite.
- **AWS CodePipeline**: Managed CI/CD service on AWS.
- **Argo CD**: Declarative GitOps tool for Kubernetes.
- **Tekton**: Kubernetes-native pipeline framework.
- **Spinnaker**: Multi-cloud CD platform.

# Key Concepts
- **Infrastructure as Code (IaC)**: Manage infra via config files (Terraform, CloudFormation).
- **Blue-Green Deployment**: Run two identical environments, switch traffic.
- **Canary Release**: Gradually roll out changes to subset of users.
- **Rollback**: Revert to previous version if issues detected.
- **Immutable Infrastructure**: Replace servers rather than modify them.
- **GitOps**: Use Git as single source of truth for infrastructure and apps.
- **Shift Left**: Move testing earlier in development cycle.
- **Pipeline as Code**: Define pipelines in version-controlled files.

# Best Practices
- **Fast Feedback**: Keep pipeline execution under 10 minutes.
- **Reproducible Builds**: Same inputs always produce same outputs.
- **Ephemeral Environments**: Create/destroy test envs on demand.
- **Secret Management**: Store credentials securely (Vault, AWS Secrets Manager).
- **Pipeline Triggers**: Run on commit, schedule, or manual approval.
- **Artifact Versioning**: Unique version for each build (semantic versioning).
- **Infrastructure Parity**: Keep dev/test/prod environments similar.
- **Monitoring**: Track pipeline metrics (success rate, duration).

# Security Considerations
- **Least Privilege**: Limit pipeline permissions.
- **SBOM**: Software Bill of Materials tracks dependencies.
- **Signing**: Verify artifact integrity with digital signatures.
- **Static Application Security Testing (SAST)**: Analyze source code for vulnerabilities.
- **Dynamic Application Security Testing (DAST)**: Test running applications.
- **Dependency Scanning**: Check for vulnerable libraries.
- **Secrets Scanning**: Detect accidentally committed credentials.

# Cloud-Native CI/CD
- **Serverless CI/CD**: AWS CodeBuild, Google Cloud Build.
- **Kubernetes-Native**: Argo Workflows, Tekton Pipelines.
- **Service Mesh**: Istio for canary deployments.
- **Feature Flags**: Toggle features without redeploying.
- **Chaos Engineering**: Test resilience in production (Chaos Monkey).
