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
| 2 | - Tìm hiểu Amazon VPC, CIDR và Subnet<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Xác định dải CIDR cho VPC<br>&nbsp;&nbsp;+ Chia Public Subnet và Private Subnet<br>&nbsp;&nbsp;+ Cấu hình Route Table cho các Subnet | 27/04/2026 | 27/04/2026 | AWS Networking Guide |
| 3 | - Tìm hiểu Internet Gateway và NAT Gateway<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Gắn Internet Gateway cho Public Subnet<br>&nbsp;&nbsp;+ Tạo NAT Gateway cho Private Subnet<br>&nbsp;&nbsp;+ Kiểm tra kết nối Internet từ tài nguyên private | 28/04/2026 | 28/04/2026 | AWS Documentation |
| 4 | - Tìm hiểu Security Group và Network ACL<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Cấu hình Security Group<br>&nbsp;&nbsp;+ Cấu hình Network ACL<br>&nbsp;&nbsp;+ Kiểm thử allow/deny traffic<br>&nbsp;&nbsp;+ Phân biệt Stateful và Stateless | 29/04/2026 | 29/04/2026 | Security Essentials |
| 5 | - Tìm hiểu VPC Peering, Transit Gateway và Elastic Load Balancing (ELB)<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Phân tích mô hình kết nối nhiều VPC<br>&nbsp;&nbsp;+ So sánh Peering và Transit Gateway<br>&nbsp;&nbsp;+ Ghi chú vai trò ELB trong kiến trúc High Availability | 30/04/2026 | 30/04/2026 | AWS Study Group |
| 6 | - Tìm hiểu EC2 Instance Connect Endpoint<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Cấu hình EC2 Instance Connect Endpoint<br>&nbsp;&nbsp;+ Kết nối an toàn vào EC2 trong Private Subnet<br>&nbsp;&nbsp;+ Kiểm tra kết nối không cần Bastion Host | 01/05/2026 | 01/05/2026 | AWS Workshop |
| 7 | - Tìm hiểu AWS CloudFormation và Key Pair<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Đọc cấu trúc CloudFormation Template<br>&nbsp;&nbsp;+ Tạo Key Pair<br>&nbsp;&nbsp;+ Kết nối SSH bảo mật vào EC2 Instance | 02/05/2026 | 02/05/2026 | AWS CloudFormation Guide |

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

### Hình ảnh thực hành tuần 3:

![Tạo Security Group](/images/worklog/Tao_SecurityGroup.jpg)

![Tạo Gateway](/images/worklog/Tao_Gateway.jpg)
