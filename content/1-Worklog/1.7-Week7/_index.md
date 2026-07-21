---
title: "Week 7 Worklog"
date: 2026-05-25
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 Objectives:
* Master the enterprise identity management model with **IAM**, **Amazon Cognito**, and **AWS Organizations** (SCP).
* Set up a Single Sign-On mechanism (**AWS Identity Center/SSO**) for centralized multi-account access management.
* Enforce international security standards through **AWS Security Hub** and encrypt data at rest with **AWS KMS**.
* Begin exploring **AWS Lambda** and the Serverless model: When to use Lambda instead of traditional EC2.
* Consolidate knowledge of the Shared Responsibility Model and how AWS divides security responsibilities with customers.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| Mon | - Learn about Amazon FSx for Windows File Server<br>- **Practice:**<br>&nbsp;&nbsp;+ Set up Multi-AZ File Server<br>&nbsp;&nbsp;+ Configure SMB Share<br>&nbsp;&nbsp;+ Enable Data Deduplication<br>&nbsp;&nbsp;+ Test read/write performance and manage sessions | 25/05/2026 | 25/05/2026 | Lab 000025 |
| Tue | - Learn about AWS Identity and Access Management (IAM)<br>- Learn about Shared Responsibility Model<br>- **Practice:**<br>&nbsp;&nbsp;+ Create IAM User<br>&nbsp;&nbsp;+ Create IAM Group<br>&nbsp;&nbsp;+ Create IAM Role<br>&nbsp;&nbsp;+ Apply Least Privilege policy | 26/05/2026 | 26/05/2026 | AWS IAM Guide |
| Wed | - Learn about Amazon Cognito, JWT Token, and OAuth 2.0<br>- **Practice:**<br>&nbsp;&nbsp;+ Create User Pool<br>&nbsp;&nbsp;+ Create Identity Pool<br>&nbsp;&nbsp;+ Configure authentication for web/mobile application | 27/05/2026 | 27/05/2026 | AWS Security Docs |
| Thu | - Learn about AWS Organizations and Service Control Policies (SCP)<br>- **Practice:**<br>&nbsp;&nbsp;+ Create Organizational Unit (OU)<br>&nbsp;&nbsp;+ Set up Service Control Policy<br>&nbsp;&nbsp;+ Compare SCP and IAM Policy | 28/05/2026 | 28/05/2026 | AWS Organizations |
| Fri | - Learn about AWS Identity Center (SSO) and AWS KMS<br>- **Practice:**<br>&nbsp;&nbsp;+ Configure Identity Source<br>&nbsp;&nbsp;+ Assign centralized access for multiple AWS accounts<br>&nbsp;&nbsp;+ Create Customer Managed Key<br>&nbsp;&nbsp;+ Apply encryption to S3 and EBS | 29/05/2026 | 29/05/2026 | AWS Study Group |
| Sat | - Learn about AWS Security Hub and AWS Lambda<br>- **Practice:**<br>&nbsp;&nbsp;+ Enable Security Hub<br>&nbsp;&nbsp;+ Configure CIS Benchmark and AWS Best Practices<br>&nbsp;&nbsp;+ Analyze Compliance Score<br>&nbsp;&nbsp;+ Note common Serverless Function use cases | 30/05/2026 | 30/05/2026 | Lab 000018 & Personal |

### Week 7 Achievements:

* **Dedicated Storage & Identity Management:**
    * Successfully deployed **Amazon FSx** Multi-AZ, optimized capacity with Data Deduplication, and preserved data integrity with Shadow Copies.
    * Built a rigorous IAM permission system that ensures the Least Privilege principle at every layer.
* **Multi-Account Governance & Application Authentication:**
    * Built an enterprise-grade hierarchical structure via **AWS Organizations**, controlling the maximum permissions of all member accounts with **SCP**.
    * Understood the user authentication and authorization flow for applications through **Amazon Cognito**.
* **Centralized Security & Encryption:**
    * Used **AWS KMS** to protect sensitive data at rest and mastered the lifecycle of encryption key management.
    * Established **Security Hub** as a "command center" for continuous monitoring, early detection of misconfigurations, and benchmarking against international security standards.

{{% notice success %}}
**Summary:** Week 7 elevates security thinking to a new level: from managing individual users to a comprehensive Identity & Access Management architecture for enterprise multi-account environments.
{{% /notice %}}
