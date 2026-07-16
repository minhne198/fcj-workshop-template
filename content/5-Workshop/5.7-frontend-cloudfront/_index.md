---
title : "Triển khai Frontend lên S3 và CloudFront"
date : 2024-01-01
weight : 7
chapter : false
pre : " <b> 5.7. </b> "
---

## Mục tiêu

Bước này triển khai giao diện tĩnh của AWS_OmniStay lên Amazon S3 và phân phối ra internet thông qua Amazon CloudFront. S3 bucket vẫn bật Block Public Access; người dùng không truy cập trực tiếp vào S3 mà truy cập qua CloudFront Origin Access Control (OAC). CloudFront cũng được cấu hình thêm origin ALB để forward các request API về backend.

Luồng truy cập sau khi hoàn thành:

```text
User Browser -> CloudFront
  -> Static files: S3 frontend private bucket
  -> API requests /api/*: Application Load Balancer -> EC2 backend
  -> Health requests /health*: Application Load Balancer -> EC2 backend
```

## 1. Chuẩn bị frontend production trên máy local

Tạo bản frontend dùng cho production. File `config.js` cần cấu hình API theo đường dẫn tương đối `/api` để browser gọi cùng domain CloudFront.

Ví dụ nội dung `frontend/public/config.js`:

```js
window.__APP_CONFIG__ = {
  API_BASE: '/api'
};
```

Nếu đã có file mẫu `frontend/public/config.aws.example.js`, có thể copy thành `config.js` trước khi upload.

```powershell
Copy-Item frontend\public\config.aws.example.js frontend\public\config.js -Force
```

Các file/thư mục chính cần có khi upload:

```text
public/index.html
public/home.html
public/admin.html
public/config.js
src/api.js
src/session.js
src/admin.js
assets/
```

> **Ảnh cần dán:** Nội dung `config.js` thể hiện `API_BASE: '/api'`.
>
> **Ảnh cần dán:** Cấu trúc thư mục frontend trước khi upload.

## 2. Upload frontend lên S3 bucket

Vào **S3** -> frontend bucket `omnistay-frontend-<account-id>`.

Thực hiện:

1. Chọn **Upload**.
2. Chọn **Add folder** hoặc kéo thả các folder/file frontend.
3. Upload nội dung bên trong thư mục frontend, không upload cả thư mục bọc ngoài.
4. Đảm bảo trên S3 có các path:

```text
public/index.html
public/home.html
public/admin.html
public/config.js
src/api.js
src/session.js
src/admin.js
assets/
```

Không upload thành dạng sai như:

```text
omnistay-frontend/public/index.html
```

> **Ảnh cần dán:** Object list trong frontend bucket có `public/`, `src/`, `assets/`.
>
> **Ảnh cần dán:** Tab Permissions của bucket vẫn bật Block Public Access.

## 3. Tạo CloudFront Distribution với S3 Origin

Vào **CloudFront** -> **Distributions** -> **Create distribution**.

Cấu hình S3 origin:

| Trường | Giá trị |
| --- | --- |
| Origin domain | S3 frontend bucket |
| Origin name | `omnistay-frontend-s3` |
| Origin access | Origin Access Control settings |
| OAC name | `omnistay-frontend-oac` |
| Signing behavior | Sign requests |
| Viewer protocol policy | Redirect HTTP to HTTPS |
| Allowed methods | GET, HEAD |
| Cache policy | CachingOptimized |
| Default root object | `public/index.html` |

Sau khi tạo distribution, CloudFront sẽ gợi ý bucket policy cho S3. Copy policy này và gắn vào frontend bucket.

> **Ảnh cần dán:** CloudFront distribution domain name.
>
> **Ảnh cần dán:** Origin S3 `omnistay-frontend-s3` sử dụng OAC.
>
> **Ảnh cần dán:** Default root object là `public/index.html`.

## 4. Gắn bucket policy cho S3 frontend bucket

Vào **S3** -> frontend bucket -> **Permissions** -> **Bucket policy**.

Dán bucket policy do CloudFront gợi ý. Mục tiêu là chỉ cho CloudFront distribution được đọc object trong bucket, không mở bucket public.

> **Ảnh cần dán:** Bucket policy cho phép CloudFront OAC truy cập frontend bucket.

## 5. Thêm ALB Origin cho backend API

Trong CloudFront distribution, vào **Origins** -> **Create origin**.

Cấu hình:

| Trường | Giá trị |
| --- | --- |
| Origin domain | DNS name của `omnistay-alb` |
| Origin name | `omnistay-api-alb` |
| Protocol | HTTP only |
| HTTP port | 80 |

ALB vẫn nhận HTTP nội bộ từ CloudFront, còn người dùng truy cập CloudFront bằng HTTPS.

> **Ảnh cần dán:** CloudFront origins có cả S3 frontend origin và ALB backend origin.

## 6. Cấu hình behavior cho API và health check

Thêm behavior `/api/*`:

| Trường | Giá trị |
| --- | --- |
| Path pattern | `/api/*` |
| Origin | `omnistay-api-alb` |
| Viewer protocol policy | Redirect HTTP to HTTPS |
| Allowed methods | GET, HEAD, OPTIONS, PUT, POST, PATCH, DELETE |
| Cache policy | CachingDisabled |
| Query strings | Forward |

Thêm behavior `/health*`:

| Trường | Giá trị |
| --- | --- |
| Path pattern | `/health*` |
| Origin | `omnistay-api-alb` |
| Viewer protocol policy | Redirect HTTP to HTTPS |
| Allowed methods | GET, HEAD, OPTIONS |
| Cache policy | CachingDisabled |

Behavior mặc định `*` vẫn trỏ về S3 frontend origin.

> **Ảnh cần dán:** CloudFront behavior list có `Default (*) -> S3`, `/api/* -> ALB`, `/health* -> ALB`.

## 7. Cập nhật CloudFront domain vào Parameter Store

Sau khi CloudFront deploy xong, ghi lại domain dạng:

```text
dxxxxxxxxxxxxx.cloudfront.net
```

Vào **Systems Manager** -> **Parameter Store** và tạo hoặc cập nhật:

```text
/omnistay/prod/AWS__CloudFrontDomain = dxxxxxxxxxxxxx.cloudfront.net
```

Nếu backend cần dùng CloudFront domain thật trong runtime, tạo Launch Template version mới để cập nhật biến môi trường rồi cho ASG dùng version mới.

> **Ảnh cần dán:** Parameter `/omnistay/prod/AWS__CloudFrontDomain` đã được cập nhật, không chứa thông tin nhạy cảm.

## 8. Invalidate CloudFront cache

Sau khi upload hoặc cập nhật frontend, vào **CloudFront** -> Distribution -> **Invalidations** -> **Create invalidation**.

Object paths:

```text
/*
```

Đợi status chuyển sang `Completed`.

> **Ảnh cần dán:** CloudFront invalidation có status `Completed`.

## Kết quả cần đạt

Sau bước này, người dùng có thể truy cập website thông qua CloudFront. Static files được lấy từ S3 private bucket qua OAC, còn các request `/api/*` và `/health*` được CloudFront forward về ALB backend.
