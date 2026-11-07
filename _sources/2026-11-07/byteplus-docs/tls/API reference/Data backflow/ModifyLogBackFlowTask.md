---
title: "ModifyLogBackFlowTask"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/ModifyLogBackFlowTask"
---

Use the ModifyLogBackFlowTask API to update log backflow tasks.

<span id=".6K-35rGC6K-05piO"></span>
## Request instructions


* Request method: PUT

* Request URL: https://{tls\-endpoint}/ModifyLogBackFlowTask


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists request parameters specific to this API, as well as some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="Body"></span>
### Body


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|QueryParams |Object of [QueryParams](https://docs.byteplus.com/en/docs/38/90627#queryparams) |No |/ |Scheduled SQL field configuration, used to specify sorting, filtering, and returned field parameters when querying logs. |
|ScheduleSqlTaskInfo |Object of [ScheduleSqlTaskInfo](https://docs.byteplus.com/en/docs/38/90627#schedulesqltaskinfo) |No |/ |Configuration details for scheduled SQL tasks, including target topic information, execution cycle, timeout, and more. |
|ShipperToTosInfo |Object of [ShipperToTosInfo](https://docs.byteplus.com/en/docs/38/90627#shippertotosinfo) |No |/ |Delivery task configuration specifies parameters for log delivery in log backflow tasks.<br><br>If left empty, no delivery will occur. |
|TaskId |String |Yes |d4bd\-53f1\-43ff\-b88a\-64ee1be5\*\*\*\* |Task ID of the log backflow task to be deleted. |


<span id="queryparams"></span>
### QueryParams


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|Asc |Boolean |No |true |Specifies whether the sort order of the query result is ascending.<br><br><br>* `true`: Sorts in ascending order.<br><br>* `false`: Sorts in descending order. |
|Limit |Integer |No |100 |Sets the maximum number of log entries returned when querying logs. |
|Order |String |No |Start |Specify the sort field for query logs. If left blank, sorting defaults to the `Start` field. |
|Fields |Array of [Field](https://docs.byteplus.com/en/docs/38/90627#field) |No |/ |Specify the list of fields to return when querying logs. If not specified, all fields are returned. |
|Filters |Array of [Filter](https://docs.byteplus.com/en/docs/38/90627#filter) |No |/ |Specifies filter criteria for querying logs. The relationship between multiple conditions defaults to `AND`. |


<span id="schedulesqltaskinfo"></span>
### ScheduleSqlTaskInfo


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|DestRegion |String |No |cn\-north\-1 |The region of the target topic. If not specified, the current region will be used by default. |
|MaxTimeout |Integer |No |300 |The maximum timeout for scheduled SQL tasks, in seconds. |
|DestTopicID |String |Yes |2a9bd4bd\-53f1\-43ff\-b88a\-64ee1be5\*\*\*\* |The target log topic ID for scheduled SQL tasks specifies where SQL query results are written. |
|RequestCycle |Object of [RequestCycle](https://docs.byteplus.com/en/docs/38/90627#requestcycle) |No |/ |Execution cycle for query or analysis requests. |
|MaxRetryTimes |Integer |No |3 |Maximum retry attempts for scheduled SQL task failures. The default value is `3`. |
|ProcessSqlDelay |Integer |No |60 |The query latency of a scheduled SQL task, measured in seconds. |
|ProcessTimeWindow |String |No |@m\-15m,@m |Scheduling window expression: Specifies the execution time window for scheduled SQL tasks. This expression uses a specific format to define the start and end time of a task. |


<span id="shippertotosinfo"></span>
### ShipperToTosInfo


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|ContentInfo |Object of [ContentInfo](https://docs.byteplus.com/en/docs/38/90627#contentinfo) |No |`/` |Configure the content format for log delivery. |
|TosShipperInfo |Object of [TosShipperInfo](https://docs.byteplus.com/en/docs/38/90627#tosshipperinfo) |No |/ |Configuration details for delivery to TOS, including bucket name, prefix directory, compression format, and more. |


<span id="field"></span>
### Field


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|Alias |String |No |user_name |Field aliases used to replace the original field names in query results. The alias will be used as the field name in the results when querying logs. |
|Column |String |No |user_name |Specify the field names to return when querying logs to filter for certain fields within the logs. |


<span id="filter"></span>
### Filter


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|Field |String |No |status |Specify the field name used as a filtering condition when querying logs. This field serves as the base criterion for filtering. |
|Value |Object of Value |No |/ |Specifies the single value corresponding to the comparison operator in filter criteria when querying logs. |
|Values |Array of String |No |["200","404","500"] |Used to specify the multi\-value list corresponding to the `IN` or `NOT IN` operators in query log filter criteria. When `Operator` is `IN` or `NOT IN`, this field is required. |
|Operator |String |No |= |Specifies the comparison operator in the filter conditions for log queries. The supported values are as follows.<br><br><br>* `>`: Greater than<br><br>* `<`: Less than<br><br>* `=`: Equal to<br><br>* `IN`: Included in the specified value list<br><br>* `NOT IN`: Not included in the specified value list<br><br>* `NULL`: The field value is empty<br><br>* `NOT NULL`: The field value is not empty |


<span id="requestcycle"></span>
### RequestCycle


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|Time |Integer |Yes |`10` |Scheduled cycle or specific execution time (minutes from 00:00). Valid range: 1–1440 minutes. |
|Type |String |Yes |`Period` |Scheduling cycle type. Optional values:<br><br><br>* Period: schedules tasks periodically, meaning tasks run at regular intervals.<br><br>* Fixed: schedules tasks at a regular time every day.<br><br>* Cron: uses a Cron expression. |
|CronTab |String |No |`0 18 * * *` |Cron expression: TLS schedules alert tasks to run at specified intervals using Cron expressions. The minimum unit for a Cron expression is minutes, using a 24\-hour format. For example, `0 18 * * *` means the alert task runs daily at 18:00. |
|CronTimeZone |String |No |`GMT+0800` |When Type is set to `Cron`, you must also set the time zone. For a list of common time zones, see [Select Time Zone](https://docs.byteplus.com/docs/6470/1347854). |


<span id="contentinfo"></span>
### ContentInfo


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|Format |String |No |`json` |Log content parsing format.<br><br><br>* When delivering to TOS, you can configure json, jsonl, or csv formats.<br><br>* When delivering to Kafka, you can configure original or json formats. |
|CsvInfo |Object of [CsvInfo](https://docs.byteplus.com/en/docs/38/90627#csvinfo) |No |`/` |CSV format log content configuration. |
|JsonInfo |Object of [JsonInfo](https://docs.byteplus.com/en/docs/38/90627#jsoninfo) |No |`/` |Configure log content in JSON/JSONL format. |


<span id="tosshipperinfo"></span>
### TosShipperInfo


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|Bucket |String |Yes |`mytos` |Select a TOS bucket. It must be in the same region as the source log topic.<br><br><br>* Consist only of numbers, hyphens (\-), and lowercase letters (a\-z).<br><br>* Start and end with a number or letter.<br><br>* Length must be between 3 and 63 characters. |
|Prefix |String |No |`testprefix` |The top\-level directory name of the storage bucket. All log data delivered via this delivery configuration will be sent to this directory.<br><br><br>* Cannot start with a forward slash (/) or backslash (\), and cannot contain consecutive forward slashes (/).<br><br>* Cannot start with `..` as a folder name.<br><br>* Folder names must be unique in the same bucket. |
|MaxSize |Integer |No |`5` |The maximum size of raw files that can be delivered to each shard, that is, the size of uncompressed log files. Measured in MiB, with a value range of 5–256. |
|Compress |String |No |`snappy` |Compression formats currently supported: snappy, gzip, lz4, none. |
|Interval |Integer |No |`300` |Delivery interval in seconds, ranging from 300 to 900. |
|PartitionFormat |String |No |`%Y/%m/%d/%H/%M` |Log shard assignment rules.<br><br><br>* The subdirectory naming format supports [strftime](http://man7.org/linux/man-pages/man3/strptime.3.html) syntax. The default setting is `%Y/%m/%d/%H/%M`, for example: 2022/06/30/14/00.<br><br>* It cannot start with forward slashes ( / ) or backslashes ( \ ). |


<span id="csvinfo"></span>
### CsvInfo


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|Keys |Array of String |Yes |`["user","log","ip"]` |Configure the fields to deliver.<br><br><br>* Only letters, numbers, and `_-./` are supported, and entries must not start with `_`.<br><br>* The key name must be unique within the same index.<br><br>* Length must be between 1 and 128 characters. |
|Delimiter |String |Yes |`,` |Separator. You can use a comma, tab, pipe, semicolon, or space. |
|EscapeChar |String |Yes |`false` |Escape character: When the field contains a separator, wrap the field with an escape character. Currently, only single quotes, double quotes, and empty strings are supported. |
|PrintHeader |Boolean |Yes |`false` |Print the key on the first line. |
|NonFieldContent |String |Yes |`test` |Invalid field padding content, length: 0–128 characters. |


<span id="jsoninfo"></span>
### JsonInfo


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|Keys |Array of String |No |["__content", "pod_name"] |When delivering in JSON/JSONL format, if this parameter is not set, all fields will be delivered, including `__content__` (required), `__source__`, `__path__`, `__time__`, `__image_name__`, `__container_name__`, `__pod_name__`, `__pod_uid__`, `namespace`, `__tag____client_ip__`, and `__tag____receive_time__`. |
|Enable |Boolean |Yes |`true` |Enable flag. |
|Escape |Boolean |No |`true` |Escape characters This must be set to true. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This interface does not have specific return parameters. For more information, see [Return Structure](https://docs.byteplus.com/en/docs/tls/response-message).

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
PUT https://{tls-endpoint}/ModifyLogBackFlowTask HTTP/1.1
Content-Type: application/json
{
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
                    "__pod_name__"
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
    "TaskId": "d4bd-53f1-43ff-b88a-64ee1be5****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
Content-Type: application/json; charset=utf-8
{}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error Code

You can see [Common Error Codes](https://docs.byteplus.com/en/docs/tls/common-error-codes) to get more error code information.
