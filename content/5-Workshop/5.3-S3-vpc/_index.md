---
title : "Build AWS network infrastructure"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

## Objective

This step creates the network foundation for AWS_OmniStay. The system needs public subnets to receive traffic from the internet through ALB and NAT Gateway, and private subnets to run backend EC2, RDS MySQL, and ElastiCache Redis more securely.

The network model uses 2 Availability Zones for higher availability:

- 2 public subnets for ALB and NAT Gateway.
- 2 private app subnets for EC2 backend.
- 2 private data subnets for RDS and Redis.

## 1. Create VPC

Go to **VPC** -> **Your VPCs** -> **Create VPC**.

Configuration:

| Field | Value |
| --- | --- |
| Resource to create | VPC only |
| Name tag | `omnistay-vpc` |
| IPv4 CIDR | `10.0.0.0/16` |
| Tenancy | Default |

After creation, verify that the VPC has CIDR `10.0.0.0/16` and is in the correct region `ap-southeast-1`.

![VPC details](/images/531.jpg)
<p align="center"><em>Figure 5.3.1: VPC created successfully.</em></p>

## 2. Create 6 subnets

Go to **VPC** -> **Subnets** -> **Create subnet**. All subnets belong to `omnistay-vpc`.

| Subnet name | AZ | IPv4 CIDR | Role |
| --- | --- | --- | --- |
| `omnistay-public-a` | `ap-southeast-1a` | `10.0.1.0/24` | Public subnet for ALB/NAT |
| `omnistay-public-b` | `ap-southeast-1b` | `10.0.2.0/24` | Public subnet for ALB/NAT |
| `omnistay-app-a` | `ap-southeast-1a` | `10.0.10.0/24` | Private app subnet for EC2 |
| `omnistay-app-b` | `ap-southeast-1b` | `10.0.11.0/24` | Private app subnet for EC2 |
| `omnistay-data-a` | `ap-southeast-1a` | `10.0.20.0/24` | Private data subnet for RDS/Redis |
| `omnistay-data-b` | `ap-southeast-1b` | `10.0.21.0/24` | Private data subnet for RDS/Redis |

After creating the 2 public subnets, enable **Auto-assign public IPv4 address** for `omnistay-public-a` and `omnistay-public-b`.

![VPC details](/images/532.jpg)
<p align="center"><em>Figure 5.3.2: Six subnets created.</em></p>

## 3. Create Internet Gateway

Go to **VPC** -> **Internet Gateways** -> **Create internet gateway**.

Configuration:

| Field | Value |
| --- | --- |
| Name tag | `omnistay-igw` |
| Attach VPC | `omnistay-vpc` |

After creating it, select the Internet Gateway, go to **Actions** -> **Attach to VPC**, and attach it to `omnistay-vpc`.

![VPC details](/images/533.jpg)
<p align="center"><em>Figure 5.3.3: Internet Gateway.</em></p>

![VPC details](/images/534.jpg)
<p align="center"><em>Figure 5.3.4: Attach Internet Gateway to VPC.</em></p>

## 4. Create public route table

Go to **VPC** -> **Route tables** -> **Create route table**.

Configuration:

| Field | Value |
| --- | --- |
| Name | `omnistay-public-rt` |
| VPC | `omnistay-vpc` |

Routes:

| Destination | Target |
| --- | --- |
| `10.0.0.0/16` | local |
| `0.0.0.0/0` | `omnistay-igw` |

Subnet associations:

- `omnistay-public-a`
- `omnistay-public-b`

![VPC details](/images/535.jpg)
<p align="center"><em>Figure 5.3.5: Public route table with internet route.</em></p>

## 5. Create NAT Gateways

NAT Gateway allows EC2 instances in private app subnets to access outbound internet for downloading packages, calling AWS services, or sending logs without using public IP addresses.

Create the first NAT Gateway:

| Field | Value |
| --- | --- |
| Name | `omnistay-nat-a` |
| Subnet | `omnistay-public-a` |
| Connectivity type | Public |
| Elastic IP allocation | Automatic |

Create the second NAT Gateway:

| Field | Value |
| --- | --- |
| Name | `omnistay-nat-b` |
| Subnet | `omnistay-public-b` |
| Connectivity type | Public |
| Elastic IP allocation | Automatic |

![VPC details](/images/537.jpg)
<p align="center"><em>Figure 5.3.7: Creating NAT Gateway.</em></p>

## 6. Create private route tables for app subnets

Create a route table for the app subnet in AZ-a:

| Field | Value |
| --- | --- |
| Name | `omnistay-app-a-rt` |
| VPC | `omnistay-vpc` |
| Route | `0.0.0.0/0 -> omnistay-nat-a` |
| Subnet association | `omnistay-app-a` |

Create a route table for the app subnet in AZ-b:

| Field | Value |
| --- | --- |
| Name | `omnistay-app-b-rt` |
| VPC | `omnistay-vpc` |
| Route | `0.0.0.0/0 -> omnistay-nat-b` |
| Subnet association | `omnistay-app-b` |

Private data subnets containing RDS and Redis do not need an internet route in the basic demo flow. They only receive internal connections from backend EC2 through Security Groups.

![VPC details](/images/536.jpg)
<p align="center"><em>Figure 5.3.6: Private app route table created.</em></p>

## Expected Result

After this step, the system has a dedicated VPC, separated public/private subnets, internet access for public subnets, NAT Gateway access for app subnets, and a ready network foundation for ALB, EC2, RDS, and Redis.
