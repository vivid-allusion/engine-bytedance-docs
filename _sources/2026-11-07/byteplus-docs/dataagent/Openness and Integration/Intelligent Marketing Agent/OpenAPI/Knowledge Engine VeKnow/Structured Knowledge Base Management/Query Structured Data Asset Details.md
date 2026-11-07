---
title: "Query Structured Data Asset Details"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/query-structured-data-asset-details"
---

Call this interface to query the source of the specified data assets, status, file size, number of rows and recent errors and other public metadata.

* Caller: Open API application, external agent, or integration service.

* Precondition: The caller has access to the knowledge base.

# Interface description

* Interface name: get_asset_structured_knowledge_v1_kbs__kb_id__assets__asset_id__get

* Interface address:/structured_knowledge/v1/kbs/{kb_id}/assets/

* Request method: GET

# Request parameters

## Path

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|kb_id |String |Yes |Structured Knowledge Base ID, returned by the Create Knowledge Base or Query Knowledge Base List interface |
|asset_id |String |Yes |Structured data asset ID, returned by the Create Asset or Query Asset List interface |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Object |Yes |Data. See the **data** table for details. |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|asset_id |String |Yes |Structured Data Asset Unique ID |
|kb_id |String |Yes |The structured knowledge base ID to which the asset belongs |
|asset_name |String |Yes |Structured Data Asset Name |
|source_type |String |Yes |file type<br><br><br>* EXCEL<br><br>* CSV<br><br>* CLICKHOUSE<br><br>* HIVE |
|status |String |Yes |state<br><br><br>* DRAFT<br><br>* READY_PENDING_IMPORT<br><br>* READY<br><br>* DISABLED<br><br>* DELETED<br><br>* CREATE_FAILED<br><br>* IMPORTING<br><br>* IMPORT_FAILED<br><br>* DELETING<br><br>* DELETE_FAILED |
|source |Object |Yes |Source data, see the **source** table below for details |
|folder_id |String |No |Asset ownership directory ID |
|source_file_name |String |No |Original upload file name; dataset source can be empty |
|file_size |Number |No |Original file size in bytes; dataset source can be empty |
|row_count |Number |No |The number of rows of data currently written to OpenSearch |
|last_error |String |No |The reason for the last processing failure; empty when there is no failure |
|created_by |String |No |creator account |
|create_time |Number |No |Creation time, Unix millisecond timestamp |
|update_time |Number |No |Last updated time, Unix millisecond timestamp |

## source

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|source_type |String |Yes |file type<br><br><br>* EXCEL<br><br>* CSV<br><br>* CLICKHOUSE<br><br>* HIVE |
|file_id |String |No |Excel/CSV uploaded file ID |
|dataset_id |String |No |Prep Dataset ID for ClickHouse/Hive |
|dataset_name |String |No |Prep Dataset Name for ClickHouse/Hive |
|database_name |String |No |source database name |
|table_name |String |No |Source data table name |
|sheet_name |String |No |Excel worksheet name; CSV is usually the default |
