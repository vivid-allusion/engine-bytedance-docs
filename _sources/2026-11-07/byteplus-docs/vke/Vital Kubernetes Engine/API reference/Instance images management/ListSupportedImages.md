---
title: "ListSupportedImages"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/ListSupportedImages"
---

Obtain the list of images supported by ECS instance specifications that correspond to nodes.

<span id=".5o6l5Y-j6K-05piO"></span>
## API description


* Only Kubernetes clusters v1.30 and later versions support nodes that use veLinux 2.0 or Ubuntu 22.x series images.

* veLinux 2.0 and Ubuntu 22.x series images use cgroup v2 by default.


<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point for your business region.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=ListSupportedImages&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListSupportedImages&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table describes the API request parameters. You also need to provide public parameters when calling this API. See [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters) for details.


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListSupportedImages |The API name. The name of the current API is `ListSupportedImages`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|InstanceTypeIds |Array of String |Yes |["ecs.g1ie.large"] |The IDs of the ECS instance specifications that correspond to nodes. You can call the [ListNodePools](https://docs.byteplus.com/en/docs/vke/ListNodePools) API to obtain the instance specification IDs. You can specify up to 10 instance specification IDs at a time. |
|Intersection |Boolean |No |true |Whether to obtain the image intersection. Valid values:<br><br><br>* **true**: Returns images supported by ‌all selected instance specifications‌.<br><br>* **false**: (Default) Returns images supported by the ‌specified instance specification‌. |
|KubernetesVersion |String |No |v1.28.3\-vke.1 |The Kubernetes version of the cluster. You can obtain the list of supported images based on the instance specification and Kubernetes version. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vke.cn-beijing.byteplusapi.com.cn?Action=ListSupportedImages&Version=2022-05-12
Content-Type: application/json
{
    "InstanceTypeIds": [
        "ecs.g1ie.**.**.**.**.**.**",
        "ecs.g3ilt.**.**.**.**.**.**"
    ],
    "Intersection": false,
    "KubernetesVersion": "v1.28.3-vke.1"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following table contains the response parameters of this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Items |Array of [SupportedImagesResponse](https://docs.byteplus.com/en/docs/90/75639#supportedimagesresponse) |\- |The list of returned image information. |
|IntersectionItems |Array of [ImageResponse](https://docs.byteplus.com/en/docs/90/75639#imageresponse) |\- |The image intersection list. |


<span id="supportedimagesresponse"></span>
### SupportedImagesResponse


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|InstanceTypeId |String |ecs.g1i\*\*\*\*\*\*\* |The ID of the node specification. |
|SupportedImages |Array of [ImageResponse](https://docs.byteplus.com/en/docs/90/75639#imageresponse) |\- |The list of images supported by instance specifications that correspond to nodes. |


<span id="imageresponse"></span>
### ImageResponse


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|ImageId |String |img\-1\*\*\*\*\*\* |The image ID. |
|ImageName |String |ubuntu\-20.04 |Image name. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104********",
        "Action": "ListSupportedImages",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {
        "Items": [
            {
                "InstanceTypeId": "ecs.g1i*******",
                "SupportedImages": [
                    {
                        "ImageId": "img-1*****",
                        "ImageName": "ubuntu-20.04"
                    },
                    {
                        "ImageId": "img-3*****",
                        "ImageName": "ubuntu-20.04"
                    }
                ]
            },
            {
                "InstanceTypeId": "ecs.g3i********",
                "SupportedImages": [
                    {
                        "ImageId": "img-3*****",
                        "ImageName": "ubuntu-20.04"
                    }
                ]
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no proprietary error codes for this API. See [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes) for details about public error codes.
