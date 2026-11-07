---
title: "Start Parsing the Document"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/start-parsing-the-document"
---

Calling this interface triggers the document parsing task to divide the document content into chunks and index it so that it can be retrieved.

# Prerequisite

Before calling the current interface, you should complete the previous preparation step:

1. Upload file scene please call [File Associate with Knowledge Base](https://docs.byteplus.com/docs/dataagent/file-associate-with-knowledge-base) first.

2. Please call [Edit Document Configuration](https://docs.byteplus.com/docs/dataagent/edit-document-configuration) first to update the slice configuration scene.

# Interface description

* Interface name: run_document_run_post

* Interface address: /document/run

* Request method: POST

# Request parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|doc_id |Array |Yes |Document ID List |
|run |Number |Yes |running state |
|datasource_id |Number |No |Data Source ID |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Boolean |No |Parse successfully returns true |
