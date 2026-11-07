---
title: "New Label"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/new-label"
---

Call this interface to create a new document/knowledge base label.

# Interface description

* Interface name: add_label_permission_add_label_post

* Interface address:/permission/add_label

* Request method: POST

# **Request parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|label_name |String |Yes |label name |
|label_type |String |Yes |document tag type<br><br><br>* multiple_value_text<br><br>* single_value_text |
|label_values |Array < String \> or Array < Object \> |Yes |Label value, separated by ',', data type is<br><br>Array < String \>; In addition, support Array < Object \> type, add LabelValue, parameter description see the following **label_values** table |
|kb_id |Number |No |Knowledge Base ID |
|description |String |No |describe |
|prompt_version |String |No |Cue word version |

## label_values

* **Situation 1:**  String array, pass in label value

* **Situation 2:**  Object array, add LabelValue, parameter description is as follows

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|name |String |Yes |label value name |
|description |String |No |label value description |

# **Response parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |String |No |data |
