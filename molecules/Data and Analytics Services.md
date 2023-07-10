AWS offers [[Athena]], [[Redshift]], [[OpenSearch]], [[Kinesis#Kinesis Data Stream]], [[Kinesis#Kinesis Data Firehose]],  [[EMR]], [[QuickSight]], [[Glue]], [[Lake Formation]] and [[Flink]].


| Service         | Purpose                      | Architecture                                                   |
| ------------------ | ---------------------------- | -------------------------------------------------------------- |
| [[Redshift]]       | Data warehouse               | Handles exabyte-scale data. Indexes for high performance.      |
| [[Glue]]           | ETL                          | Serverless. Out-of-the-box integration for Athena. ETL.             |
| [[Lake Formation]] | Data Lake                    | Serverless. Fine-grained permissions.                          |
| [[QuickSight]]     | BI Analytics Visualization   | Users and Role are separately managed from [[IAM]].            |
| [[Athena]]         | SQL for S3                   | Serverless. Federated query. Glue. Cost optimization - no etl. |
| [[Data Pipeline]]  | Workflow Automation with ETL | Supports [[Hybrid Cloud Architecture]]                         |
| [[EMR]]            | Map Reduce                   | Scalable data pipelines, Big Data                              |
| [[OpenSearch]]     | Search                       | Unstructured data search                                                               |

** Redshift versus Athena**
![[redshift-spectrum-athena-comparison-table.png|512]]
Fig. Comparison

### Database Technology Use-Cases

| AWS Service(s)                                                     | Database Type | Use Cases                                                                                          |
| ------------------------------------------------------------------ | ------------- | -------------------------------------------------------------------------------------------------- |
| Amazon [[RDS]], [[Aurora]], Amazon [[Redshift]]                    | Relational    | Traditional applications, ERP, CRM, e-Commerce                                                     |
| [[DynamoDB]]                                                       | Key-value     | High-traffic web applications, ecommerce systems, gaming applications                              |
| Amazon [[ElastiCache]] for Memcached, Amazon ElastiCache for Redis | In-Memory     | Caching, session management, gaming leaderboards, geospatial applications                          |
| Amazon [[DocumentDB]]                                              | Document      | Content management, catalogs, user profiles                                                        |
| Amazon [[Keyspaces]]                                               | Wide column   | High-scale industrial applications for equipment maintenance, fleet management, route optimization |
| Neptune                                                            | Graph         | Fraud detection, social networking, and recommendation engines.                                    |
| Timestream                                                         | Time series   | IoT applications, Development Operations (DevOps), industrial telemetry                            |
| Amazon QLDB                                                        | Ledger        | Systems of record, supply chain, registrations, banking transactions                               |
|                                                                    |               |                                                                                                    |

Fig. Table: AWS Database Technology and Use-Cases