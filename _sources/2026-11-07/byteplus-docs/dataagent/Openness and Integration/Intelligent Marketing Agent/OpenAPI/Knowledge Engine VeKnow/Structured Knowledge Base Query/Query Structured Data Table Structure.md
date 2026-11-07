---
title: "Query Structured Data Table Structure"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/query-structured-data-table-structure"
---

Calling this interface queries the logical fields, filter/vector/return capabilities, and OpenSearch index ready status without exposing the underlying mapping.

* Caller: Open API application, external agent, or integration service.

* Precondition: The caller has access to the knowledge base.

# Interface description

* Interface name: get_schema_structured_knowledge_v1_kbs__kb_id__assets__asset_id__schema_get

* Interface address:/structured_knowledge/v1/kbs/{kb_id}/assets/{asset_id}/schema

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
|data |Object |Yes |Data. See the **data** table below for details |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|asset_id |String |Yes |Structured Data Asset ID |
|index_ready |Boolean |Yes |Whether the OpenSearch index has been created and can be queried |
|fields |Array |No |Logical field configuration currently in effect. See the **fields** table below for details |
|field_capabilities |Array |No |The front end or caller can be used to construct a capability view of filter, vector, and return field candidates. See **field_capabilities** table below for details |
|operation_task_ref |String |No |Asynchronous task references triggered by schema changes, such as vector backfill tasks |

## fields

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|source_column_name |String |No |Original field/column name; user\-added field is empty |
|field_name |String |Yes |After importing the field name, as the product semantic field key |
|display_name |String |Yes |field presentation name |
|data_type |String |Yes |data type<br><br><br>* string<br><br>* int<br><br>* long<br><br>* float<br><br>* bool<br><br>* datetime |
|enabled |Boolean |No |Whether to enable and participate in recall/display candidates |
|vector_enabled |Boolean |No |Whether to enable vector indexing |
|filter_enabled |Boolean |No |Is it allowed as a filter condition? |
|return_enabled |Boolean |No |Is it allowed as a return field? |
|description |String |No |Field description |
|allowed_operators |Array |No |Allowed filtering operators; default by type if not passed<br><br><br>* eq<br><br>* ne<br><br>* gt<br><br>* ge<br><br>* lt<br><br>* le<br><br>* between<br><br>* is_null<br><br>* is_not_null<br><br>* contains<br><br>* not_contains<br><br>* in<br><br>* not_in |

## field_capabilities

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|field_name |String |Yes |Logical field name, used when calling filtering, vector retrieval, and returning fields |
|display_name |String |Yes |field presentation name |
|data_type |String |No |data type<br><br><br>* string<br><br>* int<br><br>* long<br><br>* float<br><br>* bool<br><br>* datetime |
|enabled |Boolean |No |Is the field currently enabled? |
|filter_enabled |Boolean |No |Is the field allowed as an exact filter condition? |
|vector_enabled |Boolean |No |Has the user turned on vector indexing for this field? |
|vector_status |String |No |* DISABLED<br><br>* PENDING<br><br>* PROCESSING<br><br>* READY<br><br>* FAILED |
|vector_searchable |Boolean |No |Whether the field currently has vector retrieval capabilities, only true when the vector is built |
|return_enabled |Boolean |No |Is the field allowed to appear in the recall return field? |
|supported_operators |Array |No |List of filter operators supported by this field data type<br><br><br>* eq<br><br>* ne<br><br>* gt<br><br>* ge<br><br>* lt<br><br>* le<br><br>* between<br><br>* is_null<br><br>* is_not_null<br><br>* contains<br><br>* not_contains<br><br>* in<br><br>* not_in |
