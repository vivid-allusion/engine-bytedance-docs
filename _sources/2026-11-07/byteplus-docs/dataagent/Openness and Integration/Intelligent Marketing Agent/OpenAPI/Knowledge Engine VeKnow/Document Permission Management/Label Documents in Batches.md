---
title: "Label Documents in Batches"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/label-documents-in-batches"
---

Call this interface to bind labels for multiple documents in batches and return the processing results of each document. Before calling this interface, you should create a label by calling [New Label](https://docs.byteplus.com/docs/dataagent/new-label).

# Interface description

* Interface name: attach_label_with_docs_permission_attach_label_with_docs_post

* Request method: POST

* Interface address:/permission/attach_label_with_docs

# **Request parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|document_id |Number or Array < Number \> |Yes |Document ID, supports single incoming ( `Number`type), supports batch incoming ( `Array < Number >`type) |
|labels |Array |Yes |Label ID and Label Value ID, see **labels** table below |
|overwrite |Boolean |No |Whether to overwrite existing labels |

## labels

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|label_id |Number |Yes |Tag ID |
|label_name |String |No |label name |
|label_value_ids |Array < Number \> or Array < Object \> |Yes |Label values, see **label_value_ids** table for details |

## label_value_ids

* **Situation 1** : Array < Number \> type, pass in tag value.

* **Situation 2** : Array < Object \> type, containing parameters as shown in the table below.

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|label_value_id |Number |Yes |tag value ID |
|label_value_builder |String |No |Label Value Builder |

# **Response parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |String |No |data |
