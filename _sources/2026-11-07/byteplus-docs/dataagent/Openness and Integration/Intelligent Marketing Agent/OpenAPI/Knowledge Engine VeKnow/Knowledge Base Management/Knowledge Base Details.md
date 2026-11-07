---
title: "Knowledge Base Details"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/knowledge-base-details"
---

Call this interface to obtain knowledge base details, including ID, operation time, description, type, creator, and scheduling configuration.

# Interface description

* Interface name: detail_kb_detail_get

* Interface address:/kb/detail

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
|data |Object |Yes |Knowledge base details, detailed parameter description see the following **data** table |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|create_time |Number |No |Create timestamp |
|create_date |String |No |creation time |
|update_time |Number |No |Update timestamp |
|update_date |String |No |update time |
|id |Number |Yes |Knowledge Base ID |
|avatar |String |No |Avatar base64 string |
|tenant_id |Number |Yes |Tenant ID |
|name |String |Yes |Knowledge base name |
|language |String |No |locale |
|description |String |No |Knowledge Base Description |
|type |String |No |knowledge base modal type<br><br><br>* normal<br><br>* vision |
|category |String |No |Knowledge base category<br><br><br>* general<br><br>* subject |
|content_type |String |Yes |Knowledge content type |
|subject_id |Number |No |principal ID |
|embd_id |String |No |Default embed model ID |
|permission |String |No |Permission type (me |
|created_by |String |Yes |creator |
|doc_num |Number |Yes |number of documents |
|token_num |Number |Yes |number of tokens |
|chunk_num |Number |Yes |number of blocks |
|similarity_threshold |Number |Yes |similarity threshold |
|vector_similarity_weight |Number |Yes |vector similarity weight |
|parser_id |String |Yes |Default parser ID |
|parser_config |Object |No |Parser Configuration |
|status |String |Yes |Whether it is valid (0: obsolete, 1: valid) |
|actions |Array |No |operation permission list |
|schedule_config |Object |No |Scheduling configuration, see **schedule_config** table below |
|llm_id |String |No |Large Language Model ID |
|default_doc_id |Number |No |Default Virtual Document ID |
|auto_labels |Array |No |Automatically generated list of tag IDs |
|default_doc_state |String |No |Default document state |
|warnings |Array |No |Machine\-readable warning messages |

## schedule_config

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|schedule_type |Number |No |Scheduling type: 0 (no update required), 1 (regular update), default 0 |
|frequency |String |No |Frequency: daily, weekly, monthly |
|time_setting |String |No |Time setting (HH: mm format) |
|day_of_week |Array |No |Day of the week (0 = Monday, 6 = Sunday) |
|day_of_month |Array |No |What day of the month (0 = 1) |
|bdb_task_id |Number |No |BDB Task ID |
