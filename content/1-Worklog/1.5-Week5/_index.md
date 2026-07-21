---
title: "Week 5 Worklog"
date: 2026-05-11
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Week 5 Objectives:
* Deploy a **Hub-and-Spoke** network architecture using **AWS Transit Gateway (TGW)** to connect multiple VPCs efficiently and manageably.
* Practice **Infrastructure as Code (IaC)** with CloudFormation to provision complex infrastructure in minutes.
* Deep-dive into **Amazon EC2**: Instance types, Graviton chips, the Nitro virtualization system, and EBS vs. Instance Store storage.
* Automate server configuration using **User Data** and query instance information via **Instance Metadata**.
* Get started with **Amazon S3**: Create a Bucket and practice basic object storage operations.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| Mon | - Learn about Hub-and-Spoke networking with AWS Transit Gateway<br>- **Practice:**<br>&nbsp;&nbsp;+ Use CloudFormation to create 4 VPCs<br>&nbsp;&nbsp;+ Create sample servers in each VPC<br>&nbsp;&nbsp;+ Create Transit Gateway Attachments<br>&nbsp;&nbsp;+ Plan TGW route tables | 11/05/2026 | 11/05/2026 | AWS Module 02 |
| Tue | - Learn about routing through Transit Gateway<br>- **Practice:**<br>&nbsp;&nbsp;+ Configure each VPC Route Table to point to TGW<br>&nbsp;&nbsp;+ Use Reachability Analyzer to test connectivity<br>&nbsp;&nbsp;+ Analyze packet flow between Private Subnets | 12/05/2026 | 12/05/2026 | AWS Module 02 |
| Wed | - Learn about EC2 Instance Types, Graviton, Nitro, and Snapshots<br>- **Practice:**<br>&nbsp;&nbsp;+ Compare Intel, AMD, and ARM Graviton<br>&nbsp;&nbsp;+ Differentiate Full Snapshot and Incremental Snapshot<br>&nbsp;&nbsp;+ Note when to choose each Instance Type | 13/05/2026 | 13/05/2026 | AWS Module 03 |
| Thu | - Learn about User Data and Instance Metadata<br>- **Practice:**<br>&nbsp;&nbsp;+ Configure User Data to install Web Server automatically<br>&nbsp;&nbsp;+ Verify Apache/Nginx after EC2 startup<br>&nbsp;&nbsp;+ Query Instance Metadata through `169.254.169.254` | 14/05/2026 | 14/05/2026 | AWS Module 03 |
| Fri | - Learn about Auto Scaling Group and Amazon S3<br>- **Practice:**<br>&nbsp;&nbsp;+ Analyze scale-out/scale-in conditions based on CPU metrics<br>&nbsp;&nbsp;+ Create Amazon S3 Bucket<br>&nbsp;&nbsp;+ Upload and download basic objects | 15/05/2026 | 15/05/2026 | AWS Module 03 |
| Sat | - Learn about EBS, Instance Store, and resource cleanup process<br>- **Practice:**<br>&nbsp;&nbsp;+ Compare data durability between EBS and Instance Store<br>&nbsp;&nbsp;+ Delete TGW Attachments<br>&nbsp;&nbsp;+ Delete Transit Gateway<br>&nbsp;&nbsp;+ Delete CloudFormation Stack in the correct order | 16/05/2026 | 16/05/2026 | Personal |

### Week 5 Achievements:

* **Regarding Network Architecture:**
    * Replaced the complex VPC Peering model with **Transit Gateway**, enabling centralized management and easy scaling to dozens of VPCs.
    * Learned to use Reachability Analyzer to debug network connectivity visually, without manual ping-based trial and error.
* **Regarding Compute & Storage:**
    * Mastered cost optimization by selecting the right Instance type and leveraging ARM **Graviton** chips, saving up to 40% on compute costs.
    * Clearly understood the risk of data loss with **Instance Store** and the durability of **EBS** (data replicated within the same AZ).
    * Automated software deployment from the moment an EC2 instance is launched using User Data scripts.
* **Regarding Amazon S3:**
    * Understood the basics of S3's object storage model and how it differs from traditional file/block storage.

{{% notice warning %}}
**Important Note:** Transit Gateway charges per hour for each active Attachment. When deleting, follow the strict order: **TGW Attachments → Transit Gateway → CloudFormation Stack** to ensure no orphaned resources incur unexpected charges.
{{% /notice %}}

### Week 5 practice screenshots:

![Week 5 practice - 522](/images/522.jpg)

![Week 5 practice - 532](/images/532.jpg)
