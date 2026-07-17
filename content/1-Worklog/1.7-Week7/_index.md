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
| Mon | - Deploy a complete **Amazon FSx (Lab 000025)**: Set up a Multi-AZ File Server, configure SMB shares, and enable Data Deduplication.<br>- Test read/write performance and manage user sessions on the file server. | 25/05/2026 | 25/05/2026 | Lab 000025 |
| Tue | - Practice advanced **IAM** administration: Create Users/Groups with granular permissions, apply Least Privilege, and use IAM Roles for role-based access control.<br>- Study the Shared Responsibility Model between AWS and the customer. | 26/05/2026 | 26/05/2026 | AWS IAM Guide |
| Wed | - Configure **Amazon Cognito**: Set up User Pools and Identity Pools to authenticate users for web/mobile applications.<br>- Understand JWT Tokens and OAuth 2.0 in the context of modern authentication flows. | 27/05/2026 | 27/05/2026 | AWS Security Docs |
| Thu | - Multi-account governance with **AWS Organizations**: Create Organizational Units (OUs) and set up **Service Control Policies (SCP)** to control the maximum permissions of member accounts.<br>- Understand the difference between SCPs and IAM Policies in the permission model. | 28/05/2026 | 28/05/2026 | AWS Organizations |
| Fri | - Deploy **AWS Identity Center (SSO)**: Configure an Identity Source and centrally assign access permissions for multiple AWS accounts.<br>- Practice encrypting data with **AWS KMS**: Create a Customer Managed Key and apply it to S3 and EBS. | 29/05/2026 | 29/05/2026 | AWS Study Group |
| Sat | - Activate **AWS Security Hub (Lab 000018)**: Configure security standards (CIS Benchmark, AWS Best Practices) and analyze the Compliance Score.<br>- Explore an overview of **AWS Lambda** and common Serverless Function use cases. | 30/05/2026 | 30/05/2026 | Lab 000018 & Personal |

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
