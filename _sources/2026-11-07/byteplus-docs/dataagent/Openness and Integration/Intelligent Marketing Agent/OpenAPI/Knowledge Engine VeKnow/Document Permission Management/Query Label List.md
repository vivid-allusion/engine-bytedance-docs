---
title: "Query Label List"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/query-label-list"
---

Call this interface to query the label list under the current tenant by page, and support keyword, knowledge base and automatic label filtering.

# Interface description

* Interface name: list_labels_permission_list_labels_get

* Interface address:/permission/list_labels

* Request method: GET

# **Request parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|page_number |Number |Yes |Page numbers, starting at 1 |
|page_size |Number |Yes |page size |
|keywords |String |No |keyword |
|kb_id |Number |Yes |Knowledge Base ID |
|kb_auto_labels_only |Boolean |No |Whether to return only automatic labels |

# **Response parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Object |Yes |Paging label query results, see the **data** table below for details |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|total |Number |Yes |total |
|page |Number |Yes |page number |
|page_size |Number |Yes |page size |
|items |Array |Yes |List of labels, see the **items** table below |

## items

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|create_time |Number |No |Create timestamp |
|create_date |String |No |creation time |
|update_time |Number |No |Update timestamp |
|update_date |String |No |update time |
|label_id |Number |Yes |Tag ID |
|label_name |String |No |label name |
|label_type |String |Yes |document tag type<br><br><br>* multiple_value_text<br><br>* single_value_text |
|label_values |Array |No |List of label values, see **label_values** table below |
|label_value_builder |String |No |Label Value Builder<br><br><br>* manual<br><br>* chat_model |
|prompt_version |String |No |Cue word version |
|label_usage |Number |No |tag usage |

### label_values

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|id |Number |Yes |tag value ID |
|value |String |No |label value |
|value_usage |Number |No |tag value usage |
|label_value_builder |String |No |Label Value Builder<br><br><br>* manual<br><br>* chat_model |
