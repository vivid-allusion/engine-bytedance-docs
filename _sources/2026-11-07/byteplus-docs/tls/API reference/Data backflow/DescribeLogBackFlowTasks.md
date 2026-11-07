---
title: "DescribeLogBackFlowTasks"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/DescribeLogBackFlowTasks"
---

Use the DescribeLogBackFlowTasks API to view the list of log backflow tasks.

<span id=".6K-35rGC6K-05piO"></span>
## Request instructions


* Request method: GET

* Request URL: https://{tls\-endpoint}/DescribeLogBackFlowTasks


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists only unique request parameters for this API and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="Query"></span>
### Query


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|PageNumber |Integer |No |1 |The page number in a paginated query. The default value is 1, which means data is returned starting from the first page. |
|PageSize |Integer |No |20 |Page size The default is 20, with a maximum of 100 |
|TopicIDList |String |No |topic1 |List of `TopicID` for filtering data backflow tasks |
|TaskId |String |No |d4bd\-53f1\-43ff\-b88a\-64ee1be5\*\*\*\* |ID of the log backfill task. |
|TaskName |String |No |log\-data\-backflow\-task\-name |Name of the log backflow task. |
|Status |Integer |No |1 |Status of return tasks, used to filter tasks by specific status. |
|ScheduleSQLTaskId |String |No |ffdaa6b6\-3c9f\-424c\-8664\-fc0d222c\*\*\*\* |Scheduled SQL task ID. |
|ShipperId |String |No |4a9bd4bd\-53f1\-43ff\-b88a\-64ee1be5\*\*\*\* |Task delivery ID |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The table below lists only the return parameters specific to this API. For more information, see [Return Structure](https://docs.byteplus.com/en/docs/tls/response-message).


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|LogBackFlowTasks |Array of [LogBackFlowTaskInfo](https://docs.byteplus.com/en/docs/38/90626#logbackflowtaskinfo) |/ |List of details for data backflow tasks. |
|Total |Integer |10 |Total number of data backflow tasks, indicating the number of tasks that meet the current query criteria. |


<span id="logbackflowtaskinfo"></span>
### LogBackFlowTaskInfo


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Status |Integer |2 |Status of the data backflow task. Supported values are as follows.<br><br><br>* `0`: Task completed<br><br>* `1`: Task being created<br><br>* `2`: Task ended<br><br>* `3`: Task being deleted<br><br>* `4`: Task creation failed<br><br>* `5`: Task execution failed |
|TaskId |String |d4bd\-53f1\-43ff\-b88a\-64ee1be5\*\*\*\* |Task ID of the data backflow task |
|TaskName |String |backflow_task |Name of the data backflow task. |
|CreateTime |Integer |1630000000 |Creation time of the data backflow task, in seconds. |
|ModifyTime |Integer |1630000000 |The most recent modification time of the data backflow task, measured in seconds. |
|Description |String |/ |Description of the data backflow task. |
|QueryParams |Object of [QueryParams](https://docs.byteplus.com/en/docs/38/90626#queryparams) |/ |Scheduled SQL field configuration used to specify sorting, filtering criteria, and return fields for log queries. |
|RelaTasksInfo |Object of [RelaTasksInfo](https://docs.byteplus.com/en/docs/38/90626#relatasksinfo) |/ |Backflow task association information. |
|IamProjectName |String |`default` |Name of the access control project. |
|BackFlowEndTime |Integer |1735747200 |End time of the backflow task, in seconds If set to `nil`, the backflow remains ongoing and no specific end time is set. |
|ShipperToTosInfo |Object of [ShipperToTosInfo](https://docs.byteplus.com/en/docs/38/90626#shippertotosinfo) |/ |Delivery task configuration for specifying parameters related to log delivery in log backflow tasks.<br><br>If left blank, no delivery will occur. |
|BackFlowStartTime |Integer |1735660800 |Start time of the backflow task, in seconds. |
|ScheduleSqlTaskInfo |Object of [ScheduleSqlTaskInfo](https://docs.byteplus.com/en/docs/38/90626#schedulesqltaskinfo) |/ |Configuration details for scheduled SQL tasks, including target topic information, execution cycle, timeout, and other settings. |
|LogBackFlowTaskSource |Object of [LogBackFlowTaskSource](https://docs.byteplus.com/en/docs/38/90626#logbackflowtasksource) |/ |Data source information for the data return task. |


<span id="queryparams"></span>
### QueryParams


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Asc |Boolean |true |Specify whether the query results are sorted in ascending order.<br><br><br>* `true`: Sorts in ascending order.<br><br>* `false`: Sorts in descending order. |
|Limit |Integer |100 |Set the maximum number of log entries returned when querying logs. |
|Order |String |Start |Specify the sorting field when querying logs. If left blank, the results are sorted by the `Start` field by default. |
|Fields |Array of [Field](https://docs.byteplus.com/en/docs/38/90626#field) |/ |Specify the list of fields to return when querying logs. If not specified, all fields will be returned. |
|Filters |Array of [Filter](https://docs.byteplus.com/en/docs/38/90626#filter) |/ |Specifies filter criteria for querying logs. By default, multiple criteria are combined using `AND`. |


<span id="relatasksinfo"></span>
### RelaTasksInfo


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|ShipperID |String |`ffdaa6b6-3c9f-424c-8664-fc0d222c****` |Delivery task ID. |
|DestRegion |String |`cn-north-1` |Target Region identifier. |
|ShipperName |String |`backflow_shipper_***` |Task name for delivery. |
|ScheduleSQLTaskId |String |`ffdaa6b6-3c9f-424c-8664-fc0d222c****` |Cron SQL task ID. |
|ScheduleSQLTaskName |String |`backflow_sql_***` |Timer SQL task name. |


<span id="shippertotosinfo"></span>
### ShipperToTosInfo


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|ContentInfo |Object of [ContentInfo](https://docs.byteplus.com/en/docs/38/90626#contentinfo) |`/` |Content format configuration for delivered logs. |
|TosShipperInfo |Object of [TosShipperInfo](https://docs.byteplus.com/en/docs/38/90626#tosshipperinfo) |/ |Configuration details for delivery to TOS, including bucket name, prefix directory, compression format, and other settings. |


<span id="schedulesqltaskinfo"></span>
### ScheduleSqlTaskInfo


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|DestRegion |String |cn\-north\-1 |The region where the destination topic is located. If not specified, the current region is used by default. |
|MaxTimeout |Integer |300 |The maximum timeout for a scheduled SQL task, in seconds. |
|DestTopicID |String |2a9bd4bd\-53f1\-43ff\-b88a\-64ee1be5\*\*\*\* |Target log topic ID for the scheduled SQL task, used to specify where the SQL query results are written. |
|RequestCycle |Object of [RequestCycle](https://docs.byteplus.com/en/docs/38/90626#requestcycle) |/ |Execution cycle for query or analysis requests. |
|MaxRetryTimes |Integer |3 |The maximum number of retries when a scheduled SQL task fails to execute; the default value is 3. |
|ProcessSqlDelay |Integer |60 |Query latency of the scheduled SQL task, in seconds. |
|ProcessTimeWindow |String |@m\-15m,@m |Scheduling window expression, used to specify the execution time window for timed SQL tasks This expression defines the start and end times of the task using a specific format. |


<span id="logbackflowtasksource"></span>
### LogBackFlowTaskSource


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|SourceType |String |Topic |The data source type of the log rollback task, which specifies the source type for the rollback task. |
|LogBackFlowTaskTopicSource |Object of [LogBackFlowTaskTopicSource](https://docs.byteplus.com/en/docs/38/90626#logbackflowtasktopicsource) |/ |Data source configuration for the log backfill task, including the log topic ID and its project ID. |


<span id="field"></span>
### Field


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Alias |String |user_name |Field alias, used to replace the original field name in query results. When querying logs, the alias will be displayed as the field name in the returned results. |
|Column |String |user_name |Specify the field names to return when querying logs, helping filter for specific fields needed in the logs. |


<span id="filter"></span>
### Filter


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Field |String |status |Specifies the field name in the log query filter conditions, which acts as the base field for filtering. |
|Value |Object of Value |/ |Specifies the comparison operator used for filtering conditions when querying logs. |
|Values |Array of String |["200","404","500"] |Specifies the multi\-value list for `IN` or `NOT IN` operators used as filters in log queries When `Operator` is `IN` or `NOT IN`, this field is required. |
|Operator |String |= |Used to specify comparison operators in filter criteria when querying logs. The supported values are as follows.<br><br><br>* `>`: greater than;<br><br>* `<`: less than;<br><br>* `=`: equal to;<br><br>* `IN`: included in the specified value list;<br><br>* `NOT IN`: not included in the specified value list;<br><br>* `NULL`: the field value is empty;<br><br>* `NOT NULL`: the field value is not empty. |


<span id="contentinfo"></span>
### ContentInfo


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Format |String |`json` |Log content parsing format.<br><br><br>* Supports configuration as json, jsonl, or csv when sending to TOS.<br><br>* Supports configuration as original or json when sending to Kafka. |
|CsvInfo |Object of [CsvInfo](https://docs.byteplus.com/en/docs/38/90626#csvinfo) |`/` |CSV format log content configuration. |
|JsonInfo |Object of [JsonInfo](https://docs.byteplus.com/en/docs/38/90626#jsoninfo) |`/` |Configures log content in JSON/JSONL format. |


<span id="tosshipperinfo"></span>
### TosShipperInfo


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Bucket |String |`mytos` |Select a TOS bucket. It must be in the same region as the source log topic.<br><br><br>* Consist only of numbers, hyphens (\-), and lowercase letters (a\-z).<br><br>* Start and end with a number or letter.<br><br>* Be between 3 and 63 characters long. |
|Prefix |String |`testprefix` |Top\-level directory name for the bucket. All log data submitted by this delivery configuration will be sent to this directory.<br><br><br>* Cannot start with a forward slash (/) or backslash (\), and cannot contain consecutive forward slashes (/).<br><br>* Cannot start with `..` as the folder name.<br><br>* Folder names must be unique in the same bucket. |
|MaxSize |Integer |`5` |The maximum size of the original file that can be delivered for each shard, which refers to the uncompressed log file size. The unit is MiB. The value range is 5–256. |
|Compress |String |`snappy` |Compression format. Currently supports snappy, gzip, lz4, and none. |
|Interval |Integer |`300` |Delivery interval in seconds. The value range is 300–900. |
|PartitionFormat |String |`%Y/%m/%d/%H/%M` |Partitioning rule for log delivery.<br><br><br>* Subdirectory naming supports [strftime](http://man7.org/linux/man-pages/man3/strptime.3.html) syntax. The default is set to `%Y/%m/%d/%H/%M`, such as 2022/06/30/14/00.<br><br>* It cannot start with forward slashes ( / ) or backslashes ( \ ). |
|Region |String |`cn-beijing` |The region where the target storage bucket is located. This parameter is not exposed in external APIs. |
|Endpoint |String |`https://ep-xxxx.tos.cn-beijing.privatelink.volces.com` |The proxy cluster accesses the target domain name, and the external API does not expose this parameter. |
|ProxyPoint |String |`custom1` |Proxy cluster access point. The external API does not expose this parameter. |


<span id="requestcycle"></span>
### RequestCycle


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Time |Integer |`10` |The schedule cycle or specific time for scheduled execution (the number of minutes from 00:00). The range is 1–1440, in minutes. |
|Type |String |`Period` |Scheduling cycle type Optional values:<br><br><br>* Period: Scheduling occurs at regular intervals<br><br>* Fixed: Scheduling occurs at a fixed time each day<br><br>* Cron: Use Cron expressions |
|CronTab |String |`0 18 * * *` |TLS uses a Cron expression to schedule alert tasks. The minimum granularity of a Cron expression is minutes, using 24\-hour format. For example, `0 18 * * *` means the alert task runs every day at 18:00. |
|CronTimeZone |String |`GMT+0800` |When setting Type to `Cron`, you also need to set the time zone. For common time zone options, see [Select Time Zone](https://docs.byteplus.com/docs/6470/1347854). |


<span id="logbackflowtasktopicsource"></span>
### LogBackFlowTaskTopicSource


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|TopicID |String |`0fdaa6b6-3c9f-424c-8664-fc0d222c****` |Log topic ID. |
|ProjectId |String |`c7e0e442-19bf-4fb3-b547-5992fb8b****` |Log project ID for the log topic. |


<span id="csvinfo"></span>
### CsvInfo


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Keys |Array of String |`["user","log","ip"]` |Configure the fields to be delivered.<br><br><br>* Only letters, numbers, and `_-./` are supported. Starting with `_` is not allowed.<br><br>* The Key name must be unique within the same index.<br><br>* Length: 1–128 characters. |
|Delimiter |String |`,` |Separator. Comma, tab, vertical bar, semicolon, and space are supported. |
|EscapeChar |String |`false` |Escape character: When a field contains a separator, use an escape character to enclose the field. Currently, only single quotes, double quotes, and empty characters are supported. |
|PrintHeader |Boolean |`false` |Whether to print the Key on the first line. |
|NonFieldContent |String |`test` |Invalid field fill content, length 0–128. |


<span id="jsoninfo"></span>
### JsonInfo


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Keys |Array of String |["__content", "pod_name"] |When delivering in JSON/JSONL format, if you do not configure this parameter, all fields will be delivered, including `__content__` (required), `__source__`, `__path__`, `__time__`, `__image_name__`, `__container_name__`, `__pod_name__`, `__pod_uid__`, `namespace`, `__tag____client_ip__`, and `__tag____receive_time__`. |
|Enable |Boolean |`true` |Enable flag. |
|Escape |Boolean |`true` |Enable escaping. Must be set to true. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
GET https://{tls-endpoint}/DescribeLogBackFlowTasks?&PageNumber=1&PageSize=20&TopicIDList=topic1&TaskId=d4bd-53f1-43ff-b88a-64ee1be5****&TaskName=log-data-backflow-task-name&Status=1&ScheduleSQLTaskId=ffdaa6b6-3c9f-424c-8664-fc0d222c****&ShipperId=4a9bd4bd-53f1-43ff-b88a-64ee1be5**** HTTP/1.1
Content-Type: application/json
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
Content-Type: application/json; charset=utf-8
{
    "LogBackFlowTasks": [
        {
            "Status": 2,
            "TaskId": "d4bd-53f1-43ff-b88a-64ee1be5****",
            "TaskName": "backflow_task",
            "CreateTime": 1630000000,
            "ModifyTime": 1630000000,
            "Description": "This is a sample backflow task",
            "QueryParams": {
                "Asc": true,
                "Limit": 100,
                "Order": "Start",
                "Fields": [
                    {
                        "Alias": "user_name",
                        "Column": "user_name"
                    }
                ],
                "Filters": [
                    {
                        "Field": "status",
                        "Value": "200",
                        "Values": [
                            "200",
                            "404",
                            "500"
                        ],
                        "Operator": "="
                    }
                ]
            },
            "RelaTasksInfo": {
                "ShipperID": "ffdaa6b6-3c9f-424c-8664-fc0d222c****",
                "DestRegion": "cn-north-1",
                "ShipperName": "backflow_shipper_***",
                "ScheduleSQLTaskId": "ffdaa6b6-3c9f-424c-8664-fc0d222c****",
                "ScheduleSQLTaskName": "backflow_sql_***"
            },
            "IamProjectName": "default",
            "BackFlowEndTime": 1735747200,
            "ShipperToTosInfo": {
                "ContentInfo": {
                    "Format": "json",
                    "CsvInfo": {
                        "Keys": [
                            "user",
                            "log",
                            "ip"
                        ],
                        "Delimiter": ",",
                        "EscapeChar": "\"",
                        "PrintHeader": true,
                        "NonFieldContent": "test"
                    },
                    "JsonInfo": {
                        "Keys": [
                            "__content",
                            "pod_name"
                        ],
                        "Enable": true,
                        "Escape": true
                    }
                },
                "TosShipperInfo": {
                    "Bucket": "mytos",
                    "Prefix": "testprefix",
                    "Region": "cn-beijing",
                    "MaxSize": 5,
                    "Compress": "snappy",
                    "Endpoint": "https://ep-xxxx.tos.cn-beijing.privatelink.volces.com",
                    "Interval": 300,
                    "ProxyPoint": "custom1",
                    "PartitionFormat": "%Y/%m/%d/%H/%M"
                }
            },
            "BackFlowStartTime": 1735660800,
            "ScheduleSqlTaskInfo": {
                "DestRegion": "cn-north-1",
                "MaxTimeout": 300,
                "DestTopicID": "2a9bd4bd-53f1-43ff-b88a-64ee1be5****",
                "RequestCycle": {
                    "Time": 10,
                    "Type": "Period",
                    "CronTab": "0 18 * * *",
                    "CronTimeZone": "GMT+0800"
                },
                "MaxRetryTimes": 3,
                "ProcessSqlDelay": 60,
                "ProcessTimeWindow": "@m-15m,@m"
            },
            "LogBackFlowTaskSource": {
                "SourceType": "Topic",
                "LogBackFlowTaskTopicSource": {
                    "TopicID": "0fdaa6b6-3c9f-424c-8664-fc0d222c****",
                    "ProjectId": "c7e0e442-19bf-4fb3-b547-5992fb8b****"
                }
            }
        }
    ],
    "Total": 10
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error Code

You can see [public error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes) for more error code information.
