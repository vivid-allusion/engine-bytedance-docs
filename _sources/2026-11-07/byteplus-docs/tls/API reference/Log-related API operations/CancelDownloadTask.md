---
title: "CancelDownloadTask"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-canceldownloadtask"
---

Call interface CancelDownloadTask to cancel a log download task.

<span id="request-syntax"></span>
## Request syntax


* Request Method：**POST**

* Request URL：**https://tls\-{Region}.bytepluses.com/CancelDownloadTask**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|TaskId |String |True |`4a9bd4bd-53f1-43ff-b88a-64ee1be5****` |The ID of the download task. |


<span id="responses"></span>
## Responses

There are no unique return parameters for this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).

<span id="sample-request"></span>
## Sample Request

```json
POST https://tls-{Region}.bytepluses.com/CancelDownloadTask HTTP/1.1
Content-Type: application/json
{
    "TaskId":"4a9bd4bd-53f1-43ff-b88a-64ee1be5****"
}
```


<span id="sample-response"></span>
## Sample Response

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8  
...
{}
```


<span id="error-code"></span>
## Error code

For more information, see [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).

&nbsp;
