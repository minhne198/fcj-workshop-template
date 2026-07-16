---
title : "Giới thiệu"
date : 2024-01-01 
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---


### Giới thiệu dự án AWS_OmniStay

Dự án **AWS_OmniStay** là một ứng dụng web đặt phòng khách sạn trực tuyến (quy mô tương tự mẫu thu nhỏ của Booking.com hoặc Agoda.com). Ngoài việc xử lý các nghiệp vụ cốt lõi như tìm kiếm phòng trống theo địa điểm/ngày đặt, đặt phòng theo thời gian thực và quản lý lịch sử giao dịch, mục tiêu tối thượng của bài thực hành này là triển khai toàn bộ hệ thống lên môi trường Điện toán đám mây Amazon Web Services (AWS) để tối ưu hóa hiệu năng, tính bảo mật và khả năng chịu tải[cite: 11].

Bài workshop này sẽ hướng dẫn từng bước xây dựng, cấu hình và vận hành một hạ tầng phân tầng (N-tier Architecture) hoàn chỉnh nhằm chứng minh 3 tính chất nền tảng của Cloud Computing[cite: 11]:

### Workshop Objectives

Workshop này hướng dẫn từng bước triển khai hệ thống **AWS_OmniStay** trên nền tảng Amazon Web Services (AWS), từ khâu chuẩn bị môi trường đến xây dựng hạ tầng, triển khai ứng dụng và đánh giá hiệu năng. Sau khi hoàn thành Workshop, người thực hiện sẽ có thể:

- Chuẩn bị môi trường phát triển và cấu hình tài khoản AWS.
- Triển khai giao diện Frontend lên **Amazon S3** và phân phối nội dung thông qua **Amazon CloudFront**.
- Thiết kế và triển khai hạ tầng mạng sử dụng **Amazon VPC**, Public Subnets và Private Subnets.
- Triển khai ứng dụng **ASP.NET Core (.NET 8)** trên các máy chủ **Amazon EC2**.
- Xây dựng hệ thống cơ sở dữ liệu **Amazon RDS MySQL Multi-AZ** nhằm đảm bảo tính sẵn sàng cao.
- Triển khai **Amazon ElastiCache Redis** để tăng tốc độ phản hồi của hệ thống.
- Cấu hình **Application Load Balancer (ALB)** để phân phối lưu lượng truy cập đến các máy chủ ứng dụng.
- Thiết lập **Auto Scaling Group (ASG)** nhằm tự động mở rộng hoặc thu hẹp số lượng EC2 dựa trên mức sử dụng CPU.
- Giám sát tài nguyên bằng **Amazon CloudWatch** và kiểm soát chi phí triển khai bằng **AWS Budget**.
- Thực hiện kiểm thử chịu tải bằng **Locust** và đánh giá hiệu quả của Redis Cache cũng như Auto Scaling thông qua các chỉ số hiệu năng.
### Workshop Scope

Workshop tập trung triển khai và đánh giá các dịch vụ cốt lõi của AWS phục vụ cho hệ thống đặt phòng khách sạn trực tuyến AWS_OmniStay. Phạm vi triển khai bao gồm:

| Thành phần | Mục đích |
| :--- | :--- |
| Amazon S3 | Lưu trữ mã nguồn Frontend dưới dạng Static Website. |
| Amazon CloudFront | Phân phối nội dung tĩnh thông qua mạng lưới CDN. |
| Origin Access Control (OAC) | Bảo vệ S3 Bucket, chỉ cho phép CloudFront truy cập. |
| Amazon VPC | Xây dựng môi trường mạng riêng biệt cho hệ thống. |
| Amazon EC2 | Chạy ứng dụng Backend ASP.NET Core Web API. |
| Application Load Balancer | Cân bằng tải giữa nhiều EC2 Instance. |
| Auto Scaling Group | Tự động mở rộng hoặc thu hẹp số lượng EC2 theo tải hệ thống. |
| Amazon RDS MySQL | Lưu trữ dữ liệu nghiệp vụ của hệ thống. |
| Amazon ElastiCache Redis | Lưu trữ dữ liệu đệm nhằm tăng tốc độ phản hồi. |
| Amazon CloudWatch | Theo dõi hiệu năng và thiết lập cảnh báo. |
| AWS Budget | Giám sát và kiểm soát chi phí sử dụng dịch vụ AWS. |
| Locust | Mô phỏng người dùng đồng thời để kiểm thử khả năng chịu tải của hệ thống. |

1. **Tính Sẵn sàng cao (High Availability - HA):** Hệ thống được phân bổ trên nhiều Vùng sẵn sàng (Availability Zones - AZs) để đảm bảo không có điểm lỗi đơn lẻ (Single Point of Failure). Website vẫn hoạt động bình thường ngay cả khi một trung tâm dữ liệu gặp sự cố vật lý[cite: 11].
2. **Tính Tự động co giãn (Auto Scaling):** Hạ tầng máy chủ tính toán tự động co giãn số lượng instance dựa trên nhu cầu sử dụng thực tế của khách hàng (Scale-out khi tải cao và Scale-in khi thấp để tối ưu chi phí)[cite: 11].
3. **Cơ chế Caching dữ liệu:** Tối ưu hóa tốc độ phản hồi thông qua tầng lưu trữ đệm bộ nhớ đệm, giảm thiểu gánh nặng truy vấn trực tiếp vào Cơ sở dữ liệu quan hệ cho các yêu cầu lặp đi lặp lại[cite: 11].

---
### Expected System Objectives

Ngoài việc triển khai thành công các dịch vụ AWS, Workshop còn hướng tới việc đánh giá hiệu quả của kiến trúc thông qua các mục tiêu định lượng sau:

- Đảm bảo hệ thống luôn sẵn sàng phục vụ khi một Availability Zone gặp sự cố bằng cách triển khai các thành phần dự phòng.
- Tự động mở rộng số lượng EC2 Instance khi **CPU Utilization vượt quá 70%** và tự động thu hẹp khi tải giảm nhằm tối ưu chi phí vận hành.
- Giảm thời gian phản hồi của các truy vấn phổ biến từ khoảng **150 ms (Cache MISS)** xuống còn khoảng **4–5 ms (Cache HIT)** nhờ sử dụng Amazon ElastiCache Redis.
- Phân phối nội dung tĩnh thông qua Amazon CloudFront để giảm độ trễ truy cập và tăng tốc độ tải trang cho người dùng.
- Theo dõi và kiểm soát chi phí sử dụng AWS bằng AWS Budget với ngưỡng cảnh báo **10 USD** trong suốt quá trình triển khai Workshop.
 
### Sơ đồ kiến trúc tổng thể (Architecture Diagram)

Hệ thống được thiết kế theo đúng quy chuẩn kiến trúc Cloud tốt nhất (AWS Well-Architected Framework), chia tách rõ ràng giữa môi trường Public tiếp nhận lưu lượng và môi trường Private cô lập hoàn toàn cho ứng dụng cũng như dữ liệu[cite: 11].


![AWS OmniStay Infrastructure Architecture](/images/aws-omnistay-architecture.png)

### Architecture Request Flow

Luồng xử lý yêu cầu của hệ thống được mô tả như sau:

```text
                User
                  │
                  ▼
          Amazon CloudFront
                  │
        (Static Content Request)
                  │
                  ▼
         Amazon S3 Private Bucket
                  │
                  │
        (API Request: /api/*)
                  ▼
     Application Load Balancer (ALB)
                  │
                  ▼
      Auto Scaling Group (EC2)
                  │
        ASP.NET Core Web API
          │                 │
          ▼                 ▼
 Amazon ElastiCache     Amazon RDS
       Redis             MySQL Multi-AZ
```

Trong kiến trúc trên, các tệp tĩnh như HTML, CSS và JavaScript được lưu trữ trong Amazon S3 và chỉ được truy cập thông qua Amazon CloudFront bằng cơ chế Origin Access Control (OAC). Đối với các yêu cầu API, Application Load Balancer sẽ phân phối lưu lượng đến các EC2 trong Auto Scaling Group. Backend ưu tiên truy vấn Redis trước để giảm thời gian phản hồi; nếu dữ liệu chưa tồn tại trong bộ nhớ đệm, hệ thống sẽ truy vấn xuống Amazon RDS MySQL và đồng thời cập nhật lại Redis cho các lần truy cập tiếp theo.

#### Giải thích luồng hoạt động của request:

* **Tầng phân phối nội dung tĩnh (Frontend Static Assets Distributed):** Người dùng truy cập trang web thông qua dịch vụ phân giải tên miền **Amazon Route 53** nối tới CDN **Amazon CloudFront**[cite: 11]. Toàn bộ giao diện HTML, CSS, và JavaScript tĩnh được lưu trữ an toàn trong **Amazon S3 Private Bucket** và chỉ cho phép CloudFront tiếp cận qua cơ chế **Origin Access Control (OAC)**[cite: 11]. Hệ thống được bảo vệ vòng ngoài bằng **AWS WAF** nhằm ngăn chặn các cuộc tấn công DDoS, SQL Injection và XSS[cite: 11].
* **Tầng xử lý logic ứng dụng (API Backend Layer):** Mọi request API (đường dẫn `/api/*`) gửi từ trình duyệt sẽ được CloudFront điều hướng tới cổng dịch vụ của **Application Load Balancer (ALB)** nằm tại Public Subnets[cite: 11]. ALB thực hiện kiểm tra sức khỏe (Health Check) liên tục và phân phối đều lưu lượng đến các máy chủ ảo **Amazon EC2** chạy ứng dụng ASP.NET Core Web API thông qua cổng giao tiếp `8080` phía trong Private App Subnets[cite: 11].
* **Tầng cơ sở dữ liệu và bộ nhớ đệm (Database & Cache Layer):** Khi khách hàng thực hiện tìm kiếm phòng trống, ứng dụng .NET sẽ kiểm tra bộ nhớ đệm **Amazon ElastiCache Redis** trước[cite: 11]. Nếu dữ liệu đã tồn tại (Cache HIT), kết quả được trả về ngay lập tức với độ trễ cực thấp (< 5ms)[cite: 11]. Nếu chưa có dữ liệu (Cache MISS), hệ thống mới thực hiện truy vấn xuống hệ quản trị cơ sở dữ liệu **Amazon RDS MySQL** (Cấu hình Multi-AZ Primary + Standby để dự phòng thảm họa)[cite: 11].

---

### Ngăn xếp Công nghệ (Tech Stack) Sử dụng

| Tầng chức năng | Công nghệ / Dịch vụ áp dụng | Vai trò chi tiết trong Workshop |
| :--- | :--- | :--- |
| **Client / Frontend** | HTML5, CSS3, Bootstrap 5.3, Vanilla JavaScript[cite: 11] | Xây dựng giao diện responsive kết nối bất đồng bộ gọi API bằng Fetch/Axios[cite: 11]. |
| **API / Backend** | ASP.NET Core (.NET 8 LTS), Entity Framework Core[cite: 11] | Xử lý logic nghiệp vụ, xác thực JWT, thực thi Transaction ngăn chặn Overbooking[cite: 11]. |
| **Compute / Routing** | Amazon EC2, Application Load Balancer, Route 53[cite: 11] | Cung cấp tài nguyên tính toán và cân bằng tải phân phối traffic cho Web API[cite: 11]. |
| **Storage / CDN** | Amazon S3, Amazon CloudFront[cite: 11] | Lưu trữ mã nguồn frontend riêng tư, tăng tốc tải trang qua mạng lưới Edge Location[cite: 11]. |
| **Database / Cache** | Amazon RDS MySQL 8.0, ElastiCache Redis[cite: 11] | Lưu trữ dữ liệu nghiệp vụ lâu dài và xử lý lớp đệm tăng tốc độ tìm kiếm[cite: 11]. |
| **Operations / Security**| Amazon CloudWatch, CloudWatch Alarms, AWS Budget, IAM[cite: 11] | Giám sát tài nguyên, thiết lập cảnh báo vượt chi phí và phân quyền bảo mật cho EC2[cite: 11]. |
| **Load Testing** | Locust (Python Framework)[cite: 11] | Công cụ giả lập hàng trăm user truy cập đồng thời để kiểm tra khả năng Auto Scaling[cite: 11]. |

### Expected Outcome

Sau khi hoàn thành toàn bộ Workshop, người thực hiện sẽ xây dựng thành công một hệ thống đặt phòng khách sạn trực tuyến có khả năng triển khai trên nền tảng Amazon Web Services với các đặc điểm sau:

- Frontend được lưu trữ trên Amazon S3 và phân phối thông qua Amazon CloudFront.
- Backend ASP.NET Core hoạt động ổn định phía sau Application Load Balancer.
- Hệ thống có khả năng tự động mở rộng bằng Auto Scaling Group dựa trên mức sử dụng CPU.
- Cơ sở dữ liệu Amazon RDS MySQL được triển khai theo mô hình Multi-AZ nhằm nâng cao tính sẵn sàng.
- Amazon ElastiCache Redis giúp giảm đáng kể thời gian phản hồi của các truy vấn phổ biến.
- Toàn bộ hệ thống được giám sát bằng Amazon CloudWatch và kiểm soát chi phí bằng AWS Budget.
- Kết quả kiểm thử chịu tải bằng Locust cho thấy hệ thống đáp ứng tốt khi có nhiều người dùng truy cập đồng thời, đồng thời chứng minh hiệu quả của cơ chế Redis Cache và Auto Scaling trong việc cải thiện hiệu năng cũng như khả năng mở rộng của ứng dụng.
