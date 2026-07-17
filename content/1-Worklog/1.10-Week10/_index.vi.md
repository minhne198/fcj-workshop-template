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
| 2 | - Tìm hiểu tổng quan về **Data Lake (Lab 000035)**: Kiến trúc lưu trữ tập trung và vai trò của S3 trong hệ thống dữ liệu lớn.<br>- Thực hành tạo **AWS Glue Database** và cấu hình Crawler để tự động lập danh mục dữ liệu. | 15/06/2026 | 15/06/2026 | Lab 000035 |
| 3 | - Thực hành toàn bộ quy trình **ETL với AWS Glue**: Tạo Glue Job, làm sạch dữ liệu và lưu đầu ra vào S3.<br>- Khám phá Glue Studio để thiết kế ETL pipeline trực quan, không cần code. | 16/06/2026 | 16/06/2026 | Lab 000035 & 000060 |
| 4 | - Truy vấn dữ liệu trực tiếp trên S3 bằng **Amazon Athena** với SQL chuẩn, không cần cơ sở dữ liệu riêng.<br>- Trực quan hóa kết quả phân tích bằng **Amazon QuickSight**: Tạo Dataset, biểu đồ và Dashboard báo cáo. | 17/06/2026 | 17/06/2026 | Lab 000035 |
| 5 | - Thực hành **IAM Role & Conditions (Lab 000043)**: Cấu hình điều kiện truy cập theo IP Address và thời gian đăng nhập.<br>- Kiểm thử **Switch Role** và đánh giá hiệu quả mô hình kiểm soát truy cập động trong doanh nghiệp. | 18/06/2026 | 18/06/2026 | Lab 000043 |
| 6 | - Khám phá tích hợp **Generative AI (Lab 000039)**: Cấu hình **DynamoDB Zero-ETL Integration** để đồng bộ dữ liệu sang OpenSearch.<br>- Tìm hiểu Vector Embedding và Semantic Search bằng **Amazon Bedrock** và tiềm năng ứng dụng AI trong doanh nghiệp. | 19/06/2026 | 19/06/2026 | Lab 000039 |
| 7 | - Thực hành **AWS Glue DataBrew (Lab 000072)**: Làm sạch dữ liệu, xử lý Missing Values và xây dựng Recipe tự động hóa.<br>- Tìm hiểu kiến trúc **Amazon Redshift** (Data Warehouse): Tạo Cluster, nạp dữ liệu và chạy truy vấn phân tích SQL. | 20/06/2026 | 20/06/2026 | Lab 000072 & 000073 |

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
