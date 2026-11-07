---
title: "PutLogs"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-putlogs"
---

Call the PutLogs interface to upload logs to the specified topic.

<span id="8a7eced5"></span>
## Instructions for use

This interface is used to upload structured logs to the specified log topic. Currently, only PB format is supported ([Protocol Buffer](https://github.com/google/protobuf)), the log data is displayed in the form of a log group. Please refer to TLS PB format [Data encoding method](https://docs.byteplus.com/docs/tls/data-encoding-method).

When uploading logs, writing is supported through load balancing mode and HashKey routing shard mode.


* HashKey routing shard mode: when writing logs, data is written to the specified shard in an orderly manner. It is suitable for scenarios that require high orderliness for data writing and consumption. For example, a certain producer can be hashed to the shard based on the name, thus ensuring that the data written and consumed on this shard is strictly in order. Even during the merging and splitting process, it can strictly ensure that the Key will only appear on one shard at a time.

   At this time, you need to set a HashKey. TLS will write the data into the shard that contains this key value. The range of HashKey values is [00000000000000000000000000000000\-ffffffffffffffffffffffffffffffff).

* Load balancing mode: Automatically write data packets to any currently available shard according to the principle of load balance. This mode is suitable for scenarios where write and consumption behavior is independent of the shard, such as not in order.


Log upload related interfaces (PutLogs, WebTracks) share a call frequency and traffic limit amount, the specific limit is as follows:


* The total request frequency limit of the interface is 500 times/Shard/second. Exceeding the frequency limit will result in an ExceedQPSLimit error.

* The total traffic limit of the interface is 5MiB/Shard/s, and the traffic limit after log decompression in each shard is 30MiB/s. ExceedRateLimit will be reported if the traffic limit is exceeded. In large traffic scenarios, it is recommended to enable shard automatic splitting to avoid affecting data writing efficiency.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">A LogGroupList cannot exceed 5MiB, the maximum size of the original log that can be written each time is 5MiB, each log in the log group cannot exceed 1MiB, and the number of logs in a LogGroup cannot exceed 10,000. The server level will check the length of the log data written to each PutLogs request. If the limit is exceeded, the entire request fails and no log data is successfully written.</div>


* <div data-tips="true" data-tips-type="tip">When configuring the key\-value index of a field, if statistics is not enabled, word segmentation is not configured, and Chinese is not enabled, or statistics is not enabled, the field length cannot exceed 32KiB, otherwise the index creation fails.</div>



<span id="ac2be8d3"></span>
## Request syntax


* Request Method：POST

* Request URL：https://tls\-{Region}.bytepluses.com/PutLogs


<span id="27d42670"></span>
## Request header


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Content\-Type |String |Required |Application/x\-protobuf |The format of the log content. It needs to be set to`application/x-protobuf`, indicating that the log is uploaded in PB format. |
|x\-tls\-bodyrawsize |String |Required |1024 |The original size (before compression) of the request body, in bytes. |
|X\-tls\-hashkey |String |Optional |7fffffffffffffffffffffffffffffff |The HashKey of the log group, which specifies the shard to be written to by the current log group.<br><br><br>* If this parameter is not set, it means that the default load balance mode is used to write the log, and the data packet is written to any of the currently available shards.<br><br>* Setting this parameter indicates that the log is collected using the HashKey Routing Shard mode, and TLS will write data to the shard containing the specified key value. The value range of this parameter is [00000000000000000000000000000000\-ffffffffffffffffffffffffffffffff). |
|X\-tls\-compresstype |String |Optional |LZ4 |The compression format of the request body. Not compressed by default. Supported settings are:<br><br><br>* Lz4: The compression format is lz4.<br><br>* Zlib: The compression format is zlib.<br><br>   If you upload logs through the Windows SDK, only the zlib compression format is supported. |


<span id="89d43e17"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/docs/tls/common-parameters).

<span id="599e6913"></span>
### Query


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|TopicId |String |Yes |4A \*\*\*\*\*\*\*\*\*\* n |Log subject ID. |


<span id="3d44a1b3"></span>
### Body

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Please refer to TLS PB format <a href="https://docs.byteplus.com/docs/tls/data-encoding-method">Data encoding method</a>.</div>



|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|LogGroupList |Message |Yes |True |LogGroup list, which includes the encapsulated log group list contents.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The total size of the LogGroupList cannot exceed 5MiB.</div><br> |


LogGroup description


|Name |Type |Required |Description |
|---|---|---|---|
|Logs |Repeated Log |Required |An array of logs, consisting of one or more logs, each representing a log.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The number of logs in a LogGroup cannot exceed 10000.</div><br> |
|Filename |String |optional |Log file name. |
|Source |String |optional |Log source, usually identified by the machine IP. |
|LogTags |Repeated LogTags |optional |A list of custom tag fields (LogTags) for a LogGroup, consisting of one or more tags. After setting the `LogTags`, TLS adds the tag fields for all incoming log content for the PutLogs request. |


Log instructions:


|Name |Type |Required |Description |
|---|---|---|---|
|Time |Integer |Required |Log time, in Unix format timestamp, supports seconds or milliseconds, milliseconds are recommended. |
|Contents |Repeated LogContent |optional |The log content consists of one or more LogContents, each of which is a collection of key\-value key\-value pairs in a log. |


Content description


|Name |Type |Required |Description |
|---|---|---|---|
|Key |String |Required |The key value of a field group in a single log.<br><br><br>* Key is a UTF\-8 encoded string that supports letters, numbers, spaces, underscores ( *), hyphens (\-), and slashes (/), and does not support underscores (* ), spaces, or terminations. The string size is 1~ 128 bytes.<br><br>* `__content__` to store the field used by the full text of the log when configuring the full\-text index only, do not use this field for the key\-value index.<br><br>* The following fields cannot be used:<br><br>   * `__time__`<br><br>   * `__source__`<br><br>   * `__path__`<br><br>   * `__tls_key__`<br><br>   * `__tls_time__`<br><br>   * `__mq_offset__`<br><br>   * `__package_offset__` |
|Value |String |Required |Field value. |


LogTag:


|Name |Type |Required |Description |
|---|---|---|---|
|Key |String |Required |The custom tag field key. |
|Value |String |Required |The custom tag field value. |


<span id="31df0b67"></span>
## Response parameter

There are no unique return parameters for this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/docs/tls/response-message).

<span id="b5ebad39"></span>
## Request example

```json
POST https://tls-{Region}.bytepluses.com/PutLogs?TopicId=c1
Content-Type: application/x-protobuf
x-tls-hashkey: 7fffffff
x-tls-compresstype: lz4
x-tls-bodyrawsize: 1024
...
<LogGroupList in PB format>
```


<span id="85abaf9d"></span>
## Response example

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8 
...
```


<span id="c668385b"></span>
## Error code

The following table lists the error codes related to the interface and business logic. For common error codes, please refer to [Common error codes](https://docs.byteplus.com/docs/tls/common-error-codes).


|Error Code |HTTP status code |Message |Description |
|---|---|---|---|
|InvalidArgument |400 |Invalid argument key% s, value% s, please check argument. |Parameter is invalid. |
|DeserializeFailed |400 |Deserialization failed, please check argument. |Deserialization failed |
|TopicNotExist |404 |Topic does not exist. |The journal topic does not exist. |
|InternalServerError |500 |We encountered an unexpected server error, please try again later. |Internal server error. |
