# data-analyst-ramandeep
# Project 1 Objective
 - The project focuses on migrating the City of Vancouver's data to an AWS cloud platform, with the objective of building a comprehensive data analytics pipeline. Its goal is to streamline data processing, analysis, and visualization across various city departments, ensuring scalability, security, and efficiency in managing the city's data.

## Table of Contents
 - [Methodology](#methodology)
 - [AWS Services](#aws-services)
 - [Data Pipeline Implementation](#data-pipeline-implementation)
 - [Data Analysis](#data-analysis)
 - [Outcome](#outcome)
 - [Insights and Findings](#insights-and-findings)
 - [Cost Estimation](#cost-estimation)
 - [Conclusion](#conclusion)

## Methodology

### Data Analytical Question Formulation
 - Delved into the data for 2023 and 2024 to produce a metric called “Percentage of Calls handled.” The metric will provide the percentage of calls handled in the years 2023 and 2024, respectively
 - Percentage of calls handled = (Number of calls handled/ Number of calls offered) * 100
   
   <kbd> <img src="https://github.com/user-attachments/assets/b4ba5957-631f-40cb-843f-3cbc6c1e20c9" /> </kbd>

### Data Discovery
- Focussed on the procedure ‘Contact Centre Metrics’ in the Government and Finance department for the city of Vancouver. [Link](https://opendata.vancouver.ca/explore/dataset/3-1-1-contact-centre-metrics/information/)
- Utilized datasets in Excel Format is as shown below.
   
  <kbd> <img src="https://github.com/user-attachments/assets/83f35f73-b08c-4036-9ee7-a5299c6434ee" /> </kbd>
  
  
### Dataset Preparation
 - Involved:
    - Data collection
    - ETL processes
    - Data cleaning using AWS Glue DataBrew.

### Data Pipeline Design
 - Designed using draw.io to automate data processing stages.

<kbd> <img src="https://github.com/user-attachments/assets/1db2d1a2-0146-4cdc-8ca0-635b5c38f8c3" /> </kbd>

### Data Analysis
 - Performed queries and derived insights using AWS Athena.
   
## AWS Services
 - AWS Services:
    - Amazon S3 for storage
    - EC2 for computation
    - AWS Glue for ETL processes
    - Athena for data analysis.
 
## Data Pipeline Implementation:
 - The ETL processes were implemented using AWS Glue.
 - Various transformation operations were performed, including schema changes, aggregation, and union functions:
   - Schema Change Operation: The schema of both the 2023 and 2024 datasets was modified by removing unnecessary columns and retaining and renaming the columns BI_ID, Year, calls_offered, and calls_handled.
   - Aggregate Operation: The records in the 'Year' column of the 2023 and 2024 datasets were aggregated to group the data effectively.
   - Union Operation: The Union function was applied to combine the 2023 and 2024 datasets into a single, cohesive dataset, merging records from both inputs.
   - Change Schema Refinement: Unwanted columns were further removed using an additional schema change operation to streamline the dataset.
   - Derived Column: A new metric, Calls Handled Percentage, was calculated using the SQL expression
     Calls handled Percentage = (calls_handled/calls_offered) *100.
   
<kbd> <img src="https://github.com/user-attachments/assets/24320c3c-9672-441f-a97a-d27af10cc2a5" /> </kbd>
<kbd> <img src="https://github.com/user-attachments/assets/cb39031b-63ff-44e3-8d94-faaec68a40d1" /> </kbd>

## Data Analysis
 - Data analysis was performed using AWS Athena.
 - SQL database was utilized to analyze the content of the dataset.
 - Table DDL

sql
  --Contact Centre Table --
CREATE EXTERNAL TABLE `gov_fin_contactcentre_table_ramandeep`(
  `year` string, 
  `percent_of_calls_handled` string)
ROW FORMAT DELIMITED 
  FIELDS TERMINATED BY ',' 
STORED AS INPUTFORMAT 
  'org.apache.hadoop.mapred.TextInputFormat' 
OUTPUTFORMAT 
  'org.apache.hadoop.hive.ql.io.HiveIgnoreKeyTextOutputFormat'
LOCATION
  's3://project1-govfin-ramandeep-dataset/Government and Finance Domain/Curated/Yearly Analysis'
TBLPROPERTIES (
  'classification'='csv', 
  'skip.header.line.count'='1', 
  'transient_lastDdlTime'='1724308959')

 - Data as pulled from the AWS Athena Database is as shown below:
   
<kbd> <img src="https://github.com/user-attachments/assets/cb2a351d-4d43-4c0b-bc08-6ab839cfa19d" /> </kbd>

## Outcome
 - General Server and Web Server were set up using Amazon EC2 for internal and external data access.
 - Published the annual analysis report on the percentage of calls handled for public access.
   
<kbd> <img src="https://github.com/user-attachments/assets/77a924dd-3efb-46c8-aef0-2a18660fa08f" /> </kbd>

## Insights and Findings
 - 2023: The percentage of calls handled was 94.19%, indicating a high efficiency in managing calls at the '3-1-1 contact center' for the City of Vancouver during this year.
 - 2024: The percentage of calls handled dropped slightly to 92.93%. This reduction, although minor, indicates a slight decline in the call-handling efficiency compared to the previous year.
 - Comparison: There is a noticeable decrease of approximately 1.26% in the percentage of calls handled from 2023 to 2024. This could be due to various factors, such as an increase in call volume, changes in operational procedures, or resource allocation challenges.

## Cost Estimation
 - Amazon S3: Estimated annual expense of $285.846 for storage across four buckets.
 - AWS Glue DataBrew: Estimated yearly cost of $32.04 for cleaning and restructuring datasets.
 - AWS Glue: Estimated total cost of $13.20 for ETL job runs.
 - Amazon Athena: Estimated annual expense of $35.76 for querying and analysis.
 - EC2: Total yearly cost of $225.96 for hosting general and web servers.

## Conclusion
 - The project showcases the effectiveness of using AWS cloud services for large-scale data analytics and highlights the capabilities in automating data workflows and gaining insights for city management.


# Project 2 Objective
 - To design and implement a secure, efficient, and scalable Data Analytics Platform (DAP) for the City of Vancouver using AWS cloud services. This platform aims to facilitate the migration, storage, processing, and analysis of city datasets to enhance data-driven decision-making while ensuring data protection, governance, and compliance with privacy standards.

## Table of Contents
 - [Data Discovery](#data-discovery)
 - [ETL Workflow](#etl-workflow)
 - [Data protection](#data-protection)
 - [Data Governance](#data-governance)
 - [Data Monitoring](#data-monitoring)
 - [AWS Services Used](aws-services-used)
 - [DAP Architectural Analysis](#dap-architectural-analysis)
 - [Insights and Findings](#insights-and-findings)
 - [Conclusion](#conclusion)

### Data Discovery
- The same data 311 contact centre was used in the Government and Finance department for the city of Vancouver.

### ETL Workflow
 - Implemented using AWS Glue for ETL processes.
  
### Data Protection
 - Identity and Access Management (IAM)
    - User Access Control: IAM is used to create users, user groups, and roles to manage access to AWS resources. The project assigns specific roles, such as 'LabRole,' to ensure that only authorized users have the necessary permissions.
    - Policy Creation: Policies are defined to grant the minimum required permissions for users, ensuring that each user or group can access only the resources they need.
 - Encryption and Decryption
    - AWS Key Management Service (KMS):
    - Symmetric Key: Used to encrypt and decrypt data using the same key. This key is used for encrypting data stored in Amazon S3 buckets, ensuring that only authorized users can access the data.
    - Asymmetric Key: A pair of public and private keys is used for encryption and decryption. This method is used for data that requires higher security, allowing encryption with one key and decryption with another.
 - Data Storage Security in Amazon S3
    - Bucket Policies and Access Controls: Access to the S3 buckets is restricted using IAM roles and bucket policies to ensure that only authorized users and services can access the data.
    - ETL Pipeline Security: The ETL pipeline processes data through AWS Glue with encryption mechanisms to protect data during transformation.
 - Techniques for Integrity Protection
    - Data Integrity Checks: Encryption and decryption mechanisms ensure that data is secure and unaltered during storage and transmission. For example:
    - Versioning in S3: Amazon S3 versioning is configured to keep previous versions of objects, preventing data loss from accidental deletions or alterations.
<kbd> <img src="https://github.com/user-attachments/assets/57d421b2-800f-46c3-bfa4-77a91f42af5b" /> </kbd>
 - Monitoring and Auditing
    - Replication: Replication provides data protection by automatically making several copies of the data in different buckets, whether in the same region or different regions.
<kbd> <img src="https://github.com/user-attachments/assets/1d2d988e-8167-4751-b786-56664aabd2d2" /> </kbd>

### Data Governance
 - Data Quality Management
    - AWS Glue: ETL Pipeline - The ETL (Extract, Transform, Load) pipeline using AWS Glue is designed to clean, process, and structure the data before it is stored in the "Trusted" zone. This ensures that the data used for analytics is of high quality, complete, and ready for analysis.
    - Data Quality Checks: During the data processing phase, AWS Glue performs data quality checks to remove duplicates, fill in missing values, and format the data according to predefined standards.
    - Conditional Routing: Only records that pass data quality checks are moved into the trusted zone, ensuring that the dataset used for analytics is accurate and reliable.
 - Data Privacy Management
    - Encryption and Access Control: Data privacy is enforced by encrypting sensitive data using AWS KMS and restricting access through IAM policies. Only authorized users with the appropriate roles can access and manipulate sensitive data, ensuring that privacy is maintained.
 - Data Versioning: S3 versioning is enabled to maintain a history of changes to the data. This allows for the recovery of previous versions in case of accidental deletions or modifications, supporting data governance by providing data lineage and audit trails.
    - LabRole Implementation: A predefined role ('LabRole') is assigned to manage permissions for encryption keys, data access, and usage within the platform, ensuring consistent governance policies across the platform.
   
### Data Monitoring
 - AWS CloudWatch for Real-Time Monitoring
    - Resource Monitoring: AWS CloudWatch is used to monitor key metrics of AWS resources, such as CPU utilization, memory usage, and network activity. It provides real-time insights into the performance of the data analytics platform.
    - Custom Metrics and Dashboards: CloudWatch allows the creation of custom metrics and dashboards for specific aspects of the data analytics platform. For example, monitoring the status of S3 buckets, ETL pipelines in AWS Glue, and data processing jobs helps track data flow and detect anomalies.
    - Alarms and Notifications: CloudWatch Alarms are set up to trigger notifications when certain thresholds are breached (e.g., unusually high data access attempts and resource usage spikes). This proactive monitoring helps in identifying and mitigating potential security incidents or performance issues.
<kbd> <img src="https://github.com/user-attachments/assets/53b7ffa0-86c6-4edd-b427-d1dc45151f34" /> </kbd>
 - AWS CloudTrail for Audit Logging
    - Activity Logging: AWS CloudTrail captures and logs all API calls made within the AWS environment. This includes actions performed on data stored in S3, modifications to IAM roles, and operations within AWS Glue.
    - Audit Trails: CloudTrail logs serve as an audit trail, documenting who accessed or modified the data and when these actions occurred. This is crucial for tracking unauthorized access attempts and ensuring compliance with data governance policies.
    - Event History: CloudTrail maintains a history of events for a specified period, allowing for a retrospective analysis of data access and usage patterns. This can be used to detect unusual activity or verify compliance with data privacy regulations.
<kbd> <img src="https://github.com/user-attachments/assets/09aa4205-e325-4717-948e-f16937369441" /> </kbd>

## AWS Services Utilised
 - AWS Services:
   - IAM: Access control and user management.
   - KMS: Encryption and key management.
   - S3: Data storage and management with encryption and versioning.
   - AWS Glue: Data integration, ETL, and data quality management.
   - CloudWatch: Real-time monitoring and alerting.
   - CloudTrail: Audit logging and activity tracking.
   - S3 Access Logs: Data access monitoring and auditing.
   - Cost Explorer: Cost tracking and optimization.
 
## DAP Architectural Analysis
 - Operational Excellence
   - Best Practices: AWS best practices enhance operational efficiency, reliability, and scalability, using IAM for fine-grained access control and AWS Glue for structured data processing.
   - Disaster Recovery: S3 bucket replication and versioning ensure disaster recovery, enabling data recovery from accidental deletion or corruption.
   - Real-Time Monitoring: AWS CloudWatch enables real-time performance monitoring, providing automated alerts for metrics like CPU usage and memory consumption.
 - Security
   - Comprehensive Security Practices: IAM roles and policies enforce least privilege access, ensuring restricted access to only necessary resources.
   - Data Encryption: AWS KMS provides encryption for sensitive data in S3 buckets, utilizing both symmetric and asymmetric techniques to protect confidentiality.
   - Auditing and Monitoring: AWS CloudTrail logs all user activities, providing a detailed audit trail to detect potential security incidents and ensure accountability.
 - Reliability
   - Data Redundancy and Versioning: S3 versioning maintains multiple object versions, ensuring data integrity in the event of accidental modifications.
   - Regular Backups: Regular backups, facilitated by S3 replication and AWS Glue, enable fast data restoration in case of failure.
   - Data Quality and Integrity: AWS Glue automates data governance, ensuring data quality through validation and integrity checks.
 - Performance Efficiency
   - Optimized Resource Usage: S3 efficiently handles large datasets, with performance optimized by CloudWatch monitoring and resource tuning.
   - Right Sizing of Resources: The platform ensures optimal resource allocation, avoiding over-provisioning by right-sizing instances and storage.
 - Cost Optimization
   - Cost Management: AWS Cost Explorer tracks and analyzes cost patterns, identifying savings opportunities by optimizing storage and minimizing redundant data.
   - Elastic Resource Allocation: The platform dynamically adjusts resource allocation based on current needs, such as scaling to a web server during data publishing.
 - Sustainability
   - Long-Term Efficiency and Scalability: The architecture supports long-term sustainability by rightsizing resources and minimizing waste while ensuring scalability.
   - Resource Efficiency: Optimization of instances and storage minimizes the platform's carbon footprint and supports efficient data management.
 
## Insights and Findings
 - Secure Data Analytics Platform: The project implements a secure platform using AWS, with data protection ensured via IAM and KMS for access control and encryption.
 - Effective Data Governance: AWS Glue handles ETL processes and data quality checks, ensuring only clean, high-quality data is used, further supported by IAM policies and S3 structuring.
 - Comprehensive Data Monitoring: AWS CloudWatch and CloudTrail enable real-time monitoring, ensuring operational transparency and detecting anomalies swiftly.
 - Scalability and Cost Optimization: S3 and Glue ensure a scalable architecture capable of handling large datasets, while AWS Cost Explorer manages cost efficiency.
 - Enhanced Data Security and Privacy: Role-based access control and encryption ensure compliance and data integrity, with S3 versioning supporting data recovery. 

## Conclusion
 - The AWS Data Analytics Platform for the City of Vancouver provides a secure, scalable, and efficient solution for managing and analyzing city datasets. By utilizing a range of AWS services, such as IAM, KMS, S3, Glue, CloudWatch, and CloudTrail, the platform ensures strong data protection, governance, and real-time monitoring. This comprehensive approach safeguards sensitive information through encryption and access controls while also improving data quality and integrity with detailed ETL processes and governance protocols.
 - Built for adaptability, the platform scales to accommodate varying data volumes and analytical demands while maintaining cost efficiency. It establishes a solid foundation for data-driven decision-making, adhering to strict privacy and compliance standards. This project demonstrates the effectiveness of cloud-based solutions in meeting the intricate data management requirements of public sector organizations. Looking ahead, the platform can be enhanced with advanced analytics and automated governance for deeper insights and ongoing optimization.
