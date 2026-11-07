---
title: "ListSupportedGpuDriverVersions"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/ListSupportedGpuDriverVersions"
---

Obtain a list of GPU driver versions supported by the image.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point for your business region.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=ListSupportedGpuDriverVersions&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListSupportedGpuDriverVersions&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table contains the request parameters for the API. You also need to provide public parameters when calling this API.  See [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters) for details.


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListSupportedGpuDriverVersions |The API name. The name of the current API is `ListSupportedGpuDriverVersions`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|ImageId |String |Yes |image\-ybqi99s7yq\*\*\* |ID of the image used by the ECS instance.<br><br>Image IDs vary based on different types of images. For details, see [Public images supported by VKE](https://docs.byteplus.com/en/docs/vke/Overview-of-operating-system-images#.5a655Zmo5pyN5Yqh5pSv5oyB55qE5YWs5YWx6ZWc5YOP). |
|InstanceTypeIds |Array of String |no |["ecs.gni3cg.5xlarge"] |Instance specification IDs. You can enter up to 100 elements. |
|InstanceTypeFamilies |Array of String |no |["ecs.gni3cg"] |The instance families of the instance specifications. You can enter up to 10 elements. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST https://vke.cn-beijing.byteplusapi.com.cn?Action=ListSupportedGpuDriverVersions&Version=2022-05-12
Content-Type: application/json
{
    "ImageId": "image-ybqi99s7yq***",
    "InstanceTypeIds": [
        "ecs.gni3cg.5xlarge"
    ],
    "InstanceTypeFamilies": [
        "ecs.gni3cg"
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following table contains the response parameters of this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|GpuDriverVersions |Array of String |["535.216.03"] |The GPU driver versions that can be installed for the specifications of the instances that serve as nodes. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListSupportedGpuDriverVersions",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {
        "GpuDriverVersions": [
            "535.216.03"
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no proprietary error codes for this API. See [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes) for details about public error codes.
