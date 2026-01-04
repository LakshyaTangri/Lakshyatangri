## A Data Engineer / Architect Portfolio Overview



My AWS data stack:

## My AWS Data Stack

| Data Size | File Type               | Primary Language | Ingestion / Extract Tools                          | Processing / Transform                            | Orchestration / Workflow                     | Catalog / Governance                                            | Database Model Type                                           | Database / Engine                                             | Storage                                                     | Consumption (BI / ML / API)                                                                    |
| --------- | ----------------------- | ---------------- | -------------------------------------------------- | ------------------------------------------------- | -------------------------------------------- | --------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- | ----------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| 1MB–1GB   | csv, xls, xlsx          | Python / SQL     | AWS SDK (Boto3), custom scripts, direct S3 uploads | Lambda, small Glue jobs, AWS SDK for pandas       | EventBridge, simple Step Functions           | Glue Data Catalog (optional), Lake Formation (light)            | Relational (Operational OLTP)                                 | Amazon RDS / Amazon Aurora                                    | Amazon S3                                                   | QuickSight, direct app queries via RDS/Aurora, Lambda APIs                                     |
| 1GB–100GB | JSON, csv (NoSQL + raw) | Python           | AWS DMS, AWS AppFlow, Kafka Connect (MSK)          | Glue jobs, EMR/EMR Serverless, AWS SDK for pandas | Step Functions, MWAA (Airflow), EventBridge  | Glue Data Catalog, Lake Formation                               | NoSQL (Document / Key-Value, Operational) + Data Lake (files) | Amazon DynamoDB / Amazon DocumentDB (operational), S3 as lake | Amazon S3                                                   | QuickSight on Athena, app access via DynamoDB/DocumentDB, ML via SageMaker                     |
| 100GB–1TB | csv, Parquet            | Python / SQL     | AWS Glue connectors, AWS DMS, MSK (Kafka)          | Glue ETL, EMR (Spark), AWS SDK for pandas         | Step Functions, MWAA (Airflow)               | Glue Data Catalog, Lake Formation                               | Analytical Warehouse (OLAP) + Data Lake                       | Amazon Redshift (incl. Spectrum) / Amazon Athena              | Amazon S3 (Parquet)                                         | QuickSight, ad‑hoc SQL via Athena/Redshift, ML via SageMaker                                   |
| 10TB+     | Parquet, graph data     | Python / SQL     | MSK (Kafka), AWS DMS (CDC), Kinesis Data Streams   | EMR/EMR Serverless, Glue ETL, AWS SDK for pandas  | Step Functions, MWAA, Event‑driven pipelines | Glue Data Catalog, Lake Formation, fine‑grained access controls | Graph (Neptune) + Lakehouse / Large‑scale Analytics (OLAP)    | Amazon Neptune (graph workloads) / Amazon Redshift / Athena   | Amazon S3 (multi‑tier, lifecycle to S3 Glacier for archive) | QuickSight, Neptune graph queries, large‑scale analytics via Redshift/Athena, ML via SageMaker |



My Data Stack outside AWS:
| Data Size | File Type           | Primary Language      | Extract / Ingestion Tools                              | Processing / Transform                             | Orchestration / Workflow                          | Catalog / Governance                                                                  | Database Model Type                                      | Database / Engine                                                            | Storage                                                             | Consumption (BI / ML / API)                                                                 |
| --------- | ------------------- | --------------------- | ------------------------------------------------------ | -------------------------------------------------- | ------------------------------------------------- | ------------------------------------------------------------------------------------- | -------------------------------------------------------- | ---------------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| 1MB–1GB   | CSV, XLS            | Python / SQL          | Custom scripts, REST APIs, cloud SDKs, CSV uploads     | dbt (for SQL), Python ETL scripts, pandas          | Cron, lightweight schedulers, Prefect             | Basic metadata in DB, optional open‑source catalog (e.g., OpenMetadata)               | Relational (Operational OLTP)                            | PostgreSQL / MySQL (managed or self‑hosted)                                  | Object storage (MinIO, GCS, Azure Blob)                             | Metabase / Superset / Looker Studio, direct app queries, small APIs                         |
| 1GB–100GB | JSON, CSV (NoSQL)   | Python                | Airbyte, Fivetran, Stitch, Kafka Connect               | Spark / Flink jobs, dbt where SQL‑friendly, Python | Airflow / Prefect / Dagster                       | Data catalog (e.g., OpenMetadata, DataHub), role‑based access                         | NoSQL (Document / Wide‑Column, Operational) + Data Lake  | MongoDB Atlas / Couchbase / Cassandra                                        | Object storage + database‑native storage                            | BI tools (Superset, Looker Studio, Power BI), ML platforms (Vertex AI, MLflow)              |
| 100GB–1TB | CSV, Parquet        | Python / SQL          | Airbyte, Fivetran, Kafka, cloud transfer services      | dbt, Spark (Databricks, EMR‑like), SQL ELT         | Airflow / Prefect / Dagster                       | Central catalog (e.g., Glue‑like via Hive Metastore, Unity Catalog, Data Catalog)     | Analytical Warehouse (OLAP) + Data Lake                  | Snowflake / BigQuery / Databricks SQL / ClickHouse                           | Data lake on object storage (Parquet on GCS / Azure / MinIO)        | BI (Looker, Power BI, Tableau), notebooks, ML platforms (Vertex AI, Databricks ML)          |
| 10TB+     | Parquet, graph data | Python / SQL / Cypher | Kafka, Debezium (CDC), cloud‑native streaming services | Spark / Flink streaming, batch ELT with dbt & SQL  | Airflow / Prefect / Dagster, streaming schedulers | Lakehouse governance (Unity Catalog, Delta/Iceberg/Hudi tables, DataHub/OpenMetadata) | Graph (Neo4j) + Lakehouse / Large‑scale Analytics (OLAP) | Neo4j Aura (graph), Snowflake / BigQuery / Databricks Lakehouse / ClickHouse | Lakehouse (Parquet + Iceberg / Delta Lake / Hudi) on object storage | Enterprise BI, large‑scale analytics, real‑time features & ML from lakehouse and graph APIs |


Source systems → Land in S3 → Curate with Glue/EMR → Warehouse in Redshift → Serve via Athena/QuickSight → Optional ML in SageMaker

1. Ingestion into S3 (raw zone)

Position Amazon S3 as the single landing zone for all raw data, including batch files, CDC streams, and third-party SaaS sources.

Use AWS DMS for database replication, MSK or Kinesis for streaming data, and AppFlow or custom Boto3 pipelines for SaaS and file-based ingestion.

2. Data lake curation (S3 + Glue)

Implement a layered data lake on S3 (raw → cleaned → curated), using columnar formats such as Parquet with partitioning for performance and cost efficiency.

Use AWS Glue (optionally EMR with awswrangler) for schema inference, ETL transformations, and table registration in the Glue Data Catalog.

Apply Lake Formation for fine-grained data access control and governance.

3. Analytics warehouse in Redshift

Load high-value, frequently queried, and conformed datasets from curated S3 into Amazon Redshift to support low-latency analytical workloads.

Use Redshift COPY from S3 for ingestion and Redshift Spectrum to query data directly in the data lake when appropriate.

4. Query and BI with Athena and QuickSight

Use Amazon Athena for ad-hoc, exploratory, and cost-efficient SQL queries directly on S3 data via the Glue Data Catalog.

Use Amazon QuickSight as the primary BI and visualisation layer, connecting to both Redshift (for performance-critical dashboards) and Athena (for lake-based analysis).

5. Orchestration, data quality, and ML

Orchestrate ingestion, transformation, and warehouse loading using AWS Step Functions or Managed Airflow (MWAA), triggered on schedules or events.

Enable Artificial Intelligence / machine learning workflows with Amazon SageMaker, consuming curated S3 or Redshift data to train, evaluate, and deploy models.
