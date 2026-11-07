---
title: "Remove Document Labels"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/remove-document-labels"
---

Calls this interface to remove a label from a specified document or knowledge base.

# Interface description

* Interface name: detach_labels_permission_detach_labels_post

* Interface address:/permission/detach_labels

* Request method: POST

# **Request parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|kb_ids |Array |No |Knowledge Base ID List |
|doc_ids |Array |No |Document ID List |
|labels |Array |Yes |Label ID and Label Value ID, see **labels** table below |

## labels

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|label_id |Number |Yes |Tag ID |
|label_value_ids |Array |Yes |Label value ID list |

# **Response parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Error |No |data |
