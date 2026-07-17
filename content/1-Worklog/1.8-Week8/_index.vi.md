---
title: "Worklog Tuần 8"
date: 2026-06-01
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8:
* Tối ưu chi phí và tự động hóa quản lý vòng đời tài nguyên AWS bằng **AWS Lambda** kết hợp **CloudWatch Events**.
* Làm chủ kỹ thuật phân loại và quản lý tài nguyên hệ thống với **Resource Tags** và **Resource Groups**.
* Áp dụng phân quyền nâng cao bằng **IAM Policy điều kiện Tags** và **IAM Permission Boundary** để kiểm soát quyền tối đa người dùng.
* Bước đầu triển khai bảo mật dữ liệu với **AWS KMS**: Tạo KMS Key và cấu hình mã hóa cho Amazon S3.
* Thực thi nguyên tắc **Least Privilege** xuyên suốt trong mọi cấu hình IAM để giảm thiểu bề mặt tấn công.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2 | - Triển khai **Tối ưu chi phí EC2 (Lab 000022)**: Tạo IAM Role cho Lambda, xây dựng Function tự động tắt EC2 ngoài giờ làm việc.<br>- Cấu hình **CloudWatch Event Rule** theo lịch cron để kích hoạt Lambda tự động. | 01/06/2026 | 01/06/2026 | Lab 000022 |
| 3 | - Hoàn thiện Lambda Function tự động **khởi động lại EC2** vào đầu giờ làm việc buổi sáng.<br>- Kiểm thử cơ chế tự động hóa, xem log qua CloudWatch Logs và xử lý các lỗi runtime nếu có. | 02/06/2026 | 02/06/2026 | Lab 000022 |
| 4 | - Thực hành **Resource Tags (Lab 000027)**: Gắn thẻ phân loại cho EC2, S3, VPC theo môi trường (dev/staging/prod).<br>- Tạo **Resource Groups** để nhóm và giám sát tài nguyên theo tiêu chí thẻ. | 03/06/2026 | 03/06/2026 | Lab 000027 |
| 5 | - Thực hành **IAM Policy kết hợp Tags (Lab 000028)**: Xây dựng Policy chỉ cho phép quản lý EC2 khi Instance có đúng Tag quy định.<br>- Kiểm thử phân quyền theo kịch bản thực tế và xác nhận hoạt động đúng Least Privilege. | 04/06/2026 | 04/06/2026 | Lab 000028 |
| 6 | - Triển khai **IAM Permission Boundary (Lab 000030)**: Tạo Policy giới hạn quyền EC2 chỉ trong Region được chỉ định.<br>- Áp dụng Permission Boundary cho IAM User và kiểm thử khả năng truy cập tại các Region khác nhau. | 05/06/2026 | 05/06/2026 | Lab 000030 |
| 7 | - Bắt đầu tìm hiểu **AWS KMS**: Tạo Customer Managed Key và thực hành cấu hình mã hóa đối tượng trên S3.<br>- Phân quyền truy cập KMS Key bằng IAM Policy theo mô hình Key Policy + IAM Policy. | 06/06/2026 | 06/06/2026 | Lab 000033 |

### Kết quả đạt được tuần 8:

* **Tối ưu chi phí & Tự động hóa:**
    * Triển khai thành công cơ chế tự động bật/tắt **EC2** bằng **Lambda + CloudWatch**, giúp tiết kiệm chi phí điện toán ngoài giờ làm việc lên đến 60-70%.
    * Nắm rõ vòng đời thực thi Lambda và cách phối hợp giữa Lambda, CloudWatch Events và IAM Role.
* **Quản lý tài nguyên & Phân loại hệ thống:**
    * Xây dựng quy trình tagging nhất quán giúp tổ chức tài nguyên rõ ràng theo môi trường, dự án và đội nhóm.
    * Sử dụng Resource Groups để có cái nhìn tổng quan và dễ dàng thực hiện các tác vụ hàng loạt.
* **Kiểm soát quyền truy cập nâng cao:**
    * Thiết lập **IAM Policy điều kiện Tags** để phân quyền theo ngữ cảnh, không chỉ theo dịch vụ.
    * Áp dụng **Permission Boundary** như lớp bảo vệ tối thượng, ngăn chặn leo thang đặc quyền (Privilege Escalation).
* **Bảo mật dữ liệu với KMS:**
    * Hiểu mô hình bảo mật hai lớp của AWS KMS: Key Policy (ai quản lý key) và IAM Policy (ai sử dụng key).

{{% notice success %}}
**Tóm tắt:** Tuần 8 tập trung vào tư duy vận hành tinh gọn (FinOps) và bảo mật theo chiều sâu — hai yếu tố then chốt để quản trị môi trường AWS quy mô lớn một cách bền vững và hiệu quả.
{{% /notice %}}
