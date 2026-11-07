---
title: "Upload Structured File"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/upload-structured-file"
---

Call this interface to upload a CSV or Excel file, and return the file_id used for subsequent asset creation and import.

* Caller: Open API application, external agent, or integration service.

* Precondition: The caller has editing privileges on the target knowledge base.

# Interface description

* Interface name: upload_structured_file_structured_knowledge_v1_files_post

* Interface address:/structured_knowledge/v1/files

* Request method: POST

# Request parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|file |String |Yes |CSV or Excel files to be uploaded; file size and format limits are governed by structured knowledge base upload rules |
|kb_id |String |Yes |Target structured knowledge base ID for permission checksum file attribution |
|source_type |String |Yes |file type<br><br><br>* EXCEL<br><br>* CSV<br><br>* CLICKHOUSE<br><br>* HIVE |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Object |Yes |data |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|file_id |String |Yes |Upload file unique ID, create assets and write source_config when importing file_id |
|file_name |String |Yes |original file name |
|source_type |String |Yes |file type<br><br><br>* EXCEL<br><br>* CSV<br><br>* CLICKHOUSE<br><br>* HIVE |
|file_size |Number |No |File size, in bytes |
|sheets |Array |No |Optional sheet list; CSV returns default |
|upload_status |String |No |file upload status |
