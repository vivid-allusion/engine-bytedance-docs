---
title: "Upload File"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/upload-file"
---

Call this interface to upload files to the knowledge base system, support a variety of file formats, and return file meta information. After calling the current interface, the file has not yet started parsing, and must continue to call [File Associate with Knowledge Base](https://docs.byteplus.com/docs/dataagent/file-associate-with-knowledge-base) to complete the file association knowledge base and parsing parameter configuration.

# Interface description

* Interface name: upload_file_upload_post

* Interface address: /file/upload

* Request method: POST

# Request parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|files |Array |Yes |List of files to be uploaded |

# **Response parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Array |No |File data, see the **data** table below for details |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|create_time |Number |No |Create timestamp |
|create_date |String |No |creation time |
|update_time |Number |No |Update timestamp |
|update_date |String |No |update time |
|id |Number |No |Document ID |
|parent_id |Number |No |Parent ID |
|tenant_id |Number |No |Tenant ID |
|created_by |String |No |creator |
|type |String |No |file type |
|name |String |Yes |file name |
|location |String |No |File storage location |
|size |Number |No |file size |
|url |String |No |Download address |
|success |Boolean |No |Was it successful? |
|message |String |No |result message |
