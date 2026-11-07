---
title: "Response Example"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLB-Response-Example"
---

<span id="响应结果"></span>
## Response Results

All response results must contain the RequestId, Action, Version, Service, and Region fields.

<span id="正常返回示例"></span>
### Sample of a normal response

After an API is successfully called, the success response contains the request ID and response parameters. The HTTP status code is 2xx.

```Plain Text
{
    "ResponseMetadata": {
        "RequestId": "202010201722300102****",
        "Action": "{Action}",
        "Version": "{Version}",
        "Service": "{Service}",
        "Region": "{Region}"
    },
    "Result":"..."
}
```


If a request is normally processed, the response contains two fields `ResponseMetadata` and `Result`. The following table describes the fields:


|Field |Description |
|---|---|
|RequestID |The unique identifier of each API request. |
|action |Name of the requested API. A common request parameter. |
|Version |Version number of the API. A common request parameter. |
|Service |The requested service. A common request parameter. |


*The value of the Result parameter varies based on the specific API called.* 

<span id="异常返回示例"></span>
### Example of an unexpected response

When an API call error occurs, the request ID and error information are returned. In this case, the response is known as an abnormal response. The HTTP status code is 4xx or 5xx.

You can troubleshoot faults based on the error code and error message. For more information, refer to common error codes and specific error codes of each API.

```Plain Text
{
    "ResponseMetadata": {
        "RequestId": "202010201722300102****",
        "Action": "{Action}",
        "Version": "{Version}",
        "Service": "{Service}",
        "Region": "{Region}",
        "Error": {
            "Code": "InvalidActionOrVersion",
            "Message": "Could not find operation GetUserById for version 2020-04-01
        }
    }
}
```


In contrast to a normal response, in an abnormal response, the `Result` field is no longer contained, and the Error field is unexpectedly added to `ResponseMetadata`. The following table describes the fields:


|Field |Description |
|---|---|
|Error |Error indicates that the request has failed. |
|Code |Error code. You can rectify faults by searching the documentation based on the error code. |
|Message |The detailed cause of the error. This message assists you in troubleshooting faults. |
|RequestID |The request ID, which is the unique identifier of an API request. If you cannot resolve the error yourself, contact us through the ticket system and provide the request ID to obtain technical support. |
