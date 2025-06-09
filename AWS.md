# AWS Interview Preparation Guide

## Cloud Fundamentals
### What is Cloud Computing?
- On-demand delivery of IT resources over the internet
- Pay-as-you-go pricing instead of upfront costs

### AWS Global Infrastructure
- **Regions**: Physical locations with multiple data centers
- **Availability Zones**: Isolated data centers within a region
- **Edge Locations**: CDN endpoints for CloudFront

## AWS Architecture Principles
### Design Principles
- Implement loose coupling between components
- Design for failure (nothing fails 100% of the time)
- Scale horizontally, not vertically
- Implement elasticity (auto-scaling)
- Think parallel for faster processing

### Well-Architected Framework
- Operational Excellence
- Security
- Reliability
- Performance Efficiency
- Cost Optimization

## Core AWS Services

### EC2 (Elastic Compute Cloud)
- Virtual servers in the cloud
- Types: On-Demand, Spot, Reserved, Dedicated
- AMI = Preconfigured server templates
- Security Groups = Virtual firewalls

### S3 (Simple Storage Service)
- Object storage for files
- Storage Classes: Standard, IA, Glacier
- Features: Versioning, Lifecycle Policies
- 99.999999999% durability

### VPC (Virtual Private Cloud)
- Your private network in AWS
- Contains subnets (public/private)
- Route tables control traffic
- NACLs = Stateless firewall rules

### IAM (Identity Access Management)
- Controls who can do what
- Users + Groups + Roles + Policies
- Principle of least privilege
- MFA for extra security

## Database Services

### RDS
- Managed relational databases
- Supports MySQL, PostgreSQL, etc.
- Automated backups + patching

### DynamoDB
- Fully managed NoSQL database
- Single-digit millisecond latency
- Auto-scaling capability

## Pricing Models

### EC2 Pricing Options
- On-Demand: Pay by the hour
- Reserved: 1-3 year commitment (cheaper)
- Spot: Bid for unused capacity (cheapest)
- Savings Plans: Commit to usage amount

### S3 Pricing Factors
- Storage amount
- Number of requests
- Data transfer out
- Storage class used

### Cost Optimization Tips
- Right-size instances
- Use auto-scaling
- Delete unused resources
- Monitor with Cost Explorer
- Set billing alarms

## Security Essentials

### Shared Responsibility Model
- AWS secures the cloud (infrastructure)
- You secure what's in the cloud (your data)

### Key Security Services
- IAM: Access control
- KMS: Encryption keys
- CloudTrail: Logs API calls
- GuardDuty: Threat detection

## Monitoring & Management

### Core Services
- CloudWatch: Monitoring
- CloudTrail: Auditing
- Config: Resource tracking
- Systems Manager: Operational tools

## Deployment Services

### CI/CD Tools
- CodeCommit: Git repositories
- CodeBuild: Build service
- CodeDeploy: Deployment automation
- CodePipeline: Workflow orchestration

## Serverless Options

### Key Services
- Lambda: Run code without servers
- API Gateway: Create HTTP APIs
- Step Functions: Workflow coordination

## Migration Strategies

### Common Approaches
- Rehost (lift-and-shift)
- Replatform (lift-tinker-and-shift)
- Refactor (re-architect)

## Disaster Recovery

### Recovery Options
- Backup & Restore
- Pilot Light
- Warm Standby
- Multi-site active-active

## Interview Tips
- Know the AWS Well-Architected Framework
- Understand the Shared Responsibility Model
- Be familiar with core services (EC2, S3, VPC, IAM)
- Practice explaining concepts simply
- Have real-world examples ready
