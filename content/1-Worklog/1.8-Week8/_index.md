---
title: "Week 8 Worklog"
date: 2026-06-01
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Week 8 Objectives:
* Optimize costs and automate the AWS resource lifecycle using **AWS Lambda** combined with **CloudWatch Events**.
* Master resource classification and management techniques with **Resource Tags** and **Resource Groups**.
* Apply advanced permission control with **IAM Policies with Tag Conditions** and **IAM Permission Boundaries** to cap user privileges.
* Begin deploying data security with **AWS KMS**: Creating KMS Keys and configuring encryption for Amazon S3.
* Consistently enforce the **Least Privilege** principle across all IAM configurations to minimize the attack surface.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| Mon | - Deploy **EC2 Cost Optimization (Lab 000022)**: Create an IAM Role for Lambda, build a Function to automatically stop EC2 instances outside of business hours.<br>- Configure a **CloudWatch Event Rule** with a cron schedule to trigger Lambda automatically. | 01/06/2026 | 01/06/2026 | Lab 000022 |
| Tue | - Complete the Lambda Function to automatically **restart EC2** at the beginning of the business day.<br>- Test the automation mechanism, review logs in CloudWatch Logs, and resolve any runtime errors. | 02/06/2026 | 02/06/2026 | Lab 000022 |
| Wed | - Practice **Resource Tags (Lab 000027)**: Apply classification tags to EC2, S3, VPC resources by environment (dev/staging/prod).<br>- Create **Resource Groups** to group and monitor resources based on tag criteria. | 03/06/2026 | 03/06/2026 | Lab 000027 |
| Thu | - Practice **IAM Policy with Tags (Lab 000028)**: Build a Policy that only allows EC2 management when the Instance has a specific required Tag.<br>- Test permission enforcement against real-world scenarios and confirm Least Privilege is working correctly. | 04/06/2026 | 04/06/2026 | Lab 000028 |
| Fri | - Deploy **IAM Permission Boundary (Lab 000030)**: Create a Policy limiting EC2 permissions to a specific designated Region.<br>- Apply the Permission Boundary to an IAM User and test access capabilities across different Regions. | 05/06/2026 | 05/06/2026 | Lab 000030 |
| Sat | - Begin exploring **AWS KMS**: Create a Customer Managed Key and practice configuring server-side encryption for S3 objects.<br>- Learn the two-layer KMS authorization model: Key Policy (who manages the key) + IAM Policy (who uses the key). | 06/06/2026 | 06/06/2026 | Lab 000033 |

### Week 8 Achievements:

* **Cost Optimization & Automation:**
    * Successfully deployed a mechanism to automatically start/stop **EC2** using **Lambda + CloudWatch**, potentially saving 60-70% on compute costs during non-business hours.
    * Mastered the Lambda execution lifecycle and how Lambda, CloudWatch Events, and IAM Roles work together.
* **Resource Management & Classification:**
    * Built a consistent tagging strategy to organize resources clearly by environment, project, and team.
    * Used Resource Groups for an aggregated overview and to easily perform bulk operations on tagged resources.
* **Advanced Access Control:**
    * Established **IAM Policy with Tag Conditions** for context-aware permissions, beyond simple service-level authorization.
    * Applied **Permission Boundaries** as the ultimate guard rail, preventing privilege escalation by any user or role.
* **Data Security with KMS:**
    * Understood AWS KMS's two-layer security model, enabling fine-grained control over who can manage vs. who can use encryption keys.

{{% notice success %}}
**Summary:** Week 8 focuses on lean operational thinking (FinOps) and defense-in-depth security — two key pillars for sustainably and efficiently managing large-scale AWS environments.
{{% /notice %}}
