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
| 2 | - Hoàn thiện **AWS KMS (Lab 000033)**: Tạo CMK, cấu hình mã hóa Server-Side Encryption (SSE-KMS) cho S3 Bucket.<br>- Phân quyền truy cập khóa mã hóa thông qua IAM Policy kết hợp với Key Policy. | 08/06/2026 | 08/06/2026 | Lab 000033 |
| 3 | - Cấu hình **AWS CloudTrail** để ghi nhận toàn bộ hoạt động API của tài khoản vào S3 Bucket.<br>- Thực hiện truy vấn nhật ký bằng **Amazon Athena** và kiểm tra khả năng phát hiện hành vi truy cập bất thường. | 09/06/2026 | 09/06/2026 | Lab 000033 |
| 4 | - Nghiên cứu nền tảng cơ sở dữ liệu: Primary Key, Foreign Key, Index, sự khác biệt giữa mô hình **SQL (RDBMS)** và **NoSQL**.<br>- Phân tích mô hình xử lý dữ liệu **OLTP** (giao dịch) và **OLAP** (phân tích) trong hệ thống doanh nghiệp. | 10/06/2026 | 10/06/2026 | AWS Database Overview |
| 5 | - Thực hành với **Amazon RDS**: Tạo DB Instance, cấu hình Multi-AZ Deployment và thực hành Automated Backup.<br>- Khám phá **Amazon Aurora** và lợi thế so với RDS MySQL/PostgreSQL thông thường (hiệu năng, khả năng mở rộng). | 11/06/2026 | 11/06/2026 | AWS RDS & Aurora |
| 6 | - Thực hành **IAM nâng cao (Lab 000044)**: Tạo User, Group, IAM Role và thiết lập Switch Role để thay đổi quyền linh hoạt.<br>- Triển khai **IAM Role cho EC2 (Lab 000048)** để truy cập S3 mà không cần lưu Access Key trong ứng dụng. | 12/06/2026 | 12/06/2026 | Lab 000044 & 000048 |
| 7 | - Tìm hiểu kiến trúc **Data Lake trên AWS**: S3 làm nền tảng lưu trữ tập trung cho dữ liệu có cấu trúc và phi cấu trúc.<br>- Nghiên cứu vai trò của từng tầng trong kiến trúc Data Lake: Ingestion → Storage → Catalog → Analytics. | 13/06/2026 | 13/06/2026 | AWS Analytics Docs |

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
