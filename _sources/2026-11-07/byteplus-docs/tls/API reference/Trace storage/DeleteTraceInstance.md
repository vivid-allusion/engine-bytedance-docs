---
title: "DeleteTraceInstance"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/DeleteTraceInstance"
---

Call the DeleteTraceInstance API to delete the trace instance.

Deleting a trace instance will also remove the related topic and index.

<span id=".6K-35rGC6K-05piO"></span>
## Request instructions


* Request method: DELETE

* Request URL: https://{tls\-endpoint}/DeleteTraceInstance


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists parameters specific to this API and some common parameters. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="Body"></span>
### Body


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|TraceInstanceId |String |Yes |`0fdaa6b6-3c9f-424c-8664-fc0d222c****` |Trace instance ID. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Return parameters

This API does not have specific return parameters. For more information, see [Return structure](https://docs.byteplus.com/en/docs/tls/response-message).

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
DELETE https://{tls-endpoint}/DeleteTraceInstance HTTP/1.1
Content-Type: application/json
{
    "TraceInstanceId": "0fdaa6b6-3c9f-424c-8664-fc0d222c****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error Code

You can visit [Common Error Codes](https://docs.byteplus.com/en/docs/tls/common-error-codes) to get more information about error codes.
