---
title: "DeleteServiceConnection"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/DeleteServiceConnection"
---

Delete service connection

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the region where your resources are located. For details, refer to [service address](https://docs.byteplus.com/en/docs/cp/Service_Addresses).


* Request method: POST

* Request URL: https://cp.ap\-southeast\-1.byteplusapi.com.cn?Action=DeleteServiceConnection&Version=2023\-05\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Ye |DeleteServiceConnection |The API name. The name of the current API is `DeleteServiceConnection`. |
|Version |String |Ye |2023\-05\-01 |The API version. The current version of the API is `2023-05-01`. |
|Id |String |Ye |my_svc_\*\*\*\* |Service connection ID. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cp.ap-southeast-1.byteplusapi.com.cn?Action=DeleteServiceConnection&Version=2023-05-01 HTTP/1.1
Content-Type: application/json
{
    "Id": "my_svc_****"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This interface has no unique response parameters.

<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20250916181546A268B606D03ECAD5****",
        "Action": "DeleteServiceConnection",
        "Version": "2023-05-01",
        "Service": "cp",
        "Region": "ap-southeast-1"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The current interface currently does not have independent error codes. If an exception occurs when calling the interface, you can refer to the [public error codes](https://docs.byteplus.com/en/docs/cp/Public_error_codes) for troubleshooting.
