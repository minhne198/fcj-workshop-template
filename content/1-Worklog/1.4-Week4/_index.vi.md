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
| 2 | - Tạo **Key Pair** và sử dụng CloudFormation Template để triển khai nhanh hệ thống mạng gồm VPC, Subnet, Security Group.<br>- Cấu hình Security Group chi tiết cho máy chủ Windows trong môi trường Multi-AZ. | 04/05/2026 | 04/05/2026 | AWS Study Group |
| 3 | - Nghiên cứu và cấu hình **Route 53 Resolver Inbound/Outbound Endpoints**.<br>- Tạo Forwarding Rules để đồng bộ DNS resolution giữa môi trường Cloud và hạ tầng On-premises. | 05/05/2026 | 05/05/2026 | AWS Networking Guide |
| 4 | - Khởi tạo **VPC Peering Connection** giữa 2 VPC để kết nối không qua internet công cộng.<br>- Cấu hình bảng định tuyến hai chiều để lưu lượng có thể đi qua đường kết nối Peering. | 06/05/2026 | 06/05/2026 | AWS Documentation |
| 5 | - Kiểm tra bảo mật lưu lượng liên mạng thông qua NACL và Security Group.<br>- Triển khai **Microsoft AD** giả lập và thiết lập DNS cross-domain trong mô hình Hybrid. | 07/05/2026 | 07/05/2026 | AWS Documentation |
| 6 | - Nghiên cứu tổng quan về **AWS Transit Gateway**: Kiến trúc hub-and-spoke và lợi ích so với VPC Peering thuần túy.<br>- Tìm hiểu cách TGW Route Table điều phối lưu lượng giữa các Attachment. | 08/05/2026 | 08/05/2026 | AWS Module 02 |
| 7 | - Tổng hợp hình ảnh thực hành, rà soát toàn bộ cấu hình CloudFormation, Route 53, VPC Peering.<br>- Tìm hiểu về các loại EC2 Instance Type và khi nào nên chọn chip Graviton để tối ưu chi phí. | 09/05/2026 | 09/05/2026 | Cá nhân |

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
