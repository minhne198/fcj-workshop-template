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
| Mon | - Learn about Backend API completion and Redis Cache<br>- **Practice:**<br>&nbsp;&nbsp;+ Complete `HotelsController.cs`<br>&nbsp;&nbsp;+ Complete `BookingsController.cs`<br>&nbsp;&nbsp;+ Complete `AdminController.cs`<br>&nbsp;&nbsp;+ Integrate Redis Cache into SearchService<br>&nbsp;&nbsp;+ Verify Cache HIT under 5ms and 5-minute TTL | 29/06/2026 | 29/06/2026 | Visual Studio 2022 |
| Tue | - Phase 4 - Learn about Compute layer with EC2, ALB, and Target Group<br>- **Practice:**<br>&nbsp;&nbsp;+ Create EC2 Launch Template<br>&nbsp;&nbsp;+ Write User Data script to install .NET 8 automatically<br>&nbsp;&nbsp;+ Create Application Load Balancer<br>&nbsp;&nbsp;+ Create Target Group and `/health` Health Check | 30/06/2026 | 30/06/2026 | AWS Console |
| Wed | - Learn about Auto Scaling Group, CloudWatch Alarm, and SNS<br>- **Practice:**<br>&nbsp;&nbsp;+ Create Auto Scaling Group Min=1, Max=4<br>&nbsp;&nbsp;+ Configure Target CPU=70%<br>&nbsp;&nbsp;+ Create CloudWatch Alarm when CPU > 70%<br>&nbsp;&nbsp;+ Configure SNS email alert for Admin | 01/07/2026 | 01/07/2026 | AWS Console |
| Thu | - Phase 5 - Learn about frontend hosting, CDN, and WAF<br>- **Practice:**<br>&nbsp;&nbsp;+ Upload HTML, CSS, JS to Amazon S3<br>&nbsp;&nbsp;+ Enable Static Website Hosting<br>&nbsp;&nbsp;+ Create CloudFront Distribution using OAC<br>&nbsp;&nbsp;+ Forward `/api/*` to ALB<br>&nbsp;&nbsp;+ Attach AWS WAF to block SQL Injection and XSS | 02/07/2026 | 02/07/2026 | AWS Console |
| Fri | - Learn about High Availability testing and Load Testing<br>- **Practice:**<br>&nbsp;&nbsp;+ Terminate 1 EC2 instance in ASG<br>&nbsp;&nbsp;+ Verify ALB routes traffic to the remaining EC2<br>&nbsp;&nbsp;+ Run Locust test with 300 concurrent users<br>&nbsp;&nbsp;+ Observe ASG scaling to 2-3 EC2 instances | 03/07/2026 | 03/07/2026 | Locust |
| Sat | - Learn about performance measurement and demo preparation<br>- **Practice:**<br>&nbsp;&nbsp;+ Compare response time without cache and with Redis cache<br>&nbsp;&nbsp;+ Finalize report<br>&nbsp;&nbsp;+ Prepare presentation slides<br>&nbsp;&nbsp;+ Practice demo 3 times with a timer | 04/07/2026 | 04/07/2026 | Personal |

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

### Week 12 practice screenshots:

![Week 12 practice - 3](/images/worklog/3.jpg)

![Week 12 practice - 4](/images/worklog/4.jpg)

![Week 12 practice - 591](/images/591.jpg)

![Week 12 practice - 592](/images/592.jpg)
