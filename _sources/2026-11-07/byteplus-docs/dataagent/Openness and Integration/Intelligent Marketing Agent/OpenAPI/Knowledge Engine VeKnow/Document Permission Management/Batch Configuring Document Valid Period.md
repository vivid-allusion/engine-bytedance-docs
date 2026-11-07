---
title: "Batch Configuring Document Valid Period"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/batch-configuring-document-valid-period"
---

Call this interface to set the valid period of multiple documents in batches, and you can choose to automatically delete them after expiration.

# Interface description

* Interface name: set_docs_valid_date_permission_document_valid_date_with_docs_post

* Interface address:/permission/document/valid_date_with_docs

* Request method: POST

# **Request parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|valid_date |String |No |Valid period, format YYYY\-MM\-DD; null means clear valid period |
|auto_delete |Boolean |No |Is it automatically deleted after expiration? |
|document_id |Number or Array < Number \> |Yes |Document id, support passing in one, or passing in multiple in the form of an array |

# **Response parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Object |No |Data, see the **data** table below for details |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|success_ids |Array |Yes |Success ID List |
|failed_ids |Array |Yes |list of failed IDs |
|invalid_ids |Array |Yes |list of invalid IDs |
|errors |Array |No |Error message list |
