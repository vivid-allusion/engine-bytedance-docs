---
title: "DeleteComponentStep"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/DeleteComponentStep"
---

Delete custom steps.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the Region where your resources are located. For details, see [Service addresses](https://docs.byteplus.com/en/docs/cp/Service_Addresses).


* Request method: POST

* Request URL: https://cp.ap\-southeast\-1.byteplusapi.com.cn?Action=DeleteComponentStep&Version=2023\-05\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |DeleteComponentStep |The API name. The current API is named `DeleteComponentStep`. |
|Version |String |Yes |2023\-05\-01 |The API version. The current version of the API is `2023-05-01`. |
|Identifier |String |Yes |custom@1.0.0/\*\*\*\* |Unique identifier for custom steps. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cp.ap-southeast-1.byteplusapi.com.cn?Action=DeleteComponentStep&Version=2023-05-01 HTTP/1.1
Content-Type: application/json
{
    "Identifier": "custom@1.0.0/****"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This interface has no unique return parameters.

<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "202404071710430739950998FB2847****",
        "Action": "DeleteComponentStep",
        "Version": "2023-05-01",
        "Service": "cp",
        "Region": "ap-southeast-1"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This API does not currently have dedicated error codes. If an exception occurs when calling the API, refer to [public error codes](https://docs.byteplus.com/en/docs/cp/Public_error_codes) for troubleshooting.
