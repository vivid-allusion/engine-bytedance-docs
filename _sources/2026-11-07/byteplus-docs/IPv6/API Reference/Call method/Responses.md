---
title: "Responses"
product: "IPv6 Gateway"
product_code: "IPv6"
source: "https://docs.byteplus.com/en/docs/IPv6/Responses"
---

All responses contain fields:`RequestId`, `Action`, `Version`, `Service`, and `Region`.

<span id="sample-of-a-normal-response"></span>
### Sample of a normal response

After you successfully call an API action, the request ID and response parameters are returned. In this case, the response is known as a normal response. The normal HTTP status code is 2xx.

```json
{
    "ResponseMetadata": {
        "RequestId": "202004011722300102****", //Obtain the value from the Header of X-Top-Request-I.
        "Action": "{Action}",//Retrieved from the query requesting the Action.
        "Version": "{Version}",//Obtained from the query requesting Version.
        "Service": "{Service}",//Obtain the value from the header of X-Top-Service.
        "Region": "{Region}" //Obtain the value from the header of the X-Top-Region.
    },
    "Result":"..."
}
```


If a request is normally processed, the response contains two fields ResponseMetadata and Result. The following table describes the fields:


|Field |Description |
|---|---|
|RequestID |The unique identifier of an API request. |
|Action |Name of the requested API. A common request parameter. |
|Version |Version number of the API. A common request parameter. |
|Service |The requested service. A common request parameter. |


The value of the Result parameter varies based on the specific API called.

<span id="example-of-an-unexpected-response"></span>
## Example of an unexpected response

When an API call error occurs, the request ID and error information are returned. In this case, the response is known as an abnormal response. The `HTTP` status code for an abnormal response is `4xx` or `5xx`.

You can troubleshoot issues based on`Code` and `Message`. For details, refer to Common error codes and API error codes.

```json
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
|RequestID |The request ID, which is the unique identifier of an API request. If you cannot resolve the error yourself, contact us through the ticket system and provide the request ID to obtain technical support. |
