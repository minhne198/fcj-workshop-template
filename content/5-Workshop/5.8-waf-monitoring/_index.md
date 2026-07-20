---
title : "Configure WAF, monitoring, and alerts"
date : 2024-01-01
weight : 8
chapter : false
pre : " <b> 5.8. </b> "
---

## Objective

This step adds protection and operations capabilities for AWS_OmniStay. AWS WAF is attached to CloudFront to filter dangerous requests. CloudWatch, SNS, and CloudWatch Alarms are used to monitor the system, detect errors, and alert when resources show signs of overload.

## 1. Create AWS WAF Web ACL for CloudFront

Go to **WAF & Shield** -> **Web ACLs** -> **Create web ACL**.

Configuration:

| Field | Value |
| --- | --- |
| Resource type | CloudFront distributions |
| Scope | Global |
| Name | `omnistay-cloudfront-waf` |
| Associated resource | AWS_OmniStay CloudFront distribution |
| Default action | Allow |

Recommended managed rule groups:

| Rule group | Purpose |
| --- | --- |
| `AWSManagedRulesCommonRuleSet` | Block common suspicious requests |
| `AWSManagedRulesKnownBadInputsRuleSet` | Block known malicious inputs |
| `AWSManagedRulesSQLiRuleSet` | Reduce SQL Injection risk |
| `AmazonIpReputationList` | Block IPs with poor reputation |

![VPC details](/images/581.jpg)
<p align="center"><em>Figure 5.8.1: Web ACL overview of `omnistay-cloudfront-waf`.</em></p>

## 2. Note about image upload rule

In the AWS_OmniStay deployment, image upload requests may be blocked by CloudFront/WAF before reaching the backend. If the frontend includes multipart/form-data image upload, check WAF sampled requests and add a narrow allow rule for the valid upload endpoint.

Rules for adding an allow rule:

- Allow only the required upload path, for example `/api/uploads/images`.
- Place the allow rule above managed rules that may block the request.
- Do not disable the whole WAF just to handle one endpoint.
- Verify that the backend still requires user authentication if the endpoint needs admin/owner permission.

![VPC details](/images/582.jpg)
<p align="center"><em>Figure 5.8.2: Allow rule for image upload if the system implements upload functionality.</em></p>

## 3. Create SNS Topic for alerts

Go to **SNS** -> **Topics** -> **Create topic**.

Configuration:

| Field | Value |
| --- | --- |
| Type | Standard |
| Name | `omnistay-alerts` |
| Subscription protocol | Email |
| Endpoint | Alert recipient email |

After creating the subscription, open the email and confirm it so the status becomes `Confirmed`.

![VPC details](/images/583.jpg)
<p align="center"><em>Figure 5.8.3: SNS topic `omnistay-alerts`.</em></p>

## 4. Create CloudWatch Dashboard

Go to **CloudWatch** -> **Dashboards** -> **Create dashboard**.

Configuration:

| Field | Value |
| --- | --- |
| Dashboard name | `OmniStay-Demo` |

Recommended widgets:

| Group | Metric |
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

The dashboard helps quickly observe the main system components during demos or load tests.

![VPC details](/images/584.jpg)
<p align="center"><em>Figure 5.8.4: CloudWatch dashboard `OmniStay-Demo`.</em></p>

## 5. Create CloudWatch Alarms

Create a high CPU alarm for the Auto Scaling Group:

| Field | Value |
| --- | --- |
| Metric | ASG CPUUtilization |
| Resource | `omnistay-api-asg` |
| Condition | Greater than 70 |
| Notification | `omnistay-alerts` |
| Alarm name | `omnistay-asg-cpu-high` |

Create a 5XX error alarm from ALB:

| Field | Value |
| --- | --- |
| Metric | `HTTPCode_Target_5XX_Count` |
| Resource | `omnistay-alb` |
| Condition | Greater than 10 |
| Notification | `omnistay-alerts` |
| Alarm name | `omnistay-alb-5xx-high` |

Create a high CPU alarm for RDS:

| Field | Value |
| --- | --- |
| Metric | RDS `CPUUtilization` |
| Resource | `omnistay-mysql` |
| Condition | Greater than 80 |
| Notification | `omnistay-alerts` |
| Alarm name | `omnistay-rds-cpu-high` |

![VPC details](/images/585.jpg)
<p align="center"><em>Figure 5.8.5: List of created CloudWatch Alarms.</em></p>

## 6. Control cost during demo

Resources that may generate hourly charges:

- NAT Gateway.
- Application Load Balancer.
- RDS MySQL.
- ElastiCache Redis/Valkey.
- AWS WAF.
- Public IPv4 address.
- CloudWatch logs/metrics if log volume is high.

During the workshop, monitor the Billing dashboard and budget alerts. If the next demo is not needed immediately, reduce ASG desired capacity or pause/delete paid resources according to the cleanup guide.

## Expected Result

After this step, CloudFront is protected by WAF, the system has an SNS topic for alerts, a CloudWatch dashboard for observation, and basic alarms for CPU, backend errors, and RDS.
