---
title: "Week 9 Worklog"
date: 2026-07-12
weight: 1
chapter: false
pre: " <b> 1.9. </b> "
---

### Week 9 Objectives:

- Researched comprehensive storage models, hash-based physical partitioning, and object-oriented CRUD scripting workflows with DynamoDB using the Python SDK (Boto3).
- Surveyed high-frequency streaming data ingestion architectures, S3 infrastructure-optimized batching principles, and real-time data stream analysis solutions using Flink SQL syntax.
- Analyzed quantitative performance differences between row-based (CSV) and columnar (Parquet) data formats, combining time-based data partitioning techniques to minimize the volume of data scanned during queries.
- Researched aesthetic standards, scientific spreadsheet layout planning, and smooth cross-sheet dynamic parameter flow control to embed interactive reports effectively.
- Explored secure internal VPC connectivity solutions and automated ETL roadmaps for synchronizing flat data into the enterprise data warehouse (Redshift).

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Researched NoSQL definitions, core components (Table, Item, Attribute), and administrative management overhead in Amazon DynamoDB.<br>- Analyzed physical hashing mechanisms based on Partition Keys and the flexibility of Composite Primary Keys (Partition Key + Sort Key).<br>- Surveyed and distinguished between Global Secondary Indexes (GSIs) and Local Secondary Indexes (LSIs) to accelerate data query performance.<br>- Compared the trade-offs in performance and cost between Eventually Consistent and Strongly Consistent read modes.<br>- Surveyed Python script structures using the AWS SDK (Boto3) library across the Client and Resource abstraction layers to execute CRUD operations.                                                                                                                                                                                                                                                                                       | 15/06/2026   | 15/06/2026      | https://000060.awsstudygroup.com/vi/ |
| 3   | - Researched Ubuntu launch procedures on Cloud9 and utilized the enca utility to inspect raw file encoding formats.<br>- Surveyed data lake partitioning methods on S3, separating logical directories for individual data tables (listings, reviews).<br>- Explored AWS Glue DataBrew: Executed Data Profiling jobs to calculate cardinality statistics and compiled recipes for data cleaning.<br>- Researched PySpark scripts on Glue Studio Notebooks to load DynamicFrames, clean data using Regex, and export Parquet formats back to S3.<br>- Surveyed Glue Crawler mechanisms for scanning clean Parquet partitions to automatically index metadata into the system catalog database.<br>- Researched advanced SQL command patterns in Athena (INNER JOIN, CTAS, CREATE VIEW) and compared Parquet compression performance against CSV.<br>- Surveyed Amazon QuickSight visualization concepts through the workflow sequence: Data source, Dataset, Analysis, Visual, and Dashboard.                                        | 16/06/2026   | 16/06/2026      | https://000070.awsstudygroup.com/vi/ |
| 4   | - Researched end-to-end data flow architectures: Ingesting streaming data via Kinesis Data Streams and Kinesis Data Firehose into S3.<br>- Surveyed high-frequency simulated data ingestion logic (2,000 records/sec) via Kinesis Data Generator authenticated through Amazon Cognito.<br>- Analyzed advanced Firehose configuration parameters: Compression mechanisms, error prefix designations, and buffer hint optimization techniques.<br>- Researched secure connection gateway solutions: Utilizing S3 Gateway Endpoints and self-referencing rules on Security Groups.                                                                                                                                                                                                                                                                                                                                                                                          | 17/06/2026   | 17/06/2026      | https://000072.awsstudygroup.com/vi/ |
| 5   | - Surveyed specialized key-value attributes in AWS Glue Tables to calculate actual record processing runtimes.<br>- Explored real-time streaming data analytics workflows using Flink SQL syntax on Apache Zeppelin via Kinesis Data Analytics.<br>- Surveyed flat data synchronization solutions pushing directly from S3 into physical Redshift schemas using Glue Studio PySpark scripts.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | 18/06/2026   | 18/06/2026      | https://000072.awsstudygroup.com/vi/ |
| 6   | - Researched advanced data formatting methods at both the field level (Field Level) and visual chart level (Visual Level).<br>- Surveyed techniques to improve professional reporting UI aesthetics: Applying custom themes (Custom Themes), standardizing the Inter font, and removing gridlines.<br>- Researched solutions to separate scientific report sheets into KPI summary views (Summary) and detailed data tables (Details).<br>- Explored advanced visualization templates: Points on map, Sankey Diagrams, and conditional color-formatted Pivot Tables.<br>- Researched Cascading Filter architectures to constrain display logic between regional filters and broader geographical areas.<br>- Surveyed Action Filters to isolate specific charts and preserve the integrity of machine learning reports.<br>- Researched Navigation Actions combined with Parameters to automatically switch pages and enforce cross-sheet filtering. | 19/06/2026   | 19/06/2026      | https://000073.awsstudygroup.com/vi/ |


### Week 9 Achievements:

- Mastering DynamoDB Database Programming and Operations:
  - Mastered data distribution via Partition Keys, the flexibility of Composite Primary Keys, and the performance trade-offs of read consistency modes.
  - Clearly differentiated the use cases and configuration methods for Global Secondary Indexes (GSIs) and Local Secondary Indexes (LSIs).
  - Successfully established standardized Python Boto3 script structures (Client and Resource layers) to execute the complete CRUD lifecycle of data tables.

- Mastery of Serverless Data Lake and Streaming Pipeline Architectures:
  - Orchestrated Kinesis Firehose, time-partitioned S3, Glue PySpark for Parquet transformations, and Athena for serverless SQL querying.
  - Mastered VPC Gateway Endpoint solutions combined with self-referencing rules on Security Groups to securely isolate Glue Spark communication flows.
  - Mastered advanced Flink SQL script writing on Apache Zeppelin within Kinesis Data Analytics to parse volatile traffic streams.
  - Successfully explored automated ETL roadmaps for synchronizing flat data files from S3 directly into physical Redshift schemas.

- Expertise in Intelligent BI and Interactive Dashboard Solutions (QuickSight Expert):
  - Deeply understood QuickSight's core resource chain: Data source, Dataset, Analysis, Visual, and Dashboard.
  - Successfully designed ML Forecast charts, Sankey Diagrams, points on map, and conditionally color-formatted Pivot Tables.
  - Proficiently operated cascading filters, isolated action filters, and dynamic parameters (Parameters) for cross-sheet navigation and filtering.
