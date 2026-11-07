---
title: "Response"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/Sample-response"
---

All responses contain the fields: `RequestId`, `Action`, `Version`, `Service`, and `Region`.

<span id="sample-of-a-normal-response"></span>
## Sample of a normal response

If an API is called successfully, the request ID and response parameters of the API are returned. This kind of response is a normal response. In a normal response, the status code of `HTTP` is `2xx`.

```Plain Text
{
    "ResponseMetadata": {
        "RequestId": "202004011722300102****", //Obtained from the header of X-Top-Request-Id.
        "Action": "{Action}",//Obtained from the query of the request Action.
        "Version": "{Version}",//Obtained from the query of the request Version.
        "Service": "{Service}",//Obtained from the header of X-Top-Service.
        "Region": "{Region}" //Obtained from the header of X-Top-Region.
    },
    "Result":"..."
}
```


If a request is processed normally, the response contains two fields: `ResponseMetadata` and `Result`. The following table describes the fields:


|Field |Description |
|---|---|
|RequestID |The unique ID of the API request. |
|Action |The requested API action. It is a common request parameter. |
|Version |The version of the request. It is a common request parameter. |
|Service |The requested service. It is a common request parameter. |


The value of Result depends on the requested API. Different Result values are returned for different APIs.

<span id="sample-of-an-abnormal-response"></span>
## Sample of an abnormal response

If an error occurs in calling an API, the request ID and an error message are returned. This kind of response is an abnormal response. In an abnormal response, the status code of `HTTP` is `4xx` or `5xx`.

You can troubleshoot issues based on `Code` and `Message`. For details, refer to Common error codes and API error codes.

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


In contrast to a normal response, in an abnormal response, the `Result` field is no longer contained, and the `Error` field is unexpectedly added to `ResponseMetadata`. The following table describes the fields:


|Field |Description |
|---|---|
|Error |Indicates that the request failed. |
|Code |Indicates the error code. You can troubleshoot issues by referring to error code documents. |
|Message |Indicates the reason why the error occurred. It gives a reference for your troubleshooting. |
|RequestID |Indicates the unique ID of the API request. If you cannot solve a problem, use the ticket system to contact us and give the RequestID of your request. We can help you troubleshoot the problem. |
