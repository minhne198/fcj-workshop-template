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
| Mon | - Create an **S3 Bucket**, configure **Static Website Hosting**, and integrate content delivery via **CloudFront**.<br>- Set up a **Bucket Policy** to manage public access permissions securely and effectively. | 18/05/2026 | 18/05/2026 | Lab S3 (000057) |
| Tue | - Enable **Bucket Versioning** to track the history of object changes and restore previous versions when needed.<br>- Configure **Cross-Region Replication (CRR)** to replicate data to another Region for high availability. | 19/05/2026 | 19/05/2026 | Lab S3 (000057) |
| Wed | - Configure an **S3 Gateway Endpoint** and **Interface Endpoint (PrivateLink)** to access S3 from within the VPC without going through the internet.<br>- Test and confirm S3 traffic routes through the internal private connection. | 20/05/2026 | 20/05/2026 | Lab VPC (000013-14) |
| Thu | - Granularly control network traffic through **NACLs** and **Security Groups** security layers within the VPC.<br>- Practice restricting S3 access by applying Least Privilege via IAM Policy and S3 Bucket Policy. | 21/05/2026 | 21/05/2026 | AWS Study Group |
| Fri | - Set up centralized backup with **AWS Backup**: Configure Backup Plans, Backup Vaults, and test data restoration procedures.<br>- Study the **RTO** and **RPO** metrics in Disaster Recovery strategy planning. | 22/05/2026 | 22/05/2026 | AWS Study Group |
| Sat | - Explore **Amazon FSx for Windows File Server**: Multi-AZ architecture, SMB configuration, and Data Deduplication features.<br>- Consolidate lab screenshots and complete the Week 6 report. | 23/05/2026 | 23/05/2026 | Personal |

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
