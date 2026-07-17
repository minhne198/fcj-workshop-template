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
| 2 | - Hoàn thiện Backend API: `HotelsController.cs` (tìm kiếm + chi tiết), `BookingsController.cs` (đặt phòng/hủy/lịch sử), `AdminController.cs` (quản trị).<br>- Tích hợp **Redis Cache** vào SearchService: Cache HIT < 5ms, Cache MISS query RDS rồi lưu vào Redis (TTL=5 phút). | 29/06/2026 | 29/06/2026 | Visual Studio 2022 |
| 3 | - **Phase 4 - Cấu hình Compute:** Tạo EC2 Launch Template với User Data script tự động cài .NET 8 và chạy API service.<br>- Tạo **Application Load Balancer (ALB)** ở Public Subnet, cấu hình Target Group với Health Check `/health`. | 30/06/2026 | 30/06/2026 | AWS Console |
| 4 | - Tạo **Auto Scaling Group (ASG)**: Min=1, Max=4, Target CPU=70%.<br>- Thiết lập **CloudWatch Alarm** khi CPU > 70% → kích hoạt ASG Scale Out; cấu hình **SNS** gửi cảnh báo email cho Admin. | 01/07/2026 | 01/07/2026 | AWS Console |
| 5 | - **Phase 5 - Frontend & CDN:** Upload toàn bộ file tĩnh (HTML, CSS, JS) lên **Amazon S3**, bật Static Website Hosting.<br>- Tạo **CloudFront Distribution**: Origin S3 (dùng OAC), forward `/api/*` đến ALB. Gắn **AWS WAF** vào CloudFront để chặn SQL Injection, XSS. | 02/07/2026 | 02/07/2026 | AWS Console |
| 6 | - **Kiểm thử High Availability:** Chủ động terminate 1 EC2 trong ASG → kiểm tra ALB tự động chuyển traffic sang EC2 còn lại → website vẫn hoạt động bình thường.<br>- **Load Test với Locust:** Giả lập 300 người dùng truy cập đồng thời → quan sát ASG tự động scale lên 2-3 EC2. | 03/07/2026 | 03/07/2026 | Locust |
| 7 | - Đo lường và so sánh hiệu năng: Response time **không có Cache** (~100-200ms) vs **có Cache** (<5ms).<br>- Hoàn thiện báo cáo, chuẩn bị slide thuyết trình và kịch bản demo. Thực hành demo thử 3 lần có bấm giờ. | 04/07/2026 | 04/07/2026 | Cá nhân |

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
