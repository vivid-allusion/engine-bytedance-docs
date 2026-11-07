---
title: "UntagResources"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/UntagResources"
---

Delete resource labels.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide, aiming to provide you with an experience of higher stability and lower latency. You can choose an access point that is the most optimal for the region of your services according to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) document.


* Request method: POST

* Request address: https://vmp.cn\-beijing.byteplusapi.com.cn/?Action=UntagResources&Version=2021\-03\-03


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Types |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |UntagResources |API name. The API name is `UntagResources`. |
|Version |String |Yes |2021\-03\-03 |API version. The API version is `2021-03-03`. |
|ResourceType |String |Yes |Workspace |The resource type for which labels need to be deleted. ` Workspace` is the only supported type. |
|ResourceIds |Array of String |No |["e28ae750\-bbb8\-4ff4\-abf4\-1e0e0f88808c"] |A list of resource IDs of which the labels need to be deleted. |
|TagKeys |Array of String |Yes |["doc"] |The label keys to be deleted. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vmp.cn-beijing.byteplusapi.com.cn/?Action=UntagResources&Version=2021-03-03
Content-Type: application/json
{
    "ResourceType": "Workspace",
    "ResourceIds": [
        "e28ae750-bbb8-4ff4-abf4-1e0e0f88808c"
    ],
    "TagKeys": [
        "doc"
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters none

<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UntagResources",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The error codes for current API only are listed in the table below. See [ Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes) to view error codes for any APIs.


|HTTP status codes |Error codes |Error messages |Description |
|---|---|---|---|
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The account is not subscribed to the VMP Service. |
|400 |InvalidParameter.{{parameter}} |The specified parameter {{parameter}} is invalid. |An invalid parameter was found. For example, an invalid workspace name was included in requests. |
|400 |MissingParameter.{{parameter}} |The required parameter {{parameter}} is missing. |Missing required parameters. |
