---
title: "Label the Document"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/label-the-document"
---

Call this interface to add a label to the specified document.

# Interface description

* Interface name: attach_label_permission_attach_label_post

* Interface address:/permission/attach_label

* Request method: POST

# **Request parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|document_id |Number or Array <<br><br>Number\> |Yes |Document ID |
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
