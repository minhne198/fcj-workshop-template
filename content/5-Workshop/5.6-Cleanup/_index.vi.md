---
title : "Triển khai Backend API lên AWS"
date : 2024-01-01
weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---

## Mục tiêu

Bước này triển khai backend **ASP.NET Core Web API** của AWS_OmniStay lên EC2 thông qua Launch Template và Auto Scaling Group. Backend được đặt sau Application Load Balancer, chạy ở private app subnets và kết nối đến RDS MySQL, Redis/Valkey cùng các cấu hình production đã tạo ở bước trước.

## 1. Publish backend trên máy local

Từ thư mục source AWS_OmniStay, chạy kiểm thử và publish backend:

```powershell
dotnet test backend\AWSOmniStay.slnx --no-restore
dotnet publish backend\src\HotelBooking.Api\HotelBooking.Api.csproj -c Release -o C:\tmp\omnistay-publish
Compress-Archive -Path C:\tmp\omnistay-publish\* -DestinationPath C:\tmp\omnistay-api.zip -Force
```

Kết quả cần có:

```text
C:\tmp\omnistay-api.zip
```

> **Ảnh cần dán:** Terminal hiển thị `dotnet test` thành công.
>
> **Ảnh cần dán:** Thư mục hoặc file `C:\tmp\omnistay-api.zip` sau khi publish.

![VPC details](/images/562.jpg)
<p align="center"><em>Hình 5.6.1: Thư mục hoặc file `C:\tmp\omnistay-api.zip` sau khi publish.</em></p>

## 2. Upload backend artifact lên S3

Vào **S3** -> artifact bucket `omnistay-artifacts-<account-id>`.

Thực hiện:

1. Chọn **Upload**.
2. Chọn **Add files**.
3. Chọn file `C:\tmp\omnistay-api.zip`.
4. Upload file lên bucket.
5. Ghi lại object path:

```text
s3://omnistay-artifacts-<account-id>/omnistay-api.zip
```

> **Ảnh cần dán:** Object `omnistay-api.zip` trong artifact bucket.

![VPC details](/images/561.jpg)
<p align="center"><em>Hình 5.6.2: TObject `omnistay-api.zip` trong artifact bucket..</em></p>

## 3. Tạo Target Group cho backend

Vào **EC2** -> **Target Groups** -> **Create target group**.

Cấu hình:

| Trường | Giá trị |
| --- | --- |
| Target type | Instances |
| Target group name | `omnistay-api-tg` |
| Protocol | HTTP |
| Port | 8080 |
| VPC | `omnistay-vpc` |
| Health check protocol | HTTP |
| Health check path | `/health` |
| Success code | `200` |

Ở thời điểm này có thể chưa register target thủ công, vì EC2 sẽ được Auto Scaling Group tự đăng ký vào Target Group.


![VPC details](/images/563.png)
<p align="center"><em>Hình 5.6.3: Target group details của `omnistay-api-tg`.</em></p>

## 4. Tạo Application Load Balancer

Vào **EC2** -> **Load Balancers** -> **Create load balancer** -> **Application Load Balancer**.

Cấu hình:

| Trường | Giá trị |
| --- | --- |
| Name | `omnistay-alb` |
| Scheme | Internet-facing |
| IP address type | IPv4 |
| VPC | `omnistay-vpc` |
| Subnets | `omnistay-public-a`, `omnistay-public-b` |
| Security group | `SG-ALB` |
| Listener | HTTP 80 |
| Default action | Forward to `omnistay-api-tg` |

Sau khi ALB chuyển sang trạng thái `Active`, ghi lại DNS name để test backend.


## 5. Tạo Launch Template cho EC2 backend

Vào **EC2** -> **Launch Templates** -> **Create launch template**.

Cấu hình cơ bản:

| Trường | Giá trị |
| --- | --- |
| Name | `omnistay-api-template` |
| AMI | Ubuntu 24.04 hoặc Amazon Linux 2023 |
| Instance type | `t3.micro` hoặc loại nhỏ phù hợp ngân sách |
| Security group | `SG-EC2` |
| IAM instance profile | `EC2-HotelAPI-Role` |
| Storage | 8-20 GiB |

User data cần thực hiện các việc chính:

1. Cài AWS CLI và .NET runtime phù hợp.
2. Tạo thư mục `/opt/omnistay/api`.
3. Tải `omnistay-api.zip` từ S3 artifact bucket.
4. Giải nén backend artifact.
5. Tạo `systemd service` tên `omnistay-api`.
6. Thiết lập biến môi trường production như database provider, connection string, Redis endpoint, JWT config và AWS region.
7. Start service và lắng nghe ở port `8080`.

Ví dụ các biến môi trường quan trọng trong service:

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

Không đưa secret thật vào báo cáo. Khi demo nhanh có thể dùng placeholder trong tài liệu và lưu giá trị thật riêng ngoài repo.


## 6. Tạo Auto Scaling Group

Vào **EC2** -> **Auto Scaling Groups** -> **Create Auto Scaling group**.

Cấu hình:

| Trường | Giá trị |
| --- | --- |
| Name | `omnistay-api-asg` |
| Launch template | `omnistay-api-template` |
| VPC | `omnistay-vpc` |
| Subnets | `omnistay-app-a`, `omnistay-app-b` |
| Target group | `omnistay-api-tg` |
| Health check | ELB health check nếu Console cho chọn |
| Health check grace period | 300 seconds |
| Desired capacity | 1 |
| Minimum capacity | 1 |
| Maximum capacity | 2 hoặc 4 |
| Scaling policy | Target tracking |
| Metric | Average CPU utilization |
| Target value | 70 |

Auto Scaling Group sẽ tạo EC2 trong private app subnets và tự đăng ký instance vào Target Group.


![VPC details](/images/564.png)
<p align="center"><em>Hình 5.6.1: ASG gắn với target group `omnistay-api-tg`.</em></p>

## 7. Kiểm tra EC2 backend bằng Session Manager

Nếu target chưa healthy, kết nối vào EC2 qua **Session Manager**:

```text
EC2 -> Instances -> chọn instance -> Connect -> Session Manager
```

Chạy các lệnh kiểm tra:

```bash
sudo tail -n 120 /var/log/cloud-init-output.log
sudo systemctl status omnistay-api --no-pager
curl -i http://localhost:8080/health
curl -i http://localhost:8080/health/aws
```

Kết quả mong đợi:

```text
Active: active (running)
HTTP/1.1 200 OK
```


## 8. Kiểm tra Target Group và ALB

Vào **EC2** -> **Target Groups** -> `omnistay-api-tg` -> **Targets**.

Kết quả mong đợi:

```text
Healthy = 1
Unhealthy = 0
```

Sau đó mở trình duyệt:

```text
http://<alb-dns>/health
http://<alb-dns>/health/aws
```

Kết quả `/health/aws` nên thể hiện backend đang chạy production, dùng MySQL và Redis đã được cấu hình:

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
<p align="center"><em>Hình 5.6.4: Trình duyệt mở `/health/aws` qua ALB và trả JSON thành công.</em></p>

## Kết quả cần đạt

Sau bước này, backend API đã chạy trên EC2 trong private subnet, được quản lý bởi Auto Scaling Group, nhận traffic qua ALB và có health check hoạt động. Đây là nền tảng để CloudFront ở bước sau forward các request `/api/*` đến backend.
