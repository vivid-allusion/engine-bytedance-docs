---
title: "DeleteETLTask"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/DeleteETLTask"
---

Call the DeleteETLTask interface to delete the transformation task.

<span id="request-syntax"></span>
## Request syntax


* Request Method: **DELETE**

* Request URL: **https://tls\-{Region}.bytepluses.com/DeleteETLTask**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|TaskId |String |True |`4a9bd4bd-53f1-43ff-b88a-64ee1be5****` |The ID of the transformation task to be deleted. |


<span id="responses"></span>
## Responses

There are no unique return parameters for this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).

<span id="sample-request"></span>
## Sample Request

```json
DELETE https://tls-{Region}.bytepluses.com/DeleteETLTask HTTP/1.1
Content-Type: application/json
{
    "TaskId":"3fd05e87-07fb-454c-b81a-67b269c6****"
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

For common error codes, please refer to the [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).

&nbsp;
