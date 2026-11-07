---
title: "Delete Document Version"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/delete-document-version"
---

Call this interface to delete non\-valid and non\-working document versions.

# Interface description

* Interface name: delete_document_version_document_version_delete_post

* Interface address:/document/version/delete

* Request method: POST

# Request parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|doc_id |Number |Yes |Document ID |
|id |Number |Yes |Target version record ID, get version list items.id |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Boolean |No |data |
