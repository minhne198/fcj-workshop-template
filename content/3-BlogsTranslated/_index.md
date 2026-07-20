---
title: "Translated Blogs"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

During my internship and my study of **Amazon Web Services (AWS)**, I researched and summarized several articles related to architecture design, application deployment, and practical experience when working with cloud computing environments. The blogs below were built from my learning process, hands-on practice, and references to official AWS documentation. They helped me strengthen my knowledge, improve my system design mindset, and better understand deployment principles on the Cloud.

Each blog focuses on a different topic, from system architecture design workflows and security principles to selecting suitable AWS services and avoiding common mistakes when deploying applications. These topics are valuable for learning AWS in a practical way and applying the knowledge to future projects.

---

### [Blog 1 - From Requirements to Architecture: Designing a Web System on AWS](3.1-Blog1/)

This blog presents the architecture design process for a web system on AWS, starting from requirement analysis and service selection to using services such as **Amazon VPC, Amazon EC2, Amazon RDS, Amazon S3, Application Load Balancer**, and **AWS IAM**. It also discusses important design decisions related to **Public/Private Subnet** separation, system security, scalability, high availability, and cost optimization when deploying applications on AWS.

---

### [Blog 2 - 7 Common Mistakes Beginners Make When Deploying Their First Web Application on AWS](3.2-Blog2/)

This blog summarizes common mistakes beginners often make when deploying applications on AWS, such as placing resources in the wrong VPC location, configuring **Security Groups** too broadly, using **Access Keys** instead of **IAM Roles**, storing data incorrectly, misunderstanding **Region**, **Availability Zone**, and **VPC**, and forgetting to monitor the system with **Amazon CloudWatch**. It also provides recommendations and **AWS Best Practices** for building systems that are secure, manageable, and scalable in real-world environments.

---

### [Blog 3 - 7 Ways to Optimize Cost When Deploying Applications on AWS](3.3-Blog3/)

This blog shares practical cost optimization experience when using AWS, including choosing the right services and resource configurations, using **AWS Free Tier**, managing data lifecycle on **Amazon S3**, tracking cost with **AWS Budgets** and **AWS Cost Explorer**, and cleaning up unused resources. It also introduces the **Start Simple, Scale Later** principle and the **Cost Optimization** pillar in the **AWS Well-Architected Framework**, helping readers build systems that meet technical requirements while using the deployment budget effectively.
