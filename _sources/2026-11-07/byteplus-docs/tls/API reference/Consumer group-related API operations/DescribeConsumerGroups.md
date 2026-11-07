---
title: "DescribeConsumerGroups"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-describeconsumergroups"
---

Call the DescribeConsumerGroups interface to obtain information about all consumer groups under a project.

<span id="usage-notes"></span>
## Usage notes


* This interface is used to view the list of consumer group information under the specified project. It supports pagination and offset\-based queries.

* The call frequency limit for this interface is 20 times/s. Exceeding the frequency limit will cause an ExceedQPSLimit error.


<span id="request-syntax"></span>
## Request syntax


* Request Method：**GET**

* Request URL：**https://tls\-{Region}.bytepluses.com/DescribeConsumerGroups**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="query"></span>
### Query


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|PageNumber |Integer |False |`1` |The page number for pagination queries. The default is 1, which means data begins to return from the first page. |
|PageSize |Integer |False |`10` |Page size. The default is 20, with a maximum of 100. |
|ConsumerGroupName |String |False |`"test-consumergroup"` |The name of the consumer group. |
|ProjectId |String |False |`"fa************"` |The ID of the project to which the consumer group belongs. |
|ProjectName |String |False |`pt*****` |The name of the project to which the consumer group belongs. |
|TopicId |String |False |`"fa************"` |The ID of the topic to which the consumer group belongs. |
|TopicName |String |False |`test` |The name of the topic to which the consumer group belongs. |
|IamProjectName |String |False |`test` |The name of the IAM project. |


<span id="responses"></span>
## Responses

The table below only lists the return parameters specific to this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).


|Name |Type |Example |Description |
|---|---|---|---|
|ConsumerGroups |Array of [ConsumerGroupResp](https://docs.byteplus.com/en/docs/38/17259#consumergroupresp) |`{"Consumer Groups ": [ { " Project ID": "32 ********", " Consumer Group Name": "test-consumer-group", "HeartbeatTTL": 60, "OrderedConsume": false}]}` |The list of consumer groups. |
|DashboardId |String |`/` |The default built\-in dashboard ID, specifically for Kafka consumption protocol. |
|Total |Integer |`1` |The total number of consumer groups. |


<span id="consumergroupresp"></span>
### ConsumerGroupResp


|Name |Type |Example |Description |
|---|---|---|---|
|topic_id |Array of String |`c7******` |The list of topics subscribed by the consumer group. |
|ProjectID |String |`c7******` |The project ID subscribed by the consumer group. |
|ProjectName |String |`test` |The project name subscribed by the consumer group. |
|HeartbeatTTL |Integer |`60` |The heartbeat expiration time, in seconds. |
|OrderedConsume |Boolean |`false` |Whether to consume the logs in order.<br><br><br>* true: Consume the logs in order within the shard. After the shard is split, the original shard data is consumed first, and then the shard data split from that shard is consumed in parallel; After the shard is merged, the original shard data is consumed first, and then the new shard data merged from the original shard is consumed.<br><br>* false: Do not consume the logs in order. That is, all shards are consumed at the same time, and the new shards generated after the shard is split or merged will also be consumed immediately. |
|ConsumerGroupName |String |`my-consumer-group` |The name of the consumer group. |


<span id="sample-request"></span>
## Sample Request

```json
GET https://tls-{Region}.bytepluses.com/DescribeConsumerGroups?ProjectId=662***&PageNumber=1&PageSize=10 HTTP/1.1
```


<span id="sample-response"></span>
## Sample Response

```json
{
    "ConsumerGroups": [
        {
            "ProjectID": "32********",
            "ConsumerGroupName": "test-consumer-group",
            "HeartbeatTTL": 60,
            "OrderedConsume": false
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
