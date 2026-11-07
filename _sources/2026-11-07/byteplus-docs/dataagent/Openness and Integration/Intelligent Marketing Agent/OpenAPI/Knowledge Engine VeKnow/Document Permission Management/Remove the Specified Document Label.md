---
title: "Remove the Specified Document Label"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/remove-the-specified-document-label"
---

Calling this interface removes the specified label value from the specified document. The caller requires tenant administrator privileges.

# Interface description

* Interface name: remove_document_label_permission_document_label_remove_post

* Interface address:/permission/document_label/remove

* Request method: POST

# **Request parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|document_id |Number |Yes |Document ID |
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
|data |String |No |data |
