---
title: "UpdateTagDescription"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/UpdateTagDescription"
---

Update image tag description.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended to select the corresponding service address based on the region where your resources are located. For details, see [service address](https://docs.byteplus.com/en/docs/cr/Service_address).


* Request method: POST

* Request address: https://cr.ap\-sourtheast\-1.byteplusapi.com.cn?Action=UpdateTagDescription&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=UpdateTagDescription&serviceCode=cr&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

When calling this API, in addition to the following request parameters, you also need to provide the public request parameters. See [Public parameters](https://docs.byteplus.com/en/docs/cr/common-parameters) for details.


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |UpdateTagDescription |The API name. The current API name is `UpdateTagDescription`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Registry |String |Yes |registry\-prod\-1 |Name of the CR instance whose image tag description is to be updated. |
|Namespace |String |Yes |app\-backend |Name of the target namespace where the image tag description to be updated is located. |
|Repository |String |Yes |user\-service |Name of the artifact repository where the image tag description to be updated is located. |
|Name |String |Yes |v2.0.0 |Name of the image tag (Tag) whose description is to be updated. |
|Description |String |No |stable release with performance improvements and security patches |Description content of the image tag (Tag) to be updated. An empty string is allowed. The default value is `""`. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST https://cr.ap-sourtheast-1.byteplusapi.com.cn?Action=UpdateTagDescription&Version=2022-05-12
{
    "Registry": "registry-prod-1",
    "Namespace": "app-backend",
    "Repository": "user-service",
    "Name": "v2.0.0",
    "Description": "stable release with performance improvements and security patches"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

None

<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateTagDescription",
        "Version": "2022-05-12",
        "Service": "cr",
        "Region": "ap-sourtheast-1"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This interface has no specific error codes. For public error codes, please refer to the [Public error codes](https://docs.byteplus.com/en/docs/cr/common-error-codes) documentation.
