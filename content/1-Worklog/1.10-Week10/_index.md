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
| Mon | - Study the **Data Lake overview (Lab 000035)**: Centralized storage architecture and S3's role in large-scale data systems.<br>- Create an **AWS Glue Database** and configure a Crawler to automatically catalog data schemas. | 15/06/2026 | 15/06/2026 | Lab 000035 |
| Tue | - Practice the full **ETL pipeline with AWS Glue**: Create a Glue Job, cleanse data, and store processed output to S3.<br>- Explore Glue Studio to design ETL pipelines visually without writing code. | 16/06/2026 | 16/06/2026 | Lab 000035 & 000060 |
| Wed | - Query data directly on S3 using **Amazon Athena** with standard SQL, without a dedicated database server.<br>- Visualize analytical results with **Amazon QuickSight**: Create Datasets, charts, and reporting Dashboards. | 17/06/2026 | 17/06/2026 | Lab 000035 |
| Thu | - Practice **IAM Role & Conditions (Lab 000043)**: Configure access conditions based on IP Address and login time.<br>- Test **Switch Role** and evaluate the effectiveness of a dynamic access control model in an enterprise environment. | 18/06/2026 | 18/06/2026 | Lab 000043 |
| Fri | - Explore **Generative AI integration (Lab 000039)**: Configure **DynamoDB Zero-ETL Integration** to synchronize data to OpenSearch.<br>- Learn about Vector Embeddings and Semantic Search with **Amazon Bedrock** and the potential of AI in enterprise applications. | 19/06/2026 | 19/06/2026 | Lab 000039 |
| Sat | - Practice **AWS Glue DataBrew (Lab 000072)**: Cleanse data, handle Missing Values, and build Recipes for automated transformation.<br>- Explore **Amazon Redshift** architecture (Data Warehouse): Create a Cluster, load data, and run analytical SQL queries. | 20/06/2026 | 20/06/2026 | Lab 000072 & 000073 |

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
