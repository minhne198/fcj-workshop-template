---
title : "Xây dựng hạ tầng mạng trên AWS"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

## Mục tiêu

Bước này tạo lớp mạng nền tảng cho AWS_OmniStay. Hệ thống cần public subnet để nhận traffic từ internet qua ALB và NAT Gateway, đồng thời cần private subnet để chạy backend EC2, RDS MySQL và ElastiCache Redis an toàn hơn.

Mô hình mạng sử dụng 2 Availability Zones để tăng tính sẵn sàng:

- 2 public subnets cho ALB và NAT Gateway.
- 2 private app subnets cho EC2 backend.
- 2 private data subnets cho RDS và Redis.


## 1. Tạo VPC

Vào **VPC** -> **Your VPCs** -> **Create VPC**.

Cấu hình:

| Trường | Giá trị |
| --- | --- |
| Resource to create | VPC only |
| Name tag | `omnistay-vpc` |
| IPv4 CIDR | `10.0.0.0/16` |
| Tenancy | Default |

Sau khi tạo xong, kiểm tra VPC có CIDR `10.0.0.0/16` và nằm đúng region `ap-southeast-1`.
.
![VPC details](/images/531.jpg)
<p align="center"><em>Hình 5.3.1: Tạo VPC thành công.</em></p>

## 2. Tạo 6 subnets

Vào **VPC** -> **Subnets** -> **Create subnet**. Tất cả subnet đều thuộc `omnistay-vpc`.

| Subnet name | AZ | IPv4 CIDR | Vai trò |
| --- | --- | --- | --- |
| `omnistay-public-a` | `ap-southeast-1a` | `10.0.1.0/24` | Public subnet cho ALB/NAT |
| `omnistay-public-b` | `ap-southeast-1b` | `10.0.2.0/24` | Public subnet cho ALB/NAT |
| `omnistay-app-a` | `ap-southeast-1a` | `10.0.10.0/24` | Private app subnet cho EC2 |
| `omnistay-app-b` | `ap-southeast-1b` | `10.0.11.0/24` | Private app subnet cho EC2 |
| `omnistay-data-a` | `ap-southeast-1a` | `10.0.20.0/24` | Private data subnet cho RDS/Redis |
| `omnistay-data-b` | `ap-southeast-1b` | `10.0.21.0/24` | Private data subnet cho RDS/Redis |

Sau khi tạo 2 public subnet, bật **Auto-assign public IPv4 address** cho `omnistay-public-a` và `omnistay-public-b`.

![VPC details](/images/532.jpg)
<p align="center"><em>Hình 5.3.2: Tạo 6 subnets.</em></p>

## 3. Tạo Internet Gateway

Vào **VPC** -> **Internet Gateways** -> **Create internet gateway**.

Cấu hình:

| Trường | Giá trị |
| --- | --- |
| Name tag | `omnistay-igw` |
| Attach VPC | `omnistay-vpc` |

Sau khi tạo, chọn Internet Gateway vừa tạo, vào **Actions** -> **Attach to VPC** và gắn vào `omnistay-vpc`.

`omnistay-vpc`.
![VPC details](/images/533.jpg)
<p align="center"><em>Hình 5.3.3: Internet Gateway.</em></p>

![VPC details](/images/534.jpg)
<p align="center"><em>Hình 5.3.4: Attach to VPC.</em></p>

## 4. Tạo public route table

Vào **VPC** -> **Route tables** -> **Create route table**.

Cấu hình:

| Trường | Giá trị |
| --- | --- |
| Name | `omnistay-public-rt` |
| VPC | `omnistay-vpc` |

Routes:

| Destination | Target |
| --- | --- |
| `10.0.0.0/16` | local |
| `0.0.0.0/0` | `omnistay-igw` |

Subnet associations:

- `omnistay-public-a`
- `omnistay-public-b`


![VPC details](/images/535.jpg)
<p align="center"><em>Hình 5.3.5: Public route table có route.</em></p>
## 5. Tạo NAT Gateways

NAT Gateway cho phép EC2 trong private app subnet truy cập outbound internet để tải package, gọi AWS service hoặc gửi log mà không cần public IP.

Tạo NAT Gateway thứ nhất:

| Trường | Giá trị |
| --- | --- |
| Name | `omnistay-nat-a` |
| Subnet | `omnistay-public-a` |
| Connectivity type | Public |
| Elastic IP allocation | Automatic |

Tạo NAT Gateway thứ hai:

| Trường | Giá trị |
| --- | --- |
| Name | `omnistay-nat-b` |
| Subnet | `omnistay-public-b` |
| Connectivity type | Public |
| Elastic IP allocation | Automatic |

![VPC details](/images/537.jpg)
<p align="center"><em>Hình 5.3.7: Tạo NAT Gateway.</em></p>

## 6. Tạo private route tables cho app subnets

Tạo route table cho app subnet ở AZ-a:

| Trường | Giá trị |
| --- | --- |
| Name | `omnistay-app-a-rt` |
| VPC | `omnistay-vpc` |
| Route | `0.0.0.0/0 -> omnistay-nat-a` |
| Subnet association | `omnistay-app-a` |

Tạo route table cho app subnet ở AZ-b:

| Trường | Giá trị |
| --- | --- |
| Name | `omnistay-app-b-rt` |
| VPC | `omnistay-vpc` |
| Route | `0.0.0.0/0 -> omnistay-nat-b` |
| Subnet association | `omnistay-app-b` |

Private data subnets chứa RDS và Redis không cần route ra internet trong luồng demo cơ bản. Chúng chỉ nhận kết nối nội bộ từ backend EC2 thông qua Security Group.

.
![VPC details](/images/536.jpg)
<p align="center"><em>Hình 5.3.6: Tạo Route Table Private App.</em></p>
## Kết quả cần đạt

Sau bước này, hệ thống có VPC riêng, phân tách public/private subnet, có đường internet cho public subnet, có NAT Gateway cho app subnet và có nền tảng mạng sẵn sàng để triển khai ALB, EC2, RDS và Redis.
