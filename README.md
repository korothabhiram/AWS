# ☁️ AWS

## 📘 What is AWS?

Amazon Web Services (AWS) is a cloud computing platform provided by Amazon that lets individuals and businesses access IT resources—servers, storage, databases, networking, and more—over the internet, on demand and pay-as-you-go, instead of buying and running physical hardware.

---

## 🙋‍♂️ Who Should Use AWS?

- **DevOps Engineers**: Provision and automate infrastructure at scale.
- **Developers**: Deploy applications without managing physical servers.
- **Data Engineers**: Store, process, and query large datasets.
- **Architects**: Design highly available, fault-tolerant systems.
- **Tech Learners**: Get hands-on with the services most companies actually run on.

---

## 🎯 Why Use AWS?

- 🌍 Global infrastructure—regions and availability zones everywhere
- 💸 Pay-as-you-go, scale up or down on demand
- 🧩 Broadest service catalog of any cloud provider
- 🔐 Deep security, compliance, and IAM controls
- 🤖 Managed services reduce operational overhead

---

## 🏗️ IaaS vs PaaS vs SaaS on AWS

AWS spans all three service models—worth knowing which bucket a service falls into, since it tells you how much you're responsible for managing:

| Model | You manage | AWS manages | Examples |
|-------|-----------|-------------|----------|
| **IaaS** (Infrastructure as a Service) | OS, runtime, scaling, patching | Physical hardware, virtualization, networking | EC2, EBS, VPC |
| **PaaS** (Platform as a Service) | Code & config | OS, runtime, scaling, patching | Lambda, RDS, Elastic Beanstalk, ECS/EKS (control plane) |
| **SaaS** (Software as a Service) | Just your data/usage | Everything | Chime, WorkMail, QuickSight |

Most day-to-day AWS work lives in IaaS and PaaS—the categories below are organized by **function** (what the service does) rather than strictly by this model, since it's the more useful way to actually navigate and look things up.

---

## 🏛️ Pillars of the AWS Well-Architected Framework

A set of six lenses AWS recommends evaluating every workload against, useful both for designing new systems and reviewing existing ones.

| Pillar | In short |
|--------|----------|
| 🛠️ **Operational Excellence** | Run and monitor systems to deliver business value, and continually improve processes—automate changes, respond to events, and learn from failures instead of just reacting to them. |
| 🔐 **Security** | Protect data, systems, and assets through identity management, detective controls, infrastructure protection, and data protection—applied at every layer, not bolted on at the end. |
| 🛡️ **Reliability** | Ensure a workload performs its intended function correctly and consistently, including the ability to recover from infrastructure or service failures automatically. |
| ⚡ **Performance Efficiency** | Use computing resources efficiently to meet requirements, and keep up as technology and demand evolve—right-sizing and choosing the right service, not just the familiar one. |
| 💰 **Cost Optimization** | Avoid unnecessary costs by understanding spending over time, choosing the right pricing model, and matching supply to actual demand. |
| 🌱 **Sustainability** | Minimize the environmental impact of running cloud workloads—energy efficiency, resource utilization, and reducing waste at scale. |

---
# ☁️ AWS Services Reference Guide

A categorized guide to the AWS services you'll reach for most—what each one is, and when to reach for it over the others in the same category.

---

## 🖥️ Compute

| Service | What it is | Reach for it when... |
|---------|-----------|----------------------|
| **EC2** | Resizable virtual servers (instances) you fully control—the classic IaaS building block. | You need full control over the OS/runtime, run long-lived or stateful workloads, or need instance types/configs no managed service offers. |
| **Lambda** | Run code without provisioning servers—fully serverless; you pay only for execution time. | Your workload is event-driven and short-lived (seconds to minutes), and you don't want to manage any servers at all. |
| **ECS** | AWS-native container orchestrator, tightly integrated with the rest of AWS. | You're running Docker containers and want simpler setup/ops than Kubernetes, without needing K8s-specific tooling or portability. |
| **EKS** | Managed Kubernetes—AWS runs the control plane, you run workloads via standard `kubectl`. | You specifically need Kubernetes (existing K8s expertise/tooling, multi-cloud portability, or K8s-native ecosystem). |
| **Fargate** | Serverless compute layer for ECS or EKS—no EC2 instances to provision or patch. | You want containers (via ECS or EKS) but don't want to manage the underlying instances at all. |

---

## 💾 Storage

| Service | What it is | Reach for it when... |
|---------|-----------|----------------------|
| **S3** | Object storage for files of any size, accessed over HTTP/API—virtually unlimited, highly durable. | You're storing static assets, backups, logs, or data-lake content that doesn't need to look like a filesystem to a single instance. |
| **EBS** | Persistent block storage attached to a single EC2 instance—like a virtual hard drive. | You need low-latency disk for an instance's OS or data volume, and only one instance needs to access it at a time. |
| **EFS** | Managed NFS file storage that many EC2 instances or containers can mount concurrently. | Multiple compute resources need shared, simultaneous read/write access to the same files. |

---

## 🗄️ Database

| Service | What it is | Reach for it when... |
|---------|-----------|----------------------|
| **RDS** | Managed relational databases (Postgres, MySQL, MariaDB, SQL Server, Oracle)—AWS handles patching, backups, failover. | You need SQL, joins, and transactions, and want a standard, portable database engine without managing the ops yourself. |
| **Aurora** | AWS's own MySQL/Postgres-compatible engine, built for the cloud with auto-scaling storage. | You want RDS's relational model but need higher performance/availability and are fine with an AWS-proprietary engine. |
| **DynamoDB** | Fully managed, serverless NoSQL key-value/document database with single-digit millisecond latency at any scale. | You have high-throughput, known access patterns, and don't need complex joins or ad-hoc relational queries. |
| **ElastiCache** | Managed in-memory caching (Redis or Memcached). | You need a cache layer in front of a database to cut latency/read load—not a system of record on its own. |

---

## 🌐 Networking

| Service | What it is | Reach for it when... |
|---------|-----------|----------------------|
| **VPC** | Your own isolated network within AWS—subnets, route tables, gateways. | Always—every EC2/RDS/EKS resource lives inside a VPC; the decisions are around subnet layout, peering, and routing. |
| **Route 53** | Managed DNS—domain registration, DNS routing, health checks. | You need to resolve domain names to resources, or want DNS-level routing policies (latency-based, geo, failover). |
| **CloudFront** | Global CDN that caches content at edge locations close to users. | You want to cut latency and origin load for content served to geographically spread users (often in front of S3 or a load balancer). |
| **ALB** | Application Load Balancer—layer 7 (HTTP/HTTPS), content-based routing. | You're routing web traffic and need path/host-based rules, WebSockets, or per-request routing decisions. |
| **NLB** | Network Load Balancer—layer 4 (TCP/UDP), ultra-low latency, static IPs. | You need extreme performance/throughput or non-HTTP protocols, and don't need application-layer routing logic. |

---

## 🔐 Security & Identity

| Service | What it is | Reach for it when... |
|---------|-----------|----------------------|
| **IAM** | Controls who (users, roles, services) can do what across your account—the foundation everything else depends on. | Always—every other service's access is governed through IAM users, roles, and policies. |
| **KMS** | Managed creation and control of encryption keys used to protect data across AWS services. | You need to encrypt data at rest/in transit and control who can use the key to decrypt it, with audit trails. |
| **Secrets Manager** | Securely stores and can automatically rotate credentials, API keys, and other secrets. | You're storing something sensitive (DB passwords, API keys) that changes or needs rotation—costs more than Parameter Store but handles rotation for you. |
| **SSM Parameter Store** | Stores config values and secrets, simpler and cheaper than Secrets Manager. | You need config values or secrets that don't need automatic rotation—non-sensitive settings, feature flags, or static credentials on a budget. |
| **Cognito** | Managed user authentication, sign-up/sign-in, and access control for apps. | You need end-user identity (not AWS account identity) for a customer-facing app—login, MFA, social sign-in. |

---

## 📨 Messaging & Integration

| Service | What it is | Reach for it when... |
|---------|-----------|----------------------|
| **SQS** | Fully managed message queue for decoupling application components. | You need point-to-point delivery—one producer, one (or a pool of) consumer(s), with guaranteed processing and retries. |
| **SNS** | Managed pub/sub messaging that fans a single message out to many subscribers. | You need to push one event to multiple, independent subscribers at once (email, SMS, Lambda, SQS) simultaneously. |
| **EventBridge** | Serverless event bus that routes events between AWS services, SaaS apps, and your own apps based on rules. | You have many event sources/consumers and need content-based filtering and routing—the most flexible option for event-driven architectures. |

---

## 📊 Monitoring & Ops

| Service | What it is | Reach for it when... |
|---------|-----------|----------------------|
| **CloudWatch** | Metrics, logs, dashboards, and alarms for everything running in AWS. | You want to know "is it healthy right now" and "what changed"—operational and performance monitoring. |
| **CloudTrail** | Records every API call made in your account—who did what, when. | You need an audit trail for security investigations or compliance—"who did this and when," not performance data. |

---

## 🏗️ IaC & DevOps

| Service | What it is | Reach for it when... |
|---------|-----------|----------------------|
| **CloudFormation** | AWS-native infrastructure as code—declare resources in JSON/YAML templates, AWS provisions and tracks them as a "stack." | You want infrastructure as code that's deeply AWS-native, with no external tooling or state file to manage yourself. If you're already using Terraform (see the [Terraform](../Terraform) repo), you likely don't need this as well—pick one. |
| **CodePipeline** | Managed CI/CD orchestration that chains together source, build, test, and deploy stages. | You want your build/deploy pipeline to live natively in AWS alongside the infrastructure it deploys to, often paired with CodeBuild/CodeDeploy. |

---

> ✅ Keep this README as a reference for your AWS journey. Contributions welcome!
> ⭐ Star this repo if you found it helpful!
