---
title: "WebTracks"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-webtracks"
---

Call the WebTracks interface to batch upload logs to the specified log topic.

<span id="5b3bc662"></span>
## Instructions for use

This interface is used to upload multiple structured logs to the specified log topic.

Data upload requirements:


* A request cannot exceed 5MiB, the maximum size of the original log that can be written each time is 5MiB, each log in the log group cannot exceed 1MiB, and the number of logs in a LogGroup cannot exceed 10000.

* The server level will check the length of the log data written to each WebTracks request. If the limit is exceeded, the entire request fails and no log data is successfully written.


Log upload related interfaces (PutLogs, WebTracks) share a call frequency and traffic limit amount, the specific limit is as follows:


* The total request frequency limit of the interface is 500 times/Shard/second. ExceedQPSLimit will be an error if the request frequency limit is exceeded.

* The total traffic limit of the interface is 5MiB/Shard/s, and the traffic limit after log decompression in each Shard is 30MiB/s. ExceedRateLimit will be reported if the traffic limit is exceeded. In large traffic scenarios, it is recommended to turn on Shard automatic splitting to avoid affecting data writing efficiency.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Before calling this interface, you need to enable the Web Tracking function for the log topic. For detailed instructions, please refer to <a href="https://docs.byteplus.com/docs/tls/Use_web_tracking_to_collect_logs">Use web tracking to collect logs</a>.</div>


* <div data-tips="true" data-tips-type="tip">There is no need for authentication when writing data through the API interface WebTracks, which is equivalent to opening the anonymous write permission to the public network, which may generate dirty data.</div>



<span id="601d7096"></span>
## URI


|Request method |POST |
|---|---|
|URI |```json```<br>```https://tls-{Region}.bytepluses.com/WebTracks?TopicId={TopicId}&ProjectId={ProjectId}```<br> |
|transport protocol |HTTPS |


<span id="b4474f8d"></span>
## Request header


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Content\-Type |String |Required |Application/json |Format of log content. Fixed as application/json. |
|x\-tls\-bodyrawsize |String |Required |1024 |The original size (before compression) of the request body, in bytes. |
|X\-tls\-compresstype |String |Optional |LZ4 |The compressed format of the request body. Not compressed by default.<br><br>Support is set to lz4, indicating that the compression format is lz4. At this time, the compressed data needs to be passed in the request body. |


<span id="ea11dacb"></span>
## URI request parameter


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|ProjectId |String |Yes |5B \*\*\*\*\*\*\*\*\* |Log item ID. |
|TopicId |String |Yes |4A \*\*\*\*\*\*\*\*\*\* n |Log subject ID. |


<span id="5a40eb69"></span>
## Body request parameter


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Logs |Array of Log |Required |```JSON```<br>```[```<br>```{```<br>```"tap1": "person-A",```<br>```"tap2": "action-A"```<br>```}```<br>```]```<br> |LogGroup (LogGroup), which represents a collection of multiple logs, and one log represents one log.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The number of logs in a LogGroup cannot exceed 10000.</div><br> |
|Source |String |optional |Mail carrier |Log source, typically identified by the machine IP. |


Log instructions:


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Key |String |Required |Tap1 |The field name (key) of a field in a single log.<br><br>Key is a UTF\-8 encoded string, supporting letters, numbers, spaces, underscores (`_`), hyphens (`-`) and slash (`/`), and does not support underlining (`_`) begins, begins or ends with a whitespace. The string size is 1 to 128 bytes. |
|Value |String |Required |Person\-A |The field content (value) of a field in a single log. |


<span id="89a585a7"></span>
## Response parameter

None

<span id="a0d9d45f"></span>
## Example

<span id="702d6b30"></span>
### Request example

```json
POST https://tls-{Region}.bytepluses.com/WebTracks?TopicId=c1******&ProjectId=c2******
<common request header>
Content-Type: application/json
x-tls-bodyrawsize: 1024
{
    "Source": "postman",
    "Logs": [
        {
            "tap1": "person-A",
            "tap2": "action-A"
        },
        {
            "tap1": "person-B",
            "tap2": "action-B"
        }
    ]
}
```


<span id="0ab8b8a1"></span>
### Response example

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8 
...
```


<span id="e59ce6ef"></span>
## Error code


|Error Code |HTTP status code |Message |Description |
|---|---|---|---|
|InvalidArgument |400.  |Invalid argument key% s, value% s, please check argument. |Parameter is invalid. |
|DeserializeFailed |400.  |Deserialization failed, please check argument. |Deserialization failed. |
|InvalidArgument |400.  |Parameter count is less than 2 |In addition to ProjectID and TopicID, the Get request cannot have fewer than two keys. |
|TopicNotExist |404 |Topic does not exist. |The journal topic does not exist. |
|InternalServerError |500 |We encountered an unexpected server error, please try again later. |Internal server error. |


For more information, see [Common error codes](https://docs.byteplus.com/docs/tls/common-error-codes).
