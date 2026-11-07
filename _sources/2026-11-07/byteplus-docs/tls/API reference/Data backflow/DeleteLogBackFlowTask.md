---
title: "DeleteLogBackFlowTask"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/DeleteLogBackFlowTask"
---

Call the DeleteLogBackFlowTask API to delete the log backflow task.

<span id=".6K-35rGC6K-05piO"></span>
## Request instructions


* Request method: DELETE

* Request URL: https://{tls\-endpoint}/DeleteLogBackFlowTask


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters unique to this API and some common parameters. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="Body"></span>
### Body


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|TaskId |String |Yes |d4bd\-53f1\-43ff\-b88a\-64ee1be5\*\*\*\* |The task ID of the log backflow task to delete. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This endpoint has no unique response parameters. For more information, see [Response Structure](https://docs.byteplus.com/en/docs/tls/response-message).

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
DELETE https://{tls-endpoint}/DeleteLogBackFlowTask HTTP/1.1
Content-Type: application/json
{
    "TaskId": "d4bd-53f1-43ff-b88a-64ee1be5****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
Content-Type: application/json; charset=utf-8
{}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error Code

You can see [Common Error Codes](https://docs.byteplus.com/en/docs/tls/common-error-codes) for more error code details.
