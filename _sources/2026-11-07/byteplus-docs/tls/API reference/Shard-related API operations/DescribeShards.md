---
title: "DescribeShards"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-describeshards"
---

Call the DescribeShards interface to obtain a list of shards in a topic.

<span id="usage-notes"></span>
## Usage notes

The call frequency limit for this interface is 20 times/s, and exceeding the frequency limit will result in an ExceedQPSLimit error.

<span id="request-syntax"></span>
## Request syntax


* Request Method：**GET**

* Request URL：**https://tls\-{Region}.bytepluses.com/DescribeShards**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="query"></span>
### Query


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|TopicId |String |True |`4a9bd4bd-53f1-43ff-b88a-64ee1be5****` |The ID of the topic. |
|PageNumber |Integer |False |`1` |The page number when paging the query. The default is 1, that is, the return starts from the first page of data. |
|PageSize |Integer |False |`10` |The page size. The default is 20, with a maximum of 100. |


<span id="responses"></span>
## Responses

The table below only lists the return parameters specific to this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).


|Name |Type |Example |Description |
|---|---|---|---|
|Total |Integer |`9` |The total number of Shards. |
|Shards |Array of [QueryResp](https://docs.byteplus.com/en/docs/38/16752#queryresp) |`/` |The topic information. |


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
GET https://tls-{Region}.bytepluses.com/DescribeShards?TopicId=1e***** HTTP/1.1
```


<span id="sample-response"></span>
## Sample Response

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{
    "Total": 2,
    "Shards": [
        {
            "TopicId": "b62********",
            "ShardId": 0,
            "InclusiveBeginKey": "00000000000000000000000000000000",
            "ExclusiveEndKey": "7fffffffffffffffffffffffffffffff",
            "Status": "readwrite",
            "ModifyTime": "2021-08-12 16:56:18",
            "StopWriteTime": "2021-08-12 16:56:18"
        },
        {
            "TopicId": "b6*********",
            "ShardId": 1,
            "InclusiveBeginKey": "7fffffffffffffffffffffffffffffff",
            "ExclusiveEndKey": "ffffffffffffffffffffffffffffffff",
            "Status": "readwrite",
            "ModifyTime": "2021-08-12 16:56:19",
            "StopWriteTime": "2021-08-12 16:56:18"
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
