---
title : "Prerequisites before deployment"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---

## Objective

Before creating AWS resources, the working environment, naming conventions, budget, source code, and implementation values must be prepared. This preparation step helps reduce configuration mistakes when working with many connected services such as VPC, EC2, RDS, Redis, S3, CloudFront, and CloudWatch.

## Preparation Scope

This step covers the following tasks:

- Define the deployment region and resource naming convention.
- Check the AWS_OmniStay source code locally.
- Prepare tools for building, deploying, and testing.
- Create an AWS Budget to control costs during the workshop.
- Define security rules for documentation, especially avoiding passwords, secret keys, and tokens in the report.

![VPC details](/images/cautrucOmniStay.jpg)
<p align="center"><em>Figure 5.2.1: AWS_OmniStay folder structure.</em></p>

## 1. Define region and naming convention

The workshop uses region `ap-southeast-1` for the main resources. Resources use the `omnistay` prefix so they are easy to identify and filter when checking cost.

| Resource group | Name used in the workshop |
| --- | --- |
| VPC | `omnistay-vpc` |
| Public subnet | `omnistay-public-a`, `omnistay-public-b` |
| Private app subnet | `omnistay-app-a`, `omnistay-app-b` |
| Private data subnet | `omnistay-data-a`, `omnistay-data-b` |
| Application Load Balancer | `omnistay-alb` |
| Target Group | `omnistay-api-tg` |
| Auto Scaling Group | `omnistay-api-asg` |
| RDS MySQL | `omnistay-mysql` |
| ElastiCache Redis/Valkey | `omnistay-cache` |
| Frontend bucket | `omnistay-frontend-<account-id>` |
| Artifact bucket | `omnistay-artifacts-<account-id>` |

Recommended tags:

| Key | Value |
| --- | --- |
| `Project` | `AWS_OmniStay` |
| `Environment` | `demo` |
| `Owner` | Student name or student ID |

![VPC details](/images/522.jpg)
<p align="center"><em>Figure 5.2.2: AWS Console with region `ap-southeast-1` selected.</em></p>

## 2. Create AWS Budget for cost control

Some services such as NAT Gateway, ALB, RDS, ElastiCache, WAF, and public IPv4 can generate hourly charges. Therefore, the budget should be created before deployment.

Steps:

1. Go to **Billing and Cost Management**.
2. Select **Budgets**.
3. Select **Create budget**.
4. Select **Monthly cost budget**.
5. Set the budget name to `omnistay-monthly-budget`.
6. Set the demo budget to `10 USD`.
7. Configure alerts at 50%, 80%, and 100%.
8. Enter the alert recipient email and create the budget.

![VPC details](/images/523.jpg)
<p align="center"><em>Figure 5.2.3: Creating a Budget.</em></p>

## 3. Prepare deployment tools

Tools needed on the local machine:

| Tool | Purpose |
| --- | --- |
| .NET SDK | Build and publish the ASP.NET Core Web API |
| Git | Manage source code |
| AWS CLI | Upload artifacts, inspect resources, and support deployment |
| Visual Studio Code | Edit source code and documentation |
| DBeaver or MySQL client | Check data in RDS MySQL |
| Browser | Test the public website through CloudFront |

Main source code paths:

```text
backend/src/HotelBooking.Api
frontend/public
frontend/src
```

The backend is an ASP.NET Core Web API. The frontend is a static web application built with HTML, CSS, and JavaScript. In production deployment, the frontend reads API configuration from `frontend/public/config.js`.

![VPC details](/images/524.jpg)
<p align="center"><em>Figure 5.2.4: Project folders `backend`, `frontend`, and `docs`.</em></p>

## 4. Documentation security rules

During deployment, do not write the following information directly in the report:

- AWS access key or secret access key.
- RDS password.
- JWT secret.
- Production admin password.
- Payment token or webhook secret.
- Secret value contents from Secrets Manager.

Sensitive values should be stored separately outside the repository or in Secrets Manager/Parameter Store. In the report, use placeholders such as `<database-password>`, `<jwt-secret>`, and `<cloudfront-domain>`.

## 5. Values to record

During deployment, record the following values for later steps:

| Value | Purpose |
| --- | --- |
| `ARTIFACT_BUCKET` | Location for uploading the backend publish `.zip` file |
| `FRONTEND_BUCKET` | Location for uploading frontend static files |
| `RDS_ENDPOINT` | Backend connection to MySQL |
| `REDIS_ENDPOINT` | Backend connection to Redis/Valkey |
| `ALB_DNS` | Test backend through the Load Balancer |
| `CLOUDFRONT_DOMAIN` | Access the public website |
| `TARGET_GROUP_NAME` | Check backend health checks |
| `ASG_NAME` | Manage the number of backend EC2 instances |

## Expected Result

After this preparation step, the implementer has the required local tools, knows the deployment region, has a cost-control budget, and has a clear naming convention. The next steps start by building the foundational network infrastructure for the system.
