---
title: "Week 3 Worklog"
date: 2026-04-27
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Week 3 Objectives:
* Understand the architecture and role of **Amazon VPC** in creating an isolated, secure virtual network environment on the cloud.
* Master IP address management operations, Subnet division (Public/Private), and Route Table configuration.
* Implement network traffic control layers: **Security Groups** (Stateful) and **Network ACLs** (Stateless).
* Practice connecting to the Internet via **Internet Gateway** and securing outbound access from Private Subnets using **NAT Gateway**.
* Begin exploring advanced network connections like **VPC Peering** and deploying **CloudFormation** to automate infrastructure.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| Mon | - Learn about Amazon VPC, CIDR, and Subnets<br>- **Practice:**<br>&nbsp;&nbsp;+ Define CIDR range for VPC<br>&nbsp;&nbsp;+ Divide Public and Private Subnets<br>&nbsp;&nbsp;+ Configure Route Tables for Subnets | 27/04/2026 | 27/04/2026 | AWS Networking Guide |
| Tue | - Learn about Internet Gateway and NAT Gateway<br>- **Practice:**<br>&nbsp;&nbsp;+ Attach Internet Gateway to Public Subnet<br>&nbsp;&nbsp;+ Create NAT Gateway for Private Subnet<br>&nbsp;&nbsp;+ Test Internet access from private resources | 28/04/2026 | 28/04/2026 | AWS Documentation |
| Wed | - Learn about Security Groups and Network ACLs<br>- **Practice:**<br>&nbsp;&nbsp;+ Configure Security Group<br>&nbsp;&nbsp;+ Configure Network ACL<br>&nbsp;&nbsp;+ Test allow/deny traffic<br>&nbsp;&nbsp;+ Compare Stateful and Stateless behavior | 29/04/2026 | 29/04/2026 | Security Essentials |
| Thu | - Learn about VPC Peering, Transit Gateway, and Elastic Load Balancing (ELB)<br>- **Practice:**<br>&nbsp;&nbsp;+ Analyze multi-VPC connectivity models<br>&nbsp;&nbsp;+ Compare Peering and Transit Gateway<br>&nbsp;&nbsp;+ Note ELB's role in High Availability architecture | 30/04/2026 | 30/04/2026 | AWS Study Group |
| Fri | - Learn about EC2 Instance Connect Endpoint<br>- **Practice:**<br>&nbsp;&nbsp;+ Configure EC2 Instance Connect Endpoint<br>&nbsp;&nbsp;+ Connect securely to EC2 in a Private Subnet<br>&nbsp;&nbsp;+ Verify access without a Bastion Host | 01/05/2026 | 01/05/2026 | AWS Workshop |
| Sat | - Learn about AWS CloudFormation and Key Pair<br>- **Practice:**<br>&nbsp;&nbsp;+ Read CloudFormation Template structure<br>&nbsp;&nbsp;+ Create Key Pair<br>&nbsp;&nbsp;+ Connect securely to EC2 Instance by SSH | 02/05/2026 | 02/05/2026 | AWS CloudFormation Guide |

### Week 3 Achievements:

* **Regarding Network Architecture Thinking:**
    * Capable of designing and deploying a separate, secure virtual network environment on AWS according to standard architecture practices.
    * Mastered the mechanism for controlling inbound/outbound traffic through two defensive layers: Security Groups and Network ACLs.
* **Regarding Practical Deployment Skills:**
    * Know how to set up connectivity from Private Subnets to the Internet through NAT Gateway.
    * Can manage EC2 securely within an internal network without exposing the actual IP address.
    * Understand the operating principle of VPC Peering and when to upgrade to Transit Gateway.
* **Regarding IaC Foundation:**
    * Grasped the power of Infrastructure as Code (IaC) in reusing and standardizing network infrastructure.

{{% notice success %}}
**Summary:** Mastering VPC is an important stepping stone, building a solid foundation for safely deploying other services like EC2 and RDS in a controlled and optimized manner in the weeks ahead.
{{% /notice %}}

### Week 3 practice screenshots:

![Create Security Group](/images/worklog/Tao_SecurityGroup.jpg)

![Create Gateway](/images/worklog/Tao_Gateway.jpg)
