---
title: "Update Knowledge Base"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/update-knowledge-base"
---

Call this interface to update the knowledge base information, including description, scheduling information, etc.

# Interface description

* Interface name: update_kb_update_post

* Interface address:/kb/update

* Request method: POST

# Request parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|kb_id |Number |Yes |Knowledge Base ID |
|name |String |Yes |Knowledge Base Name (1\-128 characters) |
|description |String |No |Knowledge Base Description |
|schedule_config |Object |No |Scheduling configuration, see **schedule_config** table below |

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
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Error |No |Update successfully returns null |
