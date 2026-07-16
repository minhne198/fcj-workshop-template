---
title : "Cấu hình WAF, giám sát và cảnh báo"
date : 2024-01-01
weight : 8
chapter : false
pre : " <b> 5.8. </b> "
---

## Mục tiêu

Bước này bổ sung lớp bảo vệ và vận hành cho AWS_OmniStay. CloudFront được gắn AWS WAF để lọc request nguy hiểm. CloudWatch, SNS và CloudWatch Alarms được dùng để theo dõi hệ thống, phát hiện lỗi và cảnh báo khi tài nguyên có dấu hiệu quá tải.

## 1. Tạo AWS WAF Web ACL cho CloudFront

Vào **WAF & Shield** -> **Web ACLs** -> **Create web ACL**.

Cấu hình:

| Trường | Giá trị |
| --- | --- |
| Resource type | CloudFront distributions |
| Scope | Global |
| Name | `omnistay-cloudfront-waf` |
| Associated resource | CloudFront distribution của AWS_OmniStay |
| Default action | Allow |

Managed rule groups nên thêm:

| Rule group | Mục đích |
| --- | --- |
| `AWSManagedRulesCommonRuleSet` | Chặn các request phổ biến có dấu hiệu bất thường |
| `AWSManagedRulesKnownBadInputsRuleSet` | Chặn input độc hại đã biết |
| `AWSManagedRulesSQLiRuleSet` | Giảm rủi ro SQL Injection |
| `AmazonIpReputationList` | Chặn IP có reputation xấu |


![VPC details](/images/581.jpg)
<p align="center"><em>Hình 5.8.1: Web ACL overview của `omnistay-cloudfront-waf`.</em></p>

## 2. Lưu ý rule cho upload ảnh

Trong tài liệu triển khai AWS_OmniStay, có trường hợp request upload ảnh bị CloudFront/WAF chặn trước khi tới backend. Nếu frontend có chức năng upload ảnh multipart/form-data, cần kiểm tra sampled requests của WAF và thêm allow rule có phạm vi hẹp cho endpoint upload hợp lệ.

Nguyên tắc khi thêm rule:

- Chỉ allow đúng path upload cần thiết, ví dụ `/api/uploads/images`.
- Đặt rule allow phía trên các managed rules có thể block request.
- Không disable toàn bộ WAF chỉ để xử lý một endpoint.
- Kiểm tra lại backend vẫn yêu cầu xác thực người dùng nếu endpoint cần quyền admin/owner.

![VPC details](/images/582.jpg)
<p align="center"><em>Hình 5.8.2: TRule allow upload ảnh nếu hệ thống có triển khai chức năng upload.</em></p>

## 3. Tạo SNS Topic nhận cảnh báo

Vào **SNS** -> **Topics** -> **Create topic**.

Cấu hình:

| Trường | Giá trị |
| --- | --- |
| Type | Standard |
| Name | `omnistay-alerts` |
| Subscription protocol | Email |
| Endpoint | Email nhận cảnh báo |

Sau khi tạo subscription, mở email và xác nhận để trạng thái chuyển sang `Confirmed`.

![VPC details](/images/583.jpg)
<p align="center"><em>Hình 5.8.3: NS topic `omnistay-alerts`.</em></p>

## 4. Tạo CloudWatch Dashboard

Vào **CloudWatch** -> **Dashboards** -> **Create dashboard**.

Cấu hình:

| Trường | Giá trị |
| --- | --- |
| Dashboard name | `OmniStay-Demo` |

Các widget nên thêm:

| Nhóm | Metric |
| --- | --- |
| ALB | `RequestCount` |
| ALB | `HTTPCode_Target_5XX_Count` |
| ASG | `GroupDesiredCapacity` |
| ASG | `GroupInServiceInstances` |
| EC2 | `CPUUtilization` |
| RDS | `CPUUtilization` |
| RDS | `DatabaseConnections` |
| ElastiCache | `CPUUtilization` |
| ElastiCache | `CurrConnections` |

Dashboard giúp theo dõi nhanh các thành phần chính khi demo hoặc kiểm thử tải.

![VPC details](/images/584.jpg)
<p align="center"><em>Hình 5.8.4: CloudWatch dashboard `OmniStay-Demo`</em></p>

## 5. Tạo CloudWatch Alarms

Tạo alarm CPU cao cho Auto Scaling Group:

| Trường | Giá trị |
| --- | --- |
| Metric | ASG CPUUtilization |
| Resource | `omnistay-api-asg` |
| Condition | Greater than 70 |
| Notification | `omnistay-alerts` |
| Alarm name | `omnistay-asg-cpu-high` |

Tạo alarm lỗi 5XX từ ALB:

| Trường | Giá trị |
| --- | --- |
| Metric | `HTTPCode_Target_5XX_Count` |
| Resource | `omnistay-alb` |
| Condition | Greater than 10 |
| Notification | `omnistay-alerts` |
| Alarm name | `omnistay-alb-5xx-high` |

Tạo alarm CPU cao cho RDS:

| Trường | Giá trị |
| --- | --- |
| Metric | RDS `CPUUtilization` |
| Resource | `omnistay-mysql` |
| Condition | Greater than 80 |
| Notification | `omnistay-alerts` |
| Alarm name | `omnistay-rds-cpu-high` |

![VPC details](/images/585.jpg)
<p align="center"><em>Hình 5.8.5: Danh sách CloudWatch Alarms đã tạo.</em></p>

## 6. Kiểm soát chi phí trong quá trình chạy demo

Các tài nguyên cần chú ý vì có thể phát sinh phí theo giờ:

- NAT Gateway.
- Application Load Balancer.
- RDS MySQL.
- ElastiCache Redis/Valkey.
- AWS WAF.
- Public IPv4 address.
- CloudWatch logs/metrics nếu log nhiều.

Trong quá trình làm workshop, cần theo dõi Billing dashboard và budget alert. Nếu chưa demo tiếp, có thể giảm ASG desired capacity hoặc tạm dừng/xóa những tài nguyên tốn phí theo hướng dẫn cleanup riêng sau này.


## Kết quả cần đạt

Sau bước này, CloudFront được bảo vệ bằng WAF, hệ thống có SNS topic nhận cảnh báo, CloudWatch dashboard để quan sát hoạt động và các alarm cơ bản cho CPU, lỗi backend và RDS.
