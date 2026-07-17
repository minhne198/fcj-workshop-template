---
title: "Week 9 Worklog"
date: 2026-06-08
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Week 9 Objectives:
* Master comprehensive data encryption with **AWS KMS** and monitor system activity using **AWS CloudTrail**.
* Query and analyze audit logs with **Amazon Athena** to detect anomalous activity.
* Explore and practice with AWS relational database services: **Amazon RDS** and **Amazon Aurora**.
* Deploy a modern authorization model using **IAM Roles for EC2** to access resources without storing Access Keys.
* Begin exploring **AWS Data Lake architecture**: The role of S3 and the centralized data ingestion process.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| Mon | - Complete **AWS KMS (Lab 000033)**: Create a CMK, configure Server-Side Encryption (SSE-KMS) for an S3 Bucket.<br>- Authorize access to the encryption key via IAM Policy combined with Key Policy. | 08/06/2026 | 08/06/2026 | Lab 000033 |
| Tue | - Configure **AWS CloudTrail** to record all API activity in the account to an S3 Bucket.<br>- Query logs using **Amazon Athena** and verify the ability to detect anomalous resource access behavior. | 09/06/2026 | 09/06/2026 | Lab 000033 |
| Wed | - Study database fundamentals: Primary Keys, Foreign Keys, Indexes, and the difference between **SQL (RDBMS)** and **NoSQL** models.<br>- Analyze the **OLTP** (transactional) and **OLAP** (analytical) data processing models in enterprise systems. | 10/06/2026 | 10/06/2026 | AWS Database Overview |
| Thu | - Practice with **Amazon RDS**: Create a DB Instance, configure Multi-AZ Deployment, and test Automated Backup.<br>- Explore **Amazon Aurora** and its advantages over standard RDS MySQL/PostgreSQL (performance, scalability). | 11/06/2026 | 11/06/2026 | AWS RDS & Aurora |
| Fri | - Practice **Advanced IAM (Lab 000044)**: Create Users, Groups, IAM Roles, and set up Switch Role for flexible permission switching.<br>- Deploy **IAM Roles for EC2 (Lab 000048)** to access S3 without storing Access Keys in the application. | 12/06/2026 | 12/06/2026 | Lab 000044 & 000048 |
| Sat | - Explore **Data Lake architecture on AWS**: S3 as the central storage foundation for both structured and unstructured data.<br>- Study the role of each layer in a Data Lake architecture: Ingestion → Storage → Catalog → Analytics. | 13/06/2026 | 13/06/2026 | AWS Analytics Docs |

### Week 9 Achievements:

* **Data Security & Encryption:**
    * Successfully deployed **AWS KMS** with SSE-KMS, ensuring S3 data is encrypted using keys under customer control.
    * Understood the differences between SSE-S3, SSE-KMS, and SSE-C encryption strategies.
* **Monitoring & Auditing:**
    * Proficiently used **CloudTrail + Athena** to query API call logs and determine who did what and when in the AWS account.
    * Built a basic process for detecting anomalous behavior and responding to security incidents (Incident Response).
* **Databases on AWS:**
    * Understood the architecture and operational mechanics of **Amazon RDS** (Managed RDBMS) and **Aurora** (Cloud-native database engine).
    * Clearly understood the OLTP vs. OLAP distinction and can select the right service for each type of workload.
* **Modern Authorization Model:**
    * Applying **IAM Roles** instead of Access Keys eliminates the risk of credential exposure in source code or configuration files.
* **Data Analytics Foundation:**
    * Understood the high-level architecture of a Data Lake and the role of S3 as an enterprise "data lake" on AWS.

{{% notice info %}}
**Summary:** Week 9 marks the transition from infrastructure security to data security, while opening the door to the world of Data Analytics on AWS Cloud.
{{% /notice %}}
