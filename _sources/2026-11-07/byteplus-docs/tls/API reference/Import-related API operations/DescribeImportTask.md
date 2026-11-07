---
title: "DescribeImportTask"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/DescribeImportTask"
---

Call the DescribeImportTask interface to view information about a specific data import task.

<span id="request-syntax"></span>
## Request syntax


* Request Method: **GET**

* Request URL: **https://tls\-{Region}.bytepluses.com/DescribeImportTask**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="query"></span>
### Query


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|TaskId |String |False |`"fa************"` |The ID of the data import task to be queried. |


<span id="responses"></span>
## Responses

The table below only lists the return parameters specific to this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).


|Name |Type |Example |Description |
|---|---|---|---|
|TaskInfo |Object of [TaskInfo](https://docs.byteplus.com/en/docs/38/36167#taskinfo) |`/` |Detailed information of the data import task. |


<span id="taskinfo"></span>
### TaskInfo


|Name |Type |Example |Description |
|---|---|---|---|
|TaskId |String |`fa************` |The ID of the data import task. |
|status |Integer |`0` |The status of data import task.<br><br><br>* 0: Importing.<br><br>* 1: Import complete.<br><br>* 2: Import exception.<br><br>* 3: Stopping.<br><br>* 4: Stopped.<br><br>* 5: Restarting. |
|TopicId |String |`fa************` |The ID of the topic used to store data. |
|TaskName |String |`task-name-1` |The name of the data import task. |
|ProjectId |String |`fc69****` |The ID of the project used to store data. |
|TopicName |String |`topic-name` |The name of the topic used to store. |
|CreateTime |String |`1970-1-1 00:00:00` |The creation time of the data import task. |
|SourceType |String |`tos` |The type of import source. |
|TargetInfo |Object of [TargetInfo](https://docs.byteplus.com/en/docs/38/36167#targetinfo) |`/` |The information on the output side of the data import task. |
|Description |String |`this is a task` |The data import task description. |
|ProjectName |String |`myproject` |The name of the project used to store data. |
|TaskStatistics |Object of [TaskStatistics](https://docs.byteplus.com/en/docs/38/36167#taskstatistics) |`/` |The progress of the data import task. |
|ImportSourceInfo |Object of [ImportSourceInfo](https://docs.byteplus.com/en/docs/38/36167#importsourceinfo) |`/` |The information on the import source for the data import task. |


<span id="targetinfo"></span>
### TargetInfo


|Name |Type |Example |Description |
|---|---|---|---|
|Region |String |`cn-shanghai` |Region ID. |
|LogType |String |`json_log` |Specify the log parsing type during import.<br><br><br>* delimiter_log: CSV type.<br><br>* multiline_log: Multiline text type.<br><br>* minimalist_log: Single line text type.<br><br>* json_log: JSON type. |
|LogSample |String |`/` |The example of logs.<br><br>When `LogType` is set to `multiline_log`, this parameter is effective. |
|ExtractRule |Object of [ExtractRule](https://docs.byteplus.com/en/docs/38/36167#extractrule) |`/` |The log extraction rules. |


<span id="taskstatistics"></span>
### TaskStatistics


|Name |Type |Example |Description |
|---|---|---|---|
|Total |Integer |`100` |The total number of resources that have been enumerated. |
|Failed |Integer |`100` |The number of resources that failed to be imported. |
|Skipped |Integer |`20` |The number of resources whose import was skipped. |
|NotExist |Integer |`10` |The number of resources that do not exist. |
|BytesTotal |Integer |`100` |The total number of bytes of the resources that have been enumerated. |
|TaskStatus |String |`Success` |The status of the import task.<br><br><br>* Preparing: Preparation for import.<br><br>* Importing: Importing data.<br><br>* Success: Successfully completed import.<br><br>* Failed: Import failed.<br><br>* Stopped: Import has been paused. |
|Transferred |Integer |`100` |The number of resources that have been imported. |
|BytesTransferred |Integer |`100` |The number of bytes that have been imported. |


<span id="importsourceinfo"></span>
### ImportSourceInfo


|Name |Type |Example |Description |
|---|---|---|---|
|TosSourceInfo |Object of [TosSourceInfo](https://docs.byteplus.com/en/docs/38/36167#tossourceinfo) |`/` |TOS import source information.<br><br>When `sourceType` is `tos`, the `TosSourceInfo` field is required. |
|KafkaSourceInfo |Object of [KafkaSourceInfo](https://docs.byteplus.com/en/docs/38/36167#kafkasourceinfo) |`/` |Kafka import source information.<br><br>When `sourceType` is `kafka`, the `KafkaSourceInfo` field is required. |


<span id="extractrule"></span>
### ExtractRule


|Name |Type |Example |Description |
|---|---|---|---|
|Keys |Array of String |```Plain Text```<br>```[```<br>```"time",```<br>```"",```<br>```"level",```<br>```"message"```<br>```]```<br> |The list of log field.<br><br><br>* Valid only when `LogType` is `delimiter_log`.<br><br>* Supports the configuration of up to 100 field names.<br><br>* Duplicate field names cannot be configured, and all field names cannot be specified as empty. |
|Quote |String |`"` |The quota. The content wrapped by quota will not be separated but will be parsed as a complete field. It is only valid when `LogType` is `delimiter_log`. |
|TimeKey |String |`request_time` |The field name of the log time field. If the specified time field in the log is used as the log timestamp, you need to fill in the `TimeKey` and `TimeFormat`.<br><br>`TimeKey` and `TimeFormat` must appear in pairs. |
|TimeZone |String |`%Y-%m-%dT%H:%M:%S,%f` |The time zone, supports host time zone (default) and custom time zone. The custom time zone supports GMT and UTC.<br><br><br>* GMT format: GMT+08:00.<br><br>* UTC format: Asia/Shanghai. |
|Delimiter |String |`#` |The log delimiter. Valid only when `LogType` is `delimiter_log`. |
|BeginRegex |String |`[(\d+-\d+-\w+:\d+:\d+,\d+)]\s[(\w+)]\s(.*)` |The regular expression used to identify the first line in each log, which will be recognized as the start of the log. When setting `LogType` as `multiline_log`, it is necessary to configure a log sample. |
|TimeFormat |String |`%Y-%m-%dT%H:%M:%S,%f` |The format for parsing the time field. If a specified time field in the log is used as the log timestamp, you need to fill in `TimeKey` and `TimeFormat`.<br><br><br>* TimeKey and `TimeFormat` must appear in pairs.<br><br>* For how to configure the time format, please refer to [Time Format](https://docs.byteplus.com/docs/tls/time_format). |
|SkipLineCount |Integer |`2` |The number of lines of logs to be skipped. For example, if it is set to 1, when importing logs, the import will start from the second line of the CSV file.<br><br>It is valid only when the collected log type is delimiter_log and the import type is tos. |
|UnMatchLogKey |String |`LogParseFailed` |When the upload of the parsed log fails, the key name of the failed parsed log is required.<br><br>&nbsp;<br><br>`UnMatchUpLoadSwitch=true` and `UnMatchLogKey` must appear in pairs. |
|TimeExtractRegex |String |`[0-9]{0,2}\/[0-9a-zA-Z]+\/[0-9:,]+` |The regular expression for extracting time, used to extract the time value in the `TimeKey` field and parse it into the corresponding collection time. |
|UnMatchUpLoadSwitch |Boolean |`true` |Whether to upload the logs of failed analysis. `UnMatchUpLoadSwitch=true` and `UnMatchLogKey` must appear in pairs.<br><br><br>* true: Upload the logs of failed analysis.<br><br>* false: Do not upload the logs of failed analysis. |
|TimeSample |String |`2006-01-02T15:04:05Z07:00` |Time sample. Used to determine whether the time parsing format filled in is correct. |


<span id="tossourceinfo"></span>
### TosSourceInfo


|Name |Type |Example |Description |
|---|---|---|---|
|bucket |String |`import01` |The TOS bucket where the log files are located. |
|prefix |String |`accesslog/` |The path of the files to be imported in the TOS bucket. |
|region |String |`cn-shanghai` |The region where the TOS bucket is located. Cross\-region data import is supported. |
|compress_type |String |`snappy` |The compression mode for data in the TOS bucket:<br><br><br>* none: no compression<br><br>* snappy: compressed using snappy.<br><br>* gzip: compressed using gzip.<br><br>* lz4: compressed using lz4. |


<span id="kafkasourceinfo"></span>
### KafkaSourceInfo


|Name |Type |Example |Description |
|---|---|---|---|
|host |String |`kafka-cnngc7an0qpv****.kafka.***.com:9092` |The different types of Kafka clusters correspond to the different service addresses, detailed description is as follows:<br><br><br>* Message Queue for Kafka: Kafka instance access point. For more information, refer to [view endpoints](https://docs.byteplus.com/en/docs/kafka/viewing-endpoints).<br><br>   If the Kafka instance is in the same geography as the TLS project, you can use private network access, otherwise you need to use public network access.<br><br>* Self\-built Kafka cluster: IP address and port number or domain name and port number of Kafka Broker. Only public network access is supported.<br><br>   Use a half\-width comma (,) to separate multiple service addresses. |
|group |String |`mygroup` |Kafka consumer group. If not specified, the system will automatically create a Kafka consumer group. |
|topic |String |`test` |Kafka topic name. Multiple Kafka Topics should be separated by a half\-width comma (,). |
|encode |String |`UTF-8` |The encoding format of the data. Options include UTF\-8, GBK. |
|password |String |`/` |The password of the Kafka SASL user used for identity authentication. |
|protocol |String |`plaintext` |Secure transport protocol, possible values include plaintext, sasl_ssl, ssl, and sasl_plaintext. |
|username |String |`/` |The Kafka SASL username used for authentication. |
|mechanism |String |`PLAIN` |Password authentication mechanisms, available options include PLAIN, SCRAM\-SHA\-256, and SCRAM\-SHA\-512. |
|instance_id |String |`kafka-cnngbnntswg1****` |When you are using Message Queue for Kafka, this should be set to the Kafka instance ID. For more information, refer to [view instance details](https://docs.byteplus.com/en/docs/kafka/viewing-instance-details). |
|is_need_auth |Boolean |`true` |Whether to enable authentication. If you are using a public network service address , it is recommended to enable authentication. |
|initial_offset |Integer |`/` |The starting position of the data import . Optional:<br><br><br>* 0: Import from the first data in the specified Kafka topic.<br><br>* 1: Import from the latest generated data in the specified Kafka topic. |
|time_source_default |Integer |`/` |Specify the log time. Possible values:<br><br><br>* 0: Use the Kafka message timestamp.<br><br>* 1: Use the current system time. |


<span id="sample-request"></span>
## Sample Request

```json
GET https://tls-{Region}.bytepluses.com/DescribeImportTask?&TaskId="fa************" HTTP/1.1
Content-Type: application/json
```


<span id="sample-response"></span>
## Sample Response

```json
Content-Type: application/json; charset=utf-8
{
    "TaskInfo": {
        "TaskId": "841c3908-****-4811-bdb4-2b77dd4d5a41",
        "TaskName": "import-example",
        "SourceType": "tos",
        "status": 1,
        "ImportSourceInfo": {
            "TosSourceInfo": {
                "region": "cn-shanghai",
                "bucket": "tos-import-logs",
                "prefix": "test/timeJson.txt",
                "compress_type": "none"
            }
        },
        "TargetInfo": {
            "Region": "cn-shanghai",
            "LogType": "json_log",
            "ExtractRule": {
                "TimeKey": "__time__",
                "TimeFormat": "%F",
                "TimeZone": "Asia/Shanghai",
                "UnMatchUpLoadSwitch": true,
                "UnMatchLogKey": "LogParseFailed",
                "LogTemplate": {}
            },
            "UserDefineRule": {
                "Plugin": {}
            },
            "LogSample": ""
        },
        "TopicId": "5123c4b3-006****9385-a09ce05b0b88",
        "TopicName": "test",
        "TaskStatistics": {
            "TaskStatus": "Finished",
            "Transferred": 1,
            "Failed": 0,
            "Skipped": 0,
            "NotExist": 0,
            "Total": 1,
            "BytesTransferred": 657,
            "BytesTotal": 657
        },
        "Description": "",
        "CreateTime": "2024-08-27 17:37:07",
        "ProjectId": "a513edb9-45****-ad9a-019f7f1a8962",
        "ProjectName": "test"
    }
}
```


<span id="error-code"></span>
## Error code

For common error codes, please refer to the [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).

&nbsp;
