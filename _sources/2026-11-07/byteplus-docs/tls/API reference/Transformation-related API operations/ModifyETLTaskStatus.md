---
title: "ModifyETLTaskStatus"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/ModifyETLTaskStatus"
---

Call the ModifyETLTaskStatus API to modify the transformation task status.

<span id="request-syntax"></span>
## Request syntax


* Request Method: **PUT**

* Request URL: **https://tls\-{Region}.bytepluses.com/ModifyETLTaskStatus**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Enable |Boolean |True |`true` |Whether to start the data transformation task.<br><br><br>* true: Enable.<br><br>* false: Pause. |
|TaskId |String |True |`4a9bd4bd-53f1-43ff-b88a-64ee1be5****` |The transformation task ID. |


<span id="responses"></span>
## Responses

There are no unique return parameters for this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).

<span id="sample-request"></span>
## Sample Request

```json
PUT https://tls-{Region}.bytepluses.com/ModifyETLTaskStatus HTTP/1.1
Content-Type: application/json
{
    "TaskId": "063e66a3-7764-4bdc-****-709a2f4219b4",
    "Enable": true
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
