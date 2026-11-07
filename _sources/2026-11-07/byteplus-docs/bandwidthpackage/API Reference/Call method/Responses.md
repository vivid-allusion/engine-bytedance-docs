---
title: "Responses"
product: "Bandwidth Package"
product_code: "bandwidthpackage"
source: "https://docs.byteplus.com/en/docs/bandwidthpackage/Responses"
---

All response parameters carry `RequestId`, `Action`, `Version`, `Service`, and `Region`.

<span id="example-of-a-normal-response"></span>
## Example of a normal response

The request ID and response parameters are returned after an API is called. Such a response is called a normal response. The `HTTP` status code of a normal response is `2xx`.

```Plain Text
{
    "ResponseMetadata": {
        "RequestId": "202004011722300102****", //Obtained from the X-Top-Request-Id header.
        "Action": "{Action}",//Obtained from the query of the request Action.
        "Version": "{Version}",//Obtained from the query of the request Version.
        "Service": "{Service}",//Obtained from the X-Top-Service header.
        "Region": "{Region}" //Obtained from the X-Top-Region header.
    },
    "Result":"..."
}
```


After a request is processed normally, a response containing `ResponseMetadata` and `Result` is returned. The following table describes the fields.


|**Field** |**Description** |
|---|---|
|RequestID |The request ID, which is the unique identifier of an API request. |
|Action |Name of the API in a request. It is a common request parameter. |
|Version |The version number in a request. It is a common request parameter. |
|Service |Service in a request. It is a common request parameter. |


The value of the Result parameter varies based on the specific API called.

<span id="example-of-an-unexpected-response"></span>
## Example of an unexpected response

If an API call error occurs, the request ID and error message are returned. Such a response is called an unexpected response. The `HTTP` status code of an unexpected response is `4xx` or `5xx`.

You can troubleshoot errors based on the error code (`Code`) and error message (`Message`) of the specific API and common error codes.

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


Different from a normal response, an unexpected response does not contain `Result`, but contains `Error` in `ResponseMetadata`. The following table describes the fields.


|**Field** |**Description** |
|---|---|
|Error |An error occurs indicating that the request failed. |
|Code |The error code. You can resolve the issue by searching for relevant documentation based on the error code. |
|Message |Detailed cause of the error. This message assists you in troubleshooting faults. |
|RequestID |The request ID, which is the unique identifier of an API request. If you cannot resolve the error yourself, contact us through the ticket system and provide the request ID to obtain technical support. |
