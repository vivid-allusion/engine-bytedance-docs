---
title: "ModifyImportTask"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/ModifyImportTask"
---

Call the ModifyImportTask interface to modify the specified data import task.

<span id="request-syntax"></span>
## Request syntax


* Request Method: **PUT**

* Request URL: **https://tls\-{Region}.bytepluses.com/ModifyImportTask**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Description |String |False |`this is a task` |The data import task description. |
|ImportSourceInfo |Object of [ImportSourceInfo](https://docs.byteplus.com/en/docs/38/36166#importsourceinfo) |True |`/` |The information on the import source for the data import task. |
|ProjectID |String |False |`fc69****` |The ID of the project used to store data. |
|SourceType |String |True |`tos` |The type of import source. Options:<br><br><br>* tos: Import TOS data.<br><br>* kafka: Import Kafka data. |
|Status |Integer |True |`0` |The status of the data import task:<br><br><br>* 0: Importing.<br><br>* 1: Import complete.<br><br>* 2: Import exception.<br><br>* 3: Stopping.<br><br>* 4: Stopped.<br><br>* 5: Restarting. |
|TargetInfo |Object of [TargetInfo](https://docs.byteplus.com/en/docs/38/36166#targetinfo) |True |`/` |The information on the output side of the data import task. |
|TaskId |String |True |`841c3908-09e8-4811-bdb4-2b77dd4****` |The ID of the data import task. |
|TaskName |String |True |`task-name-1` |The name of data import task. |
|TopicID |String |True |`fa************` |The ID of the topic used to store data. |


<span id="importsourceinfo"></span>
### ImportSourceInfo


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|TosSourceInfo |Object of [TosSourceInfo](https://docs.byteplus.com/en/docs/38/36166#tossourceinfo) |False |`/` |TOS import source information.<br><br>When `sourceType` is `tos`, the `TosSourceInfo` field is required. |
|KafkaSourceInfo |Object of [KafkaSourceInfo](https://docs.byteplus.com/en/docs/38/36166#kafkasourceinfo) |False |`/` |Kafka import source information.<br><br>When `sourceType` is `kafka`, the `KafkaSourceInfo` field is required. |


<span id="targetinfo"></span>
### TargetInfo


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Region |String |True |`cn-shanghai` |Region ID. |
|LogType |String |True |`json_log` |Specify the log parsing type during import.<br><br><br>* delimiter_log: CSV type.<br><br>* multiline_log: Multiline text type.<br><br>* minimalist_log: Single line text type.<br><br>* json_log: JSON type. |
|LogSample |String |False |`/` |The Log sample. When setting `LogType` to `multiline_log`, it is necessary to configure the log samples.<br><br><br>* It is recommended to provide more than two log entries as examples to ensure that the regular expression can match the first line of each log.<br><br>* It is advisable to use real samples from a production environment. |
|ExtractRule |Object of [ExtractRule](https://docs.byteplus.com/en/docs/38/36166#extractrule) |False |`/` |The log extraction rules. |


<span id="tossourceinfo"></span>
### TosSourceInfo


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|bucket |String |False |`import01` |The TOS bucket where the log files are located. |
|prefix |String |False |`accesslog/` |The path of the files to be imported in the TOS bucket. |
|region |String |False |`cn-shanghai` |The region where the TOS bucket is located. Cross\-region data import is supported. |
|compress_type |String |False |`snappy` |The compression mode for data in the TOS bucket:<br><br><br>* none: no compression<br><br>* snappy: compressed using snappy.<br><br>* gzip: compressed using gzip.<br><br>* lz4: compressed using lz4. |


<span id="kafkasourceinfo"></span>
### KafkaSourceInfo


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|host |String |False |`kafka-cnngc7an0qpv****.kafka.ibytepluses.com:9092` |The different types of Kafka clusters correspond to the different service addresses, detailed description is as follows:<br><br><br>* Message Queue for Kafka: Kafka instance access point. For more information, refer to [view endpoints](https://docs.byteplus.com/en/docs/kafka/viewing-endpoints).<br><br>   If the Kafka instance is in the same geography as the TLS project, you can use private network access, otherwise you need to use public network access.<br><br>* Self\-built Kafka cluster: IP address and port number or domain name and port number of Kafka Broker. Only public network access is supported.<br><br>   Use a half\-width comma (,) to separate multiple service addresses. |
|group |String |False |`mygroup` |Kafka consumer group. If not specified, the system will automatically create a Kafka consumer group. |
|topic |String |False |`test` |Kafka topic name. Multiple Kafka Topics should be separated by a half\-width comma (,). |
|encode |String |False |`UTF-8` |The encoding format of the data. Options include UTF\-8, GBK. |
|password |String |False |`/` |The password of the Kafka SASL user used for identity authentication. |
|protocol |String |False |`plaintext` |Secure transport protocol, possible values include plaintext, sasl_ssl, ssl, and sasl_plaintext. |
|username |String |False |`/` |The Kafka SASL username used for authentication. |
|mechanism |String |False |`PLAIN` |Password authentication mechanisms, available options include PLAIN, SCRAM\-SHA\-256, and SCRAM\-SHA\-512. |
|instance_id |String |False |`kafka-cnngbnntswg1****` |When you are using Message Queue for Kafka, this should be set to the Kafka instance ID. For more information, refer to [view instance details](https://docs.byteplus.com/en/docs/kafka/viewing-instance-details). |
|is_need_auth |Boolean |False |`true` |Whether to enable authentication. If you are using a public network service address , it is recommended to enable authentication. |
|initial_offset |Integer |False |`/` |The starting position of the data import . Optional:<br><br><br>* 0: Import from the first data in the specified Kafka topic.<br><br>* 1: Import from the latest generated data in the specified Kafka topic. |
|time_source_default |Integer |False |`/` |Specify the log time. Possible values:<br><br><br>* 0: Use the Kafka message timestamp.<br><br>* 1: Use the current system time. |


<span id="extractrule"></span>
### ExtractRule


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Keys |Array of String |False |```Plain Text```<br>```[```<br>```"time",```<br>```"",```<br>```"level",```<br>```"message"```<br>```]```<br> |The list of log field.<br><br><br>* Valid only when `LogType` is `delimiter_log`.<br><br>* Supports the configuration of up to 100 field names.<br><br>* Duplicate field names cannot be configured, and all field names cannot be specified as empty. |
|Quote |String |False |`"` |The quota. The content wrapped by quota will not be separated but will be parsed as a complete field. It is only valid when `LogType` is `delimiter_log`. |
|TimeKey |String |False |`request_time` |The field name of the log time field. If the specified time field in the log is used as the log timestamp, you need to fill in the `TimeKey` and `TimeFormat`.<br><br>`TimeKey` and `TimeFormat` must appear in pairs. |
|TimeZone |String |False |`%Y-%m-%dT%H:%M:%S,%f` |The time zone, supports host time zone (default) and custom time zone. The custom time zone supports GMT and UTC.<br><br><br>* GMT format: GMT+08:00.<br><br>* UTC format: Asia/Shanghai. |
|Delimiter |String |False |`#` |The log delimiter. Valid only when `LogType` is `delimiter_log`. |
|BeginRegex |String |False |`[(\d+-\d+-\w+:\d+:\d+,\d+)]\s[(\w+)]\s(.*)` |The regular expression that needs to match the first line of the log.<br><br><br>* It is only valid when LogType is `multiline_log`.<br><br>* It must be a valid regular expression. |
|TimeFormat |String |False |`%Y-%m-%dT%H:%M:%S,%f` |The format for parsing the time field. If a specified time field in the log is used as the log timestamp, you need to fill in `TimeKey` and `TimeFormat`.<br><br><br>* TimeKey and `TimeFormat` must appear in pairs.<br><br>* For how to configure the time format, please refer to [Time Format](https://docs.byteplus.com/docs/tls/time_format). |
|SkipLineCount |Integer |False |`2` |The number of lines of logs to be skipped. For example, if it is set to 1, when importing logs, the import will start from the second line of the CSV file.<br><br>It is valid only when the collected log type is delimiter_log and the import type is tos. |
|UnMatchLogKey |String |False |`LogParseFailed` |When the upload of the parsed log fails, the key name of the failed parsed log is required.<br><br>&nbsp;<br><br>`UnMatchUpLoadSwitch=true` and `UnMatchLogKey` must appear in pairs. |
|TimeExtractRegex |String |False |`[0-9]{0,2}\/[0-9a-zA-Z]+\/[0-9:,]+` |The regular expression for extracting time, used to extract the time value in the `TimeKey` field and parse it into the corresponding collection time. |
|UnMatchUpLoadSwitch |Boolean |False |`true` |Whether to upload the logs of failed analysis. `UnMatchUpLoadSwitch=true` and `UnMatchLogKey` must appear in pairs.<br><br><br>* true: Upload the logs of failed analysis.<br><br>* false: Do not upload the logs of failed analysis. |


<span id="responses"></span>
## Responses

There are no unique return parameters for this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).

<span id="sample-request"></span>
## Sample Request

```json
PUT https://tls-{Region}.bytepluses.com/ModifyImportTask HTTP/1.1
Content-Type: application/json
{
    "ProjectID": "d1987480-*****-b403-4d087a7b866a",
    "TopicID": "fbef6560-******-83b5-4c6e345e3bb8",
    "TaskId": "53f69c58-******-8b4c-978eeaf6f8da",
    "TaskName": "import-kafka",
    "SourceType": "kafka",
    "Status": 5,
    "Description": "kafka-import desc",
    "ImportSourceInfo": {
        "KafkaSourceInfo": {
                "host": "10.249.**.*:9192",
                "topic": "app",
                "group": "TLS-f32f3e5f-c5b0-4a39-****-5c0e304da293",
                "initial_offset": 0,
                "encode": "UTF-8",
                "time_source_default": 0,
                "is_need_auth": false,
                "protocol": "",
                "mechanism": "",
                "username": "",
                "password": ""
            }
    },
    "TargetInfo":{
        "Region": "cn-shanghai",
        "LogType": "json_log"
    }
}
```


<span id="sample-response"></span>
## Sample Response

```json
Content-Type: application/json; charset=utf-8
{}
```


<span id="error-code"></span>
## Error code

For common error codes, please refer to the [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).

&nbsp;
