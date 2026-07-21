---
title: "Worklog Tuần 10"
date: 2026-06-15
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Mục tiêu tuần 10:
* Xây dựng hệ thống phân tích dữ liệu tập trung với **Data Lake**, **AWS Glue**, **Amazon Athena** và **Amazon QuickSight**.
* Làm chủ quy trình **ETL (Extract - Transform - Load)** để xử lý và chuẩn hóa dữ liệu quy mô lớn trên AWS.
* Triển khai phân quyền nâng cao với **IAM Role & IAM Conditions** kiểm soát truy cập theo IP/Thời gian.
* Khám phá ứng dụng **Generative AI trên AWS** thông qua tích hợp **DynamoDB Zero-ETL + OpenSearch + Amazon Bedrock**.
* Tìm hiểu **Data Preparation** với **AWS Glue DataBrew** và **Data Warehouse** với **Amazon Redshift**.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2 | - Tìm hiểu Data Lake và vai trò của S3 trong hệ thống dữ liệu lớn<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Tạo AWS Glue Database<br>&nbsp;&nbsp;+ Cấu hình Glue Crawler<br>&nbsp;&nbsp;+ Tự động lập danh mục dữ liệu | 15/06/2026 | 15/06/2026 | Lab 000035 |
| 3 | - Tìm hiểu quy trình ETL với AWS Glue<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Tạo Glue Job<br>&nbsp;&nbsp;+ Làm sạch dữ liệu<br>&nbsp;&nbsp;+ Lưu dữ liệu đầu ra vào S3<br>&nbsp;&nbsp;+ Thiết kế ETL pipeline bằng Glue Studio | 16/06/2026 | 16/06/2026 | Lab 000035 & 000060 |
| 4 | - Tìm hiểu Amazon Athena và Amazon QuickSight<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Truy vấn dữ liệu trên S3 bằng Athena<br>&nbsp;&nbsp;+ Tạo QuickSight Dataset<br>&nbsp;&nbsp;+ Tạo biểu đồ phân tích<br>&nbsp;&nbsp;+ Tạo Dashboard báo cáo | 17/06/2026 | 17/06/2026 | Lab 000035 |
| 5 | - Tìm hiểu IAM Role, IAM Conditions và Switch Role<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Cấu hình điều kiện truy cập theo IP Address<br>&nbsp;&nbsp;+ Cấu hình điều kiện theo thời gian đăng nhập<br>&nbsp;&nbsp;+ Kiểm thử Switch Role<br>&nbsp;&nbsp;+ Đánh giá mô hình kiểm soát truy cập động | 18/06/2026 | 18/06/2026 | Lab 000043 |
| 6 | - Tìm hiểu Generative AI integration, Vector Embedding và Semantic Search<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Cấu hình DynamoDB Zero-ETL Integration sang OpenSearch<br>&nbsp;&nbsp;+ Tìm hiểu Amazon Bedrock<br>&nbsp;&nbsp;+ Ghi chú tiềm năng ứng dụng AI trong doanh nghiệp | 19/06/2026 | 19/06/2026 | Lab 000039 |
| 7 | - Tìm hiểu AWS Glue DataBrew và Amazon Redshift<br>- **Thực hành:**<br>&nbsp;&nbsp;+ Làm sạch dữ liệu bằng DataBrew<br>&nbsp;&nbsp;+ Xử lý Missing Values<br>&nbsp;&nbsp;+ Xây dựng Recipe tự động hóa<br>&nbsp;&nbsp;+ Tạo Redshift Cluster<br>&nbsp;&nbsp;+ Nạp dữ liệu và chạy truy vấn phân tích SQL | 20/06/2026 | 20/06/2026 | Lab 000072 & 000073 |

### Kết quả đạt được tuần 10:

#### Phân tích dữ liệu & Data Lake:
* Hiểu sâu kiến trúc **Data Lake** và quy trình thu thập → lưu trữ → xử lý → phân tích dữ liệu trên AWS.
* Thực hành thành công toàn bộ pipeline **AWS Glue ETL**: Crawl cấu trúc dữ liệu → tạo Job → chạy xử lý → xuất đầu ra.
* Sử dụng **Amazon Athena** để phân tích dữ liệu serverless trực tiếp trên S3, tối ưu chi phí không cần quản lý cơ sở dữ liệu.
* Xây dựng Dashboard trực quan với **Amazon QuickSight** hỗ trợ báo cáo kinh doanh và ra quyết định dựa trên dữ liệu.

#### Quản lý quyền truy cập nâng cao:
* Thiết lập **IAM Conditions** kiểm soát truy cập theo context (IP, thời gian) — bảo mật Zero Trust cho môi trường doanh nghiệp.
* Nắm rõ cơ chế **Switch Role** giúp quản lý đa tài khoản linh hoạt mà không cần tạo nhiều tài khoản người dùng.

#### Generative AI & Data Intelligence:
* Hiểu kiến trúc tích hợp **DynamoDB → OpenSearch** qua Zero-ETL không cần pipeline ETL truyền thống.
* Nắm nguyên lý **Vector Embedding** và **Semantic Search**: Tìm kiếm theo nghĩa thay vì từ khóa chính xác nhờ Amazon Bedrock.

#### Data Preparation & Data Warehouse:
* Sử dụng **AWS Glue DataBrew** để làm sạch và chuẩn hóa dữ liệu bằng giao diện trực quan, không cần lập trình.
* Triển khai **Amazon Redshift** để lưu trữ và phân tích dữ liệu kinh doanh quy mô petabyte với hiệu năng cao.

{{% notice success %}}
**Tóm tắt:** Tuần 10 hoàn thiện bức tranh toàn cảnh về Data Analytics trên AWS — từ thu thập, xử lý, phân tích đến trực quan hóa và ứng dụng AI — đồng thời đặt nền tảng vững chắc cho việc xây dựng đồ án thực tế trong các tuần tiếp theo.
{{% /notice %}}
