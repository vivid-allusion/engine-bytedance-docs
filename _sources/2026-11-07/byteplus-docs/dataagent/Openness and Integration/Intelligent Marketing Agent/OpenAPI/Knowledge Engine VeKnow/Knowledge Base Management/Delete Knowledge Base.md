---
title: "Delete Knowledge Base"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/delete-knowledge-base"
---

Call this interface to delete the specified knowledge base.

# Interface description

* Interface name: rm_kb_rm__kb_id__delete

* Interface address:/kb/rm/

* Request method: DELETE

# **Request parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|kb_id |Number |Yes |Knowledge base ID (path parameter) |

# **Response parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Error |No |data |
