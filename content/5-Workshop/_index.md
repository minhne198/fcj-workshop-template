---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Triển khai hệ thống AWS OmniStay trên AWS

Phần Workshop ghi lại quá trình triển khai website đặt phòng khách sạn **AWS_OmniStay** lên Amazon Web Services theo từng bước thực hiện. Nội dung tập trung vào cách xây dựng hạ tầng, triển khai backend, triển khai frontend, cấu hình bảo mật, kiểm thử hệ thống và thu thập ảnh chụp màn hình làm bằng chứng.

Hệ thống được triển khai theo mô hình nhiều tầng:

- Frontend tĩnh được lưu trong Amazon S3 private bucket và phân phối qua Amazon CloudFront.
- Backend ASP.NET Core Web API chạy trên Amazon EC2 trong private subnet.
- Application Load Balancer nhận request từ CloudFront và chuyển tiếp đến backend.
- Auto Scaling Group quản lý số lượng EC2 backend.
- Amazon RDS MySQL lưu dữ liệu nghiệp vụ.
- Amazon ElastiCache Redis/Valkey làm cache cho luồng tìm kiếm khách sạn.
- AWS WAF, IAM, Security Group, Secrets Manager, Parameter Store và CloudWatch hỗ trợ bảo mật, cấu hình và vận hành.

> **Ảnh cần dán:** Sơ đồ kiến trúc tổng thể của hệ thống AWS_OmniStay. Nếu chưa có ảnh chính thức, có thể dán lại sơ đồ đã dùng ở phần 5.1.

## Nội dung

1. [Giới thiệu](5.1-Workshop-overview/)
2. [Chuẩn bị trước khi triển khai](5.2-Prerequiste/)
3. [Xây dựng hạ tầng mạng trên AWS](5.3-S3-vpc/)
4. [Cấu hình bảo mật mạng và quyền truy cập](5.4-S3-onprem/)
5. [Tạo tầng dữ liệu và cấu hình hệ thống](5.5-Policy/)
6. [Triển khai Backend API lên AWS](5.6-Cleanup/)
7. [Triển khai Frontend lên S3 và CloudFront](5.7-frontend-cloudfront/)
8. [Cấu hình WAF, giám sát và cảnh báo](5.8-waf-monitoring/)
9. [Kiểm thử hệ thống sau triển khai](5.9-system-testing/)

## Quy ước ghi chú ảnh

Trong từng bước triển khai, các vị trí cần bổ sung ảnh chụp màn hình sẽ được đánh dấu bằng dòng:

> **Ảnh cần dán:** Mô tả màn hình cần chụp.

Khi hoàn thiện báo cáo, thay các ghi chú này bằng ảnh chụp thực tế từ AWS Console, trình duyệt hoặc terminal.
