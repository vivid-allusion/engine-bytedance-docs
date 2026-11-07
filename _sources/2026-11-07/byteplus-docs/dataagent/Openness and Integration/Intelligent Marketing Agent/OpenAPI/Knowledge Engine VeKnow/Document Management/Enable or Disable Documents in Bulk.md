---
title: "Enable or Disable Documents in Bulk"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/enable-or-disable-documents-in-bulk"
---

Call this interface to enable or disable documents in batches, and also support enabling or disabling chunks under the specified document. Before calling the current interface, you can first call [Query Document](https://docs.byteplus.com/docs/dataagent/query-document) to obtain the document to be operated.

# Interface description

* Interface name: batch_enable_document_batch_enable_post

* Interface address:/document/batch_enable

* Request method: POST

# **Request parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|doc_ids |Array |No |Document ID List |
|chunk_ids |Array |No |block ID list |
|doc_id |Number |No |The document ID to which the block belongs (required when operating the block) |
|is_enabled |Boolean |Yes |Whether to enable<br><br><br>* True means enabled<br><br>* False means disabled |

# **Response parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |String |Yes |Batch operation results, see the **data** table below for details |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|success_ids |Array |Yes |Success ID List |
|failed_ids |Array |Yes |list of failed IDs |
|invalid_ids |Array |Yes |list of invalid IDs |
|errors |Array |No |Error message list |
