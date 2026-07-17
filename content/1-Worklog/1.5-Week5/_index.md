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
| Mon | - Use CloudFormation to provision 4 VPCs and sample servers within each VPC.<br>- Set up **AWS Transit Gateway**, create Attachments, and plan the TGW route tables. | 11/05/2026 | 11/05/2026 | AWS Module 02 |
| Tue | - Configure routing in each VPC to point traffic towards the TGW.<br>- Use **Reachability Analyzer** to test connectivity and analyze packet flow between Private Subnets. | 12/05/2026 | 12/05/2026 | AWS Module 02 |
| Wed | - Study EC2 Instance Types, the advantages of **ARM Graviton** chips vs. Intel/AMD, and the **Nitro** virtualization system.<br>- Differentiate between Full vs. Incremental Snapshot mechanisms and their practical applications. | 13/05/2026 | 13/05/2026 | AWS Module 03 |
| Thu | - Practice configuring **User Data** to automatically install a Web Server (Apache/Nginx) on first EC2 boot.<br>- Experiment with querying **Instance Metadata** via the internal IP address `169.254.169.254`. | 14/05/2026 | 14/05/2026 | AWS Module 03 |
| Fri | - Explore the **Auto Scaling Group** mechanism: Scale-out/scale-in conditions based on CPU metrics.<br>- Create the first **Amazon S3 Bucket** and practice basic upload/download object operations. | 15/05/2026 | 15/05/2026 | AWS Module 03 |
| Sat | - Compare performance and durability between **EBS** and **Instance Store**; choose the right type based on workload.<br>- Clean up resources: Delete TGW Attachments → TGW → CloudFormation Stack in the correct order to avoid unwanted charges. | 16/05/2026 | 16/05/2026 | Personal |

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
