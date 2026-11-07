---
title: "Get Document Label"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/get-document-label"
---

Call this interface to set the valid period of a single document, and you can choose to automatically delete it after expiration.

# Interface description

* Interface name: set_document_valid_date_permission_document_valid_date_post

* Interface address:/permission/document/valid_date

* Request method: POST

# **Request parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|document_id |Number or Array < Number \> |Yes |Document ID |
|valid_date |String |No |valid period |
|auto_delete |Boolean |No |Whether to expire and automatically delete |

# **Response parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |String |No |data |
