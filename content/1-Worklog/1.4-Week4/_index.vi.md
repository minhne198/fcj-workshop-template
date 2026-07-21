---
title: "Worklog Tuần 4"
date: 2026-05-04
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu tuần 4:
* Sử dụng **AWS CloudFormation** để tự động hóa hoàn toàn việc khởi tạo hạ tầng mạng phức tạp (IaC).
* Thiết lập hệ thống phân giải tên miền lai (**Hybrid DNS**) với **Route 53 Resolver** để đồng bộ DNS giữa AWS và On-premises.
* Kết nối an toàn giữa hai VPC bằng **VPC Peering** và kiểm soát lưu lượng liên mạng bằng Security Group/NACL.
* Bước đầu nghiên cứu kiến trúc **Amazon EC2**: Phân biệt các dòng chip (Intel, AMD, Graviton) và hệ thống ảo hóa Nitro.
* Tìm hiểu cơ chế **Transit Gateway (TGW)** như giải pháp kết nối nhiều VPC thay thế cho Peering phức tạp.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2 | - Tìm hiểu AWS CloudFormation và hạ tầng mạng Multi-AZ<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Tạo Key Pair<br>&nbsp;&nbsp;+ Triển khai VPC, Subnet, Security Group bằng CloudFormation Template<br>&nbsp;&nbsp;+ Cấu hình Security Group cho máy chủ Windows | 04/05/2026 | 04/05/2026 | AWS Study Group |
| 3 | - Tìm hiểu Route 53 Resolver và Hybrid DNS<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Cấu hình Inbound Endpoint<br>&nbsp;&nbsp;+ Cấu hình Outbound Endpoint<br>&nbsp;&nbsp;+ Tạo Forwarding Rules đồng bộ DNS giữa Cloud và On-premises | 05/05/2026 | 05/05/2026 | AWS Networking Guide |
| 4 | - Tìm hiểu VPC Peering Connection<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Tạo VPC Peering Connection giữa 2 VPC<br>&nbsp;&nbsp;+ Cấu hình Route Table hai chiều<br>&nbsp;&nbsp;+ Kiểm tra lưu lượng đi qua Peering Connection | 06/05/2026 | 06/05/2026 | AWS Documentation |
| 5 | - Tìm hiểu bảo mật lưu lượng liên mạng và mô hình Hybrid DNS<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Kiểm tra NACL và Security Group giữa các mạng<br>&nbsp;&nbsp;+ Triển khai Microsoft AD giả lập<br>&nbsp;&nbsp;+ Thiết lập DNS cross-domain trong mô hình Hybrid | 07/05/2026 | 07/05/2026 | AWS Documentation |
| 6 | - Tìm hiểu AWS Transit Gateway (TGW)<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Phân tích kiến trúc hub-and-spoke<br>&nbsp;&nbsp;+ So sánh TGW với VPC Peering<br>&nbsp;&nbsp;+ Tìm hiểu cách TGW Route Table điều phối traffic giữa các Attachment | 08/05/2026 | 08/05/2026 | AWS Module 02 |
| 7 | - Tìm hiểu EC2 Instance Type và chip Graviton<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Rà soát cấu hình CloudFormation<br>&nbsp;&nbsp;+ Rà soát Route 53 Resolver và VPC Peering<br>&nbsp;&nbsp;+ Tổng hợp hình ảnh thực hành tuần 4 | 09/05/2026 | 09/05/2026 | Cá nhân |

### Kết quả đạt được tuần 4:

* **Tự động hóa hạ tầng (IaC):**
    * Làm chủ kỹ thuật dùng **CloudFormation** để tái tạo hạ tầng mạng hoàn chỉnh chỉ bằng một Template, tiết kiệm thời gian và giảm sai sót cấu hình thủ công.
    * Hiểu rõ cấu trúc CloudFormation Template và cách sử dụng Parameters, Resources, Outputs.
* **Hệ thống DNS lai (Hybrid DNS):**
    * Cấu hình thành công **Route 53 Resolver**, giúp tài nguyên trên AWS phân giải tên miền nội bộ On-premises và ngược lại.
    * Nắm vững cách vận hành Inbound/Outbound Endpoints để điều phối các yêu cầu DNS xuyên môi trường.
* **Kết nối liên mạng:**
    * Triển khai thành công **VPC Peering**, đảm bảo dữ liệu di chuyển qua đường nội bộ AWS, tăng tốc độ và bảo mật.
    * Hiểu giới hạn của Peering (không transitive) và biết khi nào cần nâng cấp lên Transit Gateway.

{{% notice info %}}
**Tóm tắt:** Tuần 4 giúp chuyển tư duy từ quản lý đơn lẻ sang thiết kế hệ thống quy mô, kết nối đa môi trường (Cloud + On-premise) và tự động hóa hạ tầng — những kỹ năng cốt lõi của một Cloud Engineer chuyên nghiệp.
{{% /notice %}}

### Hình ảnh thực hành tuần 4:

![Cấu hình hạ tầng VPC tuần 4](/images/worklog/Screenshot%202026-05-20%20152142.jpg)

![Tạo VPC bằng CloudFormation](/images/worklog/Tao_VPCs.png.jpg)
