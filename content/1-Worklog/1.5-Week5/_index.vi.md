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
| 2 | - Tìm hiểu mô hình Hub-and-Spoke với AWS Transit Gateway<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Dùng CloudFormation khởi tạo 4 VPC<br>&nbsp;&nbsp;+ Tạo các máy chủ mẫu trong từng VPC<br>&nbsp;&nbsp;+ Tạo Transit Gateway Attachments<br>&nbsp;&nbsp;+ Lên kế hoạch bảng định tuyến TGW | 11/05/2026 | 11/05/2026 | AWS Module 02 |
| 3 | - Tìm hiểu định tuyến qua Transit Gateway<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Cấu hình Route Table trong từng VPC trỏ về TGW<br>&nbsp;&nbsp;+ Dùng Reachability Analyzer kiểm tra kết nối<br>&nbsp;&nbsp;+ Phân tích luồng gói tin giữa các Private Subnet | 12/05/2026 | 12/05/2026 | AWS Module 02 |
| 4 | - Tìm hiểu Amazon EC2 Instance Types, Graviton, Nitro và Snapshot<br>- **Thực hành:**<br>&nbsp;&nbsp;+ So sánh Intel, AMD và ARM Graviton<br>&nbsp;&nbsp;+ Phân biệt Full Snapshot và Incremental Snapshot<br>&nbsp;&nbsp;+ Ghi chú tình huống chọn Instance Type phù hợp | 13/05/2026 | 13/05/2026 | AWS Module 03 |
| 5 | - Tìm hiểu User Data và Instance Metadata<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Cấu hình User Data tự động cài Web Server<br>&nbsp;&nbsp;+ Kiểm tra Apache/Nginx sau khi EC2 khởi động<br>&nbsp;&nbsp;+ Truy vấn Instance Metadata qua `169.254.169.254` | 14/05/2026 | 14/05/2026 | AWS Module 03 |
| 6 | - Tìm hiểu Auto Scaling Group và Amazon S3<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Phân tích điều kiện scale out/in theo CPU metric<br>&nbsp;&nbsp;+ Tạo Amazon S3 Bucket<br>&nbsp;&nbsp;+ Upload và download object cơ bản | 15/05/2026 | 15/05/2026 | AWS Module 03 |
| 7 | - Tìm hiểu EBS, Instance Store và quy trình dọn dẹp tài nguyên<br>- **Thực hành:**<br>&nbsp;&nbsp;+ So sánh độ bền dữ liệu giữa EBS và Instance Store<br>&nbsp;&nbsp;+ Xóa TGW Attachments<br>&nbsp;&nbsp;+ Xóa Transit Gateway<br>&nbsp;&nbsp;+ Xóa CloudFormation Stack theo đúng thứ tự | 16/05/2026 | 16/05/2026 | Cá nhân |

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

### Hình ảnh thực hành tuần 5:

![Thực hành tuần 5 - 522](/images/522.jpg)

![Thực hành tuần 5 - 532](/images/532.jpg)
