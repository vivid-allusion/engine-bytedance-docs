---
title: "Get Document Version Content"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/get-document-version-content"
---

Calling this interface reads the contents of the specified version of the Markdown document accessible to the current tenant doc_id and version_id.

# Interface description

* Interface name: get_document_version_content_document_version_content_get

* Interface address:/document/version/content

* Request method: GET

# Request parameters

## Query

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|doc_id |Number |Yes |Document ID |
|version_id |Number |Yes |Version Record ID |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |String |No |data |
