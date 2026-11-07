---
title: "DescribeKafkaConsumer"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-describekafkaconsumer"
---

1. Call DescribeKafkaConsumer to view the Kafka consumption feature status for the specified log topic.


<span id="usage-notes"></span>
## Usage notes

The call frequency of this interface is limited to 20 times/s, and an error ExceedQPSLimit will be reported if the frequency limit is exceeded.

<span id="request-syntax"></span>
## Request syntax


* Request Method：**GET**

* Request URL：**https://tls\-{Region}.bytepluses.com/DescribeKafkaConsumer**


<span id="request-parameters"></span>
## Request parameters

<span id="query"></span>
### Query


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|TopicId |String |True |`c7e0e442-19bf-4fb3-b547-5992fb8b****` |Topic ID. |


<span id="responses"></span>
## Responses


|Name |Type |Example |Description |
|---|---|---|---|
|AllowConsume |Boolean |`true` |Specifies whether the log topic has Kafka protocol consumption enabled.<br><br><br>* true: turned on.<br><br>* false: not turned on. |
|ConsumeTopic |String |`out-0fdaa6b6-3c9f-424c-8664-fc0d222c****` |The Kafka protocol consumes topic ID in the format of out + log topic ID. Topic should specify this ID when consuming log data in this log topic through the Kafka protocol. |


<span id="sample-request"></span>
## Sample Request

```json
GET https://tls-{Region}.bytepluses.com/DescribeKafkaConsumer?TopicId=fa******** HTTP/1.1
```


<span id="sample-response"></span>
## Sample Response

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8 
{
    "AllowConsume": true,
    "ConsumeTopic": "out-fa************"
}
```


<span id="error-code"></span>
## Error code

For more information, see [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |Invalid argument key %s, value %s, please check argument. |Parameter is invalid. |
|404 |TopicNotExist |topic %s does not exist. |The journal topic does not exist. |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |


&nbsp;
