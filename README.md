## Overview

This repository showcases my work as a **Data Engineer & Architect** operating across **business, cloud, and data engineering layers**.

My AWS data stack 
| Data Size | File Type           | Database Model Type          | Database                                | Storage                              | Compute                                                 |
| --------- | ------------------- | ---------------------------- | --------------------------------------- | ------------------------------------ | ------------------------------------------------------- |
| 1MB–1GB   | CSV, XLS            | Relational (RDBMS)           | Amazon RDS / Amazon Aurora              | Amazon S3 (Warehouse)                           | AWS Lambda, AWS Glue DataBrew / Glue ETL, Amazon Athena |
| 1GB–100GB | JSON, CSV (MongoDB) | NoSQL (Document / Key-Value) | Amazon DocumentDB / Amazon DynamoDB     | Amazon S3 (Warehouse/Lakehouse)                          | Amazon EC2, AWS Lambda, Amazon EMR / AWS Glue           |
| 100GB–1TB | CSV, Parquet        | Columnar / Analytical        | Amazon Redshift, Amazon Athena          | Amazon S3 (Lakehouse/Lake + Parquet)                  | Amazon EMR (Spark), AWS Glue, Amazon EC2                |
| 10TB+     | Parquet, Graph Data | Graph / Analytical           | Amazon Neptune (Graph), Amazon Redshift | Amazon S3 (Lake + S3 Glacier for archive) | Amazon EMR, AWS Glue, Amazon EC2                        |

My Data Stack outside AWS
| Data Size | File Type           | Database Model Type            | Database / Engine                                               | Storage                                                         | Compute / Processing                                                                       |
| --------- | ------------------- | ------------------------------ | --------------------------------------------------------------- | --------------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| 1MB–1GB   | csv, xls            | Relational              | PostgreSQL / MySQL (managed or self-hosted)                     | Object storage (MinIO, GCS, Azure Blob)                         | Serverless functions (Cloud Functions / Azure Functions), lightweight Airflow / cron jobs  |
| 1GB–100GB | JSON, csv (NoSQL)   | NoSQL (Document / Wide-Column) | MongoDB Atlas / Couchbase / Cassandra                           | Object storage + database native storage                        | Kubernetes or VM-based services, Spark on small cluster, Airbyte/Fivetran/Stitch ingestion |
| 100GB–1TB | csv, Parquet        | Analytical / Columnar   | Snowflake / BigQuery / Databricks SQL / ClickHouse              | Data lake on object storage (Parquet on GCS/Azure/MinIO)        | Apache Spark (Databricks or self-managed), dbt, Airflow orchestration                      |
| 10TB+     | Parquet, graph data | Graph + Lakehouse / Analytical | Neo4j Aura (Graph), Snowflake / BigQuery  | Lakehouse (Parquet + Iceberg/Delta Lake/Hudi) on object storage | Large Spark / Trino / Presto clusters, Databricks, Kubernetes-based processing             |
