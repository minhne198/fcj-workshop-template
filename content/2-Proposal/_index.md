---
title: "Proposal"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# High-Availability Hotel Booking System on AWS
## High-Traffic Online Hotel Booking System on AWS

### 1. Executive Summary

The High-Availability Online Hotel Booking System on AWS is an e-commerce web application for the travel and accommodation domain. The core goal of this project is to build a modern infrastructure solution that keeps the system highly available, scales resources automatically based on real traffic, and optimizes response performance through caching.

By combining a high-performance **ASP.NET Core 8 (.NET 8 LTS)** backend with the cloud ecosystem of **Amazon Web Services (AWS)**, the project demonstrates how to solve high-traffic and fault-tolerance challenges that modern digital businesses often face.

### 2. Problem Statement

*Current problems:* Traditional websites deployed on physical servers or a single-server model often face serious limitations in real production environments:

* **Peak-season bottlenecks:** During holidays or travel seasons, traffic can spike sharply and overload server resources, causing slow responses, interruptions, or website downtime. Provisioning a large server from the beginning also wastes cost during low-traffic periods.
* **Single Point of Failure:** The whole application depends on one server. If the server hardware fails or loses network connectivity, the website becomes unavailable, causing revenue loss and poor user experience.
* **Database overload:** When thousands of users repeatedly search for the same rooms, the relational database must handle a heavy volume of direct queries, which can slow responses or crash the database.
* **Overbooking risk:** Without strong concurrency control, two customers may book and pay for the same room at the same time.

*Proposed solution:* The application platform is migrated to a Cloud-Native model on AWS to address these issues:

* **Load balancing and failover:** Use **Application Load Balancer (ALB)** together with **Auto Scaling Group (ASG)** to distribute traffic across **EC2** instances in multiple Availability Zones. If one zone has an infrastructure issue, the system can route traffic to the remaining zone smoothly within about 30 seconds.
* **Demand-based auto scaling:** ASG monitors CPU Utilization, increases the number of servers when traffic is high, and reduces instances when load decreases to optimize resource cost.
* **Performance optimization with Redis Cache:** Integrate **Amazon ElastiCache Redis** to cache popular search query results. This reduces response time from about 150 ms to under 5 ms and removes repeated direct query pressure from Amazon RDS MySQL.
* **Strict overbooking prevention:** Apply **Row-Level Locking (SELECT FOR UPDATE)** with high-integrity EF Core database transactions using the Serializable isolation level to lock room data during payment processing.

*Benefits and ROI:*

* **Research and practical value:** The project acts as a complete High Availability blueprint for enterprise web systems. Cloud infrastructure is defined with **AWS CDK (TypeScript)**, making it easier to manage, reproduce, and reuse for future work.
* **Operational cost optimization:** By combining auto scaling with **AWS Free Tier** benefits for EC2, RDS, and Redis, the estimated infrastructure cost for the project is very low, **under 10 USD (about 250,000 VND)** for the full graduation project lifecycle.
* **Reduced operations effort:** Monitoring and alerting are automated through CloudWatch and Amazon SNS email alerts, reducing the need for manual 24/7 system supervision.

### 3. Solution Architecture

The system uses a secure multi-tier architecture deployed inside an isolated **Amazon VPC**, clearly separating public subnets and private subnets to improve data security.

*AWS services used:*

* **Amazon VPC:** Creates an isolated network environment with 2 public subnets and 4 private subnets across 2 Availability Zones.
* **Application Load Balancer (ALB):** Receives HTTP/HTTPS traffic and distributes it to EC2 instances in private subnets.
* **Amazon EC2 & Auto Scaling Group:** Uses `t3.micro` instances running Amazon Linux 2023 as API servers, with auto scaling from 1 to a maximum of 4 servers.
* **Amazon RDS MySQL:** Stores core business data such as hotels, rooms, and invoices, with Multi-AZ support for data replication and failover.
* **Amazon ElastiCache (Redis):** Provides shared distributed caching for all EC2 instances in the ASG to accelerate queries.
* **Amazon S3 & CloudFront:** S3 stores frontend static assets and system images; CloudFront acts as a global CDN and securely accesses S3 through Origin Access Control (OAC).
* **Monitoring and security:** Integrates AWS WAF, KMS, Secrets Manager, CloudWatch, and SNS for request filtering, encryption, secure configuration, monitoring, and automated incident alerts.

### 4. Technical Implementation

*Implementation phases:*

1. **Phase 1: Network and security setup (Week 1):** Plan the VPC, divide subnets, configure route tables, NAT Gateways, and strict Security Groups.
2. **Phase 2: Cloud data layer initialization (Week 2):** Create RDS MySQL and ElastiCache Redis on AWS, connect the database, initialize schema, and seed sample data.
3. **Phase 3: Backend API development and logic optimization (Week 3):** Build business controllers with ASP.NET Core 8, integrate Redis caching, and implement transaction logic to prevent duplicate bookings.
4. **Phase 4: Frontend development (Week 4):** Build a responsive web UI using HTML5, Bootstrap, and Vanilla JavaScript, then deploy it to Amazon S3 and CloudFront.
5. **Phase 5: ASG configuration and load testing (Weeks 5-6):** Create the Launch Template, build the ALB, configure Auto Scaling rules, and use **Locust** to simulate 300 concurrent users for scaling and failover testing.
6. **Phase 6: Infrastructure as Code and automated monitoring (Weeks 7-8):** Convert manual infrastructure configuration into **AWS CDK** source code, build CloudWatch dashboards, and enable SNS alerts.

*Technical requirements:*

* **Environment:** Visual Studio 2022 or VS Code, .NET 8 SDK, Node.js for AWS CDK, and AWS CLI.
* **Professional skills:** Entity Framework Core, LINQ, Async/Await, thread-safe programming, database transactions, cloud routing, and secure IAM Roles/Policies.

### 5. Timeline and Milestones

The project timeline is planned for **9 weeks**:

* **Week 1:** Project kickoff, VPC network setup, and local environment configuration.
* **Week 2:** Deploy and configure RDS database and Redis cache on AWS.
* **Week 3:** Complete the backend API source code for Auth, Search, Booking, and Admin, with Swagger integration.
* **Week 4:** Complete frontend UI components and deploy them to S3/CloudFront.
* **Week 5:** Deploy the API to EC2 through Launch Template and configure ALB Target Group health checks.
* **Week 6:** Run load testing with Locust and tune Target CPU Tracking settings.
* **Weeks 7-8:** Package the AWS CDK source code, configure CloudWatch dashboards, and automate alerts.
* **Week 9:** Rehearse the application demo, prepare presentation slides, and defend the project.

### 6. Budget Estimate

The system follows a strict cost optimization strategy, with most resources staying within **AWS Free Tier** where possible.

*Estimated infrastructure cost table:*

* **Amazon EC2 (`t3.micro`):** 0.00 USD, within 750 free hours per month.
* **Amazon RDS MySQL (`db.t3.micro`):** 0.00 USD, within 750 free hours per month.
* **Amazon ElastiCache Redis (`cache.t3.micro`):** 0.00 USD, using the Free Tier benefit.
* **Application Load Balancer:** About 0.025 USD/hour. It is enabled only during load testing and demos, estimated at about 1.50 USD.
* **NAT Gateway:** About 0.059 USD/hour. A start/stop script is used to optimize usage, estimated at about 3.00 USD.
* **Amazon S3 & CloudFront:** About 0.20 USD for static file storage and low-volume bandwidth.

**Expected total cost:** **< 10 USD (about 250,000 VND)** for the full graduation project by shutting down paid resources or reducing Desired Capacity to 0 when they are not needed overnight.

### 7. Risk Assessment

*Risk matrix and mitigation strategy:*

* **Credential leakage risk:** Access keys may be exposed when code is pushed to a public GitHub repository. *Mitigation:* Never hard-code passwords or secret keys in source code. Use `.env` files listed in `.gitignore` and rely on **IAM Role** attached directly to the EC2 Instance Profile.
* **Budget overrun risk:** Paid resources may be left running after work sessions. *Mitigation:* Configure **AWS Budgets** with a **10 USD** alert threshold and send immediate email alerts when cost exceeds the expected limit.
* **API database connection failure during demo:** Cloud resources may have cold-start delay. *Mitigation:* Prepare a `warmup.sh` health-check script to start and verify RDS, EC2, and Redis 30 minutes before the official demo.

### 8. Expected Outcomes

* **Functional outcome:** A complete travel e-commerce application covering registration/login, smart hotel search filters, real-time booking, and an admin dashboard.
* **Cloud technical outcomes:**
  * Demonstrate **High Availability (HA):** Terminate one active server in the AWS Console during the demo while the system continues to operate without response failures.
  * Demonstrate **Auto Scaling:** CloudWatch charts show CPU reaching the high-load threshold and automatically increasing the number of servers to handle Locust traffic.
  * Demonstrate **Caching optimization:** API response time is reduced from about 150 ms to about 4 ms through distributed cache.
