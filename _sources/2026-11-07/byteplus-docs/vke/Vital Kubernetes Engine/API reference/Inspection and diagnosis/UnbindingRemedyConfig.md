---
title: "UnbindingRemedyConfig"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/unbindingremedyconfig"
---

Disassociates a self\-healing rule from a resource.

## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. See [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) and select the most suitable endpoint for the region where your business operates.

* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=UnbindingRemedyConfig&Version=2022\-05\-12

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=UnbindingRemedyConfig&serviceCode=vke&version=2022-05-12&groupName=)

## Request parameters

The following table describes the API request parameters. You also need to provide public parameters when calling this API. For details about public request parameters, see [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters).

|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |UnbindingRemedyConfig |The API name. The API name is `UnbindingRemedyConfig`. |
|Version |String |Yes |May 12, 2022 |The API version. The API version is `2022-05-12`. |
|ClusterId |String |Yes |cda5\*\*\*\*\* |Cluster ID.<br><br>You can call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to obtain cluster IDs. |
|Id |String |Yes |R202609\*\*\*\*\* |The ID of the check and self\-healing rule. |
|ResourceType |String |Yes |VkeNodePool |The resource type for which you want to disassociate a self\-healing rule. Only VkeNodePool is supported. |
|ResourceIds |Array of String |Yes |["pc51i0\*\*\*\*\*"] |The ID of the node pool for which you want to disassociate the self\-healing configuration.<br><br>You can call the [ListNodePools](https://docs.byteplus.com/en/docs/vke/ListNodePools?lang=en) API to obtain node pool IDs. |

## Sample requests

```JSON
POST https://vke.cn-beijing.byteplusapi.com.cn?Action=UnbindingRemedyConfig&Version=2022-05-12
Content-Type: application/json
{
    "ClusterId": "cda5*****",
    "Id": "R202609*****",
    "ResourceType": null,
    "ResourceIds": [
        "pc51i0*****"
    ]
}
```

## Response parameter

This API has no API\-specific response parameters. For details about common response parameters, see [Response results](https://docs.byteplus.com/en/docs/vke/Response).

## Sample responses

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UnbindingRemedyConfig",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    }
}
```

## Error code

This API has no API\-specific error codes. For details about common error codes, see [Common error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes).
