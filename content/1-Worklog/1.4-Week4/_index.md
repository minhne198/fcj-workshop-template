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
| Mon | - Learn about AWS CloudFormation and Multi-AZ network infrastructure<br>- **Practice:**<br>&nbsp;&nbsp;+ Create Key Pair<br>&nbsp;&nbsp;+ Deploy VPC, Subnets, and Security Groups with CloudFormation Template<br>&nbsp;&nbsp;+ Configure Security Groups for Windows servers | 04/05/2026 | 04/05/2026 | AWS Study Group |
| Tue | - Learn about Route 53 Resolver and Hybrid DNS<br>- **Practice:**<br>&nbsp;&nbsp;+ Configure Inbound Endpoint<br>&nbsp;&nbsp;+ Configure Outbound Endpoint<br>&nbsp;&nbsp;+ Create Forwarding Rules to synchronize DNS between Cloud and On-premises | 05/05/2026 | 05/05/2026 | AWS Networking Guide |
| Wed | - Learn about VPC Peering Connection<br>- **Practice:**<br>&nbsp;&nbsp;+ Create VPC Peering Connection between 2 VPCs<br>&nbsp;&nbsp;+ Configure bidirectional Route Tables<br>&nbsp;&nbsp;+ Verify traffic through the Peering Connection | 06/05/2026 | 06/05/2026 | AWS Documentation |
| Thu | - Learn about cross-network traffic security and Hybrid DNS model<br>- **Practice:**<br>&nbsp;&nbsp;+ Test NACLs and Security Groups between networks<br>&nbsp;&nbsp;+ Deploy a simulated Microsoft AD environment<br>&nbsp;&nbsp;+ Set up cross-domain DNS in the Hybrid model | 07/05/2026 | 07/05/2026 | AWS Documentation |
| Fri | - Learn about AWS Transit Gateway (TGW)<br>- **Practice:**<br>&nbsp;&nbsp;+ Analyze hub-and-spoke architecture<br>&nbsp;&nbsp;+ Compare TGW with VPC Peering<br>&nbsp;&nbsp;+ Learn how TGW Route Tables control traffic between Attachments | 08/05/2026 | 08/05/2026 | AWS Module 02 |
| Sat | - Learn about EC2 Instance Types and Graviton chips<br>- **Practice:**<br>&nbsp;&nbsp;+ Review CloudFormation configurations<br>&nbsp;&nbsp;+ Review Route 53 Resolver and VPC Peering<br>&nbsp;&nbsp;+ Consolidate Week 4 lab screenshots | 09/05/2026 | 09/05/2026 | Personal |

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

### Week 4 practice screenshots:

![Configure Week 4 VPC infrastructure](/images/worklog/Screenshot%202026-05-20%20152142.jpg)

![Create VPC with CloudFormation](/images/worklog/Tao_VPCs.png.jpg)
