---
title: "DeleteConsumerGroup"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-deleteconsumergroup"
---

~~Call~~ the DeleteConsumerGroup interface to delete a consumer group.

<span id="usage-notes"></span>
## Usage notes

This interface is used to delete a consumer group. The call frequency limit is 20 times/s, and exceeding the frequency limit will report an error ExceedQPSLimit.

<span id="request-syntax"></span>
## Request syntax


* Request Method：**DELETE**

* Request URL：**https://tls\-{Region}.bytepluses.com/DeleteConsumerGroup**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|ProjectID |String |True |`c7******` |The project ID to which the consumer group belongs. |
|ConsumerGroupName |String |True |`my-consumer-group` |The name of the consumer group. |


<span id="responses"></span>
## Responses

There are no unique return parameters for this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).

<span id="sample-request"></span>
## Sample Request

```json
DELETE https://tls-{Region}.bytepluses.com/DeleteConsumerGroup HTTP/1.1
Content-Type: application/json
{
    "ProjectID": "c7************",
    "ConsumerGroupName": "my-consumer-group"
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

For more information, see [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |Invalid argument key %s, value %s, please check argument. |The parameter is invalid. |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |


&nbsp;
