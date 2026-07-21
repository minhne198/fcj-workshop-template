---
title: "Week 10 Worklog"
date: 2026-06-15
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Week 10 Objectives:
* Build a centralized data analytics platform with **Data Lake**, **AWS Glue**, **Amazon Athena**, and **Amazon QuickSight**.
* Master the **ETL (Extract - Transform - Load)** pipeline to process and standardize large-scale data on AWS.
* Deploy advanced permission controls with **IAM Role & IAM Conditions** for IP/Time-based access restriction.
* Explore **Generative AI applications on AWS** through the integration of **DynamoDB Zero-ETL + OpenSearch + Amazon Bedrock**.
* Learn **Data Preparation** with **AWS Glue DataBrew** and **Data Warehousing** with **Amazon Redshift**.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| Mon | - Learn about Data Lake and S3's role in large-scale data systems<br>- **Practice:**<br>&nbsp;&nbsp;+ Create AWS Glue Database<br>&nbsp;&nbsp;+ Configure Glue Crawler<br>&nbsp;&nbsp;+ Automatically catalog data | 15/06/2026 | 15/06/2026 | Lab 000035 |
| Tue | - Learn about ETL pipeline with AWS Glue<br>- **Practice:**<br>&nbsp;&nbsp;+ Create Glue Job<br>&nbsp;&nbsp;+ Cleanse data<br>&nbsp;&nbsp;+ Store output data in S3<br>&nbsp;&nbsp;+ Design ETL pipeline with Glue Studio | 16/06/2026 | 16/06/2026 | Lab 000035 & 000060 |
| Wed | - Learn about Amazon Athena and Amazon QuickSight<br>- **Practice:**<br>&nbsp;&nbsp;+ Query S3 data with Athena<br>&nbsp;&nbsp;+ Create QuickSight Dataset<br>&nbsp;&nbsp;+ Create analytical charts<br>&nbsp;&nbsp;+ Create reporting Dashboard | 17/06/2026 | 17/06/2026 | Lab 000035 |
| Thu | - Learn about IAM Role, IAM Conditions, and Switch Role<br>- **Practice:**<br>&nbsp;&nbsp;+ Configure access condition by IP Address<br>&nbsp;&nbsp;+ Configure condition by login time<br>&nbsp;&nbsp;+ Test Switch Role<br>&nbsp;&nbsp;+ Evaluate dynamic access-control model | 18/06/2026 | 18/06/2026 | Lab 000043 |
| Fri | - Learn about Generative AI integration, Vector Embeddings, and Semantic Search<br>- **Practice:**<br>&nbsp;&nbsp;+ Configure DynamoDB Zero-ETL Integration to OpenSearch<br>&nbsp;&nbsp;+ Learn about Amazon Bedrock<br>&nbsp;&nbsp;+ Note AI application potential in enterprise systems | 19/06/2026 | 19/06/2026 | Lab 000039 |
| Sat | - Learn about AWS Glue DataBrew and Amazon Redshift<br>- **Practice:**<br>&nbsp;&nbsp;+ Cleanse data with DataBrew<br>&nbsp;&nbsp;+ Handle Missing Values<br>&nbsp;&nbsp;+ Build automated Recipe<br>&nbsp;&nbsp;+ Create Redshift Cluster<br>&nbsp;&nbsp;+ Load data and run analytical SQL queries | 20/06/2026 | 20/06/2026 | Lab 000072 & 000073 |

### Week 10 Achievements:

#### Data Analytics & Data Lake:
* Deeply understood **Data Lake** architecture and the full data journey: Collect → Store → Process → Analyze on AWS.
* Successfully practiced the complete **AWS Glue ETL** pipeline: Crawl schemas → Create Jobs → Run processing → Export output.
* Used **Amazon Athena** for serverless data analysis directly on S3, optimizing costs without managing a dedicated database.
* Built interactive Dashboards with **Amazon QuickSight** to support business reporting and data-driven decision-making.

#### Advanced Access Management:
* Configured **IAM Conditions** for context-aware access control (IP, time) — Zero Trust security for enterprise environments.
* Mastered the **Switch Role** mechanism for flexible multi-account management without proliferating user accounts.

#### Generative AI & Data Intelligence:
* Understood the **DynamoDB → OpenSearch** integration architecture via Zero-ETL without a traditional ETL pipeline.
* Learned the principle of **Vector Embeddings** and **Semantic Search**: Finding results by meaning rather than exact keywords using Amazon Bedrock.

#### Data Preparation & Data Warehouse:
* Used **AWS Glue DataBrew** to cleanse and standardize data through a visual, no-code interface.
* Deployed **Amazon Redshift** to store and analyze business data at petabyte scale with high performance.

{{% notice success %}}
**Summary:** Week 10 completes the full picture of Data Analytics on AWS — from ingestion, processing, analysis to visualization and AI application — while laying a solid foundation for building real-world capstone projects in the weeks ahead.
{{% /notice %}}
