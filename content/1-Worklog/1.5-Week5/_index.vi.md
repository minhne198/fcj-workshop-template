---
title: "Worklog Tuần 5"
date: 2026-05-11
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:
* Triển khai kiến trúc mạng hình sao (**Hub-and-Spoke**) bằng **AWS Transit Gateway (TGW)** để kết nối đa VPC hiệu quả và dễ quản lý.
* Thực hành **Infrastructure as Code (IaC)** với CloudFormation để khởi tạo hạ tầng phức tạp chỉ trong vài phút.
* Nghiên cứu sâu về **Amazon EC2**: Các loại instance type, chip Graviton, hệ thống ảo hóa Nitro và cơ chế lưu trữ EBS vs Instance Store.
* Tự động hóa cấu hình máy chủ bằng **User Data** và truy vấn thông tin qua **Instance Metadata**.
* Bước đầu làm quen với **Amazon S3**: Khởi tạo Bucket và cấu hình lưu trữ đối tượng cơ bản.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2 | - Sử dụng CloudFormation khởi tạo 4 VPC và các máy chủ mẫu trong từng VPC.<br>- Thiết lập **AWS Transit Gateway**, tạo Attachments và lên kế hoạch bảng định tuyến TGW. | 11/05/2026 | 11/05/2026 | AWS Module 02 |
| 3 | - Cấu hình định tuyến trong từng VPC để chỉ về TGW.<br>- Sử dụng **Reachability Analyzer** để kiểm tra kết nối và phân tích luồng gói tin giữa các Private Subnet. | 12/05/2026 | 12/05/2026 | AWS Module 02 |
| 4 | - Nghiên cứu EC2 Instance Types, lợi ích của chip ARM **Graviton** so với Intel/AMD và hệ thống ảo hóa **Nitro**.<br>- Phân biệt cơ chế sao lưu Snapshot (Full vs Incremental) và ứng dụng trong thực tế. | 13/05/2026 | 13/05/2026 | AWS Module 03 |
| 5 | - Thực hành cấu hình **User Data** để tự động cài đặt Web Server (Apache/Nginx) khi EC2 khởi động lần đầu.<br>- Thử nghiệm truy vấn **Instance Metadata** qua địa chỉ IP nội bộ `169.254.169.254`. | 14/05/2026 | 14/05/2026 | AWS Module 03 |
| 6 | - Tìm hiểu cơ chế **Auto Scaling Group**: Điều kiện scale out/in theo CPU metric.<br>- Khởi tạo **Amazon S3 Bucket** đầu tiên và thực hành upload/download đối tượng cơ bản. | 15/05/2026 | 15/05/2026 | AWS Module 03 |
| 7 | - So sánh hiệu năng và độ bền giữa **EBS** và **Instance Store**; chọn đúng loại theo workload.<br>- Dọn dẹp tài nguyên: Xóa TGW Attachments → TGW → CloudFormation Stack theo đúng thứ tự để tránh phí. | 16/05/2026 | 16/05/2026 | Cá nhân |

### Kết quả đạt được tuần 5:

* **Về Kiến trúc mạng (Networking):**
    * Thay thế mô hình VPC Peering phức tạp bằng **Transit Gateway**, giúp quản lý tập trung và mở rộng dễ dàng lên hàng chục VPC.
    * Biết cách dùng Reachability Analyzer để gỡ lỗi kết nối mạng một cách trực quan, không cần thử nghiệm bằng ping thủ công.
* **Về Tài nguyên tính toán (Compute & Storage):**
    * Nắm vững cách tối ưu chi phí bằng cách chọn đúng loại Instance (tối ưu CPU/Memory/GPU) và tận dụng chip ARM Graviton tiết kiệm đến 40% chi phí.
    * Hiểu rõ rủi ro mất dữ liệu khi dùng **Instance Store** và tính bền vững của **EBS** (dữ liệu được nhân bản trong cùng AZ).
    * Tự động hóa triển khai phần mềm ngay khi EC2 vừa khởi động nhờ User Data Script.
* **Về Amazon S3:**
    * Hiểu cơ bản về mô hình lưu trữ đối tượng của S3 và sự khác biệt so với lưu trữ file/block truyền thống.

{{% notice warning %}}
**Lưu ý quan trọng:** Transit Gateway tính phí theo giờ cho mỗi Attachment đang hoạt động. Khi xóa phải đúng thứ tự: **TGW Attachments → Transit Gateway → CloudFormation Stack** để tránh sót tài nguyên gây tốn phí.
{{% /notice %}}
