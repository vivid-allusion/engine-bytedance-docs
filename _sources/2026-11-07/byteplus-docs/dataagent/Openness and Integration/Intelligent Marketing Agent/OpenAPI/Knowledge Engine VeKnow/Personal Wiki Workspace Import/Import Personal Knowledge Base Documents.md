---
title: "Import Personal Knowledge Base Documents"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/import-personal-knowledge-base-documents"
---

Call this interface to upload files to the current application Token bound user's personal knowledge base, and use the server level fixed parsing configuration to submit parsing tasks.

# Interface description

* Interface name: import_local_document_knowledge_spaces_documents_import_post

* Interface address:/knowledge\-spaces/documents/import

* Request method: POST

# Request parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|file |String |Yes |file |
|parent_id |Number |No |Current directory ID; do not pass or pass 0 to indicate the root directory of the personal knowledge base |

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
|items |Array |No |Personal space import results for Mainboard have been successfully submitted. Import commit results. See the **items** table below for details |

## items

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|task_no |String |Yes |Mainboard submission logo |
|file_id |Number |No |file ID |
|document_id |Number |No |document identification |
