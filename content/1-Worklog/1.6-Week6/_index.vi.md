---
title: "Worklog Tuần 6"
date: 2026-05-18
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:
* Xây dựng hạ tầng lưu trữ đối tượng bền vững với **Amazon S3** và triển khai website tĩnh phân phối toàn cầu qua **CloudFront**.
* Làm chủ kỹ thuật bảo vệ dữ liệu: **Versioning**, **Multi-Region Replication** và kiểm soát truy cập bằng Bucket Policy.
* Cấu hình **VPC Endpoints** để kết nối nội bộ với S3 không đi qua internet công cộng, tăng bảo mật và giảm chi phí truyền tải.
* Tìm hiểu chiến lược **Disaster Recovery** theo chỉ số RTO/RPO và quản lý sao lưu tập trung với **AWS Backup**.
* Khám phá hệ thống lưu trữ tệp chuyên dụng doanh nghiệp với **Amazon FSx for Windows File Server**.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2 | - Tìm hiểu Amazon S3, Static Website Hosting và CloudFront<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Tạo S3 Bucket<br>&nbsp;&nbsp;+ Bật Static Website Hosting<br>&nbsp;&nbsp;+ Cấu hình Bucket Policy<br>&nbsp;&nbsp;+ Tích hợp CloudFront để phân phối nội dung | 18/05/2026 | 18/05/2026 | Lab S3 (000057) |
| 3 | - Tìm hiểu Bucket Versioning và Cross-Region Replication (CRR)<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Kích hoạt Bucket Versioning<br>&nbsp;&nbsp;+ Khôi phục object về phiên bản cũ<br>&nbsp;&nbsp;+ Cấu hình CRR để nhân bản dữ liệu sang Region khác | 19/05/2026 | 19/05/2026 | Lab S3 (000057) |
| 4 | - Tìm hiểu S3 Gateway Endpoint và Interface Endpoint (PrivateLink)<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Cấu hình S3 Gateway Endpoint<br>&nbsp;&nbsp;+ Cấu hình Interface Endpoint<br>&nbsp;&nbsp;+ Kiểm thử traffic S3 đi qua kết nối nội bộ | 20/05/2026 | 20/05/2026 | Lab VPC (000013-14) |
| 5 | - Tìm hiểu NACL, Security Group và phân quyền truy cập S3<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Kiểm soát lưu lượng mạng bằng NACL<br>&nbsp;&nbsp;+ Kiểm soát lưu lượng bằng Security Group<br>&nbsp;&nbsp;+ Phân quyền S3 bằng IAM Policy và S3 Bucket Policy | 21/05/2026 | 21/05/2026 | AWS Study Group |
| 6 | - Tìm hiểu AWS Backup, RTO và RPO<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Tạo Backup Plan<br>&nbsp;&nbsp;+ Tạo Backup Vault<br>&nbsp;&nbsp;+ Kiểm thử khôi phục dữ liệu<br>&nbsp;&nbsp;+ Ghi chú chiến lược Disaster Recovery | 22/05/2026 | 22/05/2026 | AWS Study Group |
| 7 | - Tìm hiểu Amazon FSx for Windows File Server<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Tìm hiểu kiến trúc Multi-AZ<br>&nbsp;&nbsp;+ Cấu hình SMB<br>&nbsp;&nbsp;+ Tìm hiểu Data Deduplication<br>&nbsp;&nbsp;+ Tổng hợp hình ảnh thực hành tuần 6 | 23/05/2026 | 23/05/2026 | Cá nhân |

### Kết quả đạt được tuần 6:

* **Lưu trữ & Phân phối nội dung:**
    * Triển khai thành công website tĩnh với tốc độ truy cập toàn cầu được tối ưu nhờ kết hợp **S3 + CloudFront CDN**.
    * Nắm vững cách quản lý vòng đời đối tượng và các lớp lưu trữ (**Storage Classes**) để giảm chi phí dài hạn.
* **Bảo mật & Tính sẵn sàng cao:**
    * Cấu hình Versioning giúp phục hồi dữ liệu bị xóa nhầm hoặc ghi đè, tránh mất dữ liệu không thể khôi phục.
    * Hiểu rõ các chỉ số **RTO/RPO** và chiến lược Disaster Recovery phù hợp với từng cấp độ yêu cầu kinh doanh.
    * Sử dụng **AWS Backup** để quản lý sao lưu nhiều dịch vụ (EC2, RDS, S3, EFS) từ một giao diện duy nhất.
* **Mạng & Kết nối nội bộ:**
    * Triển khai VPC Endpoints giúp loại bỏ sự phụ thuộc vào internet cho lưu lượng nội bộ, tăng bảo mật và giảm độ trễ.
* **Lưu trữ tệp doanh nghiệp:**
    * Hiểu được kiến trúc và ứng dụng của **Amazon FSx** trong môi trường doanh nghiệp cần chia sẻ file theo chuẩn Windows (SMB).

{{% notice info %}}
**Tóm tắt:** Tuần 6 giúp hoàn thiện tư duy Cloud Engineer trong việc kết hợp lưu trữ không giới hạn của S3, bảo mật của VPC Endpoints và khả năng phục hồi của AWS Backup — nền tảng để xây dựng ứng dụng có độ tin cậy cao trên AWS.
{{% /notice %}}

### Hình ảnh thực hành tuần 6:

![Thực hành tuần 6 - 541](/images/541.jpg)
