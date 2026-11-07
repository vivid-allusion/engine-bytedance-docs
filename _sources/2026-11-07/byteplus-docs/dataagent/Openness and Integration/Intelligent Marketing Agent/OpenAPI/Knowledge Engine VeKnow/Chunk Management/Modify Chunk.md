---
title: "Modify Chunk"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/modify-chunk"
---

Call this interface to modify the Chunk content of the file in the specified knowledge base, and support updating text, metadata and other information.

# Interface description

* Interface name: set_chunk_chunk_set_post

* Interface address:/chunk/set

* Request method: POST

# **Request parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|kb_id |Number |No |Knowledge Base ID |
|doc_id |Number |No |Document ID |
|chunk_id |String |Yes |slice identifier |
|question |String |No |question |
|title |Array |No |slice title hierarchy |
|content_with_weight |String |Yes |weighted text content |
|quality_id |Number |No |quality identifier |
|extra |Object |No |Additional information |

# **Response parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Boolean |No |Update successfully returns true |
