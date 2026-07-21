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
| 2 | - Tìm hiểu Amazon FSx for Windows File Server<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Thiết lập File Server Multi-AZ<br>&nbsp;&nbsp;+ Cấu hình SMB Share<br>&nbsp;&nbsp;+ Kích hoạt Data Deduplication<br>&nbsp;&nbsp;+ Kiểm thử hiệu năng đọc/ghi và quản lý session | 25/05/2026 | 25/05/2026 | Lab 000025 |
| 3 | - Tìm hiểu AWS Identity and Access Management (IAM)<br>- Tìm hiểu Shared Responsibility Model<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Tạo IAM User<br>&nbsp;&nbsp;+ Tạo IAM Group<br>&nbsp;&nbsp;+ Tạo IAM Role<br>&nbsp;&nbsp;+ Áp dụng chính sách Least Privilege | 26/05/2026 | 26/05/2026 | AWS IAM Guide |
| 4 | - Tìm hiểu Amazon Cognito, JWT Token và OAuth 2.0<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Tạo User Pool<br>&nbsp;&nbsp;+ Tạo Identity Pool<br>&nbsp;&nbsp;+ Cấu hình xác thực cho ứng dụng web/mobile | 27/05/2026 | 27/05/2026 | AWS Security Docs |
| 5 | - Tìm hiểu AWS Organizations và Service Control Policies (SCP)<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Tạo Organizational Unit (OU)<br>&nbsp;&nbsp;+ Thiết lập Service Control Policy<br>&nbsp;&nbsp;+ So sánh SCP và IAM Policy | 28/05/2026 | 28/05/2026 | AWS Organizations |
| 6 | - Tìm hiểu AWS Identity Center (SSO) và AWS KMS<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Cấu hình Identity Source<br>&nbsp;&nbsp;+ Gán quyền truy cập tập trung cho nhiều tài khoản AWS<br>&nbsp;&nbsp;+ Tạo Customer Managed Key<br>&nbsp;&nbsp;+ Áp dụng mã hóa cho S3 và EBS | 29/05/2026 | 29/05/2026 | AWS Study Group |
| 7 | - Tìm hiểu AWS Security Hub và AWS Lambda<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Kích hoạt Security Hub<br>&nbsp;&nbsp;+ Cấu hình CIS Benchmark và AWS Best Practices<br>&nbsp;&nbsp;+ Phân tích Compliance Score<br>&nbsp;&nbsp;+ Ghi chú các trường hợp dùng Serverless Function | 30/05/2026 | 30/05/2026 | Lab 000018 & Cá nhân |

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
