---
title: "DescribeCheckPoint"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-describecheckpoint"
---

Call the DescribeCheckPoint interface to view the current consumption checkpoint of the specified consumer group on the specified shard.

<span id="usage-notes"></span>
## Usage notes


* This interface is used to obtain the consumption checkpoint of the specified consumer group on the specified topic or shard from the server.

* The call frequency limit is 20 times/s, and exceeding the frequency limit will report an error ExceedQPSLimit.


<span id="request-syntax"></span>
## Request syntax


* Request Method：**GET**

* Request URL：**https://tls\-{Region}.bytepluses.com/DescribeCheckPoint**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="query"></span>
### Query


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|ProjectId |String |True |`"fa************"` |The project ID to which the checkpoint to be queried belongs. |
|TopicId |String |True |`"hsdgyr*****"` |The topic ID to which the checkpoint to be queried belongs. |
|ShardId |String |True |`"12"` |The shard ID to which the checkpoint to be queried belongs. |


<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|ConsumerGroupName |String |False |`consumerGroupA` |The consumer group name to which the checkpoint to be queried belongs. |


<span id="responses"></span>
## Responses

The table below only lists the return parameters specific to this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).


|Name |Type |Example |Description |
|---|---|---|---|
|ShardID |Integer |`0` |The shard ID. |
|Checkpoint |String |`NjUwYzRkYTgtMi0wMDAwMDAwMDAwMDAwMzE0LTAwNGY1LTA=` |The consumption checkpoint of the specified consumer group on the specified Shard, that is, consumption progress. |


<span id="sample-request"></span>
## Sample Request

```json
GET https://tls-{Region}.bytepluses.com/DescribeCheckPoint HTTP/1.1
```


<span id="sample-response"></span>
## Sample Response

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8 
{
    "ShardID": 0,
    "Checkpoint": "NjUwYzRkYTgtMi0wMDAwMDAwMDAwMDAwMzE0LTAwNGY1LTA="
}
```


<span id="error-code"></span>
## Error code

The following table lists the error codes related to the interface and business logic. For common error codes, please refer to the [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |Invalid argument key %s, value %s, please check argument. |The parameter is invalid. |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |


&nbsp;
