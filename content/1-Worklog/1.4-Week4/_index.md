---
title: "Week 4 Worklog"
date: 2026-05-04
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Week 4 Objectives:
* Use **AWS CloudFormation** to fully automate the provisioning of complex network infrastructure (IaC).
* Set up a **Hybrid DNS** system with **Route 53 Resolver** to synchronize DNS resolution between AWS and On-premises environments.
* Securely connect two VPCs using **VPC Peering** and control cross-network traffic with Security Group/NACL.
* Begin researching **Amazon EC2** architecture: Differentiating chip types (Intel, AMD, Graviton) and the Nitro virtualization system.
* Explore **Transit Gateway (TGW)** as a scalable alternative to complex VPC Peering meshes.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| Mon | - Create a **Key Pair** and use a CloudFormation Template to quickly provision a complete network system including VPC, Subnets, and Security Groups.<br>- Configure detailed Security Groups for Windows servers in a Multi-AZ environment. | 04/05/2026 | 04/05/2026 | AWS Study Group |
| Tue | - Research and configure **Route 53 Resolver Inbound/Outbound Endpoints**.<br>- Create Forwarding Rules to synchronize DNS resolution between the Cloud and On-premises infrastructure. | 05/05/2026 | 05/05/2026 | AWS Networking Guide |
| Wed | - Initiate a **VPC Peering Connection** between 2 VPCs for inter-network communication without traversing the public internet.<br>- Configure bidirectional route tables to allow traffic to flow through the Peering connection. | 06/05/2026 | 06/05/2026 | AWS Documentation |
| Thu | - Test cross-network traffic security through NACLs and Security Groups.<br>- Deploy a simulated **Microsoft AD** and set up cross-domain DNS in a Hybrid model. | 07/05/2026 | 07/05/2026 | AWS Documentation |
| Fri | - Research the **AWS Transit Gateway** architecture: Hub-and-spoke topology and benefits over pure VPC Peering.<br>- Understand how the TGW Route Table manages traffic between multiple Attachments. | 08/05/2026 | 08/05/2026 | AWS Module 02 |
| Sat | - Consolidate lab screenshots, review all CloudFormation, Route 53, and VPC Peering configurations.<br>- Study EC2 Instance Types and when to choose Graviton chips for cost optimization. | 09/05/2026 | 09/05/2026 | Personal |

### Week 4 Achievements:

* **Infrastructure Automation (IaC):**
    * Mastered using **CloudFormation** to reproduce a complete network infrastructure from a single Template, saving time and reducing manual configuration errors.
    * Understood the structure of a CloudFormation Template and how to use Parameters, Resources, and Outputs.
* **Hybrid DNS System:**
    * Successfully configured **Route 53 Resolver**, allowing AWS resources to resolve On-premises internal domain names and vice versa.
    * Mastered the operation of Inbound/Outbound Endpoints for cross-environment DNS request routing.
* **Advanced Network Connectivity:**
    * Successfully deployed **VPC Peering**, ensuring data travels over AWS's internal backbone network for greater speed and security.
    * Understood the limitation of Peering (non-transitive routing) and when to upgrade to Transit Gateway for larger scale.

{{% notice info %}}
**Summary:** Week 4 shifts the mindset from managing individual resources to designing large-scale systems, connecting multiple environments (Cloud + On-premise), and automating infrastructure — core skills for a professional Cloud Engineer.
{{% /notice %}}
