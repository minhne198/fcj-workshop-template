---
title : "Post-deployment system testing"
date : 2024-01-01
weight : 9
chapter : false
pre : " <b> 5.9. </b> "
---

## Objective

This step verifies AWS_OmniStay after backend, frontend, CloudFront, WAF, and monitoring have been deployed. The goal is to prove that the website is accessible from the public internet, APIs work through CloudFront, the backend connects to RDS and Redis, and operational components such as ALB, Target Group, and CloudWatch have the expected data.

## 1. Check health through CloudFront

Open a browser or use an HTTP client:

```text
https://<cloudfront-domain>/health
https://<cloudfront-domain>/health/aws
```

Expected result from `/health/aws`:

```text
environment = Production
databaseProvider = MySql
redisConfigured = true
redisConnected = true
apiBasePath = /api
```

If the response is `403`, check whether behavior `/health*` points to ALB. If the response is `502` or `504`, check Target Group, ALB origin DNS, and the ALB Security Group.

![VPC details](/images/591.jpg)
<p align="center"><em>Figure 5.9.1: Browser shows `/health/aws` through CloudFront successfully.</em></p>

## 2. Check hotel search API through CloudFront

Call the hotel search API:

```text
https://<cloudfront-domain>/api/hotels/search?city=Da%20Nang&checkIn=2026-12-10&checkOut=2026-12-12&guests=2
```

Expected result:

- API returns HTTP 200.
- Response is a JSON array.
- Hotel data exists if seed data has been loaded.
- No `403`, `502`, `503`, or `504` errors occur.

If the API fails, check CloudFront behavior `/api/*`, allowed methods, query string forwarding, and `CachingDisabled` cache policy.

## 3. Check public website UI

Open the frontend page:

```text
https://<cloudfront-domain>/public/index.html
```

Suggested testing flow:

1. Open the login page or home page.
2. Log in as admin using a demo account, without writing the password in the report.
3. Open the Admin page and verify that users, hotels, and bookings load successfully.
4. Log out.
5. Register a new customer account.
6. Search hotels in `Da Nang`.
7. Select a hotel from the search result.
8. Book a room.
9. Complete the payment/mock payment flow according to the existing feature.
10. Open booking history and verify that the booking was recorded.

![VPC details](/images/592.jpg)
<p align="center"><em>Figure 5.9.2: Public login or home page.</em></p>

## 4. Check Redis cache evidence

Call the same search URL twice:

```text
https://<cloudfront-domain>/api/hotels/search?city=Da%20Nang&checkIn=2026-12-10&checkOut=2026-12-12&guests=2
```

Then check backend logs on EC2:

```bash
sudo journalctl -u omnistay-api -n 300 --no-pager
```

Expected result:

```text
Hotel search cache MISS
Hotel search cache HIT
```

The first request is usually a cache MISS because the data is not yet in Redis. The second request should be a cache HIT if Redis works correctly and the TTL has not expired.

## 5. Check RDS evidence

Go to **RDS** -> **Databases** -> `omnistay-mysql`.

Verify:

- Database status is `Available`.
- Endpoint and port match the backend configuration.
- Security Group is `SG-RDS`.
- Metrics show CPU and database connection data.

If a database query tool is available, check the main business tables:

```text
Users
Hotels
RoomTypes
Bookings
```

## 6. Check ALB and Target Group evidence

Go to **EC2** -> **Target Groups** -> `omnistay-api-tg`.

Expected:

```text
Target health: Healthy
Health check path: /health
Port: 8080
```

Go to **EC2** -> **Load Balancers** -> `omnistay-alb`.

Expected:

- ALB state is `Active`.
- Scheme is `Internet-facing`.
- HTTP 80 listener forwards to `omnistay-api-tg`.
- ALB DNS name is available.

## 7. Check CloudWatch Dashboard

Go to **CloudWatch** -> **Dashboards** -> `OmniStay-Demo`.

After generating traffic by opening the frontend and calling APIs, the dashboard should show data for:

- ALB request count.
- ALB 5XX count.
- EC2 CPU utilization.
- ASG desired/in-service instances.
- RDS connections.
- Redis connections.

## 8. Post-deployment acceptance checklist

| Item | Expected result |
| --- | --- |
| CloudFront frontend | Public website is accessible |
| CloudFront `/api/*` | Requests are forwarded correctly to ALB |
| CloudFront `/health*` | Health check is returned from backend |
| ALB | Active and HTTP 80 listener works |
| Target Group | EC2 target is healthy |
| Backend service | `omnistay-api` is active on EC2 |
| RDS | Backend connects to MySQL successfully |
| Redis | Search flow shows cache HIT/MISS |
| WAF | Attached to CloudFront and does not block valid flows |
| CloudWatch | Dashboard and alarms are created |

## Expected Result

After the testing step, AWS_OmniStay has complete evidence for the frontend, API, backend, database, cache, load balancing, and monitoring flows. The screenshots in this section are important proof that the website and system deployment have been completed step by step.
