---
title : "Introduction"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

### AWS_OmniStay Project Introduction

**AWS_OmniStay** is an online hotel booking web application, similar to a small-scale version of Booking.com or Agoda.com. Besides handling core business features such as searching available rooms by location and dates, real-time booking, and transaction history management, the main purpose of this workshop is to deploy the whole system to Amazon Web Services (AWS) to improve performance, security, and scalability.

This workshop guides the step-by-step process of building, configuring, and operating a complete N-tier architecture to demonstrate three core properties of Cloud Computing: High Availability, Auto Scaling, and Caching.

### Project Links

- **Source code:** [AWS_OmniStay GitHub Repository](https://github.com/minhne198/AWS_OmniStay.git)
- **Video demo:** [AWS_OmniStay Demo Video Folder](https://drive.google.com/drive/folders/1UG2iVwxWX2OBc7nDoLslqoLCqRZxY5_L?usp=sharing)
- **Product link:** [AWS_OmniStay Production Website](https://d1gm8xt8e0mar4.cloudfront.net/public/home.html)

### Workshop Objectives

This workshop provides a step-by-step guide to deploying **AWS_OmniStay** on Amazon Web Services (AWS), from environment preparation to infrastructure setup, application deployment, and performance evaluation. After completing the workshop, the implementer will be able to:

- Prepare the development environment and configure an AWS account.
- Deploy the frontend to **Amazon S3** and distribute static content through **Amazon CloudFront**.
- Design and deploy network infrastructure using **Amazon VPC**, public subnets, and private subnets.
- Deploy an **ASP.NET Core (.NET 8)** application on **Amazon EC2** servers.
- Build an **Amazon RDS MySQL Multi-AZ** database layer to improve availability.
- Deploy **Amazon ElastiCache Redis** to improve system response time.
- Configure **Application Load Balancer (ALB)** to distribute traffic to application servers.
- Set up **Auto Scaling Group (ASG)** to automatically scale EC2 instances based on CPU utilization.
- Monitor resources with **Amazon CloudWatch** and control deployment cost with **AWS Budgets**.
- Perform load testing with **Locust** and evaluate the effectiveness of Redis Cache and Auto Scaling through performance metrics.

### Workshop Scope

The workshop focuses on deploying and evaluating AWS core services for the AWS_OmniStay online hotel booking system. The deployment scope includes:

| Component | Purpose |
| :--- | :--- |
| Amazon S3 | Store frontend source code as a static website. |
| Amazon CloudFront | Distribute static content through a global CDN. |
| Origin Access Control (OAC) | Protect the S3 bucket and allow access only from CloudFront. |
| Amazon VPC | Build an isolated network environment for the system. |
| Amazon EC2 | Run the ASP.NET Core Web API backend. |
| Application Load Balancer | Balance traffic across multiple EC2 instances. |
| Auto Scaling Group | Automatically increase or decrease EC2 capacity based on system load. |
| Amazon RDS MySQL | Store the system's business data. |
| Amazon ElastiCache Redis | Cache data to improve response performance. |
| Amazon CloudWatch | Monitor performance and configure alerts. |
| AWS Budgets | Monitor and control AWS service cost. |
| Locust | Simulate concurrent users for load testing. |

1. **High Availability (HA):** The system is distributed across multiple Availability Zones (AZs) to avoid a single point of failure. The website can continue operating even if one data center has a physical issue.
2. **Auto Scaling:** Compute infrastructure automatically scales the number of instances based on real user demand, scaling out during high load and scaling in during low load to optimize cost.
3. **Data Caching:** Response speed is optimized through an in-memory cache layer, reducing direct pressure on the relational database for repeated requests.

---

### Expected System Objectives

In addition to deploying AWS services successfully, the workshop evaluates the architecture through measurable objectives:

- Keep the system available when one Availability Zone has an issue by deploying redundant components.
- Automatically increase EC2 instances when **CPU Utilization exceeds 70%** and reduce capacity when load decreases to optimize operating cost.
- Reduce response time for popular queries from about **150 ms (Cache MISS)** to about **4-5 ms (Cache HIT)** using Amazon ElastiCache Redis.
- Distribute static content through Amazon CloudFront to reduce access latency and speed up page loading for users.
- Monitor and control AWS cost using AWS Budgets with a **10 USD** alert threshold throughout the workshop.

### Overall Architecture Diagram

The system follows AWS Well-Architected best practices by clearly separating the public layer that receives traffic from the private layer used for application and data resources.

![AWS OmniStay Infrastructure Architecture](/images/aws-omnistay-architecture.png)

### Architecture Request Flow

The system request flow is described below:

```text
                User
                  |
                  v
          Amazon CloudFront
                  |
        (Static Content Request)
                  |
                  v
         Amazon S3 Private Bucket
                  |
                  |
        (API Request: /api/*)
                  v
     Application Load Balancer (ALB)
                  |
                  v
      Auto Scaling Group (EC2)
                  |
        ASP.NET Core Web API
          |                 |
          v                 v
 Amazon ElastiCache     Amazon RDS
       Redis             MySQL Multi-AZ
```

In this architecture, static files such as HTML, CSS, and JavaScript are stored in Amazon S3 and can only be accessed through Amazon CloudFront using Origin Access Control (OAC). For API requests, Application Load Balancer distributes traffic to EC2 instances in the Auto Scaling Group. The backend checks Redis first to reduce response time; if data is not in cache, the system queries Amazon RDS MySQL and updates Redis for later requests.

#### Request Flow Explanation

* **Static content distribution layer:** Users access the website through Amazon Route 53 and Amazon CloudFront. HTML, CSS, and JavaScript assets are stored securely in a private Amazon S3 bucket and are only accessible by CloudFront through OAC. AWS WAF protects the outer layer from threats such as DDoS, SQL Injection, and XSS.
* **API backend layer:** Browser API requests under `/api/*` are routed by CloudFront to the **Application Load Balancer (ALB)** in public subnets. The ALB continuously performs health checks and distributes traffic to **Amazon EC2** instances running ASP.NET Core Web API on port `8080` in private app subnets.
* **Database and cache layer:** When a customer searches for available rooms, the .NET application checks **Amazon ElastiCache Redis** first. If the data exists in cache (Cache HIT), the result is returned immediately with very low latency under 5 ms. If the data is not in cache (Cache MISS), the system queries **Amazon RDS MySQL** with Multi-AZ primary and standby configuration for data durability and failover.

---

### Technology Stack Used

| Functional Layer | Technology / AWS Service | Role in the Workshop |
| :--- | :--- | :--- |
| **Client / Frontend** | HTML5, CSS3, Bootstrap 5.3, Vanilla JavaScript | Build a responsive UI and call APIs asynchronously using Fetch/Axios. |
| **API / Backend** | ASP.NET Core (.NET 8 LTS), Entity Framework Core | Handle business logic, JWT authentication, and transactions to prevent overbooking. |
| **Compute / Routing** | Amazon EC2, Application Load Balancer, Route 53 | Provide compute resources and balance traffic for the Web API. |
| **Storage / CDN** | Amazon S3, Amazon CloudFront | Store private frontend source files and accelerate page loading through edge locations. |
| **Database / Cache** | Amazon RDS MySQL 8.0, ElastiCache Redis | Store long-term business data and provide a cache layer for faster search. |
| **Operations / Security** | Amazon CloudWatch, CloudWatch Alarms, AWS Budgets, IAM | Monitor resources, configure cost alerts, and control EC2 access permissions. |
| **Load Testing** | Locust (Python Framework) | Simulate hundreds of concurrent users to test Auto Scaling behavior. |

### Expected Outcome

After completing the workshop, the implementer will build an online hotel booking system deployed on Amazon Web Services with the following characteristics:

- The frontend is stored on Amazon S3 and distributed through Amazon CloudFront.
- The ASP.NET Core backend runs reliably behind an Application Load Balancer.
- The system can automatically scale through Auto Scaling Group based on CPU utilization.
- Amazon RDS MySQL is deployed with Multi-AZ architecture to improve availability.
- Amazon ElastiCache Redis significantly reduces response time for common queries.
- The whole system is monitored with Amazon CloudWatch and cost-controlled with AWS Budgets.
- Locust load testing proves that the system can handle concurrent users and demonstrates the performance and scalability benefits of Redis Cache and Auto Scaling.
