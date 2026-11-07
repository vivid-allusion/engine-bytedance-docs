---
title: "OpenKafkaConsumer"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-openkafkaconsumer"
---

Call the OpenKafkaConsumer interface to enable Kafka protocol consumption for the specified log topic.

<span id="usage-notes"></span>
## Usage notes

After calling this interface to enable the Kafka protocol consumption function for log topics, log topics can be consumed as Kafka Topics, and each log corresponds to a Kafka message. For the specific method and configuration of consuming logs through the Kafka protocol, please refer to Consuming logs through the Kafka protocol.

The frequency of this interface call is limited to 20 times/s, and an ExceedQPSLimit error will be reported if the frequency limit is exceeded.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Private or public network read traffic will be generated when consuming logs.</div>


* <div data-tips="true" data-tips-type="tip">Turn off the Kafka protocol consumption function for 2 minutes before turning it on again.</div>



<span id="request-syntax"></span>
## Request syntax


* Request Method：**PUT**

* Request URL：**https://tls\-{Region}.bytepluses.com/OpenKafkaConsumer**


<span id="request-parameters"></span>
## Request parameters

<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|TopicId |String |True |`0fdaa6b6-3c9f-424c-8664-fc0d222c****` |Topic ID. |


<span id="responses"></span>
## Responses

none

<span id="sample-request"></span>
## Sample Request

```json
PUT https://tls-{Region}.bytepluses.com/OpenKafkaConsumer HTTP/1.1
Content-Type: application/json
{
    "TopicId": "66********"
}
```


<span id="sample-response"></span>
## Sample Response

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{}
```


<span id="error-code"></span>
## Error code

For more information, see [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |Invalid argument key %s, value %s, please check argument. |Parameter is invalid. |
|404 |TopicNotExist |topic %s does not exist. |The journal topic does not exist. |
|400 |ConsumeTopicOperateDisable |Please try this operator for consume topic after 2min. |Do not operate frequently, please do it again after 2 minutes. |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |
