---
title: "Week 2 Worklog"
date: 2026-04-22
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Week 2 Objectives:
* Complete the registration and identity verification process for the AWS Free Tier account securely.
* Configure Multi-Factor Authentication (**MFA**) to harden the Root account against external threats.
* Practice professional system administration through **IAM**, including user group management and proper permission assignment.
* Get acquainted with the concept of **Amazon VPC** and the mechanism for building an isolated, independent virtual network on AWS.
* Understand CIDR notation basics and how to segment IP addresses into logical Subnets.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| Mon | - Prepare personal information and international payment card required for account creation.<br>- Complete the entire AWS Free Tier account registration process following official guidelines. | 20/04/2026 | 20/04/2026 | AWS Documentation |
| Tue | - Activate Multi-Factor Authentication (**MFA**) for both the Root account and IAM Users.<br>- Analyze common security risks when login credentials are leaked or accounts are compromised. | 21/04/2026 | 21/04/2026 | AWS Security Blog |
| Wed | - Create an **Admin Group** and **IAM User** with the minimum necessary permissions.<br>- Apply the Least Privilege principle when assigning permissions to avoid over-granting access. | 22/04/2026 | 22/04/2026 | AWS Study Group |
| Thu | - Create and configure **Access Keys** for accessing AWS services through the AWS CLI.<br>- Practice creating and managing IAM Policies following an enterprise model. | 23/04/2026 | 23/04/2026 | AWS Workshop |
| Fri | - Review and audit all IAM security configurations set up during the week.<br>- Begin exploring **Amazon VPC** at a high level: What it is, its architecture, and why a private virtual network is needed. | 24/04/2026 | 24/04/2026 | AWS Networking Guide |
| Sat | - Deep-dive into AWS Support Plans and practice IP address subdivision using **CIDR** notation. | 25/04/2026 | 25/04/2026 | Personal |

### Week 2 Achievements:

* **Regarding Account Security:**
    * Successfully set up **MFA** protection, effectively blocking brute-force and phishing attacks.
    * Grasped the importance of never using the Root account for daily operational tasks.
* **Regarding IAM System Administration:**
    * Mastered creating **Admin Groups** and **IAM Users**, establishing a structured cloud personnel management framework.
    * Learned to configure and use **Access Keys** to manage AWS resources via the CLI.
    * Understood how to build IAM Policies that precisely control access for each entity.
* **Regarding VPC & AWS Support:**
    * Got acquainted with VPC architecture and understood why network isolation is an essential security element in the Cloud.
    * Learned the key differences between the 4 AWS support tiers (Basic, Developer, Business, Enterprise).

#### AWS Support Plans Overview

| Support Plan | Key Features | Target Audience |
| :--- | :--- | :--- |
| **Basic** | Free, covers account, billing, and technical documentation. | Individual users, students just getting started. |
| **Developer** | Adds architectural guidance and faster response times. | Development and testing environments. |
| **Business** | Automated infrastructure checks with Trusted Advisor for cost and security optimization. | Production systems in active operation. |
| **Enterprise** | 24/7 dedicated TAM support, regular reviews and proactive guidance. | Large enterprises with mission-critical systems. |

{{% notice tip %}}
**Tip:** For students or beginners, the **Basic** plan combined with the AWS Documentation is the most cost-effective way to learn without incurring additional expenses.
{{% /notice %}}

{{% notice warning %}}
**Important Note:** Always store Access Keys and MFA recovery codes in a secure location. Never upload this sensitive information to public repositories like GitHub or GitLab.
{{% /notice %}}
