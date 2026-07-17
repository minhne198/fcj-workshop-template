---
title: "Worklog Tuần 7"
date: 2026-05-25
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7:
* Làm chủ mô hình quản trị danh tính doanh nghiệp với **IAM**, **Amazon Cognito** và **AWS Organizations** (SCP).
* Thiết lập cơ chế đăng nhập một lần (**AWS Identity Center/SSO**) để quản lý truy cập đa tài khoản tập trung.
* Thực thi tiêu chuẩn bảo mật quốc tế thông qua **AWS Security Hub** và mã hóa dữ liệu nghỉ với **AWS KMS**.
* Bước đầu tìm hiểu **AWS Lambda** và mô hình Serverless: Khi nào dùng Lambda thay vì EC2 truyền thống.
* Tổng hợp kiến thức về Shared Responsibility Model và cách AWS phân chia trách nhiệm bảo mật với khách hàng.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2 | - Triển khai **Amazon FSx (Lab 000025)** hoàn chỉnh: Thiết lập File Server Multi-AZ, cấu hình SMB share và kích hoạt Data Deduplication.<br>- Kiểm thử hiệu năng đọc/ghi và quản lý session người dùng. | 25/05/2026 | 25/05/2026 | Lab 000025 |
| 3 | - Thực hành quản trị **IAM** nâng cao: Tạo User/Group với quyền chi tiết, áp dụng chính sách Least Privilege và sử dụng IAM Role để phân quyền theo vai trò.<br>- Nghiên cứu Shared Responsibility Model giữa AWS và khách hàng. | 26/05/2026 | 26/05/2026 | AWS IAM Guide |
| 4 | - Cấu hình **Amazon Cognito**: Thiết lập User Pool và Identity Pool để xác thực người dùng cho ứng dụng web/mobile.<br>- Tìm hiểu cơ chế JWT Token và OAuth 2.0 trong quy trình xác thực hiện đại. | 27/05/2026 | 27/05/2026 | AWS Security Docs |
| 5 | - Quản trị đa tài khoản với **AWS Organizations**: Tạo Organizational Unit (OU) và thiết lập **Service Control Policies (SCP)** kiểm soát quyền tối đa của từng tài khoản thành viên.<br>- Hiểu sự khác biệt giữa SCP và IAM Policy trong cơ chế phân quyền. | 28/05/2026 | 28/05/2026 | AWS Organizations |
| 6 | - Triển khai **AWS Identity Center (SSO)**: Cấu hình Identity Source và gán quyền truy cập tập trung cho nhiều tài khoản AWS.<br>- Thực hành mã hóa dữ liệu với **AWS KMS**: Tạo Customer Managed Key và áp dụng cho S3, EBS. | 29/05/2026 | 29/05/2026 | AWS Study Group |
| 7 | - Kích hoạt **AWS Security Hub (Lab 000018)**: Cấu hình các tiêu chuẩn bảo mật (CIS Benchmark, AWS Best Practices) và phân tích điểm Compliance Score.<br>- Tìm hiểu tổng quan về **AWS Lambda** và kịch bản sử dụng Serverless Function phổ biến. | 30/05/2026 | 30/05/2026 | Lab 000018 & Cá nhân |

### Kết quả đạt được tuần 7:

* **Lưu trữ chuyên dụng & Quản trị danh tính:**
    * Triển khai hoàn chỉnh **Amazon FSx** Multi-AZ, tối ưu dung lượng qua Data Deduplication và bảo toàn dữ liệu với Shadow Copies.
    * Xây dựng được hệ thống IAM phân quyền chặt chẽ, đảm bảo nguyên tắc Least Privilege ở mọi tầng.
* **Quản trị đa tài khoản & Xác thực ứng dụng:**
    * Xây dựng cấu trúc phân cấp doanh nghiệp qua **AWS Organizations**, kiểm soát quyền hạn tối đa của mọi tài khoản thành viên bằng **SCP**.
    * Hiểu quy trình xác thực và ủy quyền của người dùng ứng dụng thông qua **Amazon Cognito**.
* **Bảo mật tập trung & Mã hóa:**
    * Sử dụng **AWS KMS** để bảo vệ dữ liệu nhạy cảm ở trạng thái nghỉ, nắm rõ vòng đời quản lý khóa mã hóa.
    * Thiết lập **Security Hub** như "trung tâm chỉ huy" giám sát liên tục, phát hiện sớm các cấu hình sai lệch và đối chiếu với tiêu chuẩn bảo mật quốc tế.

{{% notice success %}}
**Tóm tắt:** Tuần 7 đưa tư duy bảo mật lên một tầm cao mới: từ quản lý người dùng đơn lẻ đến kiến trúc Identity & Access Management toàn diện cho doanh nghiệp đa tài khoản.
{{% /notice %}}
