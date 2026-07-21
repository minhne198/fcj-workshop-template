---
title: "Worklog Tuần 11"
date: 2026-06-22
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Mục tiêu tuần 11:
* Khởi động đồ án tốt nghiệp: **Hệ thống Đặt phòng Khách sạn Du lịch chịu tải cao trên AWS** (High-Availability Hotel Booking System).
* Thiết kế kiến trúc hệ thống hoàn chỉnh đảm bảo 3 tính chất: **High Availability**, **Auto Scaling** và **Caching**.
* Xây dựng hạ tầng mạng nền tảng (Phase 1): VPC, Subnet, Security Groups, IAM Role, NAT Gateway.
* Khởi tạo cơ sở dữ liệu và bộ nhớ đệm (Phase 2): **Amazon RDS MySQL** và **Amazon ElastiCache Redis**.
* Bắt đầu phát triển Backend API với **ASP.NET Core 8** và thiết kế database schema.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2 | - Tìm hiểu yêu cầu dự án AWS_OmniStay và kiến trúc tổng thể<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Phân tích yêu cầu đề tài<br>&nbsp;&nbsp;+ Vẽ kiến trúc hệ thống trên Draw.io<br>&nbsp;&nbsp;+ Xác định dịch vụ AWS cần dùng: VPC, EC2, ALB, ASG, RDS, ElastiCache, S3, CloudFront, WAF, CloudWatch, SNS | 22/06/2026 | 22/06/2026 | Tài liệu đề tài |
| 3 | - Phase 1 - Tìm hiểu hạ tầng mạng cho hệ thống N-tier<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Tạo VPC `10.0.0.0/16`<br>&nbsp;&nbsp;+ Chia 6 Subnet: 2 Public và 4 Private<br>&nbsp;&nbsp;+ Gắn Internet Gateway<br>&nbsp;&nbsp;+ Cấu hình NAT Gateway cho 2 AZ<br>&nbsp;&nbsp;+ Thiết lập Route Table cho Public/Private Subnet | 23/06/2026 | 23/06/2026 | AWS Console |
| 4 | - Tìm hiểu Security Group và IAM Role cho tầng ứng dụng<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Tạo SG-ALB<br>&nbsp;&nbsp;+ Tạo SG-EC2<br>&nbsp;&nbsp;+ Tạo SG-RDS<br>&nbsp;&nbsp;+ Tạo SG-Redis<br>&nbsp;&nbsp;+ Tạo IAM Role `EC2-HotelAPI-Role` với quyền S3 Read, CloudWatch Agent, Secrets Manager | 24/06/2026 | 24/06/2026 | AWS Console |
| 5 | - Phase 2 - Tìm hiểu Database layer với Amazon RDS và Secrets Manager<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Tạo Amazon RDS MySQL 8.0 trong Private Subnet<br>&nbsp;&nbsp;+ Bật KMS encryption<br>&nbsp;&nbsp;+ Lưu DB password vào AWS Secrets Manager | 25/06/2026 | 25/06/2026 | AWS Console |
| 6 | - Tìm hiểu Cache layer và Database Schema cho hệ thống đặt phòng<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Tạo Amazon ElastiCache Redis 7.x trong Private DB Subnet<br>&nbsp;&nbsp;+ Thiết kế bảng Users, Hotels, RoomTypes, Bookings, Reviews<br>&nbsp;&nbsp;+ Chạy SQL script tạo bảng bằng DBeaver | 26/06/2026 | 26/06/2026 | AWS Console |
| 7 | - Phase 3 - Tìm hiểu Backend API với ASP.NET Core 8<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Khởi tạo ASP.NET Core 8 Web API<br>&nbsp;&nbsp;+ Cấu hình Entity Framework Core và Pomelo MySQL driver<br>&nbsp;&nbsp;+ Viết `AuthController.cs` cho Register/Login và JWT Token<br>&nbsp;&nbsp;+ Viết `SearchService.cs` tích hợp Redis Cache | 27/06/2026 | 27/06/2026 | Visual Studio 2022 |

### Kết quả đạt được tuần 11:

* **Thiết kế kiến trúc hệ thống:**
    * Hoàn thành sơ đồ kiến trúc tổng thể trên **Draw.io** với đầy đủ các thành phần AWS: CloudFront → WAF → ALB → ASG (EC2) → RDS + Redis, S3 static hosting, CloudWatch giám sát.
    * Xác định rõ 3 tính chất chứng minh: HA (tắt 1 EC2 → vẫn chạy), Auto Scaling (500 users → EC2 tự scale), Caching (cache hit < 5ms vs 100-200ms không cache).

* **Hạ tầng mạng (Phase 1 hoàn thành):**
    * Tạo VPC hoàn chỉnh với 6 Subnet đúng vai trò: Public (ALB, NAT GW) và Private (App EC2, DB RDS/Redis).
    * Thiết lập Security Group theo mô hình layered security: chỉ ALB mới vào được EC2, chỉ EC2 mới vào được RDS và Redis.
    * IAM Role cho EC2 không dùng Access Key — áp dụng đúng nguyên tắc bảo mật hiện đại.

* **Database & Cache (Phase 2 hoàn thành):**
    * Khởi tạo thành công **Amazon RDS MySQL** với mã hóa KMS, password quản lý qua Secrets Manager.
    * Khởi tạo **ElastiCache Redis** sẵn sàng làm bộ nhớ đệm cho kết quả tìm kiếm phổ biến.
    * Database Schema thiết kế rõ ràng với đầy đủ quan hệ khoá ngoại giữa các bảng.

* **Backend API (Phase 3 khởi đầu):**
    * Project ASP.NET Core 8 khởi chạy được ở môi trường local, kết nối thành công vào RDS và Redis.
    * API xác thực hoạt động: đăng ký tài khoản, đăng nhập trả về JWT Token đúng chuẩn.

{{% notice success %}}
**Tóm tắt:** Tuần 11 hoàn thành toàn bộ nền tảng hạ tầng AWS của đồ án. Kiến trúc hệ thống được thiết kế bài bản theo mô hình 3-tier (Presentation - Application - Data) với đầy đủ tính năng HA và bảo mật theo chuẩn thực tế.
{{% /notice %}}

### Hình ảnh thực hành tuần 11:

![Kiến trúc AWS OmniStay](/images/aws-omnistay-architecture.png)

![Thực hành tuần 11 - 532](/images/532.jpg)
