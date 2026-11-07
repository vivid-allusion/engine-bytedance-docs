---
title: "Response result"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Response"
---

After you call the APIs of BytePlus, all response results will include fields, such as RequestId, Action, Version, Service, and Region.

<span id=".5q2j5bi46L-U5Zue56S65L6L"></span>
## Sample success responses

After an API is called, the request ID and the API response parameters will be returned. The HTTP status code is 2xx.

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


After the request is processed as expected, the response result will include two parts: **ResponseMetadata** and **Result**. The **Result** varies based on the different APIs. The following table describes fields.


|Parameter |Description |
|---|---|
|RequestID |The unique identifier for each API request. |
|Action |The name of the API, which is a public parameter of the request. |
|Version |The version number, which is a public parameter of the request. |
|Service |The requested service, which is a public parameter of the request. |
|Region |The region, which is a public parameter of the request. For more information about regions, see [Regions and availability zones](https://docs.byteplus.com/en/docs/vke/Regions-and-Availability-Zones). |


<span id=".5byC5bi46L-U5Zue56S65L6L"></span>
## Sample error responses

If an error occurs when you call an API, the request ID and an error message will be returned. The HTTP status code is 4xx or 5xx. You can troubleshoot based on the API error code and error message. For detailed information, see [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes) and Error code documentation for the specific API.

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
