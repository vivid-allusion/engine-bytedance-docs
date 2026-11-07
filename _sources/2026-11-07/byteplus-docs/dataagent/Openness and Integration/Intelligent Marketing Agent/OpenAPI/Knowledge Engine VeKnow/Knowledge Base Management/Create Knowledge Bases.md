---
title: "Create Knowledge Bases"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/create-knowledge-bases"
---

Call this interface to create a new knowledge base.

# Interface description

* Interface name: create_kb_create_post

* Interface address:/kb/create

* Request method: POST

# Request parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|name |String |Yes |Knowledge Base Name (1\-128 characters) |
|description |String |No |Knowledge Base Description |
|llm_id |String |No |Embedded Model ID |
|type |String |No |Knowledge base modal types: normal, vision, default "normal" |
|content_type |String |No |Type of knowledge: general, report, financial, QA, term, cache, vecdp, proxy, default "general" |
|category |String |No |Knowledge base type: general |
|subject_id |Number |No |Theme ID, default 0 |
|schedule_config |Object |No |Scheduling configuration, see below for details<br><br>**schedule_config** table |
|tenant_ids |Array |No |Tenant ID List |
|system_created |Boolean |No |Is the knowledge base created by the system? |

## schedule_config

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|schedule_type |Number |No |Scheduling type: 0 (no update required), 1 (regular update), default 0 |
|frequency |String |No |Frequency: daily, weekly, monthly |
|time_setting |String |No |Time setting (HH: mm format) |
|day_of_week |Array |No |Day of the week (0 = Monday, 6 = Sunday) |
|day_of_month |Array |No |What day of the month (0 = 1) |
|bdb_task_id |Number |No |BDB Task ID |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |Yes |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Number |Yes |Created Knowledge Base ID |
