---
title: "DeleteImportTask"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/DeleteImportTask"
---

Call the DeleteImportTask interface to delete the specified data import task.

<span id="request-syntax"></span>
## Request syntax


* Request Method: **DELETE**

* Request URL: **https://tls\-{Region}.bytepluses.com/DeleteImportTask**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|TaskId |String |True |`fa************` |The ID of the data import task to be deleted. |


<span id="responses"></span>
## Responses

There are no unique return parameters for this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).

<span id="sample-request"></span>
## Sample Request

```json
DELETE https://tls-{Region}.bytepluses.com/DeleteImportTask HTTP/1.1
Content-Type: application/json
{
    "TaskId": "f3************"
}
```


<span id="sample-response"></span>
## Sample Response

```json
HTTP/1.1 200 OK Content-Type: application/json; charset=utf-8
```


<span id="error-code"></span>
## Error code

For common error codes, please refer to the [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).

&nbsp;
