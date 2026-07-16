---
title : "Tạo tầng dữ liệu và cấu hình hệ thống"
date : 2024-01-01
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---

## Mục tiêu

Bước này tạo các dịch vụ dữ liệu và cấu hình runtime cho AWS_OmniStay, gồm Amazon RDS MySQL, Amazon ElastiCache Redis/Valkey, Secrets Manager, Parameter Store và các S3 bucket phục vụ deploy. Đây là nền tảng để backend có thể kết nối database, dùng cache và đọc cấu hình production.

## 1. Tạo DB Subnet Group cho RDS

Vào **RDS** -> **Subnet groups** -> **Create DB subnet group**.

Cấu hình:

| Trường | Giá trị |
| --- | --- |
| Name | `omnistay-db-subnet-group` |
| Description | `Private data subnets for OmniStay RDS` |
| VPC | `omnistay-vpc` |
| Subnets | `omnistay-data-a`, `omnistay-data-b` |

DB subnet group giúp RDS chạy trong private data subnets thay vì public subnet.


![VPC details](/images/551.jpg)
<p align="center"><em>Hình 5.5.1: DB Subnet Group.</em></p>

## 2. Tạo RDS MySQL

Vào **RDS** -> **Databases** -> **Create database**.

Cấu hình chính:

| Trường | Giá trị |
| --- | --- |
| Creation method | Standard create |
| Engine | MySQL |
| Template | Free tier nếu có, nếu không chọn Dev/Test |
| DB instance identifier | `omnistay-mysql` |
| Master username | `admin` |
| Master password | Tạo mật khẩu mạnh và lưu riêng |
| Storage | `20 GiB` |
| VPC | `omnistay-vpc` |
| DB subnet group | `omnistay-db-subnet-group` |
| Public access | No |
| Security group | `SG-RDS` |
| Initial database name | `hotel_booking` |
| Backup retention | 1-7 ngày |

Sau khi database chuyển sang trạng thái `Available`, ghi lại endpoint và port `3306` để cấu hình backend.


## 3. Tạo Cache Subnet Group cho Redis/Valkey

Vào **ElastiCache** -> **Subnet groups** -> **Create subnet group**.

Cấu hình:

| Trường | Giá trị |
| --- | --- |
| Name | `omnistay-cache-subnet-group` |
| VPC | `omnistay-vpc` |
| Subnets | `omnistay-data-a`, `omnistay-data-b` |


## 4. Tạo ElastiCache Redis/Valkey

Vào **ElastiCache** -> **Create cluster**.

Cấu hình:

| Trường | Giá trị |
| --- | --- |
| Engine | Valkey hoặc Redis OSS |
| Name | `omnistay-cache` |
| Cluster mode | Disabled |
| Node type | Loại nhỏ nhất phù hợp ngân sách |
| Replicas | 0 cho demo tiết kiệm |
| Port | 6379 |
| VPC | `omnistay-vpc` |
| Subnet group | `omnistay-cache-subnet-group` |
| Security group | `SG-Redis` |

Khi cluster ở trạng thái `Available`, ghi lại endpoint. Nếu bật transit encryption, connection string cần có `ssl=True`.

Ví dụ placeholder:

```text
<redis-endpoint>:6379,ssl=True,abortConnect=false
```

> **Ảnh cần dán:** ElastiCache cluster `omnistay-cache` có status `Available`.
>
> **Ảnh cần dán:** Endpoint, port, subnet group và security group của Redis/Valkey.

![VPC details](/images/552.png)
<p align="center"><em>Hình 5.5.2: ElastiCache cluster `omnistay-cache`.</em></p>

## 5. Tạo Secrets Manager cho thông tin database

Vào **Secrets Manager** -> **Store a new secret**.

Cấu hình:

| Trường | Giá trị |
| --- | --- |
| Secret type | Other type of secret |
| Secret name | `omnistay/prod/hotelbookingdb` |

Key/value gợi ý:

| Key | Value |
| --- | --- |
| `username` | `admin` |
| `password` | `<database-password>` |
| `host` | `<rds-endpoint>` |
| `port` | `3306` |
| `database` | `hotel_booking` |

Khi chụp ảnh, chỉ chụp metadata của secret, không mở phần secret value.


## 6. Tạo Parameter Store cho cấu hình runtime

Vào **Systems Manager** -> **Parameter Store** -> **Create parameter**.

Các parameter cần tạo:

| Name | Type | Value |
| --- | --- | --- |
| `/omnistay/prod/Database__Provider` | String | `MySql` |
| `/omnistay/prod/AWS__Region` | String | `ap-southeast-1` |
| `/omnistay/prod/Cache__SearchTtlSeconds` | String | `120` |
| `/omnistay/prod/AWS__S3FrontendBucket` | String | `<frontend-bucket-name>` |
| `/omnistay/prod/AWS__CloudFrontDomain` | String | `<cloudfront-domain>` |
| `/omnistay/prod/Jwt__Secret` | SecureString | `<jwt-secret>` |
| `/omnistay/prod/Admin__SeedPassword` | SecureString | `<admin-password>` |

Nếu CloudFront chưa tạo ở bước này, có thể để trống hoặc cập nhật lại parameter `/omnistay/prod/AWS__CloudFrontDomain` sau khi có domain.


## 7. Tạo S3 buckets cho frontend và artifact

Vào **S3** -> **Create bucket**.

Tạo frontend bucket:

| Trường | Giá trị |
| --- | --- |
| Bucket name | `omnistay-frontend-<account-id>` |
| Region | `ap-southeast-1` |
| Object ownership | Bucket owner enforced |
| Block Public Access | On tất cả |
| Encryption | SSE-S3 |

Tạo artifact bucket:

| Trường | Giá trị |
| --- | --- |
| Bucket name | `omnistay-artifacts-<account-id>` |
| Region | `ap-southeast-1` |
| Object ownership | Bucket owner enforced |
| Block Public Access | On tất cả |
| Encryption | SSE-S3 |

Frontend bucket dùng để lưu static files. Artifact bucket dùng để lưu file backend publish `.zip` để EC2 tải về khi khởi động.


![VPC details](/images/553.png)
<p align="center"><em>Hình 5.5.3: S3 buckets có frontend bucket và artifact bucket.</em></p>

## Kết quả cần đạt

Sau bước này, hệ thống có database MySQL, Redis/Valkey cache, nơi lưu secret/cấu hình runtime và 2 S3 bucket phục vụ triển khai ứng dụng. Backend ở bước sau sẽ dùng các giá trị này để kết nối RDS, Redis và tải artifact từ S3.
