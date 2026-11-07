---
title: "CreateLogBackFlowTask"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/CreateLogBackFlowTask"
---

seeCall the CreateLogBackFlowTask API to create a log data backflow task.

<span id=".6K-35rGC6K-05piO"></span>
## Request instructions


* Request method: POST

* Request URL: https://{tls\-endpoint}/CreateLogBackFlowTask


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists parameters unique to this API and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="Body"></span>
### Body


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|BackFlowEndTime |Integer |No |1735747200 |End time for the backflow task, measured in seconds. If set to `nil`, the task will continue without a specific end time. |
|BackFlowStartTime |Integer |No |1735660800 |The start time of the backflow task, in seconds. |
|Description |String |No |This is a test log data backflow task description |Task description provides detailed information about the purpose or content of the log backflow task. Description must meet the following requirements:<br><br><br>* Special characters such as `<`, `>`, `'`, `\`, and `;` are not supported.<br><br>* Length must be between 0 and 64 characters. |
|IamProjectName |String |No |default |Name of the access control project. |
|LogBackFlowTaskSource |Object of [LogBackFlowTaskSource](https://docs.byteplus.com/en/docs/38/90624#logbackflowtasksource) |Yes |/ |Data source information for TLS log backflow tasks, including the data source type and specific configuration. |
|QueryParams |Object of [QueryParams](https://docs.byteplus.com/en/docs/38/90624#queryparams) |Yes |/ |Timed SQL field configuration, used to specify sorting, filtering, and returned fields when querying logs. |
|ScheduleSqlTaskInfo |Object of [ScheduleSqlTaskInfo](https://docs.byteplus.com/en/docs/38/90624#schedulesqltaskinfo) |No |/ |Configuration information for scheduled SQL tasks, including target topic details, execution cycle, timeout period, and more. |
|ShipperToTosInfo |Object of [ShipperToTosInfo](https://docs.byteplus.com/en/docs/38/90624#shippertotosinfo) |No |/ |Delivery task configuration, used to specify parameters related to log delivery in a log data ingestion task.<br><br>If left empty, no delivery will be made. |
|TaskName |String |Yes |log\-data\-backflow\-task\-name |Name of the log backflow task. |


<span id="logbackflowtasksource"></span>
### LogBackFlowTaskSource


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|SourceType |String |No |Topic |The data source type for log replay tasks specifies the source type of the replay task |
|LogBackFlowTaskTopicSource |Object of [LogBackFlowTaskTopicSource](https://docs.byteplus.com/en/docs/38/90624#logbackflowtasktopicsource) |No |/ |The data source configuration for log callback tasks includes the log topic ID and the corresponding project ID. |


<span id="queryparams"></span>
### QueryParams


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|Asc |Boolean |No |true |Specify whether the query results are sorted in ascending order.<br><br><br>* `true`: Indicates sorting in ascending order.<br><br>* `false`: Indicates sorting in descending order. |
|Limit |Integer |No |100 |Set the maximum number of log entries returned when querying logs |
|Order |String |No |Start |Specify the sorting field for query logs. If left blank, logs are sorted by the `Start` field by default. |
|Fields |Array of [Field](https://docs.byteplus.com/en/docs/38/90624#field) |No |/ |Specifies the list of fields to return for log queries. If not specified, all fields are returned. |
|Filters |Array of [Filter](https://docs.byteplus.com/en/docs/38/90624#filter) |No |/ |Specify the filter conditions for query logs. The default relationship between multiple conditions is `AND`. |


<span id="schedulesqltaskinfo"></span>
### ScheduleSqlTaskInfo


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|DestRegion |String |No |cn\-north\-1 |The area where the target topic is located. If not specified, the default is the current region. |
|MaxTimeout |Integer |No |300 |The maximum timeout for scheduled SQL tasks, measured in seconds |
|DestTopicID |String |Yes |2a9bd4bd\-53f1\-43ff\-b88a\-64ee1be5\*\*\*\* |Target log topic ID for timed SQL tasks. This specifies where the SQL query results are written. |
|RequestCycle |Object of [RequestCycle](https://docs.byteplus.com/en/docs/38/90624#requestcycle) |No |/ |The execution cycle of query or analysis requests. |
|MaxRetryTimes |Integer |No |3 |Maximum retry attempts when a scheduled SQL task fails, with a default value of `3`. |
|ProcessSqlDelay |Integer |No |60 |Query latency for scheduled SQL tasks, measured in seconds. |
|ProcessTimeWindow |String |No |@m\-15m,@m |Schedule window expression for specifying the execution window of scheduled SQL tasks This expression defines the start and end times of tasks using a specific format |


<span id="shippertotosinfo"></span>
### ShipperToTosInfo


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|ContentInfo |Object of [ContentInfo](https://docs.byteplus.com/en/docs/38/90624#contentinfo) |No |`/` |Configure the content format of delivery logs. |
|TosShipperInfo |Object of [TosShipperInfo](https://docs.byteplus.com/en/docs/38/90624#tosshipperinfo) |No |/ |Delivery configuration information for TOS, including bucket name, prefix directory, compression format, and more. |


<span id="logbackflowtasktopicsource"></span>
### LogBackFlowTaskTopicSource


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|TopicID |String |No |`0fdaa6b6-3c9f-424c-8664-fc0d222c****` |Log topic ID. |
|ProjectId |String |No |`c7e0e442-19bf-4fb3-b547-5992fb8b****` |The log topic belongs to the log project ID. |


<span id="field"></span>
### Field


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|Alias |String |No |user_name |Field alias used to replace the original field name in query results. When querying logs, the returned results will display this alias as the field name. |
|Column |String |No |user_name |Specify the field names to be returned during log queries to filter specific fields that must be included in the logs. |


<span id="filter"></span>
### Filter


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|Field |String |No |status |Specifies the field name used as the base field for filtering log queries. This field serves as the filtering criterion. |
|Value |Object of Value |No |/ |Specifies the single value for comparison operators in log query filters. |
|Values |Array of String |No |["200","404","500"] |Used to specify a list of multiple values for the `IN` or `NOT IN` operators in log queries. If `Operator` is `IN` or `NOT IN`, this field is required. |
|Operator |String |No |= |Used to specify comparison operators in log query filtering conditions. The supported values are listed below.<br><br><br>* `>`: Greater than;<br><br>* `<`: Less than;<br><br>* `=`: Equal to;<br><br>* `IN`: Included in the specified value list;<br><br>* `NOT IN`: Not included in the specified list of values<br><br>* `NULL`: The field is empty<br><br>* `NOT NULL`: The field is not empty |


<span id="requestcycle"></span>
### RequestCycle


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|Time |Integer |Yes |`10` |The scheduling cycle or scheduled execution time (minutes from 00:00). Valid values are 1–1440; unit: minutes. |
|Type |String |Yes |`Period` |Scheduling cycle type. Optional values:<br><br><br>* Period: Schedule by cycle, meaning tasks are run at regular intervals.<br><br>* Fixed: Schedule at a specific time each day.<br><br>* Cron: Use a Cron expression. |
|CronTab |String |No |`0 18 * * *` |Cron expression: TLS uses Cron expressions to schedule alert tasks The minimum interval for Cron expressions is one minute, based on a 24\-hour clock For example, `0 18 * * *` means the alert task runs once every day at 18:00 |
|CronTimeZone |String |No |`GMT+0800` |Set Type to `Cron` and configure the time zone. For common time zones, see [Select Time Zone](https://docs.byteplus.com/docs/6470/1347854). |


<span id="contentinfo"></span>
### ContentInfo


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|Format |String |No |`json` |Log content parsing format<br><br><br>* When delivering to TOS, supports configuring as json, jsonl, or csv<br><br>* When delivering to Kafka, supports configuring as original or json |
|CsvInfo |Object of [CsvInfo](https://docs.byteplus.com/en/docs/38/90624#csvinfo) |No |`/` |CSV format log content configuration. |
|JsonInfo |Object of [JsonInfo](https://docs.byteplus.com/en/docs/38/90624#jsoninfo) |No |`/` |Configure log content in JSON or JSONL format. |


<span id="tosshipperinfo"></span>
### TosShipperInfo


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|Bucket |String |Yes |`mytos` |Select a TOS bucket. It must be in the same region as the source log topic.<br><br><br>* Only numbers, hyphens (\-), and letters a\-z are allowed.<br><br>* Start and end with a number or letter.<br><br>* The length must be between 3 and 63 characters. |
|Prefix |String |No |`testprefix` |Top\-level directory name of the bucket. All log data delivered by this delivery configuration will be delivered to this directory.<br><br><br>* Cannot start with a forward slash (/) or backslash (\), and consecutive forward slashes (/) are not allowed.<br><br>* Cannot start with `..` as a folder name.<br><br>* Folder names must be unique in the same bucket. |
|MaxSize |Integer |No |`5` |The maximum size of raw files that can be delivered for each shard, which refers to the uncompressed log file size. The unit is MiB. The value range is 5–256. |
|Compress |String |No |`snappy` |Compression format. Currently supports snappy, gzip, lz4, and none. |
|Interval |Integer |No |`300` |Delivery interval (seconds), range: 300–900. |
|PartitionFormat |String |No |`%Y/%m/%d/%H/%M` |The rule for sharding delivery logs.<br><br><br>* The naming format of subdirectories supports [strftime](http://man7.org/linux/man-pages/man3/strptime.3.html) syntax. The default setting is `%Y/%m/%d/%H/%M`, for example, 2022/06/30/14/00.<br><br>* It cannot start with forward slashes ( / ) or backslashes ( \ ). |


<span id="csvinfo"></span>
### CsvInfo


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|Keys |Array of String |Yes |`["user","log","ip"]` |Configure the fields required for delivery.<br><br><br>* Only letters, numbers, and `_-./` are supported, and the name cannot start with `_`.<br><br>* The key name must be unique within the same index.<br><br>* Length must be between 1 and 128 characters. |
|Delimiter |String |Yes |`,` |Separator. Comma, tab, vertical bar, semicolon, and space are supported. |
|EscapeChar |String |Yes |`false` |Escape character: when the field contains a separator, wrap the field with the escape character. Currently, only single quotes, double quotes, and empty characters are supported. |
|PrintHeader |Boolean |Yes |`false` |Print Key in the first row. |
|NonFieldContent |String |Yes |`test` |Invalid field fill content. The length must be 0 to 128 characters. |


<span id="jsoninfo"></span>
### JsonInfo


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|Keys |Array of String |No |["__content", "pod_name"] |When delivering in JSON or JSONL format, if this parameter is not configured, all fields are delivered, including `__content__` (required), `__source__`, `__path__`, `__time__`, `__image_name__`, `__container_name__`, `__pod_name__`, `__pod_uid__`, `namespace`, `__tag____client_ip__`, and `__tag____receive_time__`. |
|Enable |Boolean |Yes |`true` |Enable flag. |
|Escape |Boolean |No |`true` |Escape characters Must be set to true |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The table below only lists response parameters specific to this interface. For more information, see [Response structure](https://docs.byteplus.com/en/docs/tls/response-message).


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|TaskId |String |d4bd\-53f1\-43ff\-b88a\-64ee1be5\*\*\*\* |The unique identifier returned after creating a log backflow task, used to operate or query the task later. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://{tls-endpoint}/CreateLogBackFlowTask HTTP/1.1
Content-Type: application/json
{
    "BackFlowEndTime": 1735747200,
    "BackFlowStartTime": 1735660800,
    "Description": "This is a test log data backflow task description",
    "IamProjectName": "default",
    "LogBackFlowTaskSource": {
        "SourceType": "Topic",
        "LogBackFlowTaskTopicSource": {
            "TopicID": "0fdaa6b6-3c9f-424c-8664-fc0d222c****",
            "ProjectId": "c7e0e442-19bf-4fb3-b547-5992fb8b****"
        }
    },
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
    "ShipperToTosInfo": {
        "ContentInfo": {
            "Format": "json",
            "CsvInfo": {
                "Keys": [
                    "user",
                    "log",
                    "ip"
                ],
                "Delimiter": " ",
                "EscapeChar": "false",
                "PrintHeader": false,
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
    "TaskName": "log-data-backflow-task-name"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
Content-Type: application/json; charset=utf-8
{
    "TaskId": "d4bd-53f1-43ff-b88a-64ee1be5****"
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error Code

You can see [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes) to learn more about error codes.
