---
title: "DeleteObjectGroup"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/DeleteObjectGroup"
---

Delete the specified object group.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits

An object group with an associated alert template cannot be deleted. To delete the object group, you must first disassociate the alert template from the object group.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=DeleteObjectGroup&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteObjectGroup&serviceCode=Volc_Observe&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |DeleteObjectGroup |The API name. The API name is `DeleteObjectGroup`. |
|Version |String |Yes |2018\-01\-01 |The API version. The API version is `2018-01-01`. |
|Id |String |No |1764547228734\*\*\*\*\*\* |Object group ID. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=DeleteObjectGroup&Version=2018-01-01
Content-Type: application/json
{
    "Id": "1764547228734******"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Data |String |1764547228734\*\*\*\*\*\* |Object group ID. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20240304152908454D22F975D29B******",
        "Action": "DeleteObjectGroup",
        "Version": "2018-01-01",
        "Service": "cloudmonitor",
        "Region": "cn-beijing"
    },
    "Result": {
        "Data": "1764547228734******"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This API has no error codes unique to itself. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).

&nbsp;
