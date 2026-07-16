---
title : "Chuẩn bị trước khi triển khai"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---

## Mục tiêu

Trước khi tạo tài nguyên AWS, cần chuẩn bị môi trường làm việc, quy ước đặt tên, ngân sách, source code và danh sách thông tin sẽ dùng xuyên suốt quá trình triển khai. Bước chuẩn bị giúp hạn chế sai sót khi cấu hình nhiều dịch vụ có liên kết với nhau như VPC, EC2, RDS, Redis, S3, CloudFront và CloudWatch.

## Phạm vi chuẩn bị

Các nội dung cần hoàn thành trong bước này gồm:

- Xác định region triển khai và quy ước đặt tên tài nguyên.
- Kiểm tra source code AWS_OmniStay ở local.
- Chuẩn bị các công cụ phục vụ build, deploy và kiểm thử.
- Tạo AWS Budget để kiểm soát chi phí trong quá trình làm workshop.
- Xác định nguyên tắc bảo mật khi ghi lại tài liệu, đặc biệt là không đưa password, secret key hoặc token vào báo cáo.

![VPC details](/images/cautrucOmniStay.jpg)
<p align="center"><em>Hình 5.2.1: Cấu trúc thư mục
  của OmniStay.</em></p>

## 1. Xác định region và quy ước đặt tên

Workshop sử dụng region `ap-southeast-1` để triển khai các tài nguyên chính. Các tài nguyên được đặt tên theo tiền tố `omnistay` để dễ nhận diện và dễ lọc khi kiểm tra chi phí.

| Nhóm tài nguyên | Tên sử dụng trong workshop |
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

Các tag nên dùng cho tài nguyên:

| Key | Value |
| --- | --- |
| `Project` | `AWS_OmniStay` |
| `Environment` | `demo` |
| `Owner` | Tên hoặc mã sinh viên thực hiện |


![VPC details](/images/522.jpg)
<p align="center"><em>Hình 5.2.2: CMàn hình AWS Console đang chọn region `ap-southeast-1`.</em></p>

## 2. Tạo AWS Budget để kiểm soát chi phí

Một số dịch vụ như NAT Gateway, ALB, RDS, ElastiCache, WAF và public IPv4 có thể phát sinh chi phí theo giờ. Vì vậy cần tạo budget trước khi triển khai.

Thực hiện:

1. Vào **Billing and Cost Management**.
2. Chọn **Budgets**.
3. Chọn **Create budget**.
4. Chọn loại **Monthly cost budget**.
5. Đặt tên budget là `omnistay-monthly-budget`.
6. Đặt ngân sách demo là `10 USD`.
7. Cấu hình cảnh báo ở các ngưỡng 50%, 80% và 100%.
8. Nhập email nhận cảnh báo và tạo budget.


![VPC details](/images/523.jpg)
<p align="center"><em>Hình 5.2.3: Tạo Budget.</em></p>

## 3. Chuẩn bị công cụ triển khai

Các công cụ cần có trên máy local:

| Công cụ | Mục đích |
| --- | --- |
| .NET SDK | Build và publish ASP.NET Core Web API |
| Git | Quản lý source code |
| AWS CLI | Upload artifact, kiểm tra tài nguyên và hỗ trợ deploy |
| Visual Studio Code | Chỉnh sửa source và tài liệu |
| DBeaver hoặc MySQL client | Kiểm tra dữ liệu trong RDS MySQL |
| Trình duyệt | Kiểm thử website public qua CloudFront |

Kiểm tra source code chính:

```text
backend/src/HotelBooking.Api
frontend/public
frontend/src
```

Backend là ASP.NET Core Web API. Frontend là static web gồm HTML, CSS và JavaScript. Khi triển khai production, frontend đọc cấu hình API từ `frontend/public/config.js`.


![VPC details](/images/524.jpg)
<p align="center"><em>Hình 5.2.4: các thư mục `backend`, `frontend`, `docs` của dự án.</em></p>
## 4. Nguyên tắc bảo mật khi ghi tài liệu

Trong quá trình triển khai, không ghi trực tiếp các thông tin sau vào báo cáo:

- AWS access key hoặc secret access key.
- RDS password.
- JWT secret.
- Admin password production.
- Token thanh toán hoặc webhook secret.
- Nội dung secret value trong Secrets Manager.

Các giá trị nhạy cảm chỉ nên lưu ở ghi chú riêng ngoài repo hoặc trong Secrets Manager/Parameter Store. Trong báo cáo, sử dụng placeholder như `<database-password>`, `<jwt-secret>`, `<cloudfront-domain>`.

## 5. Danh sách giá trị cần ghi lại

Trong quá trình triển khai, cần ghi lại các giá trị sau để dùng ở các bước sau:

| Giá trị | Mục đích sử dụng |
| --- | --- |
| `ARTIFACT_BUCKET` | Nơi upload file backend publish `.zip` |
| `FRONTEND_BUCKET` | Nơi upload frontend static files |
| `RDS_ENDPOINT` | Kết nối backend đến MySQL |
| `REDIS_ENDPOINT` | Kết nối backend đến Redis/Valkey |
| `ALB_DNS` | Test backend qua Load Balancer |
| `CLOUDFRONT_DOMAIN` | Truy cập website public |
| `TARGET_GROUP_NAME` | Kiểm tra health check backend |
| `ASG_NAME` | Quản lý số lượng EC2 backend |



## Kết quả cần đạt

Sau bước chuẩn bị, người thực hiện có đủ công cụ local, biết region triển khai, có budget kiểm soát chi phí và có quy ước đặt tên rõ ràng. Các bước tiếp theo sẽ bắt đầu từ việc xây dựng hạ tầng mạng nền tảng cho hệ thống.
