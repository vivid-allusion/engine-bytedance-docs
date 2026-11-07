---
title: "DescribeCursor"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-describecursor"
---

Get the log download cursor through the DescribeCursor interface.

<span id="usage-notes"></span>
## Usage notes

This interface obtains the consumption cursor (Cursor) of the corresponding topic partition by specifying the timestamp. The calling frequency is limited to 20 times/s, and an error ExceedQPSLimit will be reported if the frequency limit is exceeded.

<span id="request-syntax"></span>
## Request syntax


* Request Method：**GET**

* Request URL：**https://tls\-{Region}.bytepluses.com/DescribeCursor**


<span id="request-parameters"></span>
## Request parameters

<span id="query"></span>
### Query


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|TopicId |String |True |`c7e0e442-19bf-4fb3-b547-5992fb8b****` |To get the log topic ID of the log cursor. |
|ShardId |Integer |True |`0` |The ID of the corresponding log partition. You can get the shard list of the specified topic through the DescribeShardId interface. |


<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|From |String |True |`begin` |Time point (Unix timestamp, in seconds) or string begin, end. Begin corresponds to the earliest log to be partitioned, and end corresponds to the next log to be written. |


<span id="responses"></span>
## Responses


|Name |Type |Example |Description |
|---|---|---|---|
|Cursor |String |`m****` |Returns the cursor value. |


<span id="sample-request"></span>
## Sample Request

```json
GET https://tls-{Region}.bytepluses.com/DescribeCursor?TopicId=********&ShardId=0
{
    "From": "begin"
}
```


<span id="sample-response"></span>
## Sample Response

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{
    "Cursor": "M********"
}
```


<span id="error-code"></span>
## Error code

For more information, see [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |Invalid argument key %s, value %s, please check argument. |Parameter is invalid. |
|404 |TopicAlreadyExist |TopicNotExist |The journal topic does not exist. |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |
