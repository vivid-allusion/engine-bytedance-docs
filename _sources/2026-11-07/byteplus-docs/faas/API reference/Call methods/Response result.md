---
title: "Response result"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Response_result"
---

After calling BytePlus OpenAPI, all response results will carry the RequestId, Action, Version, Service, Region, and other fields.

<span id="正常返回示例"></span>
## Normal sample response

After the sample interface which returns normally is successfully called, a request ID will return and the parameters will return from the interface. The HTTP status code is 2xx.

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


After the request is normally processed, the response will include **ResponseMetadata** and **Result** two parts. The **Result** is subject to the interface requested, and different interfaces will have different **Result** responses. The fields are explained as follows:


|Field |Explanation |
|---|---|
|RequestID |A unique identifier for each API request. |
|Action |The name of the interface requested is a public parameter of the request. |
|Version |The version number requested is a public parameter of the request. |
|Service |The service requested is a public parameter of the request. |
|Region |The region requested is a public parameter of the request. For more information about regions, refer to [Server-launching region](https://docs.byteplus.com/en/docs/faas/Regions_and_availability_zones). |


<span id="异常返回示例"></span>
## Abnormal sample response 

When an interface call fails, the request ID and error message are returned. The HTTP status code is 4xx or 5xx. You can troubleshoot according to the error code and the error message of the interface, while referring to [Public error code](https://docs.byteplus.com/en/docs/faas/Public_error_code) and specific interface error code.

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
