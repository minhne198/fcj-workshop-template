---
title : "Deploy Backend API to AWS"
date : 2024-01-01
weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---

## Objective

This step deploys the **ASP.NET Core Web API** backend of AWS_OmniStay to EC2 through Launch Template and Auto Scaling Group. The backend is placed behind Application Load Balancer, runs in private app subnets, and connects to RDS MySQL, Redis/Valkey, and the production configuration created in the previous step.

## 1. Publish backend locally

From the AWS_OmniStay source directory, run tests and publish the backend:

```powershell
dotnet test backend\AWSOmniStay.slnx --no-restore
dotnet publish backend\src\HotelBooking.Api\HotelBooking.Api.csproj -c Release -o C:\tmp\omnistay-publish
Compress-Archive -Path C:\tmp\omnistay-publish\* -DestinationPath C:\tmp\omnistay-api.zip -Force
```

Expected output:

```text
C:\tmp\omnistay-api.zip
```

![VPC details](/images/562.jpg)
<p align="center"><em>Figure 5.6.1: The file `C:\tmp\omnistay-api.zip` after publishing.</em></p>

## 2. Upload backend artifact to S3

Go to **S3** -> artifact bucket `omnistay-artifacts-<account-id>`.

Steps:

1. Select **Upload**.
2. Select **Add files**.
3. Select `C:\tmp\omnistay-api.zip`.
4. Upload the file to the bucket.
5. Record the object path:

```text
s3://omnistay-artifacts-<account-id>/omnistay-api.zip
```

![VPC details](/images/561.jpg)
<p align="center"><em>Figure 5.6.2: Object `omnistay-api.zip` in the artifact bucket.</em></p>

## 3. Create Target Group for backend

Go to **EC2** -> **Target Groups** -> **Create target group**.

Configuration:

| Field | Value |
| --- | --- |
| Target type | Instances |
| Target group name | `omnistay-api-tg` |
| Protocol | HTTP |
| Port | 8080 |
| VPC | `omnistay-vpc` |
| Health check protocol | HTTP |
| Health check path | `/health` |
| Success code | `200` |

At this point, manual target registration may be skipped because the Auto Scaling Group will register EC2 instances into the Target Group automatically.

![VPC details](/images/563.png)
<p align="center"><em>Figure 5.6.3: Target group details of `omnistay-api-tg`.</em></p>

## 4. Create Application Load Balancer

Go to **EC2** -> **Load Balancers** -> **Create load balancer** -> **Application Load Balancer**.

Configuration:

| Field | Value |
| --- | --- |
| Name | `omnistay-alb` |
| Scheme | Internet-facing |
| IP address type | IPv4 |
| VPC | `omnistay-vpc` |
| Subnets | `omnistay-public-a`, `omnistay-public-b` |
| Security group | `SG-ALB` |
| Listener | HTTP 80 |
| Default action | Forward to `omnistay-api-tg` |

After ALB becomes `Active`, record its DNS name for backend testing.

## 5. Create Launch Template for EC2 backend

Go to **EC2** -> **Launch Templates** -> **Create launch template**.

Basic configuration:

| Field | Value |
| --- | --- |
| Name | `omnistay-api-template` |
| AMI | Ubuntu 24.04 or Amazon Linux 2023 |
| Instance type | `t3.micro` or another small type that fits the budget |
| Security group | `SG-EC2` |
| IAM instance profile | `EC2-HotelAPI-Role` |
| Storage | 8-20 GiB |

User data should perform these main tasks:

1. Install AWS CLI and the required .NET runtime.
2. Create `/opt/omnistay/api`.
3. Download `omnistay-api.zip` from the S3 artifact bucket.
4. Extract the backend artifact.
5. Create a `systemd service` named `omnistay-api`.
6. Configure production environment variables such as database provider, connection string, Redis endpoint, JWT config, and AWS region.
7. Start the service and listen on port `8080`.

Example of important service environment variables:

```text
ASPNETCORE_ENVIRONMENT=Production
ASPNETCORE_URLS=http://0.0.0.0:8080
Database__Provider=MySql
ConnectionStrings__HotelBookingDb=<mysql-connection-string>
ConnectionStrings__Redis=<redis-endpoint>:6379,ssl=True,abortConnect=false
Cache__SearchTtlSeconds=120
AWS__Region=ap-southeast-1
AWS__S3FrontendBucket=<frontend-bucket-name>
```

Do not include real secrets in the report. For a quick demo, use placeholders in documentation and store real values separately outside the repository.

## 6. Create Auto Scaling Group

Go to **EC2** -> **Auto Scaling Groups** -> **Create Auto Scaling group**.

Configuration:

| Field | Value |
| --- | --- |
| Name | `omnistay-api-asg` |
| Launch template | `omnistay-api-template` |
| VPC | `omnistay-vpc` |
| Subnets | `omnistay-app-a`, `omnistay-app-b` |
| Target group | `omnistay-api-tg` |
| Health check | ELB health check if the Console allows selection |
| Health check grace period | 300 seconds |
| Desired capacity | 1 |
| Minimum capacity | 1 |
| Maximum capacity | 2 or 4 |
| Scaling policy | Target tracking |
| Metric | Average CPU utilization |
| Target value | 70 |

The Auto Scaling Group creates EC2 instances in private app subnets and automatically registers them with the Target Group.

![VPC details](/images/564.png)
<p align="center"><em>Figure 5.6.4: ASG attached to target group `omnistay-api-tg`.</em></p>

## 7. Check EC2 backend with Session Manager

If the target is not healthy, connect to EC2 through **Session Manager**:

```text
EC2 -> Instances -> select instance -> Connect -> Session Manager
```

Run these checks:

```bash
sudo tail -n 120 /var/log/cloud-init-output.log
sudo systemctl status omnistay-api --no-pager
curl -i http://localhost:8080/health
curl -i http://localhost:8080/health/aws
```

Expected result:

```text
Active: active (running)
HTTP/1.1 200 OK
```

## 8. Check Target Group and ALB

Go to **EC2** -> **Target Groups** -> `omnistay-api-tg` -> **Targets**.

Expected result:

```text
Healthy = 1
Unhealthy = 0
```

Then open the browser:

```text
http://<alb-dns>/health
http://<alb-dns>/health/aws
```

The `/health/aws` result should show that the backend is running in production and using configured MySQL and Redis:

```json
{
  "environment": "Production",
  "databaseProvider": "MySql",
  "redisConfigured": true,
  "redisConnected": true,
  "apiBasePath": "/api"
}
```

![VPC details](/images/565.jpg)
<p align="center"><em>Figure 5.6.5: Browser opens `/health/aws` through ALB and returns JSON successfully.</em></p>

## Expected Result

After this step, the backend API runs on EC2 in private subnets, is managed by Auto Scaling Group, receives traffic through ALB, and has working health checks. This is the foundation for CloudFront in the next step to forward `/api/*` requests to the backend.
