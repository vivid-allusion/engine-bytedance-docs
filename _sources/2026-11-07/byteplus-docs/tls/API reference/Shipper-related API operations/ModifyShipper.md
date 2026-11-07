---
title: "ModifyShipper"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/ModifyShipper"
---

Call the ModifyShipper interface to modify the specified shipping configuration.

<span id="request-syntax"></span>
## Request syntax


* Request Method: **PUT**

* Request URL: **https://tls\-{Region}.bytepluses.com/ModifyShipper**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|ContentInfo |Object of [ContentInfo](https://docs.byteplus.com/en/docs/38/36177#contentinfo) |False |`/` |The configuration of the content format of the shipped logs. |
|KafkaShipperInfo |Object of [KafkaShipperInfo](https://docs.byteplus.com/en/docs/38/36177#kafkashipperinfo) |False |`/` |The relevant configuration for shipping to Kafka. |
|ShipperId |String |True |`4a9bd4bd-53f1-43ff-b88a-64ee1be5****` |The shipping Configuration ID. |
|ShipperName |String |False |`test` |The shipping configuration name. please refer to the [Resource Naming Convention](https://docs.byteplus.com/en/docs/tls/Limits#2c1ff6c3).<br><br>Unique within a log project. |
|ShipperType |String |False |`tos` |The shipping type.<br><br><br>* tos: ship data to TOS.<br><br>   If not configured, the default is TOS.<br><br>* kafka: ship data to Kafka. |
|Status |Boolean |False |`true` |Whether to enable the shipping configuration. The default value is true. |
|TosShipperInfo |Object of [TosShipperInfo](https://docs.byteplus.com/en/docs/38/36177#tosshipperinfo) |False |`/` |The related configurations for shipping to TOS. |


<span id="contentinfo"></span>
### ContentInfo


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Format |String |False |`json` |The log content parsing formats:<br><br><br>* When shipping data to TOS, it supports configuration in json, jsonl and csv formats.<br><br>* When shipping data to Kafka, it supports configuration in original and json formats. |
|CsvInfo |Object of [CsvInfo](https://docs.byteplus.com/en/docs/38/36177#csvinfo) |False |`/` |The configuration of log content in CSV format. |
|JsonInfo |Object of [JsonInfo](https://docs.byteplus.com/en/docs/38/36177#jsoninfo) |False |`/` |The configuration of log content in JSON/JSONL format. |


<span id="kafkashipperinfo"></span>
### KafkaShipperInfo


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Compress |String |True |`snappy` |The compression format, currently supported: snappy, gzip, lz4, none. |
|Instance |String |True |`kafka-cnngbnntswg1****` |The Kafka instance. |
|KafkaTopic |String |True |`topic-c` |The Kafka topic name. All log data shipped through this configuration will be shipped to this Topic. |


<span id="tosshipperinfo"></span>
### TosShipperInfo


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
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

There are no unique return parameters for this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).

<span id="sample-request"></span>
## Sample Request

```json
PUT https://tls-{Region}.bytepluses.com/ModifyShipper HTTP/1.1
Content-Type: application/json
PUT https://tls-{Region}.ibytepluses.com/ModifyShipper HTTP/1.1
Content-Type: application/json
{
    "ShipperId": "6e948fca-d3e*****0b-b5cca0b29383",
    "ContentInfo": {
        "Format": "json",
        "JsonInfo": {
            "Enable": true
        }
    },
    "ShipperName": "tosTimeTest-1",
    "ShipperType": "tos",
    "TosShipperInfo": {
        "Bucket": "tos-import-logs",
        "Compress": "snappy",
        "Interval": 60,
        "MaxSize": 256,
        "PartitionFormat": "%Y",
        "Prefix": "timeTest"
    },
    "ShipperStartTime": 1725012764000,
    "ShipperEndTime": 1723795560000
}
```


<span id="sample-response"></span>
## Sample Response

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

{}
```


<span id="error-code"></span>
## Error code

For common error codes, please refer to the [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).

&nbsp;
