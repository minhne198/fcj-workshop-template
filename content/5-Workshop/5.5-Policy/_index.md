---
title : "Create data layer and system configuration"
date : 2024-01-01
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---

## Objective

This step creates data services and runtime configuration for AWS_OmniStay, including Amazon RDS MySQL, Amazon ElastiCache Redis/Valkey, Secrets Manager, Parameter Store, and S3 buckets for deployment. These components allow the backend to connect to the database, use cache, and read production configuration.

## 1. Create DB Subnet Group for RDS

Go to **RDS** -> **Subnet groups** -> **Create DB subnet group**.

Configuration:

| Field | Value |
| --- | --- |
| Name | `omnistay-db-subnet-group` |
| Description | `Private data subnets for OmniStay RDS` |
| VPC | `omnistay-vpc` |
| Subnets | `omnistay-data-a`, `omnistay-data-b` |

The DB subnet group allows RDS to run in private data subnets instead of public subnets.

![VPC details](/images/551.jpg)
<p align="center"><em>Figure 5.5.1: DB Subnet Group.</em></p>

## 2. Create RDS MySQL

Go to **RDS** -> **Databases** -> **Create database**.

Main configuration:

| Field | Value |
| --- | --- |
| Creation method | Standard create |
| Engine | MySQL |
| Template | Free tier if available; otherwise choose Dev/Test |
| DB instance identifier | `omnistay-mysql` |
| Master username | `admin` |
| Master password | Create a strong password and store it separately |
| Storage | `20 GiB` |
| VPC | `omnistay-vpc` |
| DB subnet group | `omnistay-db-subnet-group` |
| Public access | No |
| Security group | `SG-RDS` |
| Initial database name | `hotel_booking` |
| Backup retention | 1-7 days |

After the database status becomes `Available`, record the endpoint and port `3306` for backend configuration.

## 3. Create Cache Subnet Group for Redis/Valkey

Go to **ElastiCache** -> **Subnet groups** -> **Create subnet group**.

Configuration:

| Field | Value |
| --- | --- |
| Name | `omnistay-cache-subnet-group` |
| VPC | `omnistay-vpc` |
| Subnets | `omnistay-data-a`, `omnistay-data-b` |

## 4. Create ElastiCache Redis/Valkey

Go to **ElastiCache** -> **Create cluster**.

Configuration:

| Field | Value |
| --- | --- |
| Engine | Valkey or Redis OSS |
| Name | `omnistay-cache` |
| Cluster mode | Disabled |
| Node type | Smallest type that fits the budget |
| Replicas | 0 for a cost-saving demo |
| Port | 6379 |
| VPC | `omnistay-vpc` |
| Subnet group | `omnistay-cache-subnet-group` |
| Security group | `SG-Redis` |

When the cluster reaches `Available`, record the endpoint. If transit encryption is enabled, the connection string should include `ssl=True`.

Example placeholder:

```text
<redis-endpoint>:6379,ssl=True,abortConnect=false
```

![VPC details](/images/552.png)
<p align="center"><em>Figure 5.5.2: ElastiCache cluster `omnistay-cache`.</em></p>

## 5. Create Secrets Manager entry for database information

Go to **Secrets Manager** -> **Store a new secret**.

Configuration:

| Field | Value |
| --- | --- |
| Secret type | Other type of secret |
| Secret name | `omnistay/prod/hotelbookingdb` |

Suggested key/value pairs:

| Key | Value |
| --- | --- |
| `username` | `admin` |
| `password` | `<database-password>` |
| `host` | `<rds-endpoint>` |
| `port` | `3306` |
| `database` | `hotel_booking` |

When taking screenshots, capture only secret metadata and do not open secret values.

## 6. Create Parameter Store values for runtime configuration

Go to **Systems Manager** -> **Parameter Store** -> **Create parameter**.

Parameters to create:

| Name | Type | Value |
| --- | --- | --- |
| `/omnistay/prod/Database__Provider` | String | `MySql` |
| `/omnistay/prod/AWS__Region` | String | `ap-southeast-1` |
| `/omnistay/prod/Cache__SearchTtlSeconds` | String | `120` |
| `/omnistay/prod/AWS__S3FrontendBucket` | String | `<frontend-bucket-name>` |
| `/omnistay/prod/AWS__CloudFrontDomain` | String | `<cloudfront-domain>` |
| `/omnistay/prod/Jwt__Secret` | SecureString | `<jwt-secret>` |
| `/omnistay/prod/Admin__SeedPassword` | SecureString | `<admin-password>` |

If CloudFront is not created at this step, the parameter `/omnistay/prod/AWS__CloudFrontDomain` can be left empty and updated later when the domain is available.

## 7. Create S3 buckets for frontend and artifacts

Go to **S3** -> **Create bucket**.

Create the frontend bucket:

| Field | Value |
| --- | --- |
| Bucket name | `omnistay-frontend-<account-id>` |
| Region | `ap-southeast-1` |
| Object ownership | Bucket owner enforced |
| Block Public Access | On for all settings |
| Encryption | SSE-S3 |

Create the artifact bucket:

| Field | Value |
| --- | --- |
| Bucket name | `omnistay-artifacts-<account-id>` |
| Region | `ap-southeast-1` |
| Object ownership | Bucket owner enforced |
| Block Public Access | On for all settings |
| Encryption | SSE-S3 |

The frontend bucket stores static files. The artifact bucket stores the backend publish `.zip` file so EC2 can download it during startup.

![VPC details](/images/553.png)
<p align="center"><em>Figure 5.5.3: S3 buckets for frontend and artifacts.</em></p>

## Expected Result

After this step, the system has a MySQL database, Redis/Valkey cache, secret/runtime configuration storage, and two S3 buckets for application deployment. The backend in the next step will use these values to connect to RDS, connect to Redis, and download the artifact from S3.
