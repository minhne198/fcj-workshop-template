---
title: "Deploy Frontend to S3 and CloudFront"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---

## Objective

This step deploys the static frontend of AWS_OmniStay to Amazon S3 and distributes it to the internet through Amazon CloudFront. The S3 bucket keeps Block Public Access enabled; users do not access S3 directly, but access it through CloudFront Origin Access Control (OAC). CloudFront is also configured with an ALB origin to forward API requests to the backend.

Access flow after completion:

```text
User Browser -> CloudFront
  -> Static files: S3 frontend private bucket
  -> API requests /api/*: Application Load Balancer -> EC2 backend
  -> Health requests /health*: Application Load Balancer -> EC2 backend
```

## 1. Prepare production frontend locally

Create a frontend build/configuration for production. The `config.js` file should configure the API as a relative path `/api` so the browser calls the same CloudFront domain.

Example `frontend/public/config.js`:

```js
window.__APP_CONFIG__ = {
  API_BASE: "/api",
};
```

If the sample file `frontend/public/config.aws.example.js` already exists, copy it to `config.js` before uploading.

```powershell
Copy-Item frontend\public\config.aws.example.js frontend\public\config.js -Force
```

Main files/folders to upload:

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

![VPC details](/images/571.jpg)

<p align="center"><em>Figure 5.7.1: Frontend folder structure before upload.</em></p>

## 2. Upload frontend to S3 bucket

Go to **S3** -> frontend bucket `omnistay-frontend-<account-id>`.

Steps:

1. Select **Upload**.
2. Select **Add folder** or drag and drop frontend folders/files.
3. Upload the contents inside the frontend directory, not the wrapper directory itself.
4. Ensure S3 contains these paths:

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

Do not upload in an incorrect nested form such as:

```text
omnistay-frontend/public/index.html
```

![VPC details](/images/572.jpg)

<p align="center"><em>Figure 5.7.2: Frontend bucket object list includes `public/`, `src/`, and `assets/`.</em></p>

## 3. Create CloudFront Distribution with S3 Origin

Go to **CloudFront** -> **Distributions** -> **Create distribution**.

S3 origin configuration:

| Field | Value |
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

After the distribution is created, CloudFront suggests a bucket policy for S3. Copy that policy and attach it to the frontend bucket.

## 4. Attach bucket policy to S3 frontend bucket

Go to **S3** -> frontend bucket -> **Permissions** -> **Bucket policy**.

Paste the bucket policy suggested by CloudFront. The goal is to allow only the CloudFront distribution to read objects in the bucket without making the bucket public.

## 5. Add ALB Origin for backend API

In the CloudFront distribution, go to **Origins** -> **Create origin**.

Configuration:

| Field | Value |
| --- | --- |
| Origin domain | DNS name of `omnistay-alb` |
| Origin name | `omnistay-api-alb` |
| Protocol | HTTP only |
| HTTP port | 80 |

The ALB still receives HTTP internally from CloudFront, while users access CloudFront through HTTPS.

![VPC details](/images/573.jpg)

<p align="center"><em>Figure 5.7.3: CloudFront origins include both the S3 frontend origin and ALB backend origin.</em></p>

## 6. Configure behaviors for API and health check

Add behavior `/api/*`:

| Field | Value |
| --- | --- |
| Path pattern | `/api/*` |
| Origin | `omnistay-api-alb` |
| Viewer protocol policy | Redirect HTTP to HTTPS |
| Allowed methods | GET, HEAD, OPTIONS, PUT, POST, PATCH, DELETE |
| Cache policy | CachingDisabled |
| Query strings | Forward |

Add behavior `/health*`:

| Field | Value |
| --- | --- |
| Path pattern | `/health*` |
| Origin | `omnistay-api-alb` |
| Viewer protocol policy | Redirect HTTP to HTTPS |
| Allowed methods | GET, HEAD, OPTIONS |
| Cache policy | CachingDisabled |

The default behavior `*` still points to the S3 frontend origin.

## 7. Update CloudFront domain in Parameter Store

After CloudFront deployment is complete, record the domain in this format:

```text
dxxxxxxxxxxxxx.cloudfront.net
```

Go to **Systems Manager** -> **Parameter Store** and create or update:

```text
/omnistay/prod/AWS__CloudFrontDomain = dxxxxxxxxxxxxx.cloudfront.net
```

If the backend needs the actual CloudFront domain at runtime, create a new Launch Template version to update the environment variable and then configure the ASG to use the new version.

## 8. Invalidate CloudFront cache

After uploading or updating the frontend, go to **CloudFront** -> Distribution -> **Invalidations** -> **Create invalidation**.

Object paths:

```text
/*
```

Wait until status becomes `Completed`.

![VPC details](/images/574.jpg)

<p align="center"><em>Figure 5.7.4: CloudFront invalidation status is `Completed`.</em></p>

## Expected Result

After this step, users can access the website through CloudFront. Static files are served from the private S3 bucket through OAC, while `/api/*` and `/health*` requests are forwarded by CloudFront to the ALB backend.
