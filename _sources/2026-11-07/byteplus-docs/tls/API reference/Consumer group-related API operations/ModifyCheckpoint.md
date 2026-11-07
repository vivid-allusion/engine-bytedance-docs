---
title: "ModifyCheckpoint"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-modifycheckpoint"
---

Calls the ModifyCheckPoint interface to reset the consumption checkpoint for the specified shard for the specified consumer group.

<span id="usage-notes"></span>
## Usage notes


* This interface is used to reset the consumption checkpoint of the consumer group. The difference from the ResetCheckPoint interface is that ModifyCheckPoint only supports resetting the consumption checkpoint recorded by the consumer group on the specified shard, while ResetCheckPoint will reset all consumption checkpoints of the specified consumer group.

* The call frequency limit is 20 times/s, and exceeding the frequency limit will report an error ExceedQPSLimit.


<span id="request-syntax"></span>
## Request syntax


* Request Method：**PUT**

* Request URL：**https://tls\-{Region}.bytepluses.com/ModifyCheckpoint**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|ProjectID |String |True |`c7******` |The project ID to which the checkpoint to be modified belongs. |
|TopicID |String |True |`b6******` |The topic ID to which the checkpoint to be modified belongs. |
|ShardID |Integer |True |`0` |The shard ID to which the checkpoint to be modified belongs. |
|ConsumerGroupName |String |True |`my-consumer-group` |The consumer group name to which the checkpoint to be modified belongs. |
|Checkpoint |String |True |`M********` |The consumption checkpoint, that is, consumption progress. |


<span id="responses"></span>
## Responses

There are no unique return parameters for this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).

<span id="sample-request"></span>
## Sample Request

```json
PUT https://tls-{Region}.bytepluses.com/ModifyCheckpoint HTTP/1.1
Content-Type: application/json
{
    "ProjectID": "c7************",
    "TopicID": "b6********",
    "ShardID": 0,
    "ConsumerGroupName": "my-consumer-group",
    "Checkpoint": "NjUwYzRkYTgtMi0wMDAwMDAwMDAwMDAwMzE0LTAwNGY1LTA="
}
```


<span id="sample-response"></span>
## Sample Response

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```


<span id="error-code"></span>
## Error code

The following table lists the error codes related to the interface and business logic. For common error codes, please refer to the [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |Invalid argument key %s, value %s, please check argument. |The parameter is invalid. |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |


&nbsp;
