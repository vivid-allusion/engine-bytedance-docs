---
title: "Delete Folder"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/delete-folder"
---

Call this interface to delete the specified folder.

# Interface description

* Interface name: delete_folder_document_folder_delete_post

* Interface address:/document/folder/delete

* Request method: POST

# **Request parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|kb_id |Number |Yes |Knowledge Base ID |
|folder_id |Number |Yes |Folder ID |

# **Response parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |String |No |data |
