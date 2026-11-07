---
title: "Response Example"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Responses"
---

All responses contain the fields: RequestId, Action, Version, Service, and Region.

## Sample of a normal response

After you successfully call an API action, the request ID and response parameters are returned. In this case, the response is known as a normal response. The normal HTTP status code is 2xx.

```Plain Text
{
    "ResponseMetadata": {
"RequestId": "202004011722300102****", //Obtained from the Header of X-Top-Request-Id.
"Action": "{Action}",//Obtained from the query of the request Action.
          "Version": "{Version}",//Obtained from the query of the request Version.
          "Service": "{Service}",//Obtained from the header of X-Top-Service.
          "Region": "{Region}" //Obtained from the header of X-Top-Region.
    },
    "Result":"..."
}
```

If a request is normally processed, the response contains two fields `ResponseMetadata` and `Result`. The following table describes the fields:

|Field |Description |
|---|---|
|RequestId |The unique identifier of an API request. |
|Action |Name of the requested API. A common request parameter. |
|Version |Version number of the API. A common request parameter. |
|Service |The requested service. A common request parameter. |

*The value of the Result parameter varies based on the specific API called.*

## Example of an unexpected response

When an API call error occurs, the request ID and error information are returned. In this case, the response is known as an abnormal response. The HTTP status code for an abnormal response is 4xx or 5xx.

You can troubleshoot issues based on Code and Message. For details, refer to Common error codes and API error codes.

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

Unlike a success response, an error response does not contain `Result` and `ResponseMetadata` contains an additional `Error` field. The following table describes the returned fields.

|Field |Description |
|---|---|
|Error |Error indicates that the request has failed. |
|Code |Error code. You can rectify faults by searching the documentation based on the error code. |
|Message |The detailed cause of the error. This message assists you in troubleshooting faults. |
|RequestId |The RequestId, which is the unique identifier of an API request. If you cannot resolve the error yourself, contact us through the ticket system and provide the request ID to obtain technical support. |
