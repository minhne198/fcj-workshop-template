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
| Mon | - Learn VPC fundamentals: IP address ranges (CIDR) and logical Subnet segmentation.<br>- Configure Route Tables to direct internal traffic between Subnets. | 27/04/2026 | 27/04/2026 | AWS Networking Guide |
| Tue | - Set up an Internet connection for the Public Subnet via **Internet Gateway**.<br>- Configure **NAT Gateway** to allow resources in Private Subnets to access the Internet without exposing their real IP. | 28/04/2026 | 28/04/2026 | AWS Documentation |
| Wed | - Practice network security: Configure **Security Groups** and **Network ACLs**, differentiate between Stateful and Stateless mechanisms.<br>- Test allow/deny traffic scenarios to understand how both security layers work in tandem. | 29/04/2026 | 29/04/2026 | Security Essentials |
| Thu | - Research inter-network connectivity: **VPC Peering** and **Transit Gateway** for connecting multiple VPCs.<br>- Explore **Elastic Load Balancing (ELB)** to distribute traffic and increase system availability. | 30/04/2026 | 30/04/2026 | AWS Study Group |
| Fri | - Practice configuring **EC2 Instance Connect Endpoint** to manage servers remotely without needing a Bastion Host.<br>- Set up and test a secure connection to an EC2 instance in a Private Subnet. | 01/05/2026 | 01/05/2026 | AWS Workshop |
| Sat | - Begin exploring **AWS CloudFormation**: The concept of IaC and how to use Templates to automate resource creation.<br>- Create a **Key Pair** and practice setting up a secure SSH connection to an EC2 Instance. | 02/05/2026 | 02/05/2026 | AWS CloudFormation Guide |

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
