---
title: "Delete Document"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/delete-document"
---

Call this interface to delete the specified document and its associated Chunk data according to the document ID.

# Interface description

* Interface name: rm_document_rm__document_id__post

* Interface address:/document/rm/

* Request method: POST

# Request parameters

|Parameter name |Type |Is it necessary to pass on? |Parameter example |Description |
|---|---|---|---|---|
|document_id |String |Yes |1 |Document ID (path parameter) |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Parameter example |Description |
|---|---|---|---|---|
|code |Number |Yes |0 |Response code: 0 = success, non\-0 = failure |
|msg |String |No |"success" |Code is not 0, error message is returned |
|message |String |No |"success" |error message |
|data |Boolean |No |true |Delete successfully returns true |
