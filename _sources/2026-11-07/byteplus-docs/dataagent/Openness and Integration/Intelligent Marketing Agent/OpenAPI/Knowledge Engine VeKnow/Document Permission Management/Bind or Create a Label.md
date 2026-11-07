---
title: "Bind or Create a Label"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/bind-or-create-a-label"
---

Call this interface to bind the label for the specified document; when the label value does not exist, the label value can be created according to the requested content and then bound. You can call [New Label](https://docs.byteplus.com/docs/dataagent/new-label) first to create labels, or you can call [Label the Document](https://docs.byteplus.com/docs/dataagent/label-the-document) to execute only existing label bindings.

# Interface description

* Interface name: attach_or_create_label_permission_attach_or_create_label_post

* Interface address:/permission/attach_or_create_label

* Request method: POST

# **Request parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|document_id |Number or Array < Number \> |Yes |Document ID, supports single incoming ( `Number`type), supports batch incoming ( `Array < Number >`type) |
|labels |Array |Yes |Label ID and Label Value ID, see **labels** table below |

## labels

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|label_name |String |No |label name |
|label_type |String |Yes |document tag type<br><br><br>* multiple_value_text<br><br>* single_value_text |
|label_values |Array |Yes |List of label values. If it is a single\-value label, please ensure that the length of the list is 1. |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |String |No |data |
