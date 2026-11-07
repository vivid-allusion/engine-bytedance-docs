---
title: "Query Structured Data Rows"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/query-structured-data-rows"
---

Invoke this interface to query structured data rows by keywords, sorting and paging conditions.

* Caller: Open API application, external agent, or integration service.

* Prerequisites: The caller has access to the knowledge base and the asset index is ready.

# Interface description

* Interface name: list_rows_structured_knowledge_v1_kbs__kb_id__assets__asset_id__rows_get

* Interface address:/structured_knowledge/v1/kbs/{kb_id}/assets/{asset_id}/rows

* Request method: GET

# Request parameters

## Path

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|kb_id |String |Yes |Structured Knowledge Base ID, returned by the Create Knowledge Base or Query Knowledge Base List interface |
|asset_id |String |Yes |Structured data asset ID, returned by the Create Asset or Query Asset List interface |

## Query

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|keyword |String |No |Keywords across searchable text fields, up to 200 characters |
|page |Number |No |Page numbers, starting at 1 |
|page_size |Number |No |Number of pages, range 1 to 100 |
|sort_field |String |No |Logical field names used for sorting; use OpenSearch default order when not passed |
|sort_order |String |No |Sort direction: asc ascending, desc descending |
|cursor |String |No |Previous next_cursor returned; must be used when deep paging |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Object |No |Data. See the **data** table below for details |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|items |Array |No |The data row for the current page. See the **items** table below for details |
|total |Number |No |Total number of rows that meet the query criteria |
|page |Number |No |Current page number, starting from 1 |
|page_size |Number |No |number of returns per page |
|next_cursor |String |No |Next page cursor; passed in cursor as is when continuing the query |
|has_more |Boolean |No |Is there a next page? |
|status |String |Yes |state<br><br><br>* DRAFT<br><br>* READY_PENDING_IMPORT<br><br>* READY<br><br>* DISABLED<br><br>* DELETED<br><br>* CREATE_FAILED<br><br>* IMPORTING<br><br>* IMPORT_FAILED<br><br>* DELETING<br><br>* DELETE_FAILED |

## items

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|row_key |String |Yes |row stable unique identifier |
|values |Object |No |Row contents organized by logical field names |
