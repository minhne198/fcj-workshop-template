---
title: "Week 6 Worklog"
date: 2026-05-18
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Objectives:
* Build a durable object storage infrastructure with **Amazon S3** and deploy a globally distributed static website via **CloudFront**.
* Master data protection techniques: **Versioning**, **Multi-Region Replication**, and access control with Bucket Policies.
* Configure **VPC Endpoints** for private S3 connectivity without traversing the public internet, enhancing security and reducing data transfer costs.
* Understand **Disaster Recovery** strategies based on RTO/RPO metrics and centralized backup management with **AWS Backup**.
* Explore enterprise-grade dedicated file storage with **Amazon FSx for Windows File Server**.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| Mon | - Learn about Amazon S3, Static Website Hosting, and CloudFront<br>- **Practice:**<br>&nbsp;&nbsp;+ Create S3 Bucket<br>&nbsp;&nbsp;+ Enable Static Website Hosting<br>&nbsp;&nbsp;+ Configure Bucket Policy<br>&nbsp;&nbsp;+ Integrate CloudFront for content delivery | 18/05/2026 | 18/05/2026 | Lab S3 (000057) |
| Tue | - Learn about Bucket Versioning and Cross-Region Replication (CRR)<br>- **Practice:**<br>&nbsp;&nbsp;+ Enable Bucket Versioning<br>&nbsp;&nbsp;+ Restore object to a previous version<br>&nbsp;&nbsp;+ Configure CRR to replicate data to another Region | 19/05/2026 | 19/05/2026 | Lab S3 (000057) |
| Wed | - Learn about S3 Gateway Endpoint and Interface Endpoint (PrivateLink)<br>- **Practice:**<br>&nbsp;&nbsp;+ Configure S3 Gateway Endpoint<br>&nbsp;&nbsp;+ Configure Interface Endpoint<br>&nbsp;&nbsp;+ Test S3 traffic through private connectivity | 20/05/2026 | 20/05/2026 | Lab VPC (000013-14) |
| Thu | - Learn about NACLs, Security Groups, and S3 access control<br>- **Practice:**<br>&nbsp;&nbsp;+ Control network traffic with NACLs<br>&nbsp;&nbsp;+ Control traffic with Security Groups<br>&nbsp;&nbsp;+ Restrict S3 access with IAM Policy and S3 Bucket Policy | 21/05/2026 | 21/05/2026 | AWS Study Group |
| Fri | - Learn about AWS Backup, RTO, and RPO<br>- **Practice:**<br>&nbsp;&nbsp;+ Create Backup Plan<br>&nbsp;&nbsp;+ Create Backup Vault<br>&nbsp;&nbsp;+ Test data restoration<br>&nbsp;&nbsp;+ Note Disaster Recovery strategy | 22/05/2026 | 22/05/2026 | AWS Study Group |
| Sat | - Learn about Amazon FSx for Windows File Server<br>- **Practice:**<br>&nbsp;&nbsp;+ Explore Multi-AZ architecture<br>&nbsp;&nbsp;+ Configure SMB<br>&nbsp;&nbsp;+ Learn about Data Deduplication<br>&nbsp;&nbsp;+ Consolidate Week 6 lab screenshots | 23/05/2026 | 23/05/2026 | Personal |

### Week 6 Achievements:

* **Storage & Content Delivery:**
    * Successfully deployed a static website with globally optimized access speed by combining **S3 + CloudFront CDN**.
    * Mastered object lifecycle management and **Storage Classes** to optimize long-term storage costs.
* **Security & High Availability:**
    * Configured Versioning as a safety net against accidental deletion or overwriting, preventing unrecoverable data loss.
    * Clearly understood **RTO/RPO** metrics and appropriate Disaster Recovery strategies for different levels of business requirements.
    * Used **AWS Backup** to manage backups for multiple services (EC2, RDS, S3, EFS) from a single unified interface.
* **Network & Private Connectivity:**
    * Deployed VPC Endpoints to eliminate internet dependency for internal data traffic, increasing security and reducing latency.
* **Enterprise File Storage:**
    * Understood the architecture and use cases of **Amazon FSx** in enterprise environments requiring Windows-compatible file sharing (SMB protocol).

{{% notice info %}}
**Summary:** Week 6 completes the Cloud Engineer's mindset on combining S3's limitless storage, VPC Endpoints' security, and AWS Backup's resilience — the foundation for building highly reliable applications on AWS.
{{% /notice %}}

### Week 6 practice screenshots:

![Week 6 practice - 541](/images/541.jpg)
