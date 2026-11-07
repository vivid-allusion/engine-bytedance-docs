---
title: "DescribeShipper"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/DescribeShipper"
---

Call the DescribeShipper interface to obtain detailed information about the shipping configuration.

<span id="request-syntax"></span>
## Request syntax


* Request Method: **GET**

* Request URL: **https://tls\-{Region}.bytepluses.com/DescribeShipper**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="query"></span>
### Query


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|ShipperId |String |True |`f3e901c3-b17f-42fd-aa8c-dc91a6c7****` |The shipping configuration ID to be queried. |


<span id="responses"></span>
## Responses

The table below only lists the return parameters specific to this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).


|Name |Type |Example |Description |
|---|---|---|---|
|ContentInfo |Object of [ContentInfo](https://docs.byteplus.com/en/docs/38/36178#contentinfo) |`/` |The configuration of the shipping format for log. |
|CreateTime |String |`2024-09-01 14:01:02` |The creation time of the shipping configuration. |
|DashboardId |String |`/` |The default built\-in dashboard ID for deployment. |
|KafkaShipperInfo |Object of [KafkaShipperInfo](https://docs.byteplus.com/en/docs/38/36178#kafkashipperinfo) |`/` |The relevant configuration for shipping to Kafka. |
|ModifyTime |String |`2024-09-01 14:01:10` |The most recent modification time of the shipping configuration. |
|ProjectId |String |`myproject` |The ID of the project where the logs to be shipped are located. |
|ProjectName |String |`myproject` |The name of the project where the log to be shipped is located. |
|ShipperEndTime |Integer |`1723709712496` |The shipping end time. |
|ShipperId |String |`4a9bd4bd-53f1-43ff-b88a-64ee1be5****` |The ID of the shipping configuration. |
|ShipperName |String |`tosship` |The name of the shipping configuration. |
|ShipperStartTime |Integer |`1723709602496` |The shipping start time. |
|ShipperType |String |`tos` |The shipping Type. |
|Status |Boolean |`true` |Whether to enable the shipping configuration. |
|TopicId |String |`c7****` |The ID of the topic where the logs to be shipped are located. |
|TopicName |String |`mytopic` |The name of the topic where the log to be shipped is located. |
|TosShipperInfo |Object of [TosShipperInfo](https://docs.byteplus.com/en/docs/38/36178#tosshipperinfo) |`/` |The related configurations for shipping to TOS. |


<span id="contentinfo"></span>
### ContentInfo


|Name |Type |Example |Description |
|---|---|---|---|
|Format |String |`json` |The log content parsing formats:<br><br><br>* When shipping data to TOS, it supports configuration in json, jsonl and csv formats.<br><br>* When shipping data to Kafka, it supports configuration in original and json formats. |
|CsvInfo |Object of [CsvInfo](https://docs.byteplus.com/en/docs/38/36178#csvinfo) |`/` |The configuration of log content in CSV format. |
|JsonInfo |Object of [JsonInfo](https://docs.byteplus.com/en/docs/38/36178#jsoninfo) |`/` |The configuration of log content in JSON/JSONL format. |


<span id="kafkashipperinfo"></span>
### KafkaShipperInfo


|Name |Type |Example |Description |
|---|---|---|---|
|EndTime |Integer |`1723709712496` |The shipping end time, in millisecond timestamp. If not configured, the shipping will continue indefinitely.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When shipping data to Kafka, it is recommended to use the <code>ShipperStartTime</code> and <code>ShipperEndTime</code> fields to configure the shipping time range. Leave the <code>StartTime</code> and <code>EndTime</code> fields empty.</div><br> |
|Compress |String |`snappy` |The compression format, currently supported: snappy, gzip, lz4, none. |
|Instance |String |`kafka-cnngbnntswg1****` |The Kafka instance. |
|StartTime |Integer |`1723709602496` |The shipping start time, in millisecond timestamp. If not configured, the default is the current time.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When shipping to Kafka, it is recommended to use the <code>ShipperStartTime</code> and <code>ShipperEndTime</code> fields to configure the shipping time range, leaving the <code>StartTime</code> and <code>EndTime</code> fields empty.</div><br> |
|KafkaTopic |String |`topic-c` |The Kafka topic name. All log data shipped through this configuration will be shipped to this Topic. |


<span id="tosshipperinfo"></span>
### TosShipperInfo


|Name |Type |Example |Description |
|---|---|---|---|
|Bucket |String |`mytos` |The name of TOS bucket. |
|Prefix |String |`testprefix` |The name of the top\-level directory of the storage bucket. All log data shipped through this shipping configuration will be shipped to this directory. |
|MaxSize |Integer |`5` |The maximum deliverable original file size for each Shard, that is, the size of the uncompressed log file. The unit is MiB, and the value range is from 5 to 256. |
|Compress |String |`snappy` |The compression formats. |
|Interval |Integer |`300` |The shipping interval, measured in seconds. |
|PartitionFormat |String |`%Y/%m/%d/%H/%M` |The partition rules for shipping logs. |


<span id="csvinfo"></span>
### CsvInfo


|Name |Type |Example |Description |
|---|---|---|---|
|Keys |Array of String |`["user","log","ip"]` |Configure the fields that need to be shipped.<br><br><br>* Only letters, numbers, and `_ -. /` are supported, and starting with `_` is not allowed.<br><br>* The Key names are unique within the same index.<br><br>* The length is from 1 to 128. |
|Delimiter |String |`,` |The separator, supports inputting comma, tab, vertical line, semicolon, space. |
|EscapeChar |String |`''` |The escape character. When the field content contains a separator, use the escape character to wrap the field. Currently, only single quotes, double quotes, and empty characters are supported. |
|PrintHeader |Boolean |`false` |Whether to print the Key in the first row. |
|NonFieldContent |String |`test` |The filling content for invalid fields, with a length of 0 to 128. |


<span id="jsoninfo"></span>
### JsonInfo


|Name |Type |Example |Description |
|---|---|---|---|
|Keys |Array of String |`["__content", "__pod_name__"]` |When shipping in JSON/JSONL format, if this parameter is not configured, it means all fields are shipped, including `__content__` (mandatory), `__source__`, `__path__`, `__time__`, `__image_name__`, `__container_name__`, `__pod_name__`, `__pod_uid__`, `namespace`, `__tag____client_ip__`, `__tag____receive_time__`. |
|Enable |Boolean |`true` |The enable flag. |
|Escape |Boolean |`true` |Whether to escape. It must be configured as true. |


<span id="sample-request"></span>
## Sample Request

```json
GET https://tls-{Region}.bytepluses.com/DescribeShipper?&ShipperId=f3e901c3-b17f-42fd-aa8c-dc91a6c7**** HTTP/1.1
Content-Type: application/json
```


<span id="sample-response"></span>
## Sample Response

```json
{
            "ShipperId": "62f555d9-d****8c8-f47cf7ab2f8e",
            "ShipperName": "csv-search-log",
            "ProjectId": "d11be*****47cf-8170-72c318262132",
            "ProjectName": "log-sy",
            "TopicId": "eca85523******56-b750-681141d6aa8a",
            "TopicName": "search-log",
            "Status": true,
            "ShipperType": "tos",
            "TosShipperInfo": {
                "Bucket": "tls-topic-shipper",
                "Prefix": "csv-search-log",
                "PartitionFormat": "%Y/%m/%d/%H",
                "MaxSize": 256,
                "Interval": 300,
                "Compress": "snappy"
            },
            "ContentInfo": {
                "Format": "csv",
                "CsvInfo": {
                    "PrintHeader": true,
                    "Keys": [
                        "account_id",
                        "status",
                        "Action",
                        "ReqID",
                        "__image_name__",
                        "__content__",
                        "__time__"
                    ],
                    "Delimiter": ",",
                    "EscapeChar": "'",
                    "NonFieldContent": ""
                },
                "JsonInfo": null
            },
            "ShipperStartTime": 1725012764000,
            "ShipperEndTime": null,
            "CreateTime": "2024-08-22 12:23:16",
            "ModifyTime": "2024-08-30 18:12:44"
        }
```


<span id="error-code"></span>
## Error code

For common error codes, please refer to the [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).

&nbsp;
