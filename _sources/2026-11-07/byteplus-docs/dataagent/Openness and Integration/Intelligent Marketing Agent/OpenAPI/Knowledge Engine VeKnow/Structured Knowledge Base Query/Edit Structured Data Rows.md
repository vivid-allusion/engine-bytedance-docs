---
title: "Edit Structured Data Rows"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/edit-structured-data-rows"
---

Call this interface to update a line of data according to the stable row_key, and keep the original value of the untransmitted field.

* Caller: Open API application, external agent, or integration service.

* Precondition: The caller has permission to edit the data asset.

# Interface description

* Interface name: update_row_structured_knowledge_v1_kbs__kb_id__assets__asset_id__rows__row_key__put

* Interface address:/structured_knowledge/v1/kbs/{kb_id}/assets/{asset_id}/rows/

* Request method: PUT

# Request parameters

## Path

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|kb_id |String |Yes |Structured Knowledge Base ID, returned by the Create Knowledge Base or Query Knowledge Base List interface |
|asset_id |String |Yes |Structured data asset ID, returned by the Create Asset or Query Asset List interface |
|row_key |String |Yes |Data row stable unique identity, by row list, import unique identity field, or write |

## Request body

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|values |Object |Yes |Partial update data organized by logical field names; undelivered fields remain unchanged |

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
|row_key |String |Yes |row stable unique identifier |
|values |Object |No |Row contents organized by logical field names |
