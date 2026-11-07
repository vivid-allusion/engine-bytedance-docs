---
title: "Response"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Response_result"
---

All responses from the  OpenAPI include fields such as RequestId, Action, Version, Service, and Region.

<span id="fBmgImEf"></span>
## Normal sample responses

A request ID and response parameters will be returned if the API is called successfully. HTTP status code is 2xx.

```json
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


When requests are processed as expected, the response contains two parts: **ResponseMetadata** and **Result**. The **Result** depends on the requested API, and different APIs return different **Result**. The fields are explained as follows:


|Field |Explanation |
|---|---|
|RequestID |This is the unique identifier for each API request. |
|Action |The requested API name is a common request parameter. |
|Version |The request version number is a common request parameter. |
|Service |The requested service is a common request parameter. |
|Region |The requested region is a common request parameter. For more information about Region, see [Service regions](https://docs.byteplus.com/en/docs/apmplus/server-launching_region). |


<span id="cAUPSpEj"></span>
## Error sample responses

A request ID and error message will be returned if errors occur when calling the API. HTTP status code is 4xx or 5xx.

You can troubleshoot by using the API error code and messages, referring to the [Public error code](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) and specific API error codes.

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
            "Message": "Could not find operation GetUserById for version 2018-01-01"
        }
    }
}
```
