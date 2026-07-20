---
title: "Blog 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

# 7 Ways to Optimize Cost When Deploying Applications on AWS

One of the biggest lessons I learned while studying and deploying applications on AWS is that **cost must be considered from the system design stage**. At first, I only focused on making the application run stably. But when I started using more services, I realized that poor resource management can cause costs to become higher than expected.

According to the **AWS Well-Architected Framework**, **Cost Optimization** is one of the key pillars alongside security, reliability, performance efficiency, operational excellence, and sustainability. This shows that cost optimization is not about blindly cutting resources; it is about using the right service, the right configuration, and the right timing.

In this blog, I share 7 practical experiences for optimizing cost when deploying applications on AWS, especially for students and beginners learning cloud computing.

---

## 1. Only use services when they are truly needed

When I first learned AWS, I was overwhelmed by the number of services the platform provides. Because I wanted the architecture to look more "professional", I thought the system needed CloudFront, AWS WAF, Auto Scaling, NAT Gateway, and Amazon ElastiCache from the beginning.

However, for small applications or student projects, using too many services does not bring much value. It increases cost and makes the system harder to manage.

![alt text](image.png)
> **Figure 1. Comparison between an architecture using too many services and a minimal architecture following the "Start Simple, Scale Later" principle.**

> **Best Practice:** Deploy only services that meet current system requirements. When user traffic increases or new needs appear, expand the architecture gradually.

---

## 2. Take advantage of AWS Free Tier

AWS Free Tier provides many services for free within certain limits, such as Amazon EC2, Amazon S3, Amazon RDS, and AWS Lambda. This is very suitable for learning, practicing, and building small projects.

During usage, I always check whether the selected service and configuration are still within Free Tier limits before creating resources.

> **Best Practice:** Always check AWS Free Tier policies before creating resources to reduce unexpected charges.

---

## 3. Stop or delete resources when they are no longer used

After finishing a lab or test deployment, many people forget to clean up AWS resources.

Examples:

- Amazon EC2 can still generate Amazon EBS storage cost even when stopped.
- Elastic IP not attached to a running EC2 instance can still be charged.
- Unused Snapshots or EBS Volumes continue to generate storage cost.

Regularly checking and cleaning up resources can significantly reduce operating cost.

> **Best Practice:** After each practice session or test deployment, check and delete resources that are no longer needed.

---

## 4. Track cost with AWS Budgets and AWS Cost Explorer

Cost control should be done regularly instead of waiting until the end of the month to check the bill.

AWS Budgets allows users to set budgets and send email alerts when cost exceeds configured thresholds. AWS Cost Explorer provides visual charts for tracking cost by service, account, or time period.

With these two tools, I can quickly identify which service is consuming the most cost and adjust it in time.

![alt text](image-1.png)
> **Figure 2. Cost tracking and management process using AWS Budgets and AWS Cost Explorer.**

> **Best Practice:** Set up AWS Budgets from the start of the project and monitor cost regularly with AWS Cost Explorer.

---

## 5. Choose the right resource size

In cloud computing, the strongest configuration is not always the best choice. What matters is selecting a configuration that matches the actual workload.

For learning environments or small websites, Amazon EC2 instance types such as `t2.micro` or `t3.micro` are often enough. Similarly, many applications only need Amazon RDS MySQL instead of Aurora.

Choosing the right configuration helps use resources efficiently and significantly reduce operating cost.

> **Best Practice:** Start with a small configuration, monitor performance, and upgrade only when the system truly needs it.

---

## 6. Manage data lifecycle and optimize storage

Storage growth over time is also a common reason for increasing cost.

For Amazon S3, I often configure **Lifecycle Rules** to automatically move infrequently accessed data to lower-cost storage classes such as **S3 Glacier Flexible Archive** or **S3 Glacier Deep Archive**. I also regularly check and delete unused Snapshots or EBS Volumes.

> **Best Practice:** Use Lifecycle Rules for Amazon S3 and periodically clean up storage resources that are no longer needed.

---

## 7. Choose a suitable Region and keep the design simple before scaling

The cost of the same AWS service can vary between Regions. Therefore, choosing a suitable Region not only reduces latency but also helps optimize cost.

I also realized that a simple architecture using Amazon EC2, Amazon RDS, Amazon S3, and Application Load Balancer is already enough for most small applications. Auto Scaling, CloudFront, or AWS WAF should only be added when the system grows and has more users.

![alt text](image-2.png)
> **Figure 3. Resource and cost optimization process throughout the AWS system deployment lifecycle.**

> **Best Practice:** Apply the **Start Simple, Scale Later** principle and expand the system only when there is real demand.

---

# Lessons Learned

Through AWS study and practice, I realized that cost optimization is not simply reducing budget. It is about using resources reasonably and efficiently.

Key lessons I learned:

- Deploy only the services that are truly necessary.
- Make the most of AWS Free Tier during learning.
- Regularly clean up unused resources.
- Track cost with AWS Budgets and AWS Cost Explorer.
- Choose the right resource size and Region.
- Design a simple architecture first, then expand when the system grows.

These principles are also the foundation of the **Cost Optimization** pillar in the AWS Well-Architected Framework.

---

# Conclusion

Cost optimization is an important skill when deploying systems on AWS. A good architecture must not only ensure performance, security, and scalability, but also use resources reasonably to avoid unnecessary cost.

For me, building the habit of tracking cost, choosing the right services, and managing resources from the beginning made my AWS learning and deployment process much more effective. I hope the experiences shared in this blog give beginners a practical perspective for designing systems that meet technical requirements while optimizing deployment budget.
