---
title: "Blog 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

# 7 Common Mistakes Beginners Make When Deploying Their First Web Application on AWS

While learning and deploying a web application on AWS, I realized that successfully creating Amazon EC2 or Amazon RDS is only the beginning. What matters more is understanding how services work together, how to build a secure architecture, and how to choose the right solution for each problem.

At first, I thought that making the application run was enough. However, after reading AWS documentation and practicing deployment, I realized that many seemingly small mistakes can directly affect system security, scalability, and operating cost.

Below are common mistakes that I personally encountered or often see among beginners learning AWS. I hope these experiences help others avoid similar issues when deploying systems.

---

### 1. Placing all resources in Public Subnets

When I first learned Amazon VPC, I thought placing Amazon EC2 and Amazon RDS in public subnets would be more convenient because I could access them directly from the Internet for testing and configuration.

![alt text](image.png)
> **Figure 1. Comparison between an unsafe deployment architecture and a recommended Public/Private Subnet architecture on AWS.**

In reality, this is a major security risk. Public subnets should only contain components that need to communicate directly with the Internet, such as Application Load Balancer or NAT Gateway. Important resources such as Amazon EC2 and Amazon RDS should be deployed in private subnets to limit direct external access.

> **Best Practice:** Design the network using a Public/Private Subnet model. Only services that need to receive or route Internet traffic should be placed in public subnets.

---

### 2. Opening Security Groups too broadly

A common mistake is configuring Security Groups with source `0.0.0.0/0` for many service ports just to make the system work faster.

![alt text](image-1.png)
> **Figure 2. Comparison between an unsafe Security Group configuration and a Least Privilege configuration.**

This configuration makes testing easier, but it significantly increases the risk of unauthorized access. Instead, each service should allow only the required connection source. For example, Application Load Balancer receives Internet traffic, Amazon EC2 only accepts connections from the Load Balancer Security Group, and Amazon RDS only accepts connections from the EC2 Security Group.

> **Best Practice:** Apply the **Least Privilege** principle by granting only the minimum required access to each system component.

---

### 3. Using Access Keys instead of IAM Roles

At first, I thought storing Access Key and Secret Access Key in a configuration file was the simplest way for an application to access Amazon S3.

![alt text](image-2.png)
> **Figure 3. Comparison between storing Access Keys in source code and using IAM Role for Amazon EC2.**

However, if the source code is accidentally made public or shared, those access keys can be exposed and the AWS account may be used without permission. For services running on AWS such as Amazon EC2, a better solution is to use IAM Role. IAM Role automatically provides temporary credentials for the application to access AWS services without storing fixed access keys in source code.

> **Best Practice:** Do not store Access Keys in source code. For EC2, Lambda, or ECS, use IAM Role to manage access permissions.

---

### 4. Storing images and files directly on EC2

When developing a web application, I used to store all images and uploaded files directly on the EC2 server, similar to running an application locally.

However, cloud architecture is designed toward a **Stateless** model. If an EC2 instance fails or is replaced by Auto Scaling, data stored on the server may no longer be available. Instead of storing files directly on EC2, Amazon S3 is a better choice because it provides durable storage, flexible scalability, and easy integration with other AWS services.

> **Best Practice:** Use Amazon S3 to store images, documents, and static files instead of storing them directly on the EC2 disk.

---

### 5. Confusing Region, Availability Zone, and VPC

When I first learned AWS, I often confused Region, Availability Zone (AZ), and VPC. This caused inaccurate architecture diagrams and incorrect placement of some services.

After studying further, I realized that a Region is a geographic area where services are deployed, an Availability Zone is an independent data center inside a Region, and a VPC is a virtual private network created in one Region and can span multiple AZs. Meanwhile, services such as Amazon S3 operate at the Region level, while AWS IAM is a Global service. Understanding the scope of each service helps design architecture correctly and avoid many deployment mistakes.

> **Best Practice:** Before designing a system, clearly identify whether each service operates at the Global, Region, or VPC level so the architecture can be arranged properly.

---

### 6. Not monitoring the system after deployment

Another mistake is focusing only on application deployment and forgetting to monitor system health.

When the application has errors or slow responses, not having logs and monitoring metrics makes root cause analysis much harder. Amazon CloudWatch helps collect logs, monitor CPU, network traffic, disk usage, and configure alerts when the system shows abnormal behavior. Monitoring from the beginning helps detect issues early and significantly reduces troubleshooting time.

> **Best Practice:** Configure Amazon CloudWatch from the beginning of deployment to track logs, performance, and alerts when needed.

---

### 7. Using too many AWS services before they are needed

When I first learned AWS, I thought a professional architecture had to include CloudFront, WAF, Auto Scaling, ElastiCache, and many other services.

However, every service increases cost, complexity, and management effort. For learning projects or small systems, using too many services is unnecessary. In my view, a good architecture is not the one with the most services, but the one that meets current requirements and can still scale flexibly in the future.

> **Best Practice:** Start with a simple architecture, then add more services when the system actually needs them.

---

# Lessons Learned

After learning and deploying applications on AWS, I realized that understanding individual services is not enough. The more important skill is combining them into an architecture that fits the system requirements.

Three principles I always keep in mind:

- **Design security from the beginning:** Separate public and private subnets, use Security Groups properly, and use IAM Roles correctly.
- **Design for scalability:** Separate application processing, database, and static data storage so the system can be upgraded more easily.
- **Choose suitable services:** Avoid deploying too many services if the application does not truly need them, in order to reduce cost and simplify management.

These principles help the architecture stay secure, easy to operate, and ready to scale when the system grows.

# Conclusion

Making mistakes while learning AWS is normal. What matters more is understanding the cause of each issue and gradually improving the architecture according to AWS recommendations.

Through deployment practice and documentation study, I realized that a good system must not only run stably but also ensure security, scalability, and cost optimization. I hope the experience shared in this blog helps beginners avoid common mistakes and become more confident when deploying their first application on AWS.
