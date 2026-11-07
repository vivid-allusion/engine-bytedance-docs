---
title: "API response"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Responses"
---

<span id=".5ZON5bqU57uT5p6c"></span>
## API response

All responses include the RequestId, Action, Version, Service, Region, and other fields.

<span id=".5q2j5bi46L-U5Zue56S65L6L"></span>
### Sample normal response

The response to a successful API call includes the request ID and API response parameters. This type of response is called a normal response. The HTTP status code is 2xx.

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


After the request is processed as expected, the response includes two parts: `ResponseMetadata` and `Result`. The content of `Result` depends on the requested operation, and each operation returns a different Result object. The following table describes the fields included in the response.


|Field |Description |
|---|---|
|RequestId |RequestId is the unique identifier for each API request. |
|Action |The name of the requested API operation, which is a common parameter for the request. |
|Version |The request version number, which is a common parameter for the request. |
|Service |The requested service, which is a common parameter for the request. |
|Region |The region where the service is located, which is a common parameter for the request. |


<span id=".5byC5bi46L-U5Zue56S65L6L"></span>
### Sample abnormal response

The response to a failed API call includes RequestId and the error message. This type of response is called an abnormal response. The HTTP status code is 4xx or 5xx.

You can troubleshoot errors based on the API error code (Code) and error message (Message) by referring to Common error codes and API error codes.

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
            "Message": "Could not find operation GetUserById for version 2018-01-01"
        }
    }
}
```


Compared to the response to a successful API call, the response to a failed API call no longer includes the `Result` field. Instead, an additional Error field containing Code and Message is added to `ResponseMetadata`. The following table describes the fields included in the response.


|Field |Description |
|---|---|
|Error |Error indicates that this request failed. |
|Code |Code contains the specific error code. You can view the error code documentation to resolve the issue independently. |
|Message |Message describes the specific cause of the error to assist your troubleshooting. |
|RequestId |RequestId is the unique identifier for each API request. If you encounter issues that cannot be resolved independently, you can contact us via Ticket System and provide the RequestId of your request. We will provide troubleshooting support. |
