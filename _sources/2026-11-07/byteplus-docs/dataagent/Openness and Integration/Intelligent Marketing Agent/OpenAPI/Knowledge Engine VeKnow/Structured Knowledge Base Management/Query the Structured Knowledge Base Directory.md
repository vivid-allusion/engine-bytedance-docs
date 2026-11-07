---
title: "Query the Structured Knowledge Base Directory"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/query-the-structured-knowledge-base-directory"
---

Call this interface to query the structured knowledge base directory tree, and return the root directory and its subdirectories with the same name as the knowledge base.

* Caller: Open API application, external agent, or integration service.

* Precondition: The caller has access to the knowledge base.

# Interface description

* Interface name: list_folders_structured_knowledge_v1_kbs__kb_id__folders_get

* Interface address:/structured_knowledge/v1/kbs/{kb_id}/folders

* Request method: GET

# Request parameters

## Path

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|kb_id |String |Yes |Structured Knowledge Base ID, returned by the Create Knowledge Base or Query Knowledge Base List interface |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Array |Yes |Data. See the **data** table below for details |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|folder_id |String |Yes |Directory unique ID; root directory is usually 0 |
|kb_id |String |Yes |The structured knowledge base ID to which the directory belongs |
|parent_folder_id |String |No |Parent directory ID; root directory has no parent directory |
|name |String |Yes |directory name |
|status |String |No |directory status |
|asset_count |Number |No |Number of data assets directly owned by the directory |
|children |Array |No |List of subdirectories. Recursive loop **data** parameter. |
