---
title: "DeleteTopic"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-deletetopic"
---

Call the DeleteTopic interface to delete a topic.

<span id="usage-notes"></span>
## Usage notes

This interface is used to delete a topic. The call frequency limit of the interface is 20 times/s. and exceeding the frequency limit will report an error ExceedQPSLimit.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After deleting the log topic, all log data and configuration information in it will be permanently deleted and cannot be recovered. Please operate with caution.</div>


<span id="request-syntax"></span>
## Request syntax


* Request Method：**DELETE**

* Request URL：**https://tls\-{Region}.bytepluses.com/DeleteTopic**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|TopicId |String |True |`C7dadas***` |The ID of the topic. |


<span id="responses"></span>
## Responses

There are no unique return parameters for this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).

<span id="sample-request"></span>
## Sample Request

```json
DELETE https://tls-{Region}.bytepluses.com/DeleteTopic HTTP/1.1
Content-Type: application/json
{
    "TopicId": "c7************"
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

The following table lists the error codes related to the interface and business logic. For common error codes, please refer to the [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |Invalid argument key %s, value %s, please check argument. |the parameter is invalid. |
|404 |TopicNotExist |topic %s does not exist |The topic does not exist. |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |


&nbsp;
