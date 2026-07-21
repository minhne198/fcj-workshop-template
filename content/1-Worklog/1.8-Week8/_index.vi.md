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
| 2 | - Tìm hiểu tối ưu chi phí EC2 bằng AWS Lambda<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Tạo IAM Role cho Lambda<br>&nbsp;&nbsp;+ Viết Lambda Function tự động tắt EC2 ngoài giờ làm việc<br>&nbsp;&nbsp;+ Cấu hình CloudWatch Event Rule theo cron schedule | 01/06/2026 | 01/06/2026 | Lab 000022 |
| 3 | - Tìm hiểu cơ chế tự động hóa vận hành EC2<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Hoàn thiện Lambda Function tự động khởi động EC2<br>&nbsp;&nbsp;+ Kiểm thử cơ chế stop/start EC2<br>&nbsp;&nbsp;+ Xem CloudWatch Logs và xử lý lỗi runtime | 02/06/2026 | 02/06/2026 | Lab 000022 |
| 4 | - Tìm hiểu Resource Tags và Resource Groups<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Gắn tag cho EC2<br>&nbsp;&nbsp;+ Gắn tag cho S3<br>&nbsp;&nbsp;+ Gắn tag cho VPC<br>&nbsp;&nbsp;+ Tạo Resource Groups theo tiêu chí tag | 03/06/2026 | 03/06/2026 | Lab 000027 |
| 5 | - Tìm hiểu IAM Policy kết hợp Tags<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Xây dựng Policy quản lý EC2 theo tag quy định<br>&nbsp;&nbsp;+ Kiểm thử kịch bản được phép/từ chối truy cập<br>&nbsp;&nbsp;+ Xác nhận hoạt động theo nguyên tắc Least Privilege | 04/06/2026 | 04/06/2026 | Lab 000028 |
| 6 | - Tìm hiểu IAM Permission Boundary<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Tạo Policy giới hạn quyền EC2 theo Region<br>&nbsp;&nbsp;+ Áp dụng Permission Boundary cho IAM User<br>&nbsp;&nbsp;+ Kiểm thử truy cập ở các Region khác nhau | 05/06/2026 | 05/06/2026 | Lab 000030 |
| 7 | - Tìm hiểu AWS Key Management Service (KMS)<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Tạo Customer Managed Key<br>&nbsp;&nbsp;+ Cấu hình mã hóa Server-Side Encryption cho S3<br>&nbsp;&nbsp;+ Phân quyền KMS bằng Key Policy và IAM Policy | 06/06/2026 | 06/06/2026 | Lab 000033 |

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
