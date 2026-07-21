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
| Mon | - Learn about EC2 cost optimization with AWS Lambda<br>- **Practice:**<br>&nbsp;&nbsp;+ Create IAM Role for Lambda<br>&nbsp;&nbsp;+ Write Lambda Function to stop EC2 outside business hours<br>&nbsp;&nbsp;+ Configure CloudWatch Event Rule with cron schedule | 01/06/2026 | 01/06/2026 | Lab 000022 |
| Tue | - Learn about EC2 operational automation<br>- **Practice:**<br>&nbsp;&nbsp;+ Complete Lambda Function to start EC2 automatically<br>&nbsp;&nbsp;+ Test EC2 stop/start automation<br>&nbsp;&nbsp;+ Review CloudWatch Logs and fix runtime errors | 02/06/2026 | 02/06/2026 | Lab 000022 |
| Wed | - Learn about Resource Tags and Resource Groups<br>- **Practice:**<br>&nbsp;&nbsp;+ Tag EC2 resources<br>&nbsp;&nbsp;+ Tag S3 resources<br>&nbsp;&nbsp;+ Tag VPC resources<br>&nbsp;&nbsp;+ Create Resource Groups using tag criteria | 03/06/2026 | 03/06/2026 | Lab 000027 |
| Thu | - Learn about IAM Policy with Tags<br>- **Practice:**<br>&nbsp;&nbsp;+ Build Policy to manage EC2 by required tag<br>&nbsp;&nbsp;+ Test allowed/denied access scenarios<br>&nbsp;&nbsp;+ Confirm Least Privilege behavior | 04/06/2026 | 04/06/2026 | Lab 000028 |
| Fri | - Learn about IAM Permission Boundary<br>- **Practice:**<br>&nbsp;&nbsp;+ Create Policy limiting EC2 permissions by Region<br>&nbsp;&nbsp;+ Apply Permission Boundary to IAM User<br>&nbsp;&nbsp;+ Test access across different Regions | 05/06/2026 | 05/06/2026 | Lab 000030 |
| Sat | - Learn about AWS Key Management Service (KMS)<br>- **Practice:**<br>&nbsp;&nbsp;+ Create Customer Managed Key<br>&nbsp;&nbsp;+ Configure Server-Side Encryption for S3<br>&nbsp;&nbsp;+ Authorize KMS access with Key Policy and IAM Policy | 06/06/2026 | 06/06/2026 | Lab 000033 |

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
