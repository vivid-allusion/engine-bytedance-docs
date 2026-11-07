---
title: "Response examples"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/Responses"
---

All returned data includes the fields of `RequestId`, `Action`, `Version`, `Service`, and `Region`.

<span id=".5q2j5bi46L-U5Zue56S65L6L"></span>
## Normal response example

After a successful API call, the response returns the request ID and API response parameters. This type of response is called a normal response. The `HTTP` status code of normal response is `2xx`.

```Plain Text
{
    "ResponseMetadata": {
        "RequestId": "202004011722300102****", //Obtain from the X-Top-Request-Id header.
        "Action": "{Action}",//Obtain from the query of the requested Action.
        "Version": "{Version}",//Obtain it from the query of the requested Version.
        "Service": "{Service}",//Get it from the X-Top-Service header.
        "Region": "{Region}" //Obtain it from the header of X-Top-Region.
    },
    "Result":"..."
}
```


After the request is processed properly, the response contains two parts: `ResponseMetadata` and `Result`. The field descriptions are as follows:


|Field |Description |
|---|---|
|RequestID |RequestID is the unique identifier for each API request. |
|Action |Name of the requested API, a common parameter for the request. |
|Version |Request version number, a common parameter for the request. |
|Service |Requested service, a common parameter for the request. |
|Service |Requested service, a common parameter for the request. |


Result varies depending on the API called. Different APIs return different Results.

<span id=".5byC5bi46L-U5Zue56S65L6L"></span>
## Error response example

When an API call fails, the response returns the request ID and error message. This type of response is called an error response. The `HTTP` status code of error response is `4xx` or `5xx`.

You can troubleshoot errors based on the API error code (`Code`) and error message (`Message`) by seeing Common error codes and API error codes.

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
            "Message": "Could not find operation GetUserById for version 2020-04-01"
        }
    }
}
```


Compared to successful results, error results no longer include the `Result` field. Instead, the `ResponseMetadata` includes an additional `Error` field. Descriptions are as follows:


|Field |Description |
|---|---|
|Error |Error indicates that this request failed. |
|Code |Code contains the specific error code. You can view the error code documentation to resolve the issue independently. |
|Message |Message describes the specific cause of the error to assist your troubleshooting. |
|RequestID |RequestID is the unique identifier for each API request. If encountering issues that cannot be resolved independently, you can contact us via Ticket System and provide the RequestID of your request. We will provide troubleshooting support. |
