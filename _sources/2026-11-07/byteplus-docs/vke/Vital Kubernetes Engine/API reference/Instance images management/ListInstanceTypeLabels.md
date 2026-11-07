---
title: "ListInstanceTypeLabels"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/ListInstanceTypeLabels"
---

Obtain the list of labels supported by ECS instance specifications that correspond to nodes.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point for your business region.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=ListInstanceTypeLabels&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListInstanceTypeLabels&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table contains the API request parameters. You also need to provide public parameters when calling this API. See [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters) for details.


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListInstanceTypeLabels |The API name. The name of the current API is `ListInstanceTypeLabels`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|InstanceTypeIds |Array of String |no |["ecs.g1ie.large"] |The IDs of the ECS instance specifications that correspond to nodes. You can call the [ListNodePools](https://docs.byteplus.com/en/docs/vke/ListNodePools) API to obtain the instance specification IDs. You can specify up to 10 instance specification IDs at a time. |


&nbsp;


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListInstanceTypeLabels |The API name. The name of the current API is `ListInstanceTypeLabels`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|InstanceTypeIds |Array of String |no |["ecs.g1ie.large"] |The IDs of the ECS instance specifications that correspond to nodes. You can call the [ListNodePools](https://docs.byteplus.com/en/docs/vke/ListNodePools) API to obtain the instance specification IDs. You can specify up to 10 instance specification IDs at a time. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST /?Action=ListInstanceTypeLabels&Version=2022-05-12 HTTP/1.1
Content-Type: application/json
{
    "InstanceTypeIds": [
        "ecs.g1ie.large"
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following table contains the response parameters of this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Items |Array of [InstanceTypeLabelResponse](https://docs.byteplus.com/en/docs/90/75640#instancetypelabelresponse) |\- |The list of returned label information. |


<span id="instancetypelabelresponse"></span>
### InstanceTypeLabelResponse


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Labels |Array of [Label](https://docs.byteplus.com/en/docs/90/75640#label) |\- |The list of labels supported by instance specifications that correspond to nodes. |
|InstanceType |String |ecs.g1ie |The instance family. |
|InstanceTypeId |String |ecs.g1ie.large |The instance specification ID. |


<span id="label"></span>
### Label


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Key |String |label\-key |The label key. |
|Value |String |label\-value |The label value. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420**********",
        "Action": "ListInstanceTypeLabels",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {
        "Items": [
            {
                "Labels": [
                    {
                        "Key": "label-key",
                        "Value": "label-value"
                    }
                ],
                "InstanceType": "ecs.g1ie",
                "InstanceTypeId": "ecs.g1ie.large"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no proprietary error codes for this API. See [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes) for details about public error codes.
