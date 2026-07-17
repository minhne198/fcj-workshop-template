---
title: "Week 11 Worklog"
date: 2026-06-22
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Week 11 Objectives:
* Launch the capstone project: **High-Availability Hotel Booking System on AWS**.
* Design a complete system architecture guaranteeing 3 key properties: **High Availability**, **Auto Scaling**, and **Caching**.
* Build the foundational network infrastructure (Phase 1): VPC, Subnets, Security Groups, IAM Role, NAT Gateway.
* Initialize the database and cache layers (Phase 2): **Amazon RDS MySQL** and **Amazon ElastiCache Redis**.
* Begin Backend API development with **ASP.NET Core 8** and design the database schema.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| Mon | - Analyze project requirements and design the overall system architecture on **Draw.io**.<br>- Identify all required AWS services: VPC, EC2, ALB, ASG, RDS, ElastiCache, S3, CloudFront, WAF, CloudWatch, SNS. | 22/06/2026 | 22/06/2026 | Project Document |
| Tue | - **Phase 1 - Network Infrastructure:** Create VPC (`10.0.0.0/16`), divide into 6 Subnets (2 Public + 4 Private), attach Internet Gateway.<br>- Configure NAT Gateways for 2 AZs, set up Route Tables for Public and Private Subnets. | 23/06/2026 | 23/06/2026 | AWS Console |
| Wed | - Create 4 Security Groups (SG-ALB, SG-EC2, SG-RDS, SG-Redis) following the principle of minimal attack surface.<br>- Create **IAM Role** `EC2-HotelAPI-Role` with necessary policies: S3 Read, CloudWatch Agent, Secrets Manager. | 24/06/2026 | 24/06/2026 | AWS Console |
| Thu | - **Phase 2 - Database Initialization:** Create **Amazon RDS MySQL 8.0** (`db.t3.micro`) in Private Subnet with KMS encryption enabled.<br>- Store DB password securely in **AWS Secrets Manager**. | 25/06/2026 | 25/06/2026 | AWS Console |
| Fri | - Create **Amazon ElastiCache Redis 7.x** (`cache.t3.micro`) in the Private DB Subnet.<br>- Design **Database Schema**: Tables for Users, Hotels, RoomTypes, Bookings, Reviews with proper foreign key relationships. Run SQL creation scripts via DBeaver. | 26/06/2026 | 26/06/2026 | AWS Console |
| Sat | - **Phase 3 - Backend API Start:** Initialize ASP.NET Core 8 Web API project, configure Entity Framework Core + Pomelo MySQL driver.<br>- Write `AuthController.cs` (Register/Login + JWT Token) and `SearchService.cs` (with Redis Cache integration for search results). | 27/06/2026 | 27/06/2026 | Visual Studio 2022 |

### Week 11 Achievements:

* **System Architecture Design:**
    * Completed the full system architecture diagram on **Draw.io** covering all AWS components: CloudFront → WAF → ALB → ASG (EC2) → RDS + Redis, S3 static hosting, CloudWatch monitoring.
    * Clearly defined the 3 properties to demonstrate: HA (terminate 1 EC2 → still running), Auto Scaling (500 users → EC2 auto scales), Caching (cache hit < 5ms vs. 100-200ms without cache).

* **Network Infrastructure (Phase 1 Complete):**
    * Created a complete VPC with 6 purposefully divided Subnets: Public (ALB, NAT GW) and Private (App EC2, DB RDS/Redis).
    * Set up Security Groups following a layered security model: only ALB can reach EC2, only EC2 can reach RDS and Redis.
    * EC2 IAM Role configured without Access Keys — correctly applying modern security best practices.

* **Database & Cache (Phase 2 Complete):**
    * Successfully initialized **Amazon RDS MySQL** with KMS encryption and password managed via Secrets Manager.
    * **ElastiCache Redis** is ready to serve as an in-memory cache for popular search results.
    * Database Schema clearly designed with proper foreign key relationships between all tables.

* **Backend API (Phase 3 Started):**
    * ASP.NET Core 8 project runs successfully in the local environment and connects to RDS and Redis.
    * Authentication API is functional: account registration and login returning valid JWT Tokens.

{{% notice success %}}
**Summary:** Week 11 completed the entire AWS infrastructure foundation for the capstone project. The system architecture is designed professionally following the 3-tier model (Presentation - Application - Data) with full HA features and security aligned with industry standards.
{{% /notice %}}
