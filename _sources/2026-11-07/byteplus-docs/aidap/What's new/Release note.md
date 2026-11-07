---
title: "Release note"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/New_feature_release_notes"
---

This topic introduces the product function updates and related documentation of the AI Native BaaS for Supabase.

> **tip**

> AI Native BaaS for Supabase is in the beta stage. If you want to use it, please contact the customer manager.

## **October 2026**

|**Function name** |**Function description** |**Release date** |**Release region** |**Related document** |
|---|---|---|---|---|
|rds_ai capability enhancement |Release version 1.4 of the rds_ai extention, adding semantic summarization, semantic classification, and semantic extraction capabilities. |2026\-10\-19<br><br> |All<br><br> |[AI (rds_ai)](https://docs.byteplus.com/en/docs/aidap/rds-ai) |
|Provide delayed deletion capability |PostgreSQL engine and Supabase engine support delayed deletion feature. Workspaces can be recovered within the delay period, useful for accidental deletion recovery scenarios. |2026\-10\-19 |All<br><br> |* [Restoring delayed deleted workspace (Supabase engine)](https://docs.byteplus.com/en/docs/aidap/supabase-restore-deleted-workspace1)<br><br>* [Restoring delayed deleted workspace (PostgreSQL engine)](https://docs.byteplus.com/en/docs/aidap/postgresql-restore-deleted-workspace) |
|Support pg_textsearch full\-text index extention |Support pg_textsearch extension to provide full\-text index\-based search capabilities. |2026\-10\-19 |Asia Pacific (Johor)<br><br> |[Full-text search (pg_textsearch)](https://docs.byteplus.com/en/docs/aidap/pg_textsearch) |
|Authentication supports Custom OAuth / OIDC Providers |Enhance the Authentication capability of Supabase engine, supporting customizable OAuth/OIDC identity providers and integration with external authentication services. |2026\-10\-19 |All<br><br> |[Configuring custom identity provider login](https://docs.byteplus.com/en/docs/aidap/Configuring_custom_identity_provider_login) |
|Authentication supports Lark app verification |Support Lark authentication in Authentication of Supabase engine, allowing users to log in and verify identity through the Lark app. |2026\-10\-19 |All<br><br> |[Configuring Feishu authorized login](https://docs.byteplus.com/en/docs/aidap/Configuring_Lark_authorized_login) |
|Provide an all\-in\-one built\-in memory service |Supabase engine offers integrated memory service capabilities, supporting in\-platform memory functions. |2026\-10\-19 |All<br><br> |[Use memory service](https://docs.byteplus.com/en/docs/aidap/Using_memory_service) |

## **August 2026**

|**Function name** |**Function description** |**Release date** |**Release region** |**Related document** |
|---|---|---|---|---|
|pgvector extension enhancement |Released 0.8.2_20260715 version extension:<br><br><br>* Supports bitmap\-based pre\-filtering capability, enabling efficient hybrid search with filtering conditions under IVF index scenarios to improve query performance.<br><br>* Supports Extended RaBitQ quantization algorithms (rabitq4/rabitq8) to enhance search performance.<br><br>* Extends the upper dimension limit supported by vector indexes: SQ8 supports 8,000 dimensions, SQ16 supports 4,000 dimensions, and RaBitQ supports 64,000 dimensions to meet higher\-dimensional vector search scenarios. |2026\-08\-24 |All |[Searching based on high-dimensional vector similarity (pgvector)](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-pg_vector) |
|Enhanced rds_ai plugin capabilities |Released version 1.3 of the rds_ai extension, adding RAG, retrieve, and rank capabilities, enabling retrieval\-augmented generation directly within the database to simplify AI application development. |2026\-08\-24 |All |[AI (rds_ai)](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-rds_ai) |
|AI Gateway supports Seedance / Seedream models |AI Gateway added support for Seedance (video generation) and Seedream (image generation) models to expand AI's multimodal generation capabilities. |2026\-08\-24 |All |[Model usage](https://docs.byteplus.com/en/docs/aidap/Supabase-Model_usage) |
|Supports sandbox service environment (invitation for testing) |Add a new sandbox compute environment to provide an isolated runtime environment for application development and testing |2026\-08\-24 |All |[Sandbox service](https://docs.byteplus.com/en/docs/aidap/Sandbox_service) |
|Supports SQL throttling |Supports SQL throttling at template and keyword levels, allowing configuration of throttling rules via control plane API to ensure database stability under high load. |2026\-08\-24 |All |[SQL concurrency control](https://docs.byteplus.com/en/docs/aidap/SQL_throttling) |
|support setting the maximum number of connections via parameters |Supports configuring the maximum number of database connections through API parameters, with options to take effect on the next wake\-up or immediate restart, meeting the connection management needs of batch configuration and commercial scenarios. |2026\-08\-24 |All |[Modifying maximum connections](https://docs.byteplus.com/en/docs/aidap/Modifying_maximum_connections) |
|Support viewing and exporting third\-party operation metrics |Added new operational observability capabilities to view and export business table access, Data API call volume and details (including user logins), supporting application operations analysis. |2026\-08\-24 |All |[Observability](https://docs.byteplus.com/en/docs/aidap/Observability) |
|Supports RLS Tester |Add RLS (row\-level security policy) tester function to support testing and verifying RLS policies directly in the console, improving policy debugging efficiency. |2026\-08\-24 |All |[Enabling row-level security (RLS)](https://docs.byteplus.com/en/docs/aidap/RLS) |
|Storage supports standard S3 protocol access |Storage exposes the /v1/s3 interface, supporting object storage access services externally through the standard S3 protocol and compatible with the existing S3 ecosystem toolchains. |2026\-08\-24 |All |[Accessing storage via the S3 protocol](https://docs.byteplus.com/en/docs/aidap/Accessing_storage_via_the_S3_protocol) |
|Support for pg_jobmon extension |Add pg_jobmon (job monitoring) extension plugin for Workspaces using the PostgreSQL engine to enhance job monitoring capabilities |2026\-08\-24 |All |[Logging extensions (pg_jobmon)](https://docs.byteplus.com/en/docs/aidap/pg_jobmon) |
|Added monitoring metric for transaction rollbacks |Provides transaction rollback count metrics to help users monitor service health status in real time. |2026\-08\-24 |All |[Monitoring metrics](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Monitoring_metrics) |

## **July 2026**

|**Function name** |**Function description** |**Release date** |**Release region** |**Related document** |
|---|---|---|---|---|
|Supports DuckDB analysis acceleration capabilities |Supports executing analytical queries through the DuckDB engine, suitable for complex aggregation, multi\-table joins, and other AP analysis scenarios. Users can directly use DuckDB’s columnar vectorized execution capabilities within the existing PostgreSQL database environment to accelerate large\-scale data analysis, reducing data migration and extra ETL costs. Also supports querying data lake files (Parquet, CSV, etc.) stored in Object Storage (BytePlus TOS) directly through the pg_duckdb extension, enabling unified cross\-storage analysis without data migration. |2026\-07\-16 |All |[Managing data lake connection](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Creating_a_connection) |
|pgvector supports quantized index |Upgrade pgvector to 0.8.2, adding two types of quantization indexes: scalar quantization (SQ8/SQ16) and binary quantization (RaBitQ), as well as IVFFlat in\-filter search capability (supported only by RaBitQ). Quantization indexes significantly reduce memory usage and improve query performance with minimal accuracy loss. |2026\-07\-16 |All |[Searching based on high-dimensional vector similarity (pgvector)](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-pg_vector) |
|Supports creating vector buckets |Supports creating vector buckets and vector tables in Supabase console for storing, managing, and retrieving vector data, helping users build AI application scenarios such as semantic search and similarity matching. |2026\-07\-16 |All |[Create a vector bucket](https://docs.byteplus.com/en/docs/aidap/Creating_a_vector_bucket) |
|Provides more monitoring metrics |New monitoring metrics for workspaces using the PostgreSQL engine include CPU usage, memory usage, QPS, total database connections, transaction success rate, and average, P50, P95, and P99 request time consumption. These help users comprehensively monitor resource usage, access pressure, and request performance to promptly identify performance bottlenecks and optimize business access strategies. |2026\-07\-16 |All |[Monitoring metrics](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Monitoring_metrics) |

## **June 2026**

|**Function name** |**Function description** |**Release date** |**Release region** |**Related document** |
|---|---|---|---|---|
|Product released |RDS for PostgreSQL is released in beta stage for the first time. |2026\-06\-10 |Asia Pacific (Johor) |[What is AI Native BaaS for Supabase?](https://docs.byteplus.com/en/docs/aidap/What_is_the_AI_Native_Database_Platform) |
