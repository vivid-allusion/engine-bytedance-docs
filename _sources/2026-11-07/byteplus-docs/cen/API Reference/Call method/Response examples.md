---
title: "Response examples"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/Responses"
---

## Response output

All responses will include fields such as RequestId, Action, Version, Service, and Region.

### Normal response example

A successful API call will return a Request ID and the corresponding response parameters, which we refer to as a normal response. The HTTP status code will be in the 2xx range.

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

After the request is processed properly, the response contains two parts: `ResponseMetadata` and `Result`. The field descriptions are as follows:

|Field |Definition |
|---|---|
|RequestId |RequestId is the unique identifier for each API request. |
|Action |Name of the requested API, a common parameter for the request. |
|Version |Request version number, a common parameter for the request. |
|Service |Requested service, a common parameter for the request. |

*Result varies depending on the API called. Different APIs return different Results.*

### Error response example

When an API call fails, the response returns the request ID and error message. This type of response is called an error response. HTTP status code will be in the 4xx or 5xx range.

If an error occurs, you can refer to the Code and Message fields in the response, along with the common error codes and API\-specific error codes, to troubleshoot the issue.

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
            "Message": "Could not find operation GetUserById for version 2020-04-01"
        }
    }
}
```

Compared to successful results, error results no longer include the `Result` field. Instead, the `ResponseMetadata` includes an additional Error field. Descriptions are as follows:

|Field |Definition |
|---|---|
|Error |Error indicates that this request failed. |
|Code |Code contains the specific error code. You can view the error code documentation to resolve the issue independently. |
|Message |Message describes the specific cause of the error to assist your troubleshooting. |
|RequestId |RequestId is the unique identifier for each API request. If encountering issues that cannot be resolved independently, you can contact us via Ticket System and provide the RequestId of your request. We will provide troubleshooting support. |
