---
title: "Bản đề xuất"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---


# High-Availability Hotel Booking System on AWS  
## Hệ thống Đặt phòng Khách sạn Du lịch chịu tải cao trên AWS  

### 1. Tóm tắt điều hành  
Hệ thống Đặt phòng Khách sạn trực tuyến chịu tải cao trên AWS là một ứng dụng web thương mại điện tử chuyên về lĩnh vực du lịch và lưu trú. Mục tiêu cốt lõi của dự án là xây dựng một giải pháp hạ tầng hiện đại, giúp hệ thống luôn giữ được trạng thái hoạt động ổn định ổn định (High Availability), có khả năng tự động co giãn tài nguyên linh hoạt theo lượng truy cập thực tế (Auto Scaling), và tối ưu hóa hiệu năng phản hồi thông qua việc lưu trữ bộ nhớ đệm (Caching). 

Bằng sự kết hợp giữa backend đạt hiệu năng cao **ASP.NET Core 8 (.NET 8 LTS)** và hệ sinh thái điện toán đám mây đám mây mạnh mẽ của **Amazon Web Services (AWS)**, dự án sẽ chứng minh cách giải quyết triệt để bài toán tải cao và dự phòng rủi ro của các doanh nghiệp số ngày nay.

### 2. Tuyên bố vấn đề  
*Vấn đề hiện tại* Các hệ thống website truyền thống khi triển khai theo mô hình máy chủ vật lý hoặc server đơn lẻ thường gặp phải các hạn chế nghiêm trọng sau trong môi trường thực tế:
* **Tắc nghẽn vào mùa cao điểm**: Vào các dịp lễ Tết hoặc mùa du lịch, lượng truy cập tăng đột biến làm quá tải tài nguyên máy chủ, gây gián đoạn dịch vụ, lag hoặc sập web. Nếu thuê cấu hình cao từ đầu thì lại gây lãng phí chi phí ở những giai đoạn thấp điểm.
* **Điểm lỗi đơn nhất (Single Point of Failure)**: Toàn bộ ứng dụng phụ thuộc vào một máy chủ duy nhất. Khi phần cứng máy chủ gặp sự cố hoặc mất mạng, website hoàn toàn tê liệt, gây thiệt hại lớn về doanh thu và trải nghiệm người dùng.
* **Quá tải Cơ sở dữ liệu**: Khi hàng ngàn người dùng thực hiện các thao tác tìm kiếm phòng trùng lặp liên tục, cơ sở dữ liệu quan hệ phải chịu áp lực truy vấn trực tiếp rất lớn, dẫn đến phản hồi chậm hoặc crash database.
* **Rủi ro trùng lặp dữ liệu (Overbooking)**: Thiếu cơ chế khóa đồng thời mạnh mẽ khiến hai khách hàng có thể đặt và thanh toán thành công cùng một phòng vào cùng một thời điểm.

*Giải pháp đề xuất* Nền tảng ứng dụng sẽ chuyển dịch hoàn toàn lên mô hình Cloud-Native trên AWS để giải quyết triệt để các bài toán trên:
* **Phân tải và Dự phòng lỗi**: Sử dụng **Application Load Balancer (ALB)** phối hợp với **Auto Scaling Group (ASG)** để phân phối lưu lượng truy cập đều sang các instance máy chủ **EC2** phân bổ ở nhiều Vùng sẵn sàng (Availability Zone - AZ) khác nhau. Nếu một vùng gặp sự cố phần cứng, hệ thống tự động định tuyến lại dòng dữ liệu sang vùng còn lại một cách mượt mà dưới 30 giây.
* **Tự động co giãn theo nhu cầu**: ASG giám sát chỉ số CPU Utilization, tự động tăng cường số lượng máy chủ khi tải cao và tự động giảm số lượng instance khi hạ tải để tiết kiệm tối đa ngân sách tài nguyên.
* **Tối ưu tốc độ với Redis Cache**: Tích hợp cụm bộ nhớ đệm **Amazon ElastiCache Redis** để lưu trữ kết quả các truy vấn tìm kiếm phổ biến. Rút ngắn thời gian phản hồi từ ~150ms xuống chỉ còn dưới < 5ms, đồng thời giải phóng hoàn toàn áp lực truy cập trực tiếp cho Database RDS MySQL.
* **Cơ chế chống Overbooking nghiêm ngặt**: Áp dụng kỹ thuật **Row-Level Locking (SELECT FOR UPDATE)** kết hợp với Database Transaction có tính toàn vẹn cao (Serializable) của EF Core để khóa dữ liệu phòng ngay tại thời điểm xử lý thanh toán.

*Lợi ích và hoàn vốn đầu tư (ROI)* * **Giá trị nghiên cứu & Thực tiễn**: Đóng vai trò như một kiến trúc mẫu chuẩn (Blueprint) hoàn chỉnh về tính Sẵn sàng cao (HA) cho các hệ thống ứng dụng Web Enterprise. Toàn bộ hạ tầng đám mây được định nghĩa bằng mã nguồn **AWS CDK (TypeScript)** giúp dễ dàng quản lý, nhân bản và tái sử dụng cho các nghiên cứu tiếp theo.
* **Tối ưu hóa chi phí vận hành**: Bằng cách tận dụng linh hoạt chính sách tự động co giãn (Scale-in khi ít người dùng) kết hợp ưu đãi từ gói **AWS Free Tier** (cho EC2, RDS, Redis), tổng chi phí vận hành hạ tầng thử nghiệm và triển khai dự án cực kỳ thấp, **ước tính chưa đến 10 USD (~250.000 VNĐ)** cho toàn bộ vòng đời đồ án.
* **Giảm thiểu thời gian quản trị**: Tự động hóa hoàn toàn luồng giám sát qua CloudWatch và cảnh báo sự cố tức thời đến Email thông qua Amazon SNS, loại bỏ yêu cầu phải có kỹ sư túc trực hệ thống 24/7.

### 3. Kiến trúc giải pháp  
Hệ thống áp dụng kiến trúc đa tầng bảo mật (Multi-tier Architecture) triển khai bên trong một mạng ảo độc lập **Amazon VPC**, tách biệt rõ ràng giữa phân vùng công khai (Public Subnets) và phân vùng bảo mật (Private Subnets) nhằm đảm bảo an toàn an ninh dữ liệu cao nhất.

*Các dịch vụ AWS sử dụng:*
* **Amazon VPC**: Thiết lập môi trường mạng cô lập bao gồm 2 Public Subnets và 4 Private Subnets trải rộng trên 2 Vùng sẵn sàng (AZ).
* **Application Load Balancer (ALB)**: Tiếp nhận dữ liệu lưu lượng cổng 80/443, điều phối tải thông minh đến các instance EC2 trong vùng Private Subnet.
* **Amazon EC2 & Auto Scaling Group**: Sử dụng instance `t3.micro` chạy hệ điều hành Amazon Linux 2023 làm máy chủ API, thiết lập cấu hình co giãn tự động từ 1 đến tối đa 4 máy chủ.
* **Amazon RDS MySQL**: Hệ quản trị CSDL quan hệ lưu thông tin cốt lõi (khách sạn, phòng, hóa đơn), hỗ trợ cấu hình Multi-AZ để đồng bộ và dự phòng dữ liệu tự động.
* **Amazon ElastiCache (Redis)**: Cung cấp bộ nhớ đệm phân tán dùng chung cho toàn bộ các instance EC2 trong ASG nhằm tăng tốc độ truy vấn.
* **Amazon S3 & CloudFront**: S3 đóng vai trò lưu trữ các asset tĩnh của Frontend và hình ảnh hệ thống; CloudFront đóng vai trò CDN phân phối nội dung tốc độ cao toàn cầu, giao tiếp an toàn qua Origin Access Control (OAC).
* **Hệ thống Giám sát & Bảo mật**: Tích hợp AWS WAF (lọc request độc hại), KMS (mã hóa dữ liệu), Secrets Manager (quản lý biến môi trường an toàn), CloudWatch (giám sát metrics) và SNS (bắn cảnh báo sự cố tự động).

### 4. Triển khai kỹ thuật  
*Các giai đoạn triển khai:*
1. **Giai đoạn 1: Thiết lập hạ tầng mạng & Bảo mật (Tuần 1)**: Quy hoạch VPC, chia Subnets, cấu hình Route Tables, NAT Gateways và thiết lập các Security Groups nghiêm ngặt.
2. **Giai đoạn 2: Khởi tạo tầng Dữ liệu đám mây (Tuần 2)**: Tạo cụm RDS MySQL và ElastiCache Redis trên AWS, thực hiện kết nối database, khởi tạo cấu trúc bảng (Schema) và đổ dữ liệu mẫu (Seed Data).
3. **Giai đoạn 3: Phát triển Backend API & Tối ưu logic (Tuần 3)**: Lập trình các Controller nghiệp vụ bằng ASP.NET Core 8, tích hợp logic xử lý Redis Cache và Transaction chống đặt trùng phòng.
4. **Giai đoạn 4: Xây dựng Giao diện Frontend (Tuần 4)**: Phát triển giao diện Web responsive (HTML5/Bootstrap/Vanilla JS), đóng gói ứng dụng và deploy lên Amazon S3 & CloudFront.
5. **Giai đoạn 5: Cấu hình ASG & Kiểm thử tải (Tuần 5-6)**: Tạo Launch Template, dựng ALB, cấu hình luật Auto Scaling. Sử dụng **Locust** giả lập 300 người dùng truy cập đồng thời để kiểm tra tính năng tự co giãn và kịch bản sập máy chủ (Failover).
6. **Giai đoạn 6: Mã hóa hạ tầng & Giám sát tự động (Tuần 7-8)**: Chuyển đổi toàn bộ cấu hình hạ tầng thủ công sang mã nguồn **AWS CDK**, thiết lập Dashboard CloudWatch và kích hoạt cảnh báo tự động qua SNS.

*Yêu cầu kỹ thuật:*
* **Môi trường**: Visual Studio 2022 / VS Code, .NET 8 SDK, Node.js (phục vụ AWS CDK), AWS CLI.
* **Kỹ năng chuyên môn**: Am hiểu Entity Framework Core, LINQ, cơ chế bất đồng bộ (Async/Await), tư duy lập trình Thread-safe và xử lý Database Transaction chuyên sâu; có kiến thức vững về định tuyến mạng đám mây, Routing, IAM Roles/Policies bảo mật.

### 5. Lộ trình & Mốc triển khai  
Lịch trình chi tiết kéo dài trong vòng **9 tuần** tuần tự như sau:
* **Tuần 1**: Khởi động dự án, thiết lập VPC mạng, cấu hình thực thi môi trường local.
* **Tuần 2**: Triển khai và cấu hình thành công cụm Database RDS và Redis Cache lên đám mây AWS.
* **Tuần 3**: Hoàn thiện 100% mã nguồn Backend API chức năng (Auth, Search, Booking, Admin) có tích hợp Swagger.
* **Tuần 4**: Xây dựng xong các thành phần giao diện UI Frontend, deploy thành công lên S3/CloudFront.
* **Tuần 5**: Triển khai API lên EC2 thông qua Launch Template, cấu hình ALB Target Group nhận diện Health Check thành công.
* **Tuần 6**: Thực hiện Load Testing bằng công cụ Locust, kiểm tra và tinh chỉnh thông số Target CPU Tracking linh hoạt.
* **Tuần 7-8**: Đóng gói mã nguồn AWS CDK hoàn chỉnh, cấu hình bảng giám sát CloudWatch và tự động hóa cảnh báo.
* **Tuần 9**: Tổng duyệt kịch bản demo ứng dụng, chuẩn bị slide báo cáo và tiến hành bảo vệ trước hội đồng.

### 6. Ước tính ngân sách  
Hệ thống áp dụng chiến lược tối ưu hóa chi phí nghiêm ngặt, hầu hết cấu hình tài nguyên đều nằm trong phạm vi **AWS Free Tier**.

*Bảng chi tiết chi phí hạ tầng ước tính khi vận hành:*
* **Amazon EC2 (`t3.micro`)**: 0.00 USD (Nằm trong 750 giờ Free Tier miễn phí mỗi tháng).
* **Amazon RDS MySQL (`db.t3.micro`)**: 0.00 USD (Nằm trong 750 giờ Free Tier miễn phí mỗi tháng).
* **Amazon ElastiCache Redis (`cache.t3.micro`)**: 0.00 USD (Hưởng gói ưu đãi Free Tier).
* **Application Load Balancer**: ~0.025 USD/giờ (Chỉ bật khi thực hiện test tải và demo, ước tính tốn khoảng ~1.50 USD).
* **NAT Gateway**: ~0.059 USD/giờ (Sử dụng script tắt/bật thông minh để tối ưu, ước tính khoảng ~3.00 USD).
* **Amazon S3 & CloudFront**: ~0.20 USD (Lưu trữ dữ liệu file tĩnh và băng thông truyền tải dữ liệu dung lượng thấp).

**Tổng chi phí dự kiến**: **< 10 USD (Khoảng 250.000 VNĐ)** cho toàn bộ quá trình thực hiện đồ án tốt nghiệp nhờ áp dụng quy tắc tắt tài nguyên / giảm Desired Capacity về mốc 0 khi không sử dụng qua đêm.

### 7. Đánh giá rủi ro  
*Ma trận rủi ro & Chiến lược giảm thiểu:*
* **Rủi ro lộ thông tin bảo mật**: Nguy cơ lộ Access Key khi đưa code lên GitHub công khai. *Giảm thiểu:* Tuyệt đối **KHÔNG** mã hóa cứng mật mã hoặc key bí mật vào code. Sử dụng file `.env` được khai báo trong `.gitignore` và chuyển sang sử dụng hoàn toàn **IAM Role** gắn trực tiếp vào Instance Profile của EC2.
* **Rủi ro vượt ngân sách (Shock hóa đơn AWS)**: Quên tắt các tài nguyên có phí sau khi kết thúc buổi làm việc. *Giảm thiểu:* Thiết lập công cụ **AWS Budgets** với hạn mức báo động ở mốc **10$**, tự động gửi email cảnh báo ngay lập tức nếu chi phí vượt ngưỡng dự kiến.
* **Rủi ro API mất kết nối Database trong lúc demo**: Do độ trễ khởi động lạnh (Cold-start) của tài nguyên đám mây. *Giảm thiểu:* Xây dựng sẵn script kiểm tra sức khỏe hệ thống tự động `warmup.sh` để kích hoạt khởi động sớm toàn bộ hệ thống (RDS, EC2, Redis) trước buổi báo cáo chính thức 30 phút.

### 8. Kết quả kỳ vọng  
* **Về mặt Chức năng**: Ứng dụng thương mại điện tử du lịch vận hành hoàn chỉnh từ khâu Đăng ký/Đăng nhập, Tìm kiếm phòng bộ lọc thông minh, Đặt phòng thời gian thực đến hiển thị trang dashboard quản trị dành cho Admin.
* **Về mặt Kỹ thuật Cloud**:
  * Chứng minh trực quan tính **Sẵn sàng cao (HA)**: Chủ động xóa (Terminate) một máy chủ đang gánh tải ngay trên giao diện AWS Console trước hội đồng, hệ thống vẫn duy trì hoạt động bình thường, không phát sinh lỗi phản hồi.
  * Chứng minh cơ chế **Tự động co giãn (Auto Scaling)**: Biểu đồ CloudWatch ghi nhận chính xác CPU đạt ngưỡng tải cao và tự động kích hoạt tăng số lượng máy chủ lên để đáp ứng lưu lượng từ công cụ test Locust.
  * Tối ưu hóa **Caching**: Chứng minh đo đạc tường minh thời gian phản hồi API giảm mạnh từ ~150ms xuống chỉ còn ~4ms nhờ cơ chế lưu cache phân tán.