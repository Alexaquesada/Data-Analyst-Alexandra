# Data-Analyst-Alexandra
# Descriptive Analysis

## Project 1: Analysis and Evaluation of Training Programs Impact on Employee Performance

### Objective
To evaluate which training programs are most effective in improving employee skills and job performance.

### Dataset
Two primary datasets were provided by the HR department:
- **Training Attendance Records (CSV/JSON):** Details on employee participation in various training programs.
- **Employee Performance Metrics (CSV/JSON):** Records of periodic performance evaluations across departments.

### Methodology

#### 1️⃣ Data Analysis

**Business Question:**  
*Which training programs are most effective in improving employee performance?*

After receiving the datasets, I explored and analyzed the data fields to identify relevant variables.  
To visualize the potential factors affecting training effectiveness, I designed a **Fishbone Diagram**, classifying causes into:
- Policies
- Tools
- Processes
- Evaluations
- Environment
- People

**Key problems identified:**
- Lack of mandatory training policies
- Outdated platforms with limited access
- Inconsistent evaluations and poor follow-up
- Low employee motivation

![image](https://github.com/user-attachments/assets/ce48be3f-c0d0-4a0a-ac32-6473b1c9171f)

The root causes identified in the Fishbone analysis highlighted multiple areas that may contribute to varying training outcomes, such as:
- Lack of mandatory training policies
- Outdated platforms and limited access to learning resources
- Inconsistent evaluation processes and poor follow-up
- Low employee motivation and communication barriers

In addition, the analysis summarized key elements:

- **Goal:** Identify which training programs improve performance.
- **Objective:** Improve skills and job performance.
- **Cause Factors:** Evaluate how training influences both skills and performance.

![image](https://github.com/user-attachments/assets/ddb5481e-33f8-4315-9606-8704511e3659)

### Tools and Technologies

- **Microsoft Excel:** For initial data exploration and Fishbone diagram development.
- **Draw.io:** For visual representation of analysis models.

### Deliverables

- Business question breakdown and root cause analysis documentation.
- Visual Fishbone diagrams.
- Problem definition report for design phase alignment.

---

## 2️⃣ Data Lake Design

Based on the analysis outcomes, a cloud-based data lake architecture was designed using AWS services to ensure scalability, security, and operational efficiency.

### Data Storage Planning

- Two separate S3 buckets were created for raw datasets, with folders organized by year, quarter, month, and week.
- Property tags applied for cost monitoring, resource identification, and long-term manageability.
- Storage classes selected according to access patterns:
  - **S3 Standard:** For frequently accessed datasets.
  - **S3 One-Zone-IA:** For less frequently accessed historical data.

### Data Analytics Platform (DAP) Setup

- Virtual Private Cloud (VPC) configured to securely isolate cloud resources.
- Subnet, internet gateway, and routing tables created for controlled access.
- EC2 instances (**t3.micro**) provisioned for compute capacity.
- Elastic Block Store (EBS) volumes attached for temporary processing.
- Security groups defined with restricted inbound/outbound rules.

### Architecture Visualization

The full architectural design was documented through a comprehensive architecture diagram.
AWS global infrastructure hierarchy.
VPC and EC2 resource allocation.
Data ingestion flow from HR users to S3 storage.
Metadata and tagging strategy.

![image](https://github.com/user-attachments/assets/34d384e9-131b-477e-b190-42f43071705b)

### Tools and Technologies

- AWS S3
- AWS VPC
- AWS EC2
- AWS EBS
- AWS Security Groups
- Draw.io for architecture visualization

### Deliverables

- Complete data lake architecture design
- AWS infrastructure deployed and validated
- Visual architecture diagrams documenting the cloud environment

---

## 3️⃣ Implementation

The design was successfully deployed on AWS following best practices:

- AWS CLI commands were used to automate EC2 instance creation, security group configuration, and metadata setup.

**Example EC2 launch command used:**

![image](https://github.com/user-attachments/assets/e055acf0-65ed-4b5d-9f99-1f4a970390f8)


- Lifecycle policies were applied to S3 buckets to automate archival and optimize storage costs over time.
- Security configurations ensured that only authorized HR personnel had access to sensitive data during ingestion.

This implementation phase successfully transformed the initial design into a fully operational cloud-based data ingestion pipeline.

---

## 4️⃣ Cost Evaluation and Data Cleaning Preparation

After the ingestion and setup of the data lake, a cost evaluation and data quality process was initiated to ensure data integrity before further analytics.

### 4.1 Cost Evaluation of Dataset Ingestion

- **AWS Pricing Calculator** was used to estimate storage costs.
- By selecting the correct storage classes:
  - **S3 Standard** for frequent access
  - **S3 One-Zone-IA** for infrequent access  
- Costs remained minimal and fully optimized.
- Deleting unnecessary files further reduced costs.

This activity improved understanding of AWS cost control and emphasized the importance of proper data governance during ingestion.

![image](https://github.com/user-attachments/assets/9a597f15-be36-477c-93b8-db0b86bc7468)

### 4.2 Dataset Cleaning Analysis & Design

The team used **AWS Glue DataBrew** to assess the quality of the ingested datasets:

- **Employee Performance Metrics**
- **Training Attendance Records**

**Key profiling activities included:**

- Identification and removal of redundant or unnecessary data fields.
- Standardization of column names and formats for consistency.
- Preparation of transformation rules to address:
  - Datatype inconsistencies
  - Null values
  - Incorrect formats

This design phase ensured that data cleaning rules were well-defined before automated processing.

![image](https://github.com/user-attachments/assets/76a42c8e-845d-439e-a0dc-5a270aec729f)

### 4.3 Dataset Cleaning Implementation

Using the pre-configured transformations, **AWS Glue DataBrew** executed the data cleaning workflows automatically:

- New cleaned datasets were generated and saved back into **Amazon S3** for further analytical processing.
- Validation of results was performed using the AWS S3 console to ensure all transformations were correctly applied.
- This serverless approach accelerated processing time and eliminated the need for managing compute infrastructure.

![image](https://github.com/user-attachments/assets/43b39e30-77db-4956-97fe-87f6756d58ee)

![image](https://github.com/user-attachments/assets/4567104f-6ed6-4dc6-b250-126e8015194e)

### Tools and Technologies

- AWS Pricing Calculator for cost analysis
- AWS Glue DataBrew for data profiling and cleaning rule configuration

### Deliverables

- Cost estimation report for data ingestion and storage
- Cleaned datasets stored in AWS S3
- Data profiling summary with identified quality issues and solutions

---

## 5️⃣ Curated Data Processing and Advanced Cost Evaluation

After the ingestion and cleaning of raw data, the next phase focused on transforming the cleaned datasets into curated, analysis-ready datasets using serverless ETL pipelines, while continuously monitoring storage costs.

### 5.1 Refining Business Question and Metrics Design

The team revisited the original business question:

**"Which training programs are most effective in improving employee performance?"**

A data science framework was applied to categorize the problem into four analytics types:

- **Descriptive:** What happened
- **Diagnostic:** Why it happened
- **Predictive:** What might happen
- **Prescriptive:** What should be done

![image](https://github.com/user-attachments/assets/687f55af-0ee5-4e55-9307-f5369d98d084)

This categorization led to the formulation of additional sub-questions, allowing for richer metric design and deeper exploration of factors contributing to training effectiveness.

### 5.2 ETL Pipeline Design with AWS Glue

Using **AWS Glue**, an ETL (Extract, Transform, Load) job was developed to automatically process the cleaned data stored in **S3**.

The ETL workflow included:

- Extracting data from the "Cleaning" folder in S3.
- Applying further transformations, including:
  - Data normalization
  - Data enrichment
- Storing the processed outputs into a curated S3 bucket under the ETL zone: `hr-ETL-ale`.
- Cataloging the resulting curated datasets into the **AWS Glue Data Catalog** for easy discovery.

### 5.3 Data Exploration with Amazon Athena

The curated datasets were explored using **Amazon Athena** through serverless SQL-based queries directly on S3.

- Simple queries were used to validate data quality and extract initial insights.
- Interactive querying was performed without needing dedicated compute resources.
- This approach maintained real-time data exploration and cost-efficiency.

### 5.4 Updated Cost Evaluation

A revised cost evaluation was conducted after ETL processing:

- AWS usage metrics reviewed:
  - Storage volume
  - Glue ETL job execution minutes
  - Athena query costs
- Preventive cost alerts were configured to proactively monitor spending thresholds.
- Efficient lifecycle management continued to keep incremental costs minimal.

![image](https://github.com/user-attachments/assets/947cf166-a58d-4543-aa0d-de193b09d071)

![image](https://github.com/user-attachments/assets/541a9086-a994-49cd-b633-4f14135c9226)

### Tools and Technologies

- AWS Glue Studio for ETL workflow design
- AWS Glue Data Catalog for metadata management
- Amazon Athena for SQL-based querying
- AWS CloudWatch for cost alarm monitoring

### Deliverables

- ETL pipelines converting cleaned data into curated datasets
- Metadata catalog for query-ready data
- Architecture diagrams from Draw.io

---

## 6️⃣ Candidate Engagement Analysis

As part of the advanced practice, an additional business problem was addressed to reinforce skills:

**Business Question:**  
*"How does candidate engagement vary across application stages and platforms?"*

### 6.1 Analysis

- A full operational architecture design was prepared starting with detailed **Excel designs**, later translated into visual architecture diagrams using **Draw.io**.
- The architecture separates public-facing data from internal protected datasets, ensuring security while enabling flexible processing.

**Design documents include:**

- Fishbone diagram analyzing causes affecting candidate engagement (Appendix A)
- Full Data Analytics Platform (DAP) Solution Architecture (Appendix B)

> 💡 **Insertar imagen aquí: Fishbone Diagram & Architecture Diagram**

### 6.2 Design

Visual diagrams were finalized using **Draw.io**, representing both data flow and system architecture.

Supporting Excel files were created to define:

- Data lake folder structure
- Cleaning rules and schema definitions
- ETL process design

This provided a comprehensive blueprint for cloud deployment.

### 6.3 Implementation

- The initial data ingestion was implemented by creating the first S3 bucket following the designed folder hierarchy.
- Four distinct datasets were ingested:
  - Web Server Page Visit Logs
  - General Server Platform Engagement Summary
  - Beanstalk Application Interaction Logs
  - Lambda Engagement Tags

- Proper tagging and metadata were applied for resource governance.
- S3 lifecycle rules were configured to optimize storage costs based on access frequency.

### 6.4 Operational Environment Architecture

The final architecture incorporated additional AWS services:

- EC2 instances (public and private subnets)
- Elastic Beanstalk containers for application hosting
- Lambda functions for tag management and event-driven processing
- Internet Gateway for external access control

![image](https://github.com/user-attachments/assets/2d8cfe75-cb7f-416c-9698-6a51e4272332)

![image](https://github.com/user-attachments/assets/df22a901-ec30-442c-91ad-b26290f28bc7)

![image](https://github.com/user-attachments/assets/95f0bd2f-6649-4b1e-b4a8-df12e620dd40)

### Tools and Technologies

- Draw.io for architecture modeling
- Excel for data preparation designs
- AWS Glue
- AWS Athena
- AWS S3
- AWS Pricing Calculator
- AWS CloudWatch
- SQL

### Deliverables

- Cost assessment report
- Visual diagrams of data architecture and ETL flow
- Fully automated ETL pipeline for HR data
- Analytical results accessible through Athena
- Cost-effective architecture with continuous monitoring
- Key insights supporting strategic HR decisions

---

# Project 2: City of Vancouver Capital Budget Analysis

### Project Title

**Descriptive analysis of data on Capital Budget in City of Vancouver**

### Objective

To design and analyze a cloud-based data platform focused on understanding budget changes made by the City of Vancouver in its **2023–2026 Capital Plan** and **2025 Capital Budget**.  
This analysis utilized a public dataset from Vancouver’s open data portal, containing detailed information on:

- Original budget allocations
- Approved revisions
- Final revised budgets
- Service area categorization (e.g. arts and culture, transportation, civic facilities, community facilities)

### Dataset

- **2023–2026 Capital Plan and 2025 Capital Budget Dataset**  
  (Source: City of Vancouver Open Data Portal)

### Methodology

As a final project exercise, I applied the full cloud data platform development cycle to this real-world dataset, consolidating skills in:

- Cloud data architecture
- Data ingestion
- Data cleaning
- Data enrichment
- Data analysis using AWS services

### Business Question

**"How have the original budgets changed compared to the revised plan in the City of Vancouver's 2023–2026 Capital Plan and 2025 Capital Budget?"**

### Dataset Source Details

- Original capital plan allocations
- Approved revisions
- Final revised capital budgets
- Categorized by service area:
  - Transportation
  - Arts and Culture
  - Civic Facilities
  - Community Facilities
  - Others

![image](https://github.com/user-attachments/assets/247f52b7-8355-4be8-937d-adc41ee1197c)

## Data Ingestion and Processing

### 1️⃣ Data Ingestion

- The dataset was ingested into **AWS S3**, with a dedicated bucket: `vcp-raw-ale`.
- The original CSV file was organized into structured subfolders following data lake best practices.

### 2️⃣ Data Profiling

- **AWS Glue DataBrew** was used to execute full data profiling:
  - File size: 362 rows × 17 columns
  - Data types: text, numeric, dates
  - Identification of null values and inconsistencies

This profiling stage guided the design of cleaning workflows to ensure data quality.

> 💡 **Insertar imagen aquí: DataBrew Profiling Summary**

### 3️⃣ Data Cleaning

- A new S3 bucket `vcp-cln-ale` was created to store cleaned data.
- Within **Glue DataBrew**:
  - Empty text fields (e.g., *Service Category 3*, *Project Name*) were replaced with `"Undefined"`.
  - Missing numeric values were replaced with `0`.
  - Negative values (representing budget reductions) were validated and retained.
- The cleaning workflow was automated in **DataBrew Job**: `vcp-cleaning job-ale`.

> 💡 **Insertar imagen aquí: DataBrew Cleaning Job Configuration**

### 4️⃣ Data Cataloging

- **AWS Glue Crawler (`vcp-crawler-ale`)** was used to catalog the cleaned dataset.
- The cleaned dataset was registered into a new **Glue Database (`vcp-data-catalog-ale`)** and converted into **Parquet** format for efficient querying.
- The dataset became fully discoverable for advanced querying via **Athena**.

### 5️⃣ Data Enrichment

Using **AWS Glue Studio**:

- A new calculated column `Budget-difference` was created:
  - `Budget-difference = Revised Budget - Original Budget`
- Aggregations were applied to compute:
  - Average budget difference per service category
  - Total budget difference
  - Project count per category
- Transformations were validated using **Glue Output Schema Preview**.

![image](https://github.com/user-attachments/assets/3ad74c8e-a9fb-4dae-83f5-bf6f09e349a8)

## Data Summarization and Querying

- The curated dataset was queried using **Amazon Athena**.
- The queries aggregated data to summarize:
  - Average Budget Difference by Service Category
  - Total Budget Difference by Service Category
  - Project Count per Category
- Output results included:
  - Service Category
  - Average Budget Difference
  - Total Budget Difference
  - Project Count
- Queries were saved and exported as CSV for reporting and visualization.

These final outputs directly answered the business question, providing actionable insights into which service areas experienced budget increases or reductions.


---

### Tools and Technologies

- AWS Glue DataBrew
- AWS Glue Studio
- AWS Glue Catalog
- Amazon Athena for analytical queries
- Draw.io for process diagrams

### Deliverables

- Complete enriched dataset with budget difference metrics
- Athena query outputs answering capital budget analysis
- Summary report with service area budget variations

![image](https://github.com/user-attachments/assets/56776665-b3a0-4f71-90ad-47292a57679c)

## Security, Governance, and Monitoring Implementation

Following the successful ingestion, cleaning, enrichment, and querying stages, the project advanced into deeper levels of cloud security, governance, monitoring, and alignment with AWS Well-Architected Framework best practices.

### 🔐 Data Security

**AWS Key Management Service (KMS):**

- A symmetric encryption key (`vcp-key-ale`) was created.
- Default encryption was activated on all S3 buckets involved (`vcp-raw-ale`, `vcp-cln-ale`, `vcp-cur-ale`) to ensure data-at-rest protection.

**Versioning and Replication:**

- **S3 Versioning** enabled to maintain file change history.
- **Cross-bucket Replication** configured to automatically copy data for improved resilience.

---

### 🔎 Data Governance and Quality Controls

**AWS Glue Studio Data Quality Rules:**

- A dedicated ETL flow (`vcp-QC-ale`) was developed to validate data completeness.
- Quality thresholds applied across multiple columns (service categories and budget values).
- Records were automatically classified into `Passed` or `Failed` folders based on validation results.
- No failures were detected at runtime, confirming high data consistency.

**ETL Adjustments:**

- Governance flow was streamlined into a single processing block based on dataset structure.

---

### 📊 Data Monitoring

**AWS CloudWatch:**

- Custom dashboard (`vcp-MCR-ale`) created to monitor bucket size metrics and Glue resource usage.
- Budget alarms (`vcp-alarm-ale`) configured to notify when cost thresholds are approached.

**AWS CloudTrail:**

- A trail (`vcp-tra-ale`) configured to enable full traceability of account activities, logging all API calls and resource changes.

---

### Tools and Technologies

- AWS KMS, S3 Encryption, S3 Versioning & Replication
- AWS Glue Quality Checks
- AWS CloudWatch, CloudTrail for monitoring and auditing

### Deliverables

- Full security configuration documentation
- Governance quality control results
- Monitoring dashboards, alarms, and audit logs

---

## Alignment with AWS Well-Architected Framework

The implementation was evaluated across AWS’s five pillars:

### 1️⃣ Operational Excellence
- Applied iterative design, error recovery, and incremental validation.
- Further opportunities remain for full operations-as-code and proactive failure anticipation.

### 2️⃣ Security
- Strong data-at-rest encryption and traceability implemented.
- IAM role-based security and incident preparedness identified as areas for future enhancement.

### 3️⃣ Reliability
- Data flow dependencies well documented.
- Partial monitoring and basic alerting configured.
- Full disaster recovery documentation pending.

### 4️⃣ Performance Efficiency
- Resource provisioning and storage optimization aligned.
- Advanced partitioning, compression, and fine-tuning recommended for further optimization.

### 5️⃣ Cost Optimization
- Serverless services (Glue, Athena) reduced operational costs.
- Lifecycle policies, tagging, and cost monitoring applied.
- Further cost savings possible through partitioning and automated reporting.

##  Recommendations

- Implement formal disaster recovery documentation.
- Fully automate security best practices (IAM roles, automated incident response).
- Optimize Athena queries with data partitioning and compression.
- Expand tagging and billing analysis using AWS Cost and Usage Reports (CUR).
- Further optimize Glue job sizing (DPUs) for performance-cost balance.

---

## Reflection on AWS Deployment and Service Models

In this module, I learned how AWS simplifies technology adoption for businesses by eliminating concerns about physical hardware. Companies like UCW previously had to purchase servers, maintain data centers, and handle all infrastructure needs. With AWS, companies use virtual servers and cloud storage while AWS manages physical infrastructure and security.

Depending on the deployment model (Private, Public, Hybrid, Multicloud), companies can combine cloud and on-premises resources.

Service models distribute responsibility differently:

- **IaaS (Infrastructure as a Service):** Company manages most components.
- **PaaS (Platform as a Service):** Company focuses on applications and data.
- **SaaS (Software as a Service):** Company mainly consumes ready-to-use software.

These models allow businesses to save costs, scale faster, and focus on using technology to drive their goals without dealing with complex technical overhead.
![image](https://github.com/user-attachments/assets/dc512bd6-894c-49c9-ba75-0d389213f14e)

![image](https://github.com/user-attachments/assets/4e8560a9-c47c-4101-b883-70b1f4b94d22)

![image](https://github.com/user-attachments/assets/4df36be2-52d1-4540-81ec-a67dda89de4a)

## Reflection on AWS Cost Analysis

In this module, I learned how the cloud not only simplifies technology adoption but also enables **smart cost savings**.

- Previously, companies had to:
  - Purchase additional physical servers to grow.
  - Maintain costly infrastructure.
  - Allocate physical space and perform ongoing hardware maintenance.

- With **AWS Cloud Services**:
  - Companies only pay for what they actually use.
  - Resources can be scaled up or down based on demand.
  - Overspending on unused capacity is avoided.

We analyzed the **Delaware North case study**, where migrating to AWS allowed the company to:

- Eliminate most physical servers.
- Improve capacity and scalability.
- Enhance security.
- Strengthen disaster recovery preparedness.

Additionally, I learned that AWS offers multiple **Support Plans** depending on organizational needs. For example:

- For the **Human Resources team** (simpler workloads), the **Developer Support Plan** is sufficient.
- This plan offers professional support access without paying for advanced enterprise services that may not be needed.

AWS Cost Management tools and flexible support options allow organizations to balance cost, performance, and service levels according to their operational priorities.

![image](https://github.com/user-attachments/assets/bf2ca5c0-fe92-4717-9384-6a6534bb99e9)

![image](https://github.com/user-attachments/assets/2b145675-ebc7-4df6-9858-e0d6da015b66)

![image](https://github.com/user-attachments/assets/ad92d02f-3e02-48d1-8fc4-66f8c3a39a97)

**AWS Global infrastructure** 

AWS has strategic points for storing the information most frequently accessed by its affiliates. This way, when someone requests that data again, the response is much faster because it is already closer and does not need to go to the main data center. Meanwhile, AWS is responsible for physically protecting the entire infrastructure, and the client company continues to decide who can view or modify its information

![image](https://github.com/user-attachments/assets/a5fd8a06-8431-442b-a3a5-460c4f52029b)

**AWS IAM** 
In this module, I learned how security and access management work in AWS using IAM. I practiced creating users, groups, and policies, and assigning permissions based on each person's role. For example, some users can only view EC2 or S3 resources, while others have permissions to manage servers. I also understood the difference between managed policies (which can apply to multiple users or groups) and inline policies (which are specific to a single user or group). In addition, we reviewed the shared responsibility model, where AWS is responsible for the physical infrastructure and basic security, while the company is responsible for managing the operating system, software, applications, and data within the virtual servers. This practice allowed me to see how, in the cloud, it is possible to give each person highly controlled access, based on what they actually need to do, while maintaining security and control over the data.

![image](https://github.com/user-attachments/assets/b60eebd8-5804-4231-8c81-c1c8c4444359)

![image](https://github.com/user-attachments/assets/b999c986-4d5f-4f7c-a80e-7c3538a051c3)

**AWS VPC**
In this module, I learned how to create a complete network within AWS to host applications. I designed the network by dividing the servers between public and private zones, controlling how they connect to the internet and to each other. I also configured security rules to protect access. Finally, I launched a web server within that network and verified that it was working correctly. Through this exercise, I understood how to build secure and organized infrastructures in the cloud, similar to traditional physical networks, but taking advantage of the flexibility offered by AWS.

![image](https://github.com/user-attachments/assets/bf87062e-3a8d-48e5-911e-b0b803db2cc2)

**AWS Lambda** 
In this module, I learned how to create a complete network within AWS to host applications. I designed the network by dividing the servers between public and private zones, controlling how they connect to the internet and to each other. I also configured security rules to protect access. Finally, I launched a web server within that network and verified that it was working correctly. Through this exercise, I understood how to build secure and organized infrastructures in the cloud, similar to traditional physical networks, but taking advantage of the flexibility offered by AWS

![image](https://github.com/user-attachments/assets/fe999f2b-e53d-479e-a023-76c9d1681553)









