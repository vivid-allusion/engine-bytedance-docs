---
title: "CreateConsumerGroup"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-createconsumergroup"
---

Call the CreateConsumerGroup interface to create a consumer group.

<span id="usage-notes"></span>
## Usage notes


* This interface is used to create a consumer group.

* Before creating a consumer group, please make sure a project and topic have been created. For detailed instructions, please refer to [Create a project](https://docs.byteplus.com/en/docs/38/docs/tls/Managing_projects#create-a-project), [Create a topic](https://docs.byteplus.com/en/docs/38/docs/tls/Managing_topics#create-a-topic).

* You can create up to 150 consumer groups for a project.

* The call frequency limit of this interface is 20 times/s. Exceeding the frequency limit will return an ExceedQPSLimit error.


<span id="request-syntax"></span>
## Request syntax


* Request Method：**POST**

* Request URL：**https://tls\-{Region}.bytepluses.com/CreateConsumerGroup**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|ProjectID |String |True |`c7******` |The ID of the project to which the consumer group belongs. |
|TopicIDList |Array of String |True |`["A1 ******", " b2 ******"]` |The list of topic IDs to be consumed by the consumer group. |
|ConsumerGroupName |String |True |`my-consumer-group` |Consumer group name. For naming rules, please refer to [Resource Naming Rules](https://docs.byteplus.com/docs/tls/Limits#resource-naming-limit). |
|HeartbeatTTL |Integer |True |`60` |The heartbeat expiration time, in seconds, with a value range of 1 to 300. |
|OrderedConsume |Boolean |True |`false` |Whether to consume the logs in order.<br><br><br>* true: Consume the logs in order within the shard. After the shard is split, the original shard data is consumed first, and then the shard data split from that shard is consumed in parallel; After the shard is merged, the original shard data is consumed first, and then the new shard data merged from the original shard is consumed.<br><br>* false: Do not consume the logs in order. That is, all shards are consumed at the same time, and the new shards generated after the shard is split or merged will also be consumed immediately. |


<span id="responses"></span>
## Responses

There are no unique return parameters for this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).

<span id="sample-request"></span>
## Sample Request

```json
POST https://tls-{Region}.bytepluses.com/CreateConsumerGroup HTTP/1.1
Content-Type: application/json
{
    "ProjectID": "c7************",
    "TopicIDList": [
        "a1******"
    ],
    "ConsumerGroupName": "my-consumer-group",
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
|400 |ExceedConsumerGroupProjectQuota |Exceed project's consumer group quota, projectID: %s |Exceeded the consumer group quota under a Project. |
|400 |ConsumerGroupAlreadyExists |consumer group already exists |The consumer group already exists. |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |


&nbsp;
