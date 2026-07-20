---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Deploying AWS OmniStay on AWS

This Workshop section documents the process of deploying the **AWS_OmniStay** hotel booking website to Amazon Web Services step by step. The content focuses on infrastructure setup, backend deployment, frontend deployment, security configuration, system testing, and collecting screenshots as implementation evidence.

The system is deployed using a multi-tier architecture:

- The static frontend is stored in a private Amazon S3 bucket and distributed through Amazon CloudFront.
- The ASP.NET Core Web API backend runs on Amazon EC2 instances in private subnets.
- Application Load Balancer receives requests from CloudFront and forwards them to the backend.
- Auto Scaling Group manages the number of backend EC2 instances.
- Amazon RDS MySQL stores business data.
- Amazon ElastiCache Redis/Valkey provides caching for hotel search flows.
- AWS WAF, IAM, Security Groups, Secrets Manager, Parameter Store, and CloudWatch support security, configuration, and operations.

## Contents

1. [Introduction](5.1-Workshop-overview/)
2. [Prerequisites before deployment](5.2-Prerequiste/)
3. [Build AWS network infrastructure](5.3-S3-vpc/)
4. [Configure network security and access permissions](5.4-S3-onprem/)
5. [Create data layer and system configuration](5.5-Policy/)
6. [Deploy Backend API to AWS](5.6-Cleanup/)
7. [Deploy Frontend to S3 and CloudFront](5.7-frontend-cloudfront/)
8. [Configure WAF, monitoring, and alerts](5.8-waf-monitoring/)
9. [Post-deployment system testing](5.9-system-testing/)

## Screenshot Note Convention

During the deployment steps, screenshot evidence is inserted directly below the related instruction. These screenshots are collected from the AWS Console, browser, and terminal to prove each implementation result.
