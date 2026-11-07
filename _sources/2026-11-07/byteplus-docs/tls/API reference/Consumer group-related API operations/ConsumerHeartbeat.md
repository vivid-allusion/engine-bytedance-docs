---
title: "ConsumerHeartbeat"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-consumerheartbeat"
---

Call the ConsumerHeartbeat interface to send the heartbeat information of a consumer in the consumer group to Torch Log Service.

<span id="usage-notes"></span>
## Usage notes


* This interface is used to report the heartbeat information of a consumer in the consumer group to Torch Log Service server, indicating that this consumer is online. After receiving this request, the server will evenly distribute the log shards to this consumer based on the number of consumers in this consumer group and the number of shards of the subscribed topic, and return the shard information that the specified consumer is responsible for consuming.

* Each active consumer should regularly report heartbeat information, and the reporting interval must not exceed the heartbeat expiration time (HeartbeatTTL), otherwise the server will regard it as offline.

* The call frequency limit of this interface is 20 times/s, and exceeding the frequency limit will report an ExceedQPSLimit error.


<span id="request-syntax"></span>
## Request syntax


* Request Method: **POST**

* Request URL: **https://tls\-{Region}.bytepluses.com/ConsumerHeartbeat**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|ProjectID |String |True |`c7******` |The project ID to which the consumer group belongs. |
|ConsumerGroupName |String |True |`my-consumer-group` |The name of the consumer group. |
|ConsumerName |String |True |`consumer-0` |Specify the name of the new consumer in the designated consumer group. Please refer to the [Resource Naming limit](https://docs.byteplus.com/en/docs/38/docs/tls/Limits#resource-naming-limit) for the naming rules. |


<span id="responses"></span>
## Responses

The table below only lists the return parameters specific to this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).


|Name |Type |Example |Description |
|---|---|---|---|
|Shards |Array of [ConsumeShard](https://docs.byteplus.com/en/docs/38/17261#consumeshard) |`{"TopicID": "e6 ********", " S hard ID": 1}` |The list of shards allocated to the specified consumer by the server. |


<span id="consumeshard"></span>
### ConsumeShard


|Name |Type |Example |Description |
|---|---|---|---|
|ShardID |Integer |`0` |The shard ID. |
|TopicID |String |`c7******` |The topic ID. |


<span id="sample-request"></span>
## Sample Request

```json
POST https://tls-{Region}.bytepluses.com/ConsumerHeartbeat HTTP/1.1
Content-Type: application/json
{
    "ProjectID": "c7************",
    "ConsumerGroupName": "my-consumer-group",
    "ConsumerName": "consumer-0"
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
            "TopicID": "e6********",
            "ShardID": 0
        },
        {
            "TopicID": "e6********",
            "ShardID": 1
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
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |


&nbsp;
