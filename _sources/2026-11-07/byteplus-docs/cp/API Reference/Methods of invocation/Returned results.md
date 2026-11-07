---
title: "Returned results"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Returned_results"
---

After calling the OpenAPI, all response results will include the RequestId, Action, Version, Service, Region, and many other fields.

<span id=".5q2j5bi46L-U5Zue56S65L6L"></span>
## Normal Sample Response

After a successful API call, the request ID and response parameters are returned. HTTP status code is 2xx.

```json
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


After the request is successfully processed, the back will contain two parts: **ResponseMetadata** and **Result**. The **Result** depends on the API being called; different APIs will return different **Result** in the back. Field descriptions


|field |Explanation |
|---|---|
|RequestID |Unique identifier for each API request. |
|Action |The interface name is a common parameter in requests. |
|Version |The version number is a common parameter in requests. |
|Service |The requested service is one of the common parameters in a request. |
|Region Code |Region is a common parameter required in requests. |


<span id=".5byC5bi46L-U5Zue56S65L6L"></span>
## Exceptional Sample Response

When an interface call fails, it returns the request ID and error information. The HTTP status code is 4xx or 5xx.

You can use the interface error code (Code) and error message (Message), and refer to [general error codes](https://docs.byteplus.com/en/docs/cp/Public_error_codes) and specific interface error codes to troubleshoot errors.

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
            "Message": "Could not find operation ListPipelines for version 2023-05-01"
        }
    }
}
```
