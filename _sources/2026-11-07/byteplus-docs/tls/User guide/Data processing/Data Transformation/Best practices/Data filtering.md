---
title: "Data filtering"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/data_filtering"
---

Data filtering is a common operation in data cleansing. You can use the data transformation feature of Torch Log Service (TLS) to filter log data stored in a topic by row or field. This topic describes typical examples of field filtering and log filtering.

<span id="字段过滤"></span>
### Field filtering

The following example displays how to filter redundant fields after key\-value extraction. After key\-value extraction is performed on the URI content field, the content field is split into multiple subfields. The content field is no longer used. It is recommended to filter out this field in the log data to prevent downstream systems from storing the redundant field.

<span id="原始日志"></span>
#### Logs

```json
[
    {
        "content":"Method=CreateTask&TaskName=MyTask&TaskType=1&Enable=true&StartTime=1672057815"
    },
    {
        "content":"Method=ModifyTask&TaskID=1234&Enable=false"
    },
    {
        "content":"Method=DeleteTask&TaskID=1236"
    }
]
```


<span id="dsl-加工规则"></span>
#### Domain Specification Language (DSL) transformation rules

```python
# Split the content field by key-value pair.
ext_kv("content", pair_sep="&", kv_sep="=", prefix="", suffix="", mode="overwrite")
# Delete the content field.
f_drop("content")
```


<span id="加工结果"></span>
#### Transformation results

```json
[
    {
        "Method": "CreateTask",
        "TaskName": "MyTask",
        "TaskType": "1",
        "Enable": "true",
        "StartTime": "1672057815"
    },
    {
        "Method": "ModifyTask",
        "TaskID": "1234",
        "Enable": "false"
    },
    {
        "Method": "DeleteTask",
        "TaskID": "1236"
    }
]
```


<span id="日志过滤"></span>
### Log filtering

The following example displays how to delete logs of which the log\-level field is DEBUG. In general, you can delete logs with a log level of DEBUG and retain logs with a log level of INFO or higher for a long period because DEBUG logs require little attention. If you delete the logs, you can prevent unnecessary logs from occupying storage resources for a long period.

<span id="原始日志"></span>
#### Logs

```json
[
    {
        "log-level":"DEBUG",
        "msg": "This is a debug msg，line 1",
    },
    {
        "log-level":"DEBUG",
        "msg": "This is a debug msg，line 2",
    },
    {
        "log-level":"INFO",
        "msg": "This is a info msg，line 3",
    }
]
```


<span id="dsl-加工规则"></span>
#### Domain Specification Language (DSL) transformation rules

```python
# Discard logs of which the log-level field is DEBUG.
c_if(op_eq(v("log-level"), "DEBUG"), e_drop())
```


<span id="加工结果"></span>
#### Transformation results

```json
[
    {
        "log-level":"INFO",
        "msg": "This is a info msg，line 3",
    }
]
```
