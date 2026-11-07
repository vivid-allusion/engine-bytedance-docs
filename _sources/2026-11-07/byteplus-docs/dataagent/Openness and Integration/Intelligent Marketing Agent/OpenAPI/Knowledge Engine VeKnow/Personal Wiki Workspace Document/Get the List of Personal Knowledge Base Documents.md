---
title: "Get the List of Personal Knowledge Base Documents"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/get-the-list-of-personal-knowledge-base-documents"
---

Call this interface to query the personal knowledge base document imported by the current application Token binding user, and the result does not include a folder.

# Interface description

* Interface name: list_personal_documents_knowledge_spaces_documents_list_post

* Interface address:/knowledge\-spaces/documents/list

* Request method: POST

# Request parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|cursor |Number |No |Previous Last document ID |
|page_size |Number |No |Number of documents per page |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Object |Yes |Data, see the **data** table below for details |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|items |Array |No |Open API tiled document list; does not return directory tree, object store internal address, or Mainboard identifier |
|next_cursor |Number |No |Next page cursor; empty means no next page |
