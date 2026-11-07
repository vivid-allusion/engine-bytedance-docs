---
title: "Move Documents or Folders"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/move-documents-or-folders"
---

Calling this interface moves the specified document or folder to the target parent folder. Before invoking the current interface, you can call [Query Folder List](https://docs.byteplus.com/docs/dataagent/query-folder-list) to get optional destination folder.

# Interface description

* Interface name: move_document_document_move_post

* Interface address:/document/move

* Request method: POST

# **Request parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|doc_id |Number |Yes |Document or Folder ID |
|parent_id |Number |Yes |Target parent folder ID, 0 means root directory, when 0 means move to knowledge base root directory |

# **Response parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Boolean |No |Move successfully returns true |
