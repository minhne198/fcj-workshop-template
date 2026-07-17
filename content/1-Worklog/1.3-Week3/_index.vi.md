---
title: "Worklog Tuần 3"
date: 2026-04-27
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3:
* Hiểu rõ kiến trúc và vai trò của **Amazon VPC** trong việc tạo ra môi trường mạng ảo cô lập và bảo mật trên đám mây.
* Thành thạo các thao tác quản lý địa chỉ IP, phân chia Subnet (Public/Private) và cấu hình bảng định tuyến (Route Table).
* Triển khai các lớp kiểm soát lưu lượng mạng: **Security Groups** (Stateful) và **Network ACLs** (Stateless).
* Thực hành kết nối Internet thông qua **Internet Gateway** và bảo mật truy cập ra ngoài từ Private Subnet qua **NAT Gateway**.
* Bước đầu tìm hiểu các kết nối mạng nâng cao như **VPC Peering** và triển khai **CloudFormation** để tự động hóa hạ tầng.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2 | - Tìm hiểu tổng quan về VPC, dải địa chỉ IP (CIDR) và cách phân chia Subnet hợp lý.<br>- Cấu hình Route Table để điều hướng lưu lượng nội bộ giữa các Subnet. | 27/04/2026 | 27/04/2026 | AWS Networking Guide |
| 3 | - Thiết lập kết nối ra Internet thông qua **Internet Gateway** cho Public Subnet.<br>- Cấu hình **NAT Gateway** để cho phép các tài nguyên trong Private Subnet truy cập Internet mà không bị lộ IP. | 28/04/2026 | 28/04/2026 | AWS Documentation |
| 4 | - Thực hành bảo mật lớp mạng: Cấu hình **Security Groups** và **Network ACLs**, phân biệt cơ chế Stateful và Stateless.<br>- Kiểm thử các kịch bản allow/deny traffic để hiểu cách hai lớp bảo mật hoạt động song song. | 29/04/2026 | 29/04/2026 | Security Essentials |
| 5 | - Nghiên cứu kết nối liên mạng: **VPC Peering** và **Transit Gateway** để kết nối nhiều VPC.<br>- Tìm hiểu **Elastic Load Balancing (ELB)** giúp phân phối tải và tăng tính sẵn sàng của hệ thống. | 30/04/2026 | 30/04/2026 | AWS Study Group |
| 6 | - Thực hành cấu hình **EC2 Instance Connect Endpoint** để quản trị máy chủ từ xa mà không cần Bastion Host.<br>- Thiết lập và kiểm thử kết nối an toàn vào EC2 trong Private Subnet. | 01/05/2026 | 01/05/2026 | AWS Workshop |
| 7 | - Bước đầu tìm hiểu **AWS CloudFormation**: Khái niệm IaC và cách sử dụng Template để khởi tạo tài nguyên tự động.<br>- Tạo **Key Pair** và thực hành kết nối SSH bảo mật vào EC2 Instance. | 02/05/2026 | 02/05/2026 | AWS CloudFormation Guide |

### Kết quả đạt được tuần 3:

* **Về Tư duy kiến trúc mạng:**
    * Có khả năng thiết kế và triển khai môi trường mạng ảo riêng biệt, bảo mật trên AWS theo đúng tiêu chuẩn kiến trúc.
    * Nắm vững cơ chế kiểm soát lưu lượng đầu vào/đầu ra thông qua hai lớp phòng thủ là Security Groups và Network ACLs.
* **Về Kỹ năng triển khai thực tế:**
    * Thành thạo quy trình thiết lập kết nối từ Private Subnet ra ngoài Internet thông qua NAT Gateway.
    * Biết cách quản trị EC2 an toàn trong mạng nội bộ mà không cần công khai địa chỉ IP thực.
    * Hiểu nguyên lý hoạt động của VPC Peering và khi nào nên chọn Transit Gateway thay thế.
* **Về Nền tảng IaC:**
    * Hiểu được sức mạnh của Infrastructure as Code (IaC) trong việc tái sử dụng và chuẩn hóa hạ tầng mạng.

{{% notice success %}}
**Tóm tắt:** Làm chủ VPC là bước đệm quan trọng, tạo nền tảng vững chắc để triển khai các dịch vụ khác như EC2, RDS một cách an toàn, có kiểm soát và tối ưu nhất trong các tuần tiếp theo.
{{% /notice %}}
