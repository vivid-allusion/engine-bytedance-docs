---
title: "RevokePermission"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/RevokePermission"
---

Revoke the RBAC permission granted to an IAM user or role by specifying the resource ID of the permission policy.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point for your business region.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=RevokePermission&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=RevokePermission&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table contains the API request parameters. You also need to provide public parameters when calling this API. See [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters) for details.


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |RevokePermission |The API name. The API name is `RevokePermission `. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Id |String |Yes |ap\*\*\*\*\*\*\*\* |The ID of the RBAC policy. |


&nbsp;


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |RevokePermission |The API name. The API name is `RevokePermission `. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Id |String |Yes |ap\*\*\*\*\*\*\*\* |The ID of the RBAC policy. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST /?Action=RevokePermission&Version=2022-05-12 HTTP/1.1
Content-Type: application/json
{
    "Id": "ap********"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

There are no response parameters proprietary to this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.

<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420********",
        "Action": "RevokePermission",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no error codes proprietary to this API. See [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes) for details.

&nbsp;
