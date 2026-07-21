---
title: "Worklog Tuần 9"
date: 2026-06-08
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Mục tiêu tuần 9:
* Làm chủ kỹ thuật mã hóa dữ liệu toàn diện với **AWS KMS** và giám sát hoạt động hệ thống bằng **AWS CloudTrail**.
* Truy vấn và phân tích nhật ký audit log bằng **Amazon Athena** để phát hiện hoạt động bất thường.
* Tìm hiểu và thực hành với các dịch vụ cơ sở dữ liệu quan hệ trên AWS: **Amazon RDS** và **Amazon Aurora**.
* Triển khai mô hình phân quyền hiện đại với **IAM Role cho EC2** để truy cập tài nguyên không cần lưu trữ Access Key.
* Bước đầu khám phá kiến trúc **Data Lake trên AWS**: Vai trò của S3 và quy trình thu thập dữ liệu tập trung.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2 | - Tìm hiểu AWS KMS và Server-Side Encryption (SSE-KMS)<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Tạo Customer Managed Key (CMK)<br>&nbsp;&nbsp;+ Cấu hình SSE-KMS cho S3 Bucket<br>&nbsp;&nbsp;+ Phân quyền truy cập bằng IAM Policy và Key Policy | 08/06/2026 | 08/06/2026 | Lab 000033 |
| 3 | - Tìm hiểu AWS CloudTrail và Amazon Athena<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Cấu hình CloudTrail ghi log API vào S3 Bucket<br>&nbsp;&nbsp;+ Tạo bảng truy vấn log bằng Athena<br>&nbsp;&nbsp;+ Kiểm tra hành vi truy cập bất thường | 09/06/2026 | 09/06/2026 | Lab 000033 |
| 4 | - Tìm hiểu nền tảng cơ sở dữ liệu<br>&nbsp;&nbsp;+ Primary Key<br>&nbsp;&nbsp;+ Foreign Key<br>&nbsp;&nbsp;+ Index<br>&nbsp;&nbsp;+ SQL (RDBMS) và NoSQL<br>- Tìm hiểu mô hình xử lý dữ liệu OLTP và OLAP | 10/06/2026 | 10/06/2026 | AWS Database Overview |
| 5 | - Tìm hiểu Amazon RDS và Amazon Aurora<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Tạo RDS DB Instance<br>&nbsp;&nbsp;+ Cấu hình Multi-AZ Deployment<br>&nbsp;&nbsp;+ Kiểm thử Automated Backup<br>&nbsp;&nbsp;+ So sánh Aurora với RDS MySQL/PostgreSQL | 11/06/2026 | 11/06/2026 | AWS RDS & Aurora |
| 6 | - Tìm hiểu IAM nâng cao và IAM Role cho EC2<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Tạo IAM User<br>&nbsp;&nbsp;+ Tạo IAM Group<br>&nbsp;&nbsp;+ Tạo IAM Role<br>&nbsp;&nbsp;+ Thiết lập Switch Role<br>&nbsp;&nbsp;+ Gắn IAM Role cho EC2 để truy cập S3 không cần Access Key | 12/06/2026 | 12/06/2026 | Lab 000044 & 000048 |
| 7 | - Tìm hiểu kiến trúc Data Lake trên AWS<br>&nbsp;&nbsp;+ Ingestion<br>&nbsp;&nbsp;+ Storage<br>&nbsp;&nbsp;+ Catalog<br>&nbsp;&nbsp;+ Analytics<br>- Ghi chú vai trò của S3 trong lưu trữ dữ liệu có cấu trúc và phi cấu trúc | 13/06/2026 | 13/06/2026 | AWS Analytics Docs |

### Kết quả đạt được tuần 9:

* **Bảo mật dữ liệu & Mã hóa:**
    * Triển khai thành công **AWS KMS** với SSE-KMS, đảm bảo dữ liệu lưu trữ trên S3 được mã hóa bằng khóa do khách hàng kiểm soát.
    * Hiểu sự khác biệt giữa SSE-S3, SSE-KMS và SSE-C trong các chiến lược mã hóa S3.
* **Giám sát & Audit:**
    * Sử dụng thành thạo **CloudTrail + Athena** để truy vấn nhật ký API call, xác định ai đã làm gì và khi nào trong tài khoản AWS.
    * Xây dựng quy trình phát hiện hành vi bất thường và đáp ứng sự cố (Incident Response) cơ bản.
* **Cơ sở dữ liệu trên AWS:**
    * Hiểu kiến trúc và cơ chế vận hành của **Amazon RDS** (Managed RDBMS) và **Aurora** (Cloud-native database).
    * Nắm rõ sự khác biệt OLTP vs OLAP và biết lựa chọn dịch vụ phù hợp cho từng loại workload.
* **Mô hình phân quyền hiện đại:**
    * Áp dụng **IAM Role** thay cho Access Key giúp loại bỏ rủi ro lộ thông tin xác thực trong source code hoặc config file.
* **Nền tảng Data Analytics:**
    * Hiểu kiến trúc tổng quan của Data Lake và vai trò của S3 như một "hồ dữ liệu" doanh nghiệp trên AWS.

{{% notice info %}}
**Tóm tắt:** Tuần 9 đánh dấu bước chuyển từ bảo mật hạ tầng sang bảo mật dữ liệu, đồng thời mở ra cánh cửa tiếp cận thế giới Data Analytics trên AWS Cloud.
{{% /notice %}}
