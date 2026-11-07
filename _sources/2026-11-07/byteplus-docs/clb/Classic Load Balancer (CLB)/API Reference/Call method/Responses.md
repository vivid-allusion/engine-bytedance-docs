---
title: "Responses"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Responses"
---

<span id="response-results"></span>
## Response results

All response results must contain the RequestId, Action, Version, Service, and Region fields.

<span id="example-of-a-normal-response"></span>
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


After a request is normally processed, the response contains `ResponseMetadata` and `Result`. The following table describes the parameters in a success response.


|**Field** |**Description** |
|---|---|
|RequestID |Unique identifier of an API request. |
|Action |Requested API name. It is a public request parameter. |
|Version |Requested version number. It is a public request parameter. |
|Service |Requested service. It is a public request parameter. |


*The Result parameter varies with the API.* 

<span id="example-of-an-unexpected-response"></span>
### Example of an unexpected response

When an error occurs during an API call, the request ID and error message are returned. The HTTP status code is 4xx or 5xx.

You can troubleshoot faults based on the error code and error message. For more information, refer to public error codes and specific error codes of each API.

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


Different from a success response, an error response does not contain the `Result` parameter, and instead contains the Error parameter in `ResponseMetadata`. The following table describes the parameters in an error response.


|**Field** |**Description** |
|---|---|
|Error |The request fails. |
|Code |Error code. You can rectify faults by searching the documentation based on the error code. |
|Message |Detailed cause of an error. The message assists you in troubleshooting faults. |
|RequestID |Unique identifier of each API request. If you cannot rectify a fault yourself, contact us through the ticket system and provide the request ID so we can help you troubleshoot the fault. |
