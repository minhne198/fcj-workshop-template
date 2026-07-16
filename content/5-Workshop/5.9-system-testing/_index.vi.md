---
title : "Kiểm thử hệ thống sau triển khai"
date : 2024-01-01
weight : 9
chapter : false
pre : " <b> 5.9. </b> "
---

## Mục tiêu

Bước này kiểm tra AWS_OmniStay sau khi đã triển khai backend, frontend, CloudFront, WAF và giám sát. Mục tiêu là chứng minh website truy cập được từ public internet, API hoạt động qua CloudFront, backend kết nối được RDS và Redis, đồng thời các thành phần vận hành như ALB, Target Group và CloudWatch có dữ liệu đúng.

## 1. Kiểm tra health qua CloudFront

Mở trình duyệt hoặc dùng công cụ gọi HTTP:

```text
https://<cloudfront-domain>/health
https://<cloudfront-domain>/health/aws
```

Kết quả mong đợi từ `/health/aws`:

```text
environment = Production
databaseProvider = MySql
redisConfigured = true
redisConnected = true
apiBasePath = /api
```

Nếu bị `403`, kiểm tra behavior `/health*` đã trỏ về ALB chưa. Nếu bị `502` hoặc `504`, kiểm tra Target Group, ALB origin DNS và Security Group của ALB.


![VPC details](/images/591.jpg)
<p align="center"><em>Hình 5.9.1: Trình duyệt hiển thị `/health/aws` qua CloudFront thành công.</em></p>

## 2. Kiểm tra API search qua CloudFront

Gọi API tìm kiếm khách sạn:

```text
https://<cloudfront-domain>/api/hotels/search?city=Da%20Nang&checkIn=2026-12-10&checkOut=2026-12-12&guests=2
```

Kết quả mong đợi:

- API trả HTTP 200.
- Response là JSON array.
- Có dữ liệu khách sạn nếu seed data đã được nạp.
- Không gặp lỗi `403`, `502`, `503` hoặc `504`.

Nếu API lỗi, kiểm tra CloudFront behavior `/api/*`, allowed methods, query strings forwarding và cache policy `CachingDisabled`.


## 3. Kiểm tra giao diện website public

Mở trang frontend:

```text
https://<cloudfront-domain>/public/index.html
```

Luồng kiểm thử đề xuất:

1. Mở trang login hoặc trang chủ.
2. Đăng nhập admin bằng tài khoản demo, không ghi password vào báo cáo.
3. Vào trang Admin để kiểm tra users, hotels và bookings load được.
4. Đăng xuất.
5. Đăng ký tài khoản customer mới.
6. Tìm kiếm khách sạn ở `Da Nang`.
7. Chọn một khách sạn trong kết quả tìm kiếm.
8. Đặt phòng.
9. Thực hiện bước thanh toán/mock payment theo chức năng hiện có.
10. Vào trang lịch sử đặt phòng để kiểm tra booking đã được ghi nhận.


![VPC details](/images/592.jpg)
<p align="center"><em>Hình 5.9.2: Trang login hoặc trang chủ public.</em></p>


## 4. Kiểm tra Redis cache evidence

Gọi cùng một URL search 2 lần:

```text
https://<cloudfront-domain>/api/hotels/search?city=Da%20Nang&checkIn=2026-12-10&checkOut=2026-12-12&guests=2
```

Sau đó kiểm tra log backend trên EC2:

```bash
sudo journalctl -u omnistay-api -n 300 --no-pager
```

Kết quả mong đợi:

```text
Hotel search cache MISS
Hotel search cache HIT
```

Lần đầu tiên thường là cache MISS vì dữ liệu chưa có trong Redis. Lần thứ hai là cache HIT nếu Redis hoạt động đúng và TTL chưa hết hạn.

## 5. Kiểm tra RDS evidence

Vào **RDS** -> **Databases** -> `omnistay-mysql`.

Cần kiểm tra:

- Database status là `Available`.
- Endpoint và port đúng với cấu hình backend.
- Security Group là `SG-RDS`.
- Metrics có dữ liệu CPU và database connections.

Nếu có công cụ query database, kiểm tra các bảng nghiệp vụ chính:

```text
Users
Hotels
RoomTypes
Bookings
```

## 6. Kiểm tra ALB và Target Group evidence

Vào **EC2** -> **Target Groups** -> `omnistay-api-tg`.

Cần thấy:

```text
Target health: Healthy
Health check path: /health
Port: 8080
```

Vào **EC2** -> **Load Balancers** -> `omnistay-alb`.

Cần thấy:

- ALB state `Active`.
- Scheme `Internet-facing`.
- Listener HTTP 80 forward về `omnistay-api-tg`.
- DNS name của ALB.

## 7. Kiểm tra CloudWatch Dashboard

Vào **CloudWatch** -> **Dashboards** -> `OmniStay-Demo`.

Sau khi tạo traffic bằng cách truy cập frontend và gọi API, dashboard nên có dữ liệu cho:

- ALB request count.
- ALB 5XX count.
- EC2 CPU utilization.
- ASG desired/in-service instances.
- RDS connections.
- Redis connections.


## 8. Checklist nghiệm thu sau triển khai

| Hạng mục | Kết quả mong đợi |
| --- | --- |
| CloudFront frontend | Truy cập được website public |
| CloudFront `/api/*` | Forward đúng về ALB |
| CloudFront `/health*` | Trả health check từ backend |
| ALB | Active, listener HTTP 80 hoạt động |
| Target Group | EC2 target healthy |
| Backend service | `omnistay-api` active trên EC2 |
| RDS | Backend kết nối MySQL thành công |
| Redis | Search có cache HIT/MISS |
| WAF | Gắn với CloudFront và không block luồng hợp lệ |
| CloudWatch | Dashboard và alarms đã tạo |

## Kết quả cần đạt

Sau bước kiểm thử, hệ thống AWS_OmniStay có bằng chứng đầy đủ về luồng frontend, API, backend, database, cache, load balancing và monitoring. Các ảnh chụp trong phần này là phần quan trọng để chứng minh quá trình triển khai website và hệ thống đã hoàn thành theo từng bước.
