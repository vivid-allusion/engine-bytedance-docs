---
title: "ManualShardSplit"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-manualshardsplit"
---

Call the ManualShardSplit interface to manually split the specified shard.

<span id="usage-notes"></span>
## Usage notes

The call frequency limit for this interface is 20 times/s, and exceeding the frequency limit will result in an ExceedQPSLimit error.

<span id="request-syntax"></span>
## Request syntax


* Request Method: **POST**

* Request URL: **https://tls\-{Region}.bytepluses.com/ManualShardSplit**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|TopicId |String |True |`4a*********` |The ID of the topic. |
|ShardId |Integer |True |`0` |The ID of the shard waiting to be manually split. |
|Number |Integer |True |`4` |The number of splits for the shard.<br><br><br>* The number of splits should be a non\-zero even number, such as 2, 4, 8, or 16.<br><br>* The total number of read\-write status shards after splitting cannot exceed 256. |


<span id="responses"></span>
## Responses

The table below only lists the return parameters specific to this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).


|Name |Type |Example |Description |
|---|---|---|---|
|Shards |Array of [QueryResp](https://docs.byteplus.com/en/docs/38/16753#queryresp) |`/` |Shard details. |


<span id="queryresp"></span>
### QueryResp


|Name |Type |Example |Description |
|---|---|---|---|
|Status |String |`readwrite` |The status of the shard.<br><br><br>* readwrite: Read and write.<br><br>* readonly: Read\-only. |
|ShardId |Integer |`0` |The ID of the shard. |
|TopicId |String |`4a9bd4bd-53f1-43ff-b88a-64ee1be5****` |The ID of the topic. |
|ModifyTime |String |`2021-05-24 16:19:46` |The modification time of the shard. |
|StopWriteTime |String |`2021-05-24 16:19:46` |The time when the shard stops writing, that is, the time of the last log written to this shard. |
|ExclusiveEndKey |String |`7fffffffffffffffffffffffffffffff` |The end key value of the shard. |
|InclusiveBeginKey |String |`00000000000000000000000000000000` |The starting key value of the shard. |


<span id="sample-request"></span>
## Sample Request

```json
POST https://tls-{Region}.bytepluses.com/ManualShardSplit HTTP/1.1
Content-Type: application/json
{
    "TopicId": "580f17e4-958f-4f0d-8085-ac7732b2****",
    "Number": 2,
    "ShardId": 0
}
```


<span id="sample-response"></span>
## Sample Response

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{
    "Shards": [
        {
            "TopicId": "580f17e4-958f-4f0d-8085-ac7732b2****",
            "ShardId": 0,
            "InclusiveBeginKey": "00000000000000000000000000000000",
            "ExclusiveEndKey": "ffffffffffffffffffffffffffffffff",
            "Status": "readonly",
            "ModifyTime": "2023-10-31 15:11:21",
            "StopWriteTime": "2023-10-31 15:11:21"
        },
        {
            "TopicId": "580f17e4-958f-4f0d-8085-ac7732b2****",
            "ShardId": 1,
            "InclusiveBeginKey": "00000000000000000000000000000000",
            "ExclusiveEndKey": "7fffffffffffffffffffffffffffffff",
            "Status": "readwrite",
            "ModifyTime": "0001-01-01 00:00:00",
            "StopWriteTime": ""
        },
        {
            "TopicId": "580f17e4-958f-4f0d-8085-ac7732b2****",
            "ShardId": 2,
            "InclusiveBeginKey": "7fffffffffffffffffffffffffffffff",
            "ExclusiveEndKey": "ffffffffffffffffffffffffffffffff",
            "Status": "readwrite",
            "ModifyTime": "0001-01-01 00:00:00",
            "StopWriteTime": ""
        }
    ]
}
```


<span id="error-code"></span>
## Error code

The following table lists the error codes related to the interface and business logic. For common error codes, please refer to the [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |Invalid argument key %s, value %s, please check argument. |The parameter is invalid. |
|404 |TopicNotExist |Topic does not exist. |The topic does not exist. |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |


&nbsp;
