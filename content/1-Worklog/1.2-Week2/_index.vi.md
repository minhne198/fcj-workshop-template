---
title: "Worklog Tuần 2"
date: 2026-04-22
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Mục tiêu tuần 2:
* Hoàn tất quy trình đăng ký và xác thực danh tính cho tài khoản AWS Free Tier một cách an toàn.
* Cấu hình lớp bảo vệ nhiều yếu tố (**MFA**) để gia cố tài khoản Root khỏi các mối đe dọa bên ngoài.
* Thực hành quản trị hệ thống chuyên nghiệp thông qua **IAM** bao gồm phân nhóm người dùng và phân quyền hợp lý.
* Làm quen với khái niệm **Amazon VPC** và cơ chế xây dựng môi trường mạng ảo riêng biệt, độc lập trên AWS.
* Hiểu cơ bản về CIDR notation và cách phân chia địa chỉ IP thành các Subnet hợp lý.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2 | - Chuẩn bị thông tin cá nhân, giấy tờ và thẻ thanh toán quốc tế cần thiết.<br>- Thực hiện toàn bộ quy trình đăng ký tài khoản AWS Free Tier theo hướng dẫn chính thống. | 20/04/2026 | 20/04/2026 | AWS Documentation |
| 3 | - Kích hoạt xác thực đa yếu tố (**MFA**) cho cả tài khoản Root lẫn IAM User.<br>- Phân tích các nguy cơ bảo mật phổ biến khi thông tin đăng nhập bị lộ hoặc tài khoản bị xâm phạm. | 21/04/2026 | 21/04/2026 | AWS Security Blog |
| 4 | - Khởi tạo **Admin Group** và người dùng **IAM User** với quyền hạn tối thiểu cần thiết.<br>- Áp dụng nguyên tắc Least Privilege trong phân quyền, tránh cấp quyền quá mức. | 22/04/2026 | 22/04/2026 | AWS Study Group |
| 5 | - Khởi tạo và cấu hình **Access Keys** để phục vụ truy cập dịch vụ AWS qua AWS CLI.<br>- Thực hành tạo và quản lý các chính sách bảo mật (IAM Policies) theo mô hình doanh nghiệp. | 23/04/2026 | 23/04/2026 | AWS Workshop |
| 6 | - Kiểm tra và rà soát lại toàn bộ cấu hình bảo mật IAM đã thiết lập trong tuần.<br>- Bước đầu tìm hiểu tổng quan về **Amazon VPC**: Khái niệm, kiến trúc và lý do cần mạng ảo riêng. | 24/04/2026 | 24/04/2026 | AWS Networking Guide |
| 7 | - Nghiên cứu chuyên sâu về các gói hỗ trợ của AWS (Support Plans) và thực hành phân chia địa chỉ IP theo dải **CIDR**. | 25/04/2026 | 25/04/2026 | Cá nhân |

### Kết quả đạt được tuần 2:

* **Về Bảo mật tài khoản:**
    * Thiết lập thành công lớp bảo vệ **MFA** cho tài khoản, ngăn chặn hiệu quả các cuộc tấn công brute-force và phishing.
    * Nắm vững tầm quan trọng của việc không bao giờ sử dụng tài khoản Root cho các tác vụ vận hành hàng ngày.
* **Về Quản trị hệ thống IAM:**
    * Thành thạo việc tạo **Admin Group** và **IAM User**, thiết lập cơ cấu quản trị nhân sự đám mây khoa học.
    * Nắm vững cách cấu hình và sử dụng **Access Keys** để vận hành tài nguyên AWS thông qua CLI.
    * Hiểu cách xây dựng các IAM Policy kiểm soát chính xác quyền truy cập của từng đối tượng.
* **Về Kiến thức VPC & Hỗ trợ AWS:**
    * Làm quen với kiến trúc VPC và hiểu tại sao việc cô lập mạng là yếu tố bảo mật thiết yếu trong môi trường Cloud.
    * Nắm được sự khác biệt giữa 4 cấp độ hỗ trợ của AWS (Basic, Developer, Business, Enterprise).

#### Tìm hiểu về các gói hỗ trợ AWS (Support Plans)

| Gói dịch vụ | Đặc điểm nổi bật | Đối tượng phù hợp |
| :--- | :--- | :--- |
| **Basic** | Miễn phí, hỗ trợ tài khoản, thanh toán và tài liệu kỹ thuật. | Người dùng cá nhân, học sinh/sinh viên bắt đầu. |
| **Developer** | Thêm hướng dẫn kiến trúc và thời gian phản hồi nhanh hơn. | Môi trường phát triển và thử nghiệm. |
| **Business** | Kiểm tra hạ tầng tự động với Trusted Advisor, tối ưu chi phí và bảo mật. | Hệ thống đang vận hành thực tế (Production). |
| **Enterprise** | Có chuyên gia TAM hỗ trợ trực tiếp 24/7, đánh giá định kỳ. | Doanh nghiệp lớn, hệ thống mission-critical. |

{{% notice tip %}}
**Lời khuyên:** Với sinh viên hay người mới bắt đầu, gói **Basic** kết hợp tra cứu tài liệu AWS Documentation là lựa chọn tối ưu nhất để học tập mà không phát sinh chi phí.
{{% /notice %}}

{{% notice warning %}}
**Ghi chú quan trọng:** Luôn bảo quản Access Keys và thông tin MFA ở nơi an toàn. Tuyệt đối không đưa các thông tin này lên kho lưu trữ công khai như GitHub hay Gitlab.
{{% /notice %}}
