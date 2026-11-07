---
title: "Query Folder List"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/query-folder-list"
---

Call this interface to obtain a list of all folders under the specified knowledge base and return it in a tree structure.

# Interface description

* Interface name: list_folder_document_folder_list_get

* Interface address:/document/folder/list

* Request method: GET

# **Request parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|kb_id |Number |Yes |Knowledge base ID (query parameters) |

# **Response parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Array |No |Folder tree list, see the **data** table below for details |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|folder_id |Number |Yes |Folder ID (root node is 0) |
|folder_name |String |Yes |Folder name (root node is the name of the knowledge base) |
|children |Array |Yes |List of child folders (recursive structure, each element structure is the same as the parent) |
|permission_meta |Object |No |Authority information, see **permission_meta** table below |

## permission_meta

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|content_visible |Boolean |No |Whether there is permission to the folder content; false means only return as a path node |
|actions |Array |No |The current user's valid permissions to the folder |
|max_action |String |No |The highest permissions for the current folder |
|source |String |No |Highest source of authority:<br><br><br>* DIRECT: Direct grant<br><br>* INHERITED: Inherited acquisition |
