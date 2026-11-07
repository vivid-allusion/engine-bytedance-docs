---
title: "Batch Deletion of Documents"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/batch-deletion-of-documents"
---

Call this interface to delete documents and their associated Chunk data in batches according to the document ID.

# Interface description

* Interface name: rm_list_document_rm_list_post

* Interface address:/document/rm_list

* Request method: POST

# **Request parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|document_ids |Array |Yes |List of document IDs to be deleted |

# **Response parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Error |Yes |Batch operation data, see the **data** table below for details |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|success_ids |Array |Yes |Success ID List |
|failed_ids |Array |Yes |list of failed IDs |
|invalid_ids |Array |Yes |list of invalid IDs |
|errors |Array |No |Error message list |
