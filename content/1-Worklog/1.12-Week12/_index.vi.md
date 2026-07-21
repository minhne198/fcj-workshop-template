---
title: "Worklog Tuần 12"
date: 2026-06-29
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

### Mục tiêu tuần 12:
* Hoàn thiện toàn bộ Backend API và Frontend của hệ thống đặt phòng khách sạn.
* Triển khai **Phase 4**: Cấu hình Application Load Balancer (ALB), Auto Scaling Group (ASG) và CloudWatch Alarm.
* Triển khai **Phase 5**: Xuất bản frontend lên S3 + CloudFront, tích hợp WAF bảo vệ hệ thống.
* Kiểm thử toàn diện: HA Test (tắt EC2), Load Test (Locust 300 users), Cache Benchmark.
* Chuẩn bị tài liệu và kịch bản demo báo cáo đề tài.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2 | - Tìm hiểu hoàn thiện Backend API và Redis Cache<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Hoàn thiện `HotelsController.cs`<br>&nbsp;&nbsp;+ Hoàn thiện `BookingsController.cs`<br>&nbsp;&nbsp;+ Hoàn thiện `AdminController.cs`<br>&nbsp;&nbsp;+ Tích hợp Redis Cache vào SearchService<br>&nbsp;&nbsp;+ Kiểm tra Cache HIT dưới 5ms và TTL 5 phút | 29/06/2026 | 29/06/2026 | Visual Studio 2022 |
| 3 | - Phase 4 - Tìm hiểu Compute layer với EC2, ALB và Target Group<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Tạo EC2 Launch Template<br>&nbsp;&nbsp;+ Viết User Data script tự động cài .NET 8<br>&nbsp;&nbsp;+ Tạo Application Load Balancer<br>&nbsp;&nbsp;+ Tạo Target Group và Health Check `/health` | 30/06/2026 | 30/06/2026 | AWS Console |
| 4 | - Tìm hiểu Auto Scaling Group, CloudWatch Alarm và SNS<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Tạo Auto Scaling Group Min=1, Max=4<br>&nbsp;&nbsp;+ Cấu hình Target CPU=70%<br>&nbsp;&nbsp;+ Tạo CloudWatch Alarm khi CPU > 70%<br>&nbsp;&nbsp;+ Cấu hình SNS gửi email cảnh báo cho Admin | 01/07/2026 | 01/07/2026 | AWS Console |
| 5 | - Phase 5 - Tìm hiểu Frontend hosting, CDN và WAF<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Upload HTML, CSS, JS lên Amazon S3<br>&nbsp;&nbsp;+ Bật Static Website Hosting<br>&nbsp;&nbsp;+ Tạo CloudFront Distribution dùng OAC<br>&nbsp;&nbsp;+ Forward `/api/*` đến ALB<br>&nbsp;&nbsp;+ Gắn AWS WAF chặn SQL Injection và XSS | 02/07/2026 | 02/07/2026 | AWS Console |
| 6 | - Tìm hiểu kiểm thử High Availability và Load Testing<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Terminate 1 EC2 trong ASG<br>&nbsp;&nbsp;+ Kiểm tra ALB chuyển traffic sang EC2 còn lại<br>&nbsp;&nbsp;+ Chạy Locust giả lập 300 người dùng đồng thời<br>&nbsp;&nbsp;+ Quan sát ASG scale lên 2-3 EC2 | 03/07/2026 | 03/07/2026 | Locust |
| 7 | - Tìm hiểu đo lường hiệu năng và chuẩn bị demo<br>- **Thực hành:**<br>&nbsp;&nbsp;+ So sánh response time không cache và có Redis cache<br>&nbsp;&nbsp;+ Hoàn thiện báo cáo<br>&nbsp;&nbsp;+ Chuẩn bị slide thuyết trình<br>&nbsp;&nbsp;+ Luyện demo thử 3 lần có bấm giờ | 04/07/2026 | 04/07/2026 | Cá nhân |

### Kết quả đạt được tuần 12:

* **Backend API hoàn chỉnh:**
    * Toàn bộ 15 API Endpoint đã được xây dựng và kiểm thử: tìm kiếm khách sạn, xem chi tiết, đăng ký/đăng nhập, đặt phòng, hủy phòng, xem lịch sử, các API admin quản trị.
    * **Redis Caching** hoạt động hiệu quả: Cache Hit trả về trong < 5ms, Cache Miss query RDS và lưu kết quả vào Redis với TTL 5 phút — giảm tải đáng kể cho database.

* **Hạ tầng Production hoàn chỉnh (Phase 4 & 5):**
    * **ALB + ASG** hoạt động ổn định: Load Balancer phân phối đều traffic, Auto Scaling Group tự động thêm EC2 khi CPU > 70%.
    * **CloudFront + S3 + WAF:** Website tĩnh phục vụ từ CDN edge với độ trễ thấp, WAF bảo vệ chống các cuộc tấn công phổ biến.
    * **CloudWatch + SNS:** Hệ thống giám sát liên tục, gửi cảnh báo email ngay khi phát hiện bất thường.

* **Kết quả kiểm thử chứng minh 3 tính chất quan trọng:**
    * ✅ **High Availability:** Tắt 1 EC2 → ALB tự chuyển sang EC2 còn lại → Website hoạt động bình thường không gián đoạn.
    * ✅ **Auto Scaling:** Giả lập 300 users bằng Locust → CPU vượt 70% → ASG tự scale từ 1 lên 2-3 EC2 trong vòng 2-3 phút.
    * ✅ **Caching:** Response time không có cache: ~150ms | Có cache (Redis): ~3ms → **Nhanh hơn ~50 lần**.

* **Chuẩn bị báo cáo & Demo:**
    * Slide thuyết trình hoàn chỉnh: giới thiệu bài toán, giải pháp AWS, kết quả kiểm thử với số liệu thực tế.
    * Kịch bản demo được luyện tập 3 lần, thời gian demo nằm trong giới hạn cho phép.

{{% notice success %}}
**Tóm tắt:** Tuần 12 đánh dấu sự hoàn thiện của đồ án **Hệ thống Đặt phòng Khách sạn Du lịch chịu tải cao trên AWS**. Dự án đã chứng minh thành công 3 tính chất cốt lõi của điện toán đám mây (High Availability, Auto Scaling, Caching) thông qua các bài kiểm thử thực tế với số liệu đo đạc cụ thể, rõ ràng.
{{% /notice %}}

### Hình ảnh thực hành tuần 12:

![Thực hành tuần 12 - 3](/images/worklog/3.jpg)

![Thực hành tuần 12 - 4](/images/worklog/4.jpg)

![Thực hành tuần 12 - 591](/images/591.jpg)

![Thực hành tuần 12 - 592](/images/592.jpg)
