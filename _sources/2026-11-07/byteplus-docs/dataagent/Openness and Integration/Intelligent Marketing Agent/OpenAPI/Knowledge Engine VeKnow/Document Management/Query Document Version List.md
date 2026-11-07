---
title: "Query Document Version List"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/query-document-version-list"
---

Call this interface to query all versions of the document and its current status.

# Interface description

* Interface name: list_document_versions_document_version_list_get

* Interface address:/document/version/list

* Request method: GET

# Request parameters

## Query

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|doc_id |Number |Yes |Document ID |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Object |Yes |See the **data** table below for a list of document versions |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|doc_id |Number |Yes |Document ID |
|active_version_id |Number |No |Current version record ID |
|operation_in_progress |Boolean |Yes |Is there an ongoing version operation? |
|items |Array |No |For a list of versions, see the **items** table below |

## items

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|id |Number |Yes |Version Record ID |
|version_no |Number |No |version serial number |
|version |String |No |display version number |
|display_version |String |No |display version number |
|version_date |Number |No |Business version date (Unix milliseconds) |
|version_rule_revision |Number |No |Version number Rule revision number |
|entry_id |Number |No |Mainboard Entry ID |
|file_id |Number |No |Source file ID |
|file_name |String |No |source file name |
|document_type |String |No |document type |
|operation |String |Yes |Version generation method |
|status |String |Yes |version status |
|is_active |Boolean |Yes |Is it the current version in effect? |
|switchable |Boolean |Yes |Is it currently possible to switch to this version? |
|deletable |Boolean |No |Can it be deleted currently? |
|delete_block_reason |String |No |Reason for non\-deletion |
|created_by |String |No |founder |
|create_time |Number |No |creation time |
|update_time |Number |No |update time |
