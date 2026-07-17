---
title: "Week 12 Worklog"
date: 2026-06-29
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

### Week 12 Objectives:
* Complete the entire Backend API and Frontend for the hotel booking system.
* Deploy **Phase 4**: Configure Application Load Balancer (ALB), Auto Scaling Group (ASG), and CloudWatch Alarms.
* Deploy **Phase 5**: Publish the frontend to S3 + CloudFront and integrate WAF for system protection.
* Conduct comprehensive testing: HA Test (terminate EC2), Load Test (Locust 300 users), Cache Benchmark.
* Prepare documentation and a demo script for the project presentation.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| Mon | - Complete the Backend API: `HotelsController.cs` (search + details), `BookingsController.cs` (book/cancel/history), `AdminController.cs` (management).<br>- Integrate **Redis Cache** into SearchService: Cache HIT < 5ms, Cache MISS queries RDS then stores result in Redis (TTL=5 mins). | 29/06/2026 | 29/06/2026 | Visual Studio 2022 |
| Tue | - **Phase 4 - Compute Configuration:** Create an EC2 Launch Template with a User Data script to auto-install .NET 8 and start the API service.<br>- Create an **Application Load Balancer (ALB)** in the Public Subnet, configure a Target Group with a `/health` Health Check. | 30/06/2026 | 30/06/2026 | AWS Console |
| Wed | - Create the **Auto Scaling Group (ASG)**: Min=1, Max=4, Target CPU=70%.<br>- Configure a **CloudWatch Alarm** for CPU > 70% to trigger ASG Scale Out; set up **SNS** to send alert emails to the Admin. | 01/07/2026 | 01/07/2026 | AWS Console |
| Thu | - **Phase 5 - Frontend & CDN:** Upload all static files (HTML, CSS, JS) to **Amazon S3**, enable Static Website Hosting.<br>- Create a **CloudFront Distribution**: Origin S3 (using OAC), forward `/api/*` to ALB. Attach **AWS WAF** to CloudFront to block SQL Injection and XSS attacks. | 02/07/2026 | 02/07/2026 | AWS Console |
| Fri | - **High Availability Test:** Deliberately terminate 1 EC2 in the ASG → verify ALB automatically routes all traffic to the remaining EC2 → website continues to operate without interruption.<br>- **Load Test with Locust:** Simulate 300 concurrent users → observe ASG automatically scaling from 1 to 2-3 EC2 instances. | 03/07/2026 | 03/07/2026 | Locust |
| Sat | - Measure and compare performance: Response time **without Cache** (~100-200ms) vs **with Cache** (<5ms).<br>- Finalize report, prepare presentation slides and demo script. Practice full demo run 3 times with a timer. | 04/07/2026 | 04/07/2026 | Personal |

### Week 12 Achievements:

* **Complete Backend API:**
    * All 15 API Endpoints built and tested: hotel search, detail view, register/login, booking, cancellation, booking history, and admin management APIs.
    * **Redis Caching** working effectively: Cache Hit returns in < 5ms; Cache Miss queries RDS and stores the result in Redis with a 5-minute TTL — significantly reducing database load.

* **Complete Production Infrastructure (Phase 4 & 5):**
    * **ALB + ASG** operating stably: Load Balancer distributes traffic evenly; Auto Scaling Group automatically adds EC2 instances when CPU exceeds 70%.
    * **CloudFront + S3 + WAF:** Static website served from CDN edge locations with low latency; WAF protects against common attack vectors.
    * **CloudWatch + SNS:** Continuous monitoring system sends email alerts immediately upon detecting anomalies.

* **Test Results Proving 3 Key Properties:**
    * ✅ **High Availability:** Terminated 1 EC2 → ALB automatically routed to the remaining EC2 → Website continued operating without any service interruption.
    * ✅ **Auto Scaling:** Simulated 300 users via Locust → CPU exceeded 70% → ASG automatically scaled from 1 to 2-3 EC2 instances within 2-3 minutes.
    * ✅ **Caching:** Response time without cache: ~150ms | With cache (Redis): ~3ms → **~50x faster**.

* **Report & Demo Preparation:**
    * Complete presentation slides: problem statement, AWS solution architecture, test results with real measured data.
    * Demo scenario practiced 3 times with timing, fitting within the allotted presentation window.

{{% notice success %}}
**Summary:** Week 12 marks the completion of the capstone project **High-Availability Hotel Booking System on AWS**. The project successfully demonstrated 3 core cloud computing properties (High Availability, Auto Scaling, Caching) through real-world test scenarios with concrete, measurable results — a strong foundation for a high-scoring presentation.
{{% /notice %}}
