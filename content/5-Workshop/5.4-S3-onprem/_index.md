---
title : "Cấu hình bảo mật mạng và quyền truy cập"
date : 2024-01-01
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

## Mục tiêu

Sau khi có VPC và subnet, bước tiếp theo là cấu hình lớp bảo mật cho từng tầng của hệ thống. AWS_OmniStay sử dụng Security Group để giới hạn traffic theo đúng luồng:

```text
Internet -> CloudFront -> ALB -> EC2 backend -> RDS MySQL / Redis
```

Backend không mở trực tiếp ra internet. RDS và Redis cũng không cho phép truy cập từ `0.0.0.0/0`; chỉ EC2 backend mới được kết nối đến các tầng dữ liệu.

## 1. Tạo Security Group cho ALB

Vào **EC2** -> **Security Groups** -> **Create security group**.

Cấu hình:

| Trường | Giá trị |
| --- | --- |
| Security group name | `SG-ALB` |
| Description | `Allow public HTTP to ALB` |
| VPC | `omnistay-vpc` |

Inbound rule:

| Type | Port | Source | Mục đích |
| --- | --- | --- | --- |
| HTTP | 80 | `0.0.0.0/0` | Cho phép người dùng truy cập ALB qua HTTP |

Outbound rule giữ mặc định **All traffic**.

> **Ảnh cần dán:** Inbound rules của `SG-ALB`, thể hiện port 80 mở từ `0.0.0.0/0`.

## 2. Tạo Security Group cho EC2 backend

Cấu hình:

| Trường | Giá trị |
| --- | --- |
| Security group name | `SG-EC2` |
| Description | `Allow ALB to API instances` |
| VPC | `omnistay-vpc` |

Inbound rule:

| Type | Port | Source | Mục đích |
| --- | --- | --- | --- |
| Custom TCP | 8080 | `SG-ALB` | Chỉ ALB được gọi vào API backend |

Với cấu hình này, EC2 backend không nhận traffic trực tiếp từ internet. Request phải đi qua ALB trước khi vào ứng dụng ASP.NET Core.

> **Ảnh cần dán:** Inbound rules của `SG-EC2`, thể hiện port 8080 chỉ nhận source từ `SG-ALB`.

## 3. Tạo Security Group cho RDS MySQL

Cấu hình:

| Trường | Giá trị |
| --- | --- |
| Security group name | `SG-RDS` |
| Description | `Allow EC2 to MySQL` |
| VPC | `omnistay-vpc` |

Inbound rule:

| Type | Port | Source | Mục đích |
| --- | --- | --- | --- |
| MySQL/Aurora | 3306 | `SG-EC2` | Chỉ backend EC2 được kết nối MySQL |

> **Ảnh cần dán:** Inbound rules của `SG-RDS`, thể hiện source là `SG-EC2`, không phải `0.0.0.0/0`.

## 4. Tạo Security Group cho Redis/Valkey

Cấu hình:

| Trường | Giá trị |
| --- | --- |
| Security group name | `SG-Redis` |
| Description | `Allow EC2 to Redis cache` |
| VPC | `omnistay-vpc` |

Inbound rule:

| Type | Port | Source | Mục đích |
| --- | --- | --- | --- |
| Custom TCP | 6379 | `SG-EC2` | Chỉ backend EC2 được kết nối Redis |

> **Ảnh cần dán:** Inbound rules của `SG-Redis`, thể hiện port 6379 chỉ nhận source từ `SG-EC2`.

## 5. Tạo IAM Role cho EC2 backend

EC2 backend cần quyền đọc artifact từ S3, dùng Session Manager để truy cập kiểm tra máy chủ và gửi log/metric lên CloudWatch. Không sử dụng access key hard-code trên EC2.

Vào **IAM** -> **Roles** -> **Create role**.

Cấu hình:

| Trường | Giá trị |
| --- | --- |
| Trusted entity | AWS service |
| Use case | EC2 |
| Role name | `EC2-HotelAPI-Role` |

Các policy cần gắn:

| Policy | Mục đích |
| --- | --- |
| `AmazonSSMManagedInstanceCore` | Kết nối EC2 qua Session Manager |
| `CloudWatchAgentServerPolicy` | Gửi log/metric lên CloudWatch |
| `AmazonS3ReadOnlyAccess` | EC2 tải backend artifact từ S3 artifact bucket |

Trong môi trường production thật, quyền S3 nên giới hạn theo đúng bucket artifact thay vì dùng quyền read-only toàn bộ S3. Trong phạm vi demo, cấu hình trên giúp triển khai nhanh và dễ kiểm tra.

> **Ảnh cần dán:** IAM role summary của `EC2-HotelAPI-Role`.
>
> **Ảnh cần dán:** Danh sách attached policies.
>
> **Ảnh cần dán:** Trust relationship cho EC2.

## 6. Kiểm tra nguyên tắc phân tầng bảo mật

Sau khi tạo xong, kiểm tra lại luồng mở port:

| Tầng | Port mở | Source hợp lệ |
| --- | --- | --- |
| ALB | 80 | Internet |
| EC2 backend | 8080 | `SG-ALB` |
| RDS MySQL | 3306 | `SG-EC2` |
| Redis/Valkey | 6379 | `SG-EC2` |

Không mở SSH/RDP public nếu không cần. Khi cần kiểm tra EC2, ưu tiên dùng **AWS Systems Manager Session Manager** thông qua IAM Role.

> **Ảnh cần dán:** Màn hình danh sách 4 Security Groups `SG-ALB`, `SG-EC2`, `SG-RDS`, `SG-Redis`.

## Kết quả cần đạt

Sau bước này, các tầng của hệ thống được cô lập đúng vai trò. ALB là điểm vào public, EC2 backend nằm trong private subnet, RDS và Redis chỉ nhận kết nối từ backend. EC2 có IAM Role để lấy artifact và phục vụ kiểm tra vận hành mà không cần lưu access key trong source code.
