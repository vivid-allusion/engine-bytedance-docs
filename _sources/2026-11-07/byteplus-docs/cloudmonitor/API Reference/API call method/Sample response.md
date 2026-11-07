---
title: "Sample response"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Sample-response"
---

All responses include fields such as RequestId, Action, Version, Service, and Region. This topic provides different sample responses.

<span id=".5q2j5bi46L-U5Zue56S65L6L"></span>
## Normal sample responses

After a successful API call, the request ID and response parameters are returned. Such a response is considered a normal response. The HTTP status code is `2xx`.

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2020102017223001022507", 
        "Action": "{Action}",
        "Version": "{Version}",
        "Service": "{Service}",
        "Region": "{Region}" 
    },
    "Result":"..."
}
```


<span id=".5byC5bi46L-U5Zue56S65L6L"></span>
## Error sample responses

When an API call fails, the request ID and error information are returned. Such a response is considered an error response. The HTTP status code is `4xx` or `5xx`.

You can troubleshoot errors based on the error code and error message by referring to the public error codes and API\-specific error codes.

```JSON
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


&nbsp;
