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
| Mon | - Learn about the AWS Free Tier account registration process<br>- **Practice:**<br>&nbsp;&nbsp;+ Prepare personal information and payment card<br>&nbsp;&nbsp;+ Register an AWS Free Tier account<br>&nbsp;&nbsp;+ Verify identity and payment method | 20/04/2026 | 20/04/2026 | AWS Documentation |
| Tue | - Learn about Multi-Factor Authentication (MFA)<br>- **Practice:**<br>&nbsp;&nbsp;+ Enable MFA for the Root Account<br>&nbsp;&nbsp;+ Enable MFA for IAM User<br>&nbsp;&nbsp;+ Review risks when credentials are exposed | 21/04/2026 | 21/04/2026 | AWS Security Blog |
| Wed | - Learn about the Least Privilege principle in IAM<br>- **Practice:**<br>&nbsp;&nbsp;+ Create Admin Group<br>&nbsp;&nbsp;+ Create IAM User<br>&nbsp;&nbsp;+ Attach minimum required permissions to user/group | 22/04/2026 | 22/04/2026 | AWS Study Group |
| Thu | - Learn about Access Keys and IAM Policy<br>- **Practice:**<br>&nbsp;&nbsp;+ Create Access Key for AWS CLI<br>&nbsp;&nbsp;+ Configure AWS CLI account access<br>&nbsp;&nbsp;+ Create and test IAM Policy following an enterprise model | 23/04/2026 | 23/04/2026 | AWS Workshop |
| Fri | - Learn about Amazon Virtual Private Cloud (VPC)<br>- **Practice:**<br>&nbsp;&nbsp;+ Review IAM security configurations<br>&nbsp;&nbsp;+ Identify VPC's role in cloud architecture<br>&nbsp;&nbsp;+ Learn the basic components of a private virtual network | 24/04/2026 | 24/04/2026 | AWS Networking Guide |
| Sat | - Learn about AWS Support Plans and CIDR<br>- **Practice:**<br>&nbsp;&nbsp;+ Compare Basic, Developer, Business, and Enterprise Support<br>&nbsp;&nbsp;+ Divide IP address ranges using CIDR<br>&nbsp;&nbsp;+ Note how to choose a suitable support plan | 25/04/2026 | 25/04/2026 | Personal |

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

### Week 2 practice screenshots:

![Enable MFA for AWS account](/images/worklog/MFA.jpg)

![Complete Week 2 practice](/images/worklog/2.jpg)
