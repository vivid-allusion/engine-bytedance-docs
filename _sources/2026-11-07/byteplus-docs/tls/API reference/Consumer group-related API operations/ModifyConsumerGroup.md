---
title: "ModifyConsumerGroup"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-modifyconsumergroup"
---

Call the ModifyConsumerGroup interface to modify the configuration of a consumer group.

<span id="usage-notes"></span>
## Usage notes

This interface is used to modify the list of topic ID subscribed by the consumer group, heartbeat expiration time, and other configurations. The modification of the consumer group name is not supported. The call frequency limit is 20 times/s, and exceeding the frequency limit will report an error ExceedQPSLimit.

<span id="request-syntax"></span>
## Request syntax


* Request Method：**DELETE**

* Request URL：**https://tls\-{Region}.bytepluses.com/ModifyConsumerGroup**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|ProjectID |String |True |`c7******` |The ID of the project to which the consumer group belongs. |
|ConsumerGroupName |String |True |`my-consumer-group` |The name of the consumer group. |
|TopicIDList |Array of String |False |`["A1 ******", " b2 ******"]` |The list of topic IDs to be consumed by the consumer group. |
|HeartbeatTTL |Integer |False |`60` |The heartbeat expiration time, in seconds, with a value range of 1 to 300. |
|OrderedConsume |Boolean |False |`false` |Whether to consume the logs in order.<br><br><br>* true: Consume the logs in order within the shard. After the shard is split, the original shard data is consumed first, and then the shard data split from that shard is consumed in parallel; After the shard is merged, the original shard data is consumed first, and then the new shard data merged from the original shard is consumed.<br><br>* false: Do not consume the logs in order. That is, all shards are consumed at the same time, and the new shards generated after the shard is split or merged will also be consumed immediately. |


<span id="responses"></span>
## Responses

There are no unique return parameters for this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).

<span id="sample-request"></span>
## Sample Request

```json
DELETE https://tls-{Region}.bytepluses.com/ModifyConsumerGroup HTTP/1.1
Content-Type: application/json
{
    "ProjectID": "c7************",
    "ConsumerGroupName": "my-consumer-group",
    "TopicIDList": [
        "a1******"
    ],
    "HeartbeatTTL": 60,
    "OrderedConsume": false
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
|400 |InvalidArgument |Invalid argument key %s, value %s, acceptable value: %s please check argument. |The parameter is invalid. |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |


&nbsp;
