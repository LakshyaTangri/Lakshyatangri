## Overview

This repository showcases my work as a **Data Engineer & Architect** operating across **business, cloud, and data engineering layers**.

My AWS data stack 
| Data Size | File Type           | Primary Language | Extract / Ingestion Tools                        | Database Model Type            | Database / Engine                       | Storage                              | 
| --------- | ------------------- | ---------------- | ------------------------------------------------ | ------------------------------ | --------------------------------------- | ------------------------------------ |
| 1MB–1GB   | csv, xls            | Python / SQL     | AWS SDK (Boto3), custom scripts, S3 uploads      | Relational (OLTP)              | Amazon RDS / Amazon Aurora              | Amazon S3                            | AWS Lambda, AWS Glue DataBrew / Glue ETL, Amazon Athena      |
| 1GB–100GB | JSON, csv (NoSQL)   | Python           | AWS DMS, AWS AppFlow, Kafka Connect (MSK)        | NoSQL (Document / Key-Value)   | Amazon DocumentDB / Amazon DynamoDB     | Amazon S3                            | Amazon EC2, AWS Lambda, Amazon EMR / AWS Glue                |
| 100GB–1TB | csv, Parquet        | Python / SQL     | AWS Glue connectors, AWS DMS, MSK (Kafka)        | Analytical / Columnar (OLAP)   | Amazon Redshift, Amazon Athena          | Amazon S3 (Parquet)                  | Amazon EMR (Spark), AWS Glue, Amazon EC2                     |
| 10TB+     | Parquet, graph data | Python / SQL     | MSK (Kafka), AWS DMS (CDC), Kinesis Data Streams | Graph + Lakehouse / Analytical | Amazon Neptune (Graph), Amazon Redshift | Amazon S3 (+ S3 Glacier for archive) | 


My Data Stack outside AWS
| Data Size | File Type           | Primary Language | Extract / Ingestion Tools                              | Database Model Type            | Database / Engine                                               | Storage                                                         | Compute / Processing                                                                       |
| --------- | ------------------- | ---------------- | ------------------------------------------------------ | ------------------------------ | --------------------------------------------------------------- | --------------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| 1MB–1GB   | csv, xls            | Python / SQL     | Custom scripts, REST APIs, cloud SDKs, CSV uploads     | Relational (OLTP)              | PostgreSQL / MySQL (managed or self-hosted)                     | Object storage (MinIO, GCS, Azure Blob)                         | Serverless functions (Cloud Functions / Azure Functions), lightweight Airflow / cron jobs  |
| 1GB–100GB | JSON, csv (NoSQL)   | Python           | Airbyte, Fivetran, Stitch, Kafka Connect               | NoSQL (Document / Wide-Column) | MongoDB Atlas / Couchbase / Cassandra                           | Object storage + database native storage                        | Kubernetes or VM-based services, Spark on small cluster, Airbyte/Fivetran/Stitch ingestion |
| 100GB–1TB | csv, Parquet        | Python / SQL     | Airbyte, Fivetran, Kafka, cloud transfer services      | Analytical / Columnar (OLAP)   | Snowflake / BigQuery / Databricks SQL / ClickHouse              | Data lake on object storage (Parquet on GCS/Azure/MinIO)        | Apache Spark (Databricks or self-managed), dbt, Airflow orchestration                      |
| 10TB+     | Parquet, graph data | Python / SQL /Cipher    | Kafka, Debezium (CDC), cloud-native streaming services | Graph + Lakehouse / Analytical | Neo4j Aura (Graph), Snowflake / BigQuery / Databricks Lakehouse | Lakehouse (Parquet + Iceberg/Delta Lake/Hudi) on object storage | Large Spark / Trino / Presto clusters, Databricks, Kubernetes-based processing             |

