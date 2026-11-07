---
title: "Query Field Enumeration Value Sample"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/query-field-enumeration-value-sample"
---

Call this interface to query the enumeration sample and the number of occurrences of the specified logical field for filter condition value selection.

* Caller: Open API application, external agent, or integration service.

* Prerequisites: The caller has access to the knowledge base and the asset index is ready.

# Interface description

* Interface name: list_field_values_structured_knowledge_v1_kbs__kb_id__assets__asset_id__fields__field_name__values_get

* Interface address:/structured_knowledge/v1/kbs/{kb_id}/assets/{asset_id}/fields/{field_name}/values

* Request method: GET

# Request parameters

## Path

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|kb_id |String |Yes |Structured Knowledge Base ID, returned by the Create Knowledge Base or Query Knowledge Base List interface |
|asset_id |String |Yes |Structured data asset ID, returned by the Create Asset or Query Asset List interface |
|field_name |String |Yes |Logical field name of the enumeration sample to aggregate |

## Query

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|keyword |String |No |Enumeration value fuzzy search keyword, up to 200 characters |
|size |Number |No |The maximum number of enumeration examples returned, ranging from 1 to 100 |

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
|items |Array |No |Field enumeration sample and its occurrences. See the **items** table below for details |

## items

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|value |String |Yes |Field enumeration sample value |
|count |Number |No |The number of occurrences of the sample value in the current asset |
