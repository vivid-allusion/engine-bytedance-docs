---
title: "CreateShipper"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/CreateShipper"
---

Call the CreateShipper to create a shipping configuration.

<span id="request-syntax"></span>
## Request syntax


* Request Method: **POST**

* Request URL: **https://tls\-{Region}.bytepluses.com/CreateShipper**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|ContentInfo |Object of [ContentInfo](https://docs.byteplus.com/en/docs/38/36175#contentinfo) |True |`/` |The configuration of the shipping format for log. |
|KafkaShipperInfo |Object of [KafkaShipperInfo](https://docs.byteplus.com/en/docs/38/36175#kafkashipperinfo) |False |`/` |The relevant configuration for shipping to Kafka. |
|ShipperEndTime |Integer |False |`1723709712496` |The shipping end time, in milliseconds timestamp. If not configured, the shipping will continue indefinitely.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When shipping data to Kafka, it is recommended to use the <code>ShipperStartTime</code> and <code>ShipperEndTime</code> fields to configure the shipping time range, leaving the <code>StartTime</code> and <code>EndTime</code> fields empty.</div><br> |
|ShipperName |String |True |`tosship` |The shipping configuration name. please refer to the [Resource Naming Convention](https://docs.byteplus.com/en/docs/tls/Limits#2c1ff6c3). |
|ShipperStartTime |Integer |False |`1723709602496` |The shipping start time, in milliseconds timestamp. If not configured, the default is the current time.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When shipping data to Kafka, it is recommended to use the <code>ShipperStartTime</code> and <code>ShipperEndTime</code> fields to configure the shipping time range, and leave the <code>StartTime</code> and <code>EndTime</code> fields empty.</div><br> |
|ShipperType |String |False |`tos` |The shipping type.<br><br><br>* tos: ship data to TOS.<br><br>* kafka: ship data to Kafka. |
|TopicId |String |True |`c7****` |The ID of the topic where the logs to be shipped are located. |
|TosShipperInfo |Object of [TosShipperInfo](https://docs.byteplus.com/en/docs/38/36175#tosshipperinfo) |False |`/` |The related configurations for shipping to TOS. |


<span id="contentinfo"></span>
### ContentInfo


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Format |String |False |`json` |The log content parsing formats:<br><br><br>* When shipping data to TOS, it supports configuration in json, jsonl and csv formats.<br><br>* When shipping data to Kafka, it supports configuration in original and json formats. |
|CsvInfo |Object of [CsvInfo](https://docs.byteplus.com/en/docs/38/36175#csvinfo) |False |`/` |The configuration of log content in CSV format. |
|JsonInfo |Object of [JsonInfo](https://docs.byteplus.com/en/docs/38/36175#jsoninfo) |False |`/` |The configuration of log content in JSON/JSONL format. |


<span id="kafkashipperinfo"></span>
### KafkaShipperInfo


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|EndTime |Integer |False |`1723709712496` |The shipping end time, in millisecond timestamp. If not configured, the shipping will continue indefinitely.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When shipping data to Kafka, it is recommended to use the <code>ShipperStartTime</code> and <code>ShipperEndTime</code> fields to configure the shipping time range. Leave the <code>StartTime</code> and <code>EndTime</code> fields empty.</div><br> |
|Compress |String |True |`snappy` |The compression format, currently supported: snappy, gzip, lz4, none. |
|Instance |String |True |`kafka-cnngbnntswg1****` |The Kafka instance. |
|StartTime |Integer |False |`1723709602496` |The shipping start time, in millisecond timestamp. If not configured, the default is the current time.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When shipping to Kafka, it is recommended to use the <code>ShipperStartTime</code> and <code>ShipperEndTime</code> fields to configure the shipping time range, leaving the <code>StartTime</code> and <code>EndTime</code> fields empty.</div><br> |
|KafkaTopic |String |True |`topic-c` |The Kafka topic name. All log data shipped through this configuration will be shipped to this Topic. |


<span id="tosshipperinfo"></span>
### TosShipperInfo


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Bucket |String |True |`mytos` |Select a TOS bucket, which must be in the same region as the source log topic.<br><br><br>* It can only contain numbers, hyphens (\-), and letters from a to z.<br><br>* It can only start and end with numbers or letters.<br><br>* The length should be within 3 to 63 characters. |
|Prefix |String |False |`testprefix` |The name of the top\-level directory of the storage bucket. All log data shipped through this shipping configuration will be shipped to this directory.<br><br><br>* It cannot start with a forward slash (/) or a backslash (\), and consecutive forward slashes (/) cannot be used.<br><br>* It is not allowed to use `..` as the folder name.<br><br>* In the same storage bucket, folder names are not allowed to be duplicated. |
|MaxSize |Integer |False |`5` |The maximum deliverable original file size for each shard, that is, the size of the uncompressed log file. The unit is MiB, and the value range is from 5 to 256. |
|Compress |String |False |`snappy` |The compression formats currently supported are snappy, gzip, lz4, and none. |
|Interval |Integer |False |`300` |The shipping interval, measured in seconds, ranges from 300 to 900. |
|PartitionFormat |String |False |`%Y/%m/%d/%H/%M` |The partition rules for shipping logs.<br><br><br>* The naming format of subdirectories supports the [strftime](http://man7.org/linux/man-pages/man3/strptime.3.html) syntax, and the default setting is `%Y/%m/%d/%H/%M`, for example, 2022/06/30/14/00.<br><br>   It cannot start with a forward slash (/) or a backslash (\). |


<span id="csvinfo"></span>
### CsvInfo


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Keys |Array of String |True |`["user","log","ip"]` |Configure the fields that need to be shipped.<br><br><br>* Only letters, numbers, and `_ -. /` are supported, and starting with `_` is not allowed.<br><br>* The Key names are unique within the same index.<br><br>* The length is from 1 to 128. |
|Delimiter |String |True |`,` |The separator, supports inputting comma, tab, vertical line, semicolon, space. |
|EscapeChar |String |True |`''` |The escape character. When the field content contains a separator, use the escape character to wrap the field. Currently, only single quotes, double quotes, and empty characters are supported. |
|PrintHeader |Boolean |True |`false` |Whether to print the Key in the first row. |
|NonFieldContent |String |True |`test` |The filling content for invalid fields, with a length of 0 to 128. |


<span id="jsoninfo"></span>
### JsonInfo


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Keys |Array of String |False |`["__content", "__pod_name__"]` |When shipping in JSON/JSONL format, if this parameter is not configured, it means all fields are shipped, including `__content__` (mandatory), `__source__`, `__path__`, `__time__`, `__image_name__`, `__container_name__`, `__pod_name__`, `__pod_uid__`, `namespace`, `__tag____client_ip__`, `__tag____receive_time__`. |
|Enable |Boolean |True |`true` |The enable flag. |
|Escape |Boolean |False |`true` |Whether to escape. It must be configured as true. |


<span id="responses"></span>
## Responses

The table below only lists the return parameters specific to this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).


|Name |Type |Example |Description |
|---|---|---|---|
|ShipperId |String |`4a9bd4bd-53f1-43ff-b88a-64ee1be5****` |The ID of shipping configuration. |


<span id="sample-request"></span>
## Sample Request

```json
POST https://tls-{Region}.bytepluses.com/CreateShipper HTTP/1.1
Content-Type: application/json
{
    "ContentInfo": {
        "Format": "json",
        "JsonInfo": {
            "Enable": true
        }
    },
    "ShipperName": "test",
    "ShipperType": "tos",
    "TopicId": "a91c0d37-4c71-xxxx-b9cf-c0fae292d357",
    "TosShipperInfo": {
        "Bucket": "import-test",
        "Compress": "none",
        "Interval": 60,
        "MaxSize": 256,
        "PartitionFormat": "%Y",
        "Prefix": "test/"
    },
    "ShipperStartTime": 1719203400000,
    "ShipperEndTime": 1719204600000
}
```


<span id="sample-response"></span>
## Sample Response

```json
{"ShipperId": "4a9bd4bd-53f1-43ff-b88a-64ee1be5****"}
```


<span id="error-code"></span>
## Error code

For common error codes, please refer to the [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).

&nbsp;
