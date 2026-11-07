---
title: "BindingRemedyConfig"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/bindingremedyconfig"
---

Binds a self\-healing specification to a resource.

## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. See [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) and select the most suitable endpoint for the region where your business operates.

* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=BindingRemedyConfig&Version=2022\-05\-12

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=BindingRemedyConfig&serviceCode=vke&version=2022-05-12&groupName=)

## Request parameters

The following table describes the API request parameters. You also need to provide public parameters when calling this API. For details about public request parameters, see [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters).

|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |BindingRemedyConfig |The API name. The API name is `BindingRemedyConfig`. |
|Version |String |Yes |May 12, 2022 |The API version. The API version is `2022-05-12`. |
|ClusterId |String |Yes |cda5\*\*\*\*\* |Cluster ID.<br><br>You can call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to obtain cluster IDs. |
|Id |String |No |R202609\*\*\*\*\* |The ID of the check and self\-healing rule.<br><br>> **tip**<br><br><br>> This parameter is not required when you use the recommended self\-healing configuration.<br> |
|UseRecommendedRemedyConfigs |Boolean |No |false |Whether to use the recommended self\-healing configuration. Valid values:<br><br><br>* **true**: Use.<br><br>* **false**: Do not use. |
|ResourceType |Integer |Yes |VkeNodePool |The bound resource type. Currently, only VkeNodePool is supported. |
|ResourceIds |Array of String |Yes |["pc51i0\*\*\*\*\*"] |The node pool ID.<br><br>You can call the [ListNodePools](https://docs.byteplus.com/en/docs/vke/ListNodePools?lang=en) API to obtain the node pool ID. |
|ClientToken |String |No |BC028527\-33B9\-4990\-A633\-84E9F9\*\*\*\*\* |A string used to ensure the idempotency of the request. This string is passed in by the caller and must be unique across different requests. ClientToken is case\-sensitive and can consist of 64 ASCII characters at most. |

## Sample requests

```JSON
POST https://vke.cn-beijing.byteplusapi.com.cn?Action=BindingRemedyConfig&Version=2022-05-12
Content-Type: application/json
{
    "ClusterId": "cda5*****",
    "Id": "R202609*****",
    "UseRecommendedRemedyConfigs": false,
    "ResourceType": null,
    "ResourceIds": [
        "pc51i0*****"
    ],
    "ClientToken": "BC028527-33B9-4990-A633-84E9F9*****"
}
```

## Response parameter

The following table contains the response parameters of this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |R202609\*\*\*\*\* |The ID of the bound self\-healing configuration. |

## Sample responses

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420**********",
        "Action": "BindingRemedyConfig",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {
        "Id": "R202609*****"
    }
}
```

## Error code

This API has no API\-specific error codes. For details about common error codes, see [Common error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes).
