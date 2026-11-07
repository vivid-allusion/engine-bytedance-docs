---
title: "DescribeLogContext"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-describelogcontext"
---

Call the DescribeLogContext interface to view the context information of the specified log.

<span id="usage-notes"></span>
## Usage notes

Torch Log Service supports viewing the context information of the specified log in the log source file when querying the log. After calling the interface SearchLogs, you can further view the context information of the specified log through this interface.

The related interfaces (SearchLogs, DescribeLogContext, and DescribeHistogram) share a quota for call frequency and concurrent limits, with specific restrictions as follows:


* For a single BytePlus account or IAM user, the request frequency limit for log query is 100 times/second, otherwise, the error ExceedQPSLimit will be received.

* For a single topic, the concurrent limit for log query is 15, otherwise, the error ExceedCountLimit will be received.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Only logs collected by LogCollector 1.0.6 or later support the context search. Log data uploaded by calling PutLogs through an SDK or using other methods does not support the context search.</div>


* <div data-tips="true" data-tips-type="tip">Before using the context search function, you need to configure the index for the topic. For details, please refer to <a href="https://docs.byteplus.com/docs/tls/Configure_indexes">Configure indexes</a>.</div>



<span id="request-syntax"></span>
## Request syntax


* Request Method：**POST**

* Request URL：**https://tls\-{Region}.bytepluses.com/DescribeLogContext**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|TopicId |String |True |`4a******` |The ID of the topic. |
|ContextFlow |String |True |`e61050c-f7b3a4bf-2` |Specify the ID of the LogGroup where the log is located. You can get this ID from the Logs in the return information of the [SearchLogs](https://docs.byteplus.com/docs/tls/api-searchlogs) interface. |
|PackageOffset |Long |True |`66` |Specify the log sequence number in the LogGroup. You can obtain this sequence number from the Logs in the return information of the [SearchLogs](https://docs.byteplus.com/docs/tls/api-searchlogs) interface. |
|Source |String |True |`127...**` |The IP Address of the source host for the logs. |
|PrevLogs |Integer |False |`10` |Specify the number of preceding log entries, that is, how many log entries to view backward. The value range is 1 to 1000, and the default value is 10. |
|NextLogs |Integer |False |`10` |Specify the number of following log entries, that is, how many log entries to view later. The value range is 1 to 1000, and the default value is 10. |


<span id="responses"></span>
## Responses

The table below only lists the return parameters specific to this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).


|Name |Type |Example |Description |
|---|---|---|---|
|LogContextInfos |Array of JSON Map |`/` |Specify the context log information of the designated log. Arrange in the order of context. When no context log can be queried based on the specified start log, this parameter is empty.<br><br>Among them, LogContextInfos displays the content of each log in the form of key\-value pairs, and each log also contains the following two fields:<br><br><br>* `___context_flow__`: The ID of the loggroup where the log is located.<br><br>* `__package_offset__`: The sequence number of the log in the loggroup. |
|PrevOver |Boolean |`true` |Whether there is any other information besides the logs within LogContextInfos.<br><br><br>* true: existence.<br><br>* false: none. |
|NextOver |Boolean |`true` |Whether there is any other next information besides the logs within LogContextInfos.<br><br><br>* true: existence.<br><br>* false: none. |


<span id="sample-request"></span>
## Sample Request

```json
POST https://tls-{Region}.bytepluses.com/DescribeLogContext HTTP/1.1
Content-Type: application/json
{
    "TopicId":"0fa67c30-d8e3-407f-a1d9-39d55cb7****",
    "ContextFlow":"e61050c909dcccc3-f7b3a4bfaf6af941-8",
    "PackageOffset":4,
    "Source":"127.**.**.**",
    "PrevLogs":10,
    "NextLogs":10
}
```


<span id="sample-response"></span>
## Sample Response

```json
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length:  0
{
    "LogContextInfos": [
       {
            "__context_flow__": "e61050c909dcccc3-f7b3a4bfaf6af941-2",
            "__package_offset__": "3",
            "__path__": "/root/my_script/tls-conf-master/input_logs/log/hashkey.log",
            "__source__": "127.**.**.**",
            "__time__": 1655788239654,
            "d": "1.23",
            "index": "7",
            "l": "987654321",
            "l1": "12344566789",
            "str": "hhhhhhhhh"
        },
        {
            "__context_flow__": "e61050c909dcccc3-f7b3a4bfaf6af941-2",
            "__package_offset__": "4",
            "__path__": "/root/my_script/tls-conf-master/input_logs/log/hashkey.log",
            "__source__": "127.**.**.**",
            "__time__": 1655788239654,
            "d": "1.23",
            "index": "7",
            "l": "987654321",
            "l1": "12344566789",
            "str": "hhhhhhhhh"
        },
        {
            "__context_flow__": "e61050c909dcccc3-f7b3a4bfaf6af941-2",
            "__package_offset__": "5",
            "__path__": "/root/my_script/tls-conf-master/input_logs/log/hashkey.log",
            "__source__": "127.**.**.**",
            "__time__": 1655788239654,
            "d": "1.23",
            "index": "7",
            "l": "987654321",
            "l1": "12344566789",
            "str": "hhhhhhhhh"
        }
    ],
    "PrevOver": true,
    "NextOver": true
}
```


<span id="error-code"></span>
## Error code

For common error codes, please refer to the [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).

&nbsp;
