---
title : "Configure network security and access permissions"
date : 2024-01-01
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

## Objective

After the VPC and subnets are ready, the next step is to configure security for each layer of the system. AWS_OmniStay uses Security Groups to restrict traffic according to the expected flow:

```text
Internet -> CloudFront -> ALB -> EC2 backend -> RDS MySQL / Redis
```

The backend is not exposed directly to the internet. RDS and Redis also do not allow access from `0.0.0.0/0`; only backend EC2 instances can connect to the data layer.

## 1. Create Security Group for ALB

Go to **EC2** -> **Security Groups** -> **Create security group**.

Configuration:

| Field | Value |
| --- | --- |
| Security group name | `SG-ALB` |
| Description | `Allow public HTTP to ALB` |
| VPC | `omnistay-vpc` |

Inbound rule:

| Type | Port | Source | Purpose |
| --- | --- | --- | --- |
| HTTP | 80 | `0.0.0.0/0` | Allow users to access ALB over HTTP |

Keep the default **All traffic** outbound rule.

![VPC details](/images/541.jpg)
<p align="center"><em>Figure 5.4.1: Inbound rules of `SG-ALB`.</em></p>

## 2. Create Security Group for EC2 backend

Configuration:

| Field | Value |
| --- | --- |
| Security group name | `SG-EC2` |
| Description | `Allow ALB to API instances` |
| VPC | `omnistay-vpc` |

Inbound rule:

| Type | Port | Source | Purpose |
| --- | --- | --- | --- |
| Custom TCP | 8080 | `SG-ALB` | Only ALB can call the backend API |

With this configuration, the EC2 backend does not receive direct traffic from the internet. Requests must go through ALB before reaching the ASP.NET Core application.

![VPC details](/images/542.jpg)
<p align="center"><em>Figure 5.4.2: Inbound rules of `SG-EC2`.</em></p>

## 3. Create Security Group for RDS MySQL

Configuration:

| Field | Value |
| --- | --- |
| Security group name | `SG-RDS` |
| Description | `Allow EC2 to MySQL` |
| VPC | `omnistay-vpc` |

Inbound rule:

| Type | Port | Source | Purpose |
| --- | --- | --- | --- |
| MySQL/Aurora | 3306 | `SG-EC2` | Only backend EC2 can connect to MySQL |

![VPC details](/images/543.jpg)
<p align="center"><em>Figure 5.4.3: Inbound rules of `SG-RDS`.</em></p>

## 4. Create Security Group for Redis/Valkey

Configuration:

| Field | Value |
| --- | --- |
| Security group name | `SG-Redis` |
| Description | `Allow EC2 to Redis cache` |
| VPC | `omnistay-vpc` |

Inbound rule:

| Type | Port | Source | Purpose |
| --- | --- | --- | --- |
| Custom TCP | 6379 | `SG-EC2` | Only backend EC2 can connect to Redis |

![VPC details](/images/544.jpg)
<p align="center"><em>Figure 5.4.4: Inbound rules of `SG-Redis`.</em></p>

## 5. Create IAM Role for EC2 backend

The EC2 backend needs permission to read artifacts from S3, use Session Manager for server inspection, and send logs/metrics to CloudWatch. Do not use hard-coded access keys on EC2.

Go to **IAM** -> **Roles** -> **Create role**.

Configuration:

| Field | Value |
| --- | --- |
| Trusted entity | AWS service |
| Use case | EC2 |
| Role name | `EC2-HotelAPI-Role` |

Attach these policies:

| Policy | Purpose |
| --- | --- |
| `AmazonSSMManagedInstanceCore` | Connect to EC2 through Session Manager |
| `CloudWatchAgentServerPolicy` | Send logs/metrics to CloudWatch |
| `AmazonS3ReadOnlyAccess` | Allow EC2 to download backend artifacts from the S3 artifact bucket |

In a real production environment, S3 permissions should be restricted to the exact artifact bucket instead of using read-only access to all S3. In this demo scope, the configuration helps deploy quickly and inspect easily.

![VPC details](/images/545.png)
<p align="center"><em>Figure 5.4.5: `EC2-HotelAPI-Role`.</em></p>

## 6. Verify security layering rules

After creating the Security Groups, verify the opened ports:

| Layer | Open port | Valid source |
| --- | --- | --- |
| ALB | 80 | Internet |
| EC2 backend | 8080 | `SG-ALB` |
| RDS MySQL | 3306 | `SG-EC2` |
| Redis/Valkey | 6379 | `SG-EC2` |

Do not open public SSH/RDP unless necessary. When EC2 inspection is needed, prefer **AWS Systems Manager Session Manager** through the IAM Role.

## Expected Result

After this step, system layers are isolated according to their roles. ALB is the public entry point, backend EC2 runs in private subnets, and RDS/Redis only accept connections from the backend. EC2 has an IAM Role to fetch artifacts and support operations without storing access keys in source code.
