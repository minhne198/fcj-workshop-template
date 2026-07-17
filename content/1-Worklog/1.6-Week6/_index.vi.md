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
| 2 | - Khởi tạo **S3 Bucket**, cấu hình **Static Website Hosting** và tích hợp phân phối nội dung qua **CloudFront**.<br>- Thiết lập **Bucket Policy** để quản lý quyền truy cập công khai an toàn và hiệu quả. | 18/05/2026 | 18/05/2026 | Lab S3 (000057) |
| 3 | - Kích hoạt **Bucket Versioning** để theo dõi lịch sử thay đổi đối tượng và khôi phục về phiên bản cũ khi cần.<br>- Cấu hình **Cross-Region Replication (CRR)** để nhân bản dữ liệu sang Region khác đảm bảo tính sẵn sàng cao. | 19/05/2026 | 19/05/2026 | Lab S3 (000057) |
| 4 | - Cấu hình **S3 Gateway Endpoint** và **Interface Endpoint (PrivateLink)** để truy cập S3 từ bên trong VPC mà không qua internet.<br>- Kiểm thử và xác nhận lưu lượng S3 đi qua đường kết nối nội bộ. | 20/05/2026 | 20/05/2026 | Lab VPC (000013-14) |
| 5 | - Kiểm soát lưu lượng mạng chi tiết qua các tầng bảo mật **NACLs** và **Security Groups** trong VPC.<br>- Thực hành phân quyền truy cập S3 theo nguyên tắc Least Privilege thông qua IAM Policy và S3 Bucket Policy. | 21/05/2026 | 21/05/2026 | AWS Study Group |
| 6 | - Thiết lập kế hoạch sao lưu tập trung với **AWS Backup**: Cấu hình Backup Plan, Backup Vault và kiểm thử khôi phục dữ liệu.<br>- Nghiên cứu các chỉ số **RTO** và **RPO** trong chiến lược khắc phục thảm họa. | 22/05/2026 | 22/05/2026 | AWS Study Group |
| 7 | - Khám phá **Amazon FSx for Windows File Server**: Kiến trúc Multi-AZ, cấu hình SMB và tính năng Data Deduplication.<br>- Tổng hợp hình ảnh thực hành và hoàn thiện báo cáo Tuần 6. | 23/05/2026 | 23/05/2026 | Cá nhân |

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
