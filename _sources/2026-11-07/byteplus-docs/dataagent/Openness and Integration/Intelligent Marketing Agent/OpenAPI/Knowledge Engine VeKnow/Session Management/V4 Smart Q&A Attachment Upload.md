---
title: "V4 Smart Q&A Attachment Upload"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/v4-smart-q-a-attachment-upload"
---

Call this interface to upload the temporary analysis attachment used by V4 intelligent Q & A, and return the attachment information that can be referenced in the Q & A message.

# Interface description

* Interface name: upload_storage_file_v4_conversation_v4_storage_upload_post

* Interface address:/conversation/v4/storage/upload

* Request method: POST

# Request parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|file |String |Yes |Upload file |
|visibility |String |No |Upload target: private bucket, public bucket |
|namespace |String |No |business namespace |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |business status code |
|msg |String |No |business status description |
|data |Object |No |The interface returns data. See the **data** table below for details |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|id |String |No |File ID |
|file_name |String |No |file name |
|object_key |String |No |Object Storage Key |
|storage_url |String |No |access address |
|visibility |String |No |file visibility<br><br><br>* private<br><br>* public |
|file_size |Number |No |File size in bytes |
|content_type |String |No |file type |
|attach_file |Object |No |Annex information, see **attach_file** table below |

## attach_file

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|id |String |No |accessory identification |
|name |String |No |Attachment name |
|object_key |String |No |Object Storage Key |
|type |String |No |Attachment type |
|storage_url |String |No |file access address |
|url |String |No |file access address |
|source_type |String |No |Attachment source type; url if access address exists |
|visibility |String |No |file visibility<br><br><br>* private<br><br>* public |
|file_size |Number |No |File size in bytes |
