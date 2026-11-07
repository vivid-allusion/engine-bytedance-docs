---
title: "Query the List of Structured Knowledge Bases"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/query-the-list-of-structured-knowledge-bases"
---

Call this interface by name keyword and status page query the current caller has access to the structured knowledge base.

* Caller: Open API application, external agent, or integration service.

* Prerequisites: Use Authorization to complete authentication.

# Interface description

* Interface name: list_kbs_structured_knowledge_v1_kbs_get

* Interface address:/structured_knowledge/v1/kbs

* Request method: GET

# Request parameters

## Query

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|kw |String |No |Knowledge base name fuzzy search keyword |
|status |String |No |Knowledge base status filters, such as ACTIVE or DISABLED |
|page |Number |No |Page numbers, starting at 1 |
|page_size |Number |No |Number of pages, range 1 to 100 |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Object |Yes |Data. See the **data** table below for details |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|items |Array |No |A list of structured knowledge bases for the current page. See the **items** table below for details |
|total |Number |No |Total number of knowledge bases that meet the query conditions |
|page |Number |No |Current page number, starting from 1 |
|page_size |Number |No |number of returns per page |

## items

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|kb_id |String |Yes |Structured Knowledge Base Unique ID |
|name |String |Yes |Structured Knowledge Base Name |
|description |String |No |Structured Knowledge Base Business Description |
|status |String |Yes |Knowledge base status, such as ACTIVE, DISABLED, or DELETED |
|asset_count |Number |No |Number of undeleted data assets in the knowledge base |
|total_row_count |Number |No |Total number of rows for all undeleted assets in the knowledge base |
|created_by |String |No |creator account |
|create_time |Number |No |Creation time, Unix millisecond timestamp |
|update_time |Number |No |Last updated time, Unix millisecond timestamp |
