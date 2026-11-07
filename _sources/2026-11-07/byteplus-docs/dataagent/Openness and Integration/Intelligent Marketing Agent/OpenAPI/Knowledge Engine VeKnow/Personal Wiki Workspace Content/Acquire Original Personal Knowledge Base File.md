---
title: "Acquire Original Personal Knowledge Base File"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/acquire-original-personal-knowledge-base-file"
---

Call this interface to obtain the original download address of the current user's personal knowledge base document; the Lark document returns the Lark original address.

# Interface description

* Interface name: get_document_source_download_knowledge_spaces_documents_source_download_get

* Interface address:/knowledge\-spaces/documents/source/download

* Request method: GET

# Request parameters

## Query

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|document_id |Number |Yes |Document ID |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Object |Yes |Data, see the **data** table below for details |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|document_id |Number |Yes |Personal Knowledge Base Document ID |
|file_name |String |Yes |original title |
|file_type |String |Yes |Original file type |
|size |Number |Yes |Original file size in bytes |
|download_url |String |Yes |The original download address; whether the signature and valid period depend on the storage backend |
|expires_at |Number |Yes |Expiration time for server level calculations, Unix millisecond timestamp; actual failure behavior depends on the storage backend |
