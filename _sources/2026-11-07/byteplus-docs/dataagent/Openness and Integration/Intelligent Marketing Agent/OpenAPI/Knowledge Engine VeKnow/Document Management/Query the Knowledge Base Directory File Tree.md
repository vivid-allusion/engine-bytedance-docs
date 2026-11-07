---
title: "Query the Knowledge Base Directory File Tree"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/query-the-knowledge-base-directory-file-tree"
---

Call this interface to obtain the knowledge base directory and file tree visible to the current user, and support name and keyword filtering.

# Interface description

* Interface name: get_document_tree_document_tree_get

* Interface address:/document/tree

* Request method: GET

# Request parameters

## Query

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|kb_id |Number |Yes |Knowledge Base ID |
|keywords |String |No |Directory or file name keywords |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Array |Yes |Data, see the **data** table below for details |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|id |Number |Yes |Resource ID |
|parent_id |Number |No |Parent ID |
|name |String |Yes |Node name |
|resource_type |String |Yes |Resource type: knowledge_folder or document |
|is_folder |Boolean |Yes |Is it a folder node? |
|file_type |String |No |file extension type |
|size |Number |No |file size |
|run |String |No |file running status |
|progress |Number |No |File processing progress |
|is_enabled |Boolean |No |Is the file enabled? |
|children |Array |No |Subdirectories and files, if any, recursively loop **data** subparameters |
