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
| Mon | - Learn about AWS KMS and Server-Side Encryption (SSE-KMS)<br>- **Practice:**<br>&nbsp;&nbsp;+ Create Customer Managed Key (CMK)<br>&nbsp;&nbsp;+ Configure SSE-KMS for S3 Bucket<br>&nbsp;&nbsp;+ Authorize access with IAM Policy and Key Policy | 08/06/2026 | 08/06/2026 | Lab 000033 |
| Tue | - Learn about AWS CloudTrail and Amazon Athena<br>- **Practice:**<br>&nbsp;&nbsp;+ Configure CloudTrail to deliver API logs to S3 Bucket<br>&nbsp;&nbsp;+ Create Athena table to query logs<br>&nbsp;&nbsp;+ Check anomalous access behavior | 09/06/2026 | 09/06/2026 | Lab 000033 |
| Wed | - Learn database fundamentals<br>&nbsp;&nbsp;+ Primary Key<br>&nbsp;&nbsp;+ Foreign Key<br>&nbsp;&nbsp;+ Index<br>&nbsp;&nbsp;+ SQL (RDBMS) and NoSQL<br>- Learn OLTP and OLAP data processing models | 10/06/2026 | 10/06/2026 | AWS Database Overview |
| Thu | - Learn about Amazon RDS and Amazon Aurora<br>- **Practice:**<br>&nbsp;&nbsp;+ Create RDS DB Instance<br>&nbsp;&nbsp;+ Configure Multi-AZ Deployment<br>&nbsp;&nbsp;+ Test Automated Backup<br>&nbsp;&nbsp;+ Compare Aurora with RDS MySQL/PostgreSQL | 11/06/2026 | 11/06/2026 | AWS RDS & Aurora |
| Fri | - Learn about advanced IAM and IAM Role for EC2<br>- **Practice:**<br>&nbsp;&nbsp;+ Create IAM User<br>&nbsp;&nbsp;+ Create IAM Group<br>&nbsp;&nbsp;+ Create IAM Role<br>&nbsp;&nbsp;+ Configure Switch Role<br>&nbsp;&nbsp;+ Attach IAM Role to EC2 so it can access S3 without Access Keys | 12/06/2026 | 12/06/2026 | Lab 000044 & 000048 |
| Sat | - Learn Data Lake architecture on AWS<br>&nbsp;&nbsp;+ Ingestion<br>&nbsp;&nbsp;+ Storage<br>&nbsp;&nbsp;+ Catalog<br>&nbsp;&nbsp;+ Analytics<br>- Note S3's role in storing structured and unstructured data | 13/06/2026 | 13/06/2026 | AWS Analytics Docs |

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
