---
title: "Acquire Personal Knowledge Base Markdown"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/acquire-personal-knowledge-base-markdown"
---

Call this interface to get the readable Markdown address of the current user's personal knowledge base document; return the empty address when the product is not ready.

# Interface description

* Interface name: get_document_content_knowledge_spaces_documents_content_get_get

* Interface address:/knowledge\-spaces/documents/content/get

* Request method: GET

# Request parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|document_id |Number |Yes |Personal Knowledge Base Document ID |

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
|content_type |String |Yes |Content MIME type, default text/markdown |
|content_url |String |Yes |Markdown the signature download address of the product; returns an empty string when the product is unavailable |
|expires_at |Number |Yes |The expiration time of the download address, Unix timestamp, in milliseconds; returns 0 when the product is unavailable. |
|version |Number |Yes |Content version identifier; use build or document timestamp without version number, minimum 1 |
