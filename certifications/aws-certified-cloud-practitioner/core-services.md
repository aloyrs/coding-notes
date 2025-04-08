# AWS CCP Certification Notes

# Key Benefits of AWS Cloud

- Trade upfront expenses for variable expenses.
- Benefit from massive economies of scale.
- Stop guessing capacity.
- Increase speed and agility.
- Stop spending money on maintaining data centers.
- Go global in minutes.

# Types of Cloud Services

- IaaS (Infrastructure as a Service): AWS EC2
- PaaS (Platform as a Service): Heroku, Vercel
- SaaS (Software as a Service): Zoom

---

# EC2 Instance Types

- General Purpose Instances: Balanced compute, memory, and networking resources.
- Compute Optimized Instances: High-performance processors for compute-intensive tasks.
- Memory Optimized Instances: Large memory sizes for memory-intensive applications.
- Accelerated Computing Instances: Use GPUs or specialized hardware for specific workloads.
- Storage Optimized Instances: Designed for workloads requiring high, sequential read and write access to large datasets.

---

# EC2 Pricing

- On-Demand Instances: Pay for compute capacity by the second or hour, with no long-term commitment.
- Reserved Instances (RI):
  - Standard Reserved Instances: Commit to a specific instance type and region for 1 or 3 years at a discounted rate.
  - Convertible Reserved Instances: Offers flexibility to change instance types or availability zones.
  - Scheduled Reserved Instances: Reserve capacity for specific time periods to receive a discount.
- EC2 Instance Savings Plans: Commit to a consistent hourly spend on an instance family for 1 or 3 years.
- Spot Instances: Buy unused EC2 capacity at a steep discount, but instances can be interrupted.
- Dedicated Hosts: Rent a physical server for regulatory compliance or licensing needs.

---

# EC2 Auto Scaling

- Horizontal Scaling: Adding more instances to handle increased load.
- Dynamic Scaling: Responds to changing demand.
- Predictive Scaling: Automatically schedules the right number of EC2 instances based on predicted demand.

---

# Elastic Load Balancing (ELB)

- Distributes incoming traffic between multiple EC2 instances (e.g., between user and frontend, or frontend and backend).

---

# AWS Messaging Services

- Amazon SNS (Simple Notification Service): A publish/subscribe service.
- Amazon SQS (Simple Queue Service): A message queuing service that enables sending messages without requiring other services to be available.

---

# Serverless Computing

- AWS Lambda: Automatically runs your code in response to events, scaling dynamically without managing servers.
- Amazon ECS: Run and scale Docker containers using API calls.
- Amazon EKS: Run Kubernetes on AWS to deploy and manage containerized applications.
- AWS Fargate: Serverless compute platform for containers, eliminating the need to manage EC2 instances.

---

# AWS Network and Security

- Availability Zone: Single data center or a group of data centers within a Region.
- AWS VPC (Virtual Private Cloud): Logically isolated network within AWS to launch and manage resources securely.
- Security Group: Virtual firewall for EC2 instances (stateful).
- Network ACL (Access Control List): Stateless firewall at the subnet level.
- VPC Peering: Connects two AWS VPCs.
- AWS Direct Connect: Dedicated private connection between on-premises data centers and VPC.
- Virtual Private Gateway: Creates a VPN connection between the VPC and an on-site VPN.
- Egress-Only Internet Gateway: Allows outbound internet access for IPv6 traffic while blocking inbound access.

---

# AWS Storage Services

- Amazon EBS (Elastic Block Store): Persistent block storage for EC2 instances.
- Amazon S3 (Simple Storage Service): Object storage for data, with different storage classes:
  - S3 Standard
  - S3 Standard-IA
  - S3 One Zone-IA
  - S3 Intelligent-Tiering
  - S3 Glacier
  - S3 Glacier Deep Archive
- Amazon EFS (Elastic File System): Shared file storage across multiple EC2 instances.
- Amazon Redshift: Data warehousing service for big data analytics.
- AWS Snow Family: Data transfer devices for edge computing and large-scale data migrations.
  - Snowcone
  - Snowball
  - Snowmobile

---

# Databases

- Amazon RDS (Relational Database Service): Managed relational databases (Aurora, MySQL, PostgreSQL, MariaDB, Oracle, MS SQL).
- Amazon DynamoDB: Key-value and document database.
- Amazon DocumentDB: Document database.
- Amazon Neptune: Graph database.
- Amazon ElastiCache: In-memory data store for caching solutions.
- AWS DMS (Database Migration Service): Migrate databases with schema conversion.

---

# AWS IAM (Identity and Access Management)

- IAM User: Identity with access keys for programmatic access.
- IAM Role: Identity assumed by trusted entities, with temporary credentials.
- IAM Group: A collection of IAM users for policy management.
- IAM Policy: JSON document defining permissions.
- MFA (Multi-Factor Authentication): Enhances security for root and IAM users.

---

# AWS Cost Management

- AWS Pricing Calculator: Estimate the cost of AWS services.
- AWS Budgets: Set budgets to track and manage usage and costs.
- AWS Cost Explorer: Visualize and analyze AWS costs and usage.
- Consolidated Billing: Aggregate bills from multiple accounts within an AWS Organization for volume discounts.
- AWS Marketplace: Digital catalog of third-party software solutions.

---

# AWS Support

- Basic Support: 24/7 access to customer service and documentation.
- Developer Support: Email support and AWS Trusted Advisor checks.
- Business Support: 24/7 access to AWS support engineers.
- Enterprise Support: Includes a Technical Account Manager (TAM) and additional support services.

---

# AWS Security and Compliance

- AWS Shield: Managed DDoS protection service.
- AWS WAF: Web application firewall for monitoring and controlling web traffic.
- AWS KMS (Key Management Service): Encryption service using cryptographic keys.
- Amazon GuardDuty: Intelligent threat detection service.
- AWS Security Hub: Aggregates security findings across AWS services and third-party tools.
- AWS Artifact: Access AWS security and compliance reports.

---

# Migration Strategies

- Rehosting: Lift-and-shift migration of applications without changes.
- Replatforming: Making optimizations to cloud environments without changing the core application.
- Refactoring: Redesigning applications using cloud-native features.
- Repurchasing: Moving to SaaS solutions (e.g., CRM systems).
- Retaining: Keeping critical applications in the source environment.
- Retiring: Removing unnecessary applications.

---

# AWS Well-Architected Framework

- Operational Excellence
- Security
- Reliability
- Performance Efficiency
- Cost Optimization
- Sustainability

WAF acronym : CROSSP

---

# AWS Cloud Adoption Framework (AWS CAF)

The AWS Cloud Adoption Framework (AWS CAF) provides guidelines, best practices, and methodologies to help organizations successfully adopt and migrate to AWS. It consists of six perspectives, each addressing different aspects of cloud adoption.

- Business Perspective focuses on aligning cloud adoption with business goals to drive organizational value and achieve business outcomes.
- People Perspective addresses the skills, roles, and responsibilities required for cloud adoption, helping organizations develop and manage a cloud-enabled workforce.
- Governance Perspective ensures proper management, risk control, and compliance in cloud environments, including defining policies and governance frameworks.
- Platform Perspective covers the design and architecture of cloud infrastructure to support applications, focusing on platform and infrastructure optimization for scalability, reliability, and security.
- Security Perspective focuses on securing data, applications, and systems in the cloud, ensuring data privacy, compliance, and protection against cyber threats.
- Operations Perspective optimizes the day-to-day management and monitoring of cloud resources to ensure efficient operations, cost management, and continuous improvement.

CAF acronym: BPOPSG (Business, People, Operations, Platform, Security, Governance)

---
