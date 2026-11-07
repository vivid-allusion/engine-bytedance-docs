---
title: "Return structure"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Responses"
---

<span id=".5ZON5bqU57uT5p6c"></span>
## Response results

All response results must contain the RequestId, Action, Version, Service, and Region fields.

<span id=".5q2j5bi46L-U5Zue56S65L6L"></span>
### Example of a normal response

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


After a request is processed normally, the response contains `ResponseMetadata` and `Result`. The following table describes the returned fields.


|Name |Description |
|---|---|
|RequestID |The unique identifier of each API request. |
|Action |Name of the requested API. A common request parameter. |
|Version |Version number of the API. A common request parameter. |
|Service |The requested service. A common request parameter. |


*The value of the Result parameter varies based on the specific API called.* 

<span id=".5byC5bi46L-U5Zue56S65L6L"></span>
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


An abnormal response does not contain `Result`. `ResponseMetadata` contains the Error parameter. The following table describes the parameters.


|Name |Description |
|---|---|
|Error |An error occurs indicating that the request failed. |
|Code |The error code. You can resolve the issue by searching for relevant documentation based on the error code. |
|Message |The detailed cause of the error. This message assists you in troubleshooting faults. |
|RequestID |The request ID, which is the unique identifier of an API request. If you cannot resolve the error yourself, contact us through the ticket system and provide the request ID to obtain technical support. |
