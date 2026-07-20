---
title: "Blog 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# From Requirements to Architecture: Designing a Web System on AWS

When I first started learning AWS, I spent a lot of time studying what each service does, such as Amazon EC2, Amazon RDS, Amazon S3, and Elastic Load Balancer. Each service has its own documentation and examples, so understanding the basic function of each one was not too difficult. However, while participating in the architecture design of a web application, I realized that understanding individual services is still not enough to build a complete system.

What matters more is understanding the relationships between services, their operating scope, and how they work together in an overall architecture. A good system is not created by using as many AWS services as possible, but by choosing the right services, placing them in the right position, and matching them to the actual requirements.

In this blog, I share the process of designing a web architecture on AWS based on what I learned and applied during my internship. The content focuses on requirement analysis, network infrastructure design, service selection, and design decisions that help the system ensure security, scalability, and cost optimization.

---

# System Requirement Analysis

Before deploying any AWS resources, the first step is to clearly define the system requirements. This step guides the whole architecture and helps avoid choosing services by instinct or deploying unnecessary components.

For a web application, common requirements include:

- Users can access the system from the Internet through HTTPS.
- There is an application server responsible for processing user requests.
- There is a database for storing system information.
- There is a storage location for images, documents, or uploaded files.
- Data and resources must be protected from unauthorized access.
- The system can scale when the number of users increases.
- The system is easy to maintain and deploy new versions to.

Based on these requirements, the architecture is built with a multi-layer model to separate system components while ensuring scalability and security from the beginning.

---

# Network Architecture Design

After requirements are identified, the next step is to design the network infrastructure. This is the foundation that determines how AWS services communicate with each other.

The whole system is deployed inside an **Amazon Virtual Private Cloud (VPC)**. Inside the VPC, resources are divided into multiple subnets and spread across two Availability Zones to improve availability.

**The overall architecture is designed as follows:**

> ![*Figure 1. Overall architecture of the web system on AWS.*](/images/VPC.png)

In this architecture:

- Two **Public Subnets** are deployed across two Availability Zones for **Application Load Balancer** and **NAT Gateway**.
- Two **Private Subnets** are used to deploy Amazon EC2 application servers.
- A **DB Subnet Group** includes two private subnets dedicated to Amazon RDS.
- **Internet Gateway** is attached directly to the VPC to provide internet connectivity for public subnets.
- **Route Table** is responsible for routing traffic between Internet Gateway, NAT Gateway, and the corresponding subnets.
- Amazon S3, IAM, and CloudWatch are Region-level or Global services, so they are used outside the VPC.

Deploying across multiple Availability Zones helps the system continue operating when one Availability Zone has an issue and also prepares the architecture for future expansion.

---

# Selecting AWS Services

After completing the network design, the next step is choosing AWS services that match the system requirements.

| Service | Role in the system |
| -------- | ------------------ |
| Amazon VPC | Build a private network environment for the whole system |
| Application Load Balancer | Receive and distribute traffic from the Internet |
| Amazon EC2 | Run the web application |
| Amazon RDS | Store relational data |
| Amazon S3 | Store images and static files |
| NAT Gateway | Allow private subnets to access the Internet outbound |
| Internet Gateway | Connect the VPC to the Internet |
| Route Table | Route traffic between components in the VPC |
| AWS IAM | Manage access permissions |
| Amazon CloudWatch | Monitor the system and collect logs |

Clearly defining the role of each service makes the system easier to manage and reduces unnecessary dependency between components.

---

# Design Decisions

## Deploying across multiple Availability Zones

One of the most important decisions is deploying resources across multiple Availability Zones instead of using only one zone.

Application Load Balancer is configured to operate across two public subnets in two different Availability Zones. This allows the Load Balancer to continue working even if one Availability Zone has an issue.

EC2 servers are also deployed across both Availability Zones and managed by Auto Scaling Group. When an EC2 instance fails, Auto Scaling can automatically create a new instance to maintain system availability.

For the database, Amazon RDS is deployed with Multi-AZ to improve availability and reduce downtime during failure events.

---

![alt text](image.png)
> Figure 2. Request flow in the system.

## Placing application servers in Private Subnets

All EC2 instances are deployed in private subnets instead of public subnets.

Users cannot access EC2 directly. They must access the system through Application Load Balancer. ALB receives requests, performs health checks, and distributes traffic to healthy EC2 instances.

This design reduces the attack surface and improves system security.

---

## Isolating the database

Amazon RDS is placed in a DB Subnet Group within private subnets.

The RDS Security Group only allows EC2 instances from the application Security Group to access the database. This prevents direct connections from the Internet and reduces the risk of unauthorized access.

In addition, Multi-AZ deployment improves recovery capability when the primary database has a failure.

---

## Storing static data on Amazon S3

Instead of storing images or documents directly on EC2, all static data is stored on Amazon S3.

This solution reduces storage pressure on application servers and allows EC2 capacity to scale without needing to synchronize files between servers.

This is also a common principle when building systems with a stateless architecture.

---

## Managing access with IAM Role

During system design, one important security principle is not storing Access Key or Secret Access Key directly in source code or on servers.

Instead, each Amazon EC2 server is attached to an **IAM Role** with the permissions needed to access Amazon S3, Amazon CloudWatch, or other AWS services. When the application needs to access AWS resources, EC2 uses temporary credentials provided by IAM instead of fixed access keys stored in source code.

This approach reduces the risk of credential leakage and follows the **Least Privilege** principle by granting each system component only the permissions it needs.

---

# Security Notes

Security should not be treated as an additional step after the system is completed. It should be considered from the architecture design stage.

In this model, multiple protection layers are applied to reduce system risk.

First, only **Application Load Balancer** is allowed to receive traffic directly from the Internet. Application servers and databases are deployed in **Private Subnets**, without public IP addresses, so they cannot be accessed directly from outside.

Next, **Security Groups** are used to control communication between components. Only Application Load Balancer can send requests to Amazon EC2, and only EC2 can connect to Amazon RDS. Restricting connections by Security Group significantly reduces unauthorized access risks.

![alt text](image-1.png)
> Figure 3. Access flow between the Internet and resources in the VPC.

Using **IAM Role** instead of Access Key also removes the risk of exposing credentials in source code or on servers.

For data transmitted between users and the system, **HTTPS** is used to encrypt data in transit, ensuring confidentiality and integrity.

Combining multiple protection layers helps the system follow recommendations in the **AWS Well-Architected Framework**, especially the **Security** pillar.

---

# Scalability and High Availability

One major advantage of AWS is the ability to scale flexibly based on demand.

In this architecture, Application Load Balancer distributes traffic to application servers. When user traffic increases, the system can add more Amazon EC2 instances through **Auto Scaling Group** without interrupting the service.

Deploying resources across multiple Availability Zones helps the system continue operating even if one Availability Zone has an issue.

For the database, Amazon RDS is deployed with **Multi-AZ**. AWS automatically fails over to the standby database if the primary instance fails, reducing downtime and improving availability.

This design is suitable for applications that require continuous availability and need a future expansion path.

---

# Cost Optimization

Besides performance and security, cost is always an important factor during system design.

For small projects or learning purposes, using too many AWS services can increase cost and make the system unnecessarily complex.

In this architecture, only services that are truly needed are selected to meet the system requirements.

Some services such as **Amazon CloudFront**, **AWS WAF**, **Amazon ElastiCache**, or advanced Auto Scaling policies are not deployed at the beginning because they are not strictly required for the current scale.

When traffic increases or the system moves to production, these services can be added without significantly changing the original architecture.

This approach helps optimize cost in the early stage while still keeping the architecture ready for future scaling.

---

# Lessons Learned

Through the process of designing and studying AWS architecture, I realized that understanding the function of each service is only the starting point.

What matters more is understanding the scope of each service and the relationships between services in the overall architecture.

Key lessons I learned:

- Always start from system requirements before selecting AWS services.
- Design network architecture from the beginning to avoid major changes during deployment.
- Clearly distinguish services at the Global, Region, and VPC scope.
- Prioritize security from the design stage.
- Do not use more services than necessary just because they are available on AWS.
- Balance performance, security, scalability, and deployment cost.

These principles make the architecture clearer and provide a strong foundation for future system development.

---

# Future Development

The current architecture satisfies the requirements of a small-to-medium web application. However, when the number of users and data volume increase, the system can continue to expand by adding more AWS services.

Possible future improvements include:

- Deploy **Amazon CloudFront** to accelerate static content delivery and reduce latency for users in different regions.
- Integrate **AWS WAF** to protect the application from common attacks such as SQL Injection and Cross-Site Scripting (XSS).
- Use **Amazon ElastiCache** to reduce database load and improve query performance.
- Build backup and recovery mechanisms using **AWS Backup**.
- Complete the CI/CD process using **AWS CodePipeline** and **AWS CodeDeploy** to automate application deployment.

Because the architecture is designed to be extensible, these components can be added without significantly affecting the current system.

---

# Conclusion

Designing architecture on AWS is not simply selecting suitable services. It is a process of making balanced decisions between performance, security, scalability, and cost.

Through requirement analysis, network infrastructure design, and suitable AWS service selection, I realized that a good architecture does not necessarily use many services. It must solve the right problem and be able to evolve in the future.

For beginners learning AWS, understanding how services work together in a complete architecture provides more value than only learning the function of each service individually.

I hope the experience and design process shared in this blog provide a useful perspective for building AWS project architectures and create a foundation for approaching more complex architecture models in the future.
