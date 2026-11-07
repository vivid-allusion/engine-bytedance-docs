---
title: "CreateKubernetesObservability"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/CreateKubernetesObservability"
---

Enables basic observability for a cluster.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. See [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) and select the most suitable endpoint for the region where your business operates.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=CreateKubernetesObservability&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateKubernetesObservability&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table describes the API request parameters. You also need to provide public parameters when calling this API. For details about public request parameters, see [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters).


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |CreateKubernetesObservability |The API name. The API name is `CreateKubernetesObservability`. |
|Version |String |Yes |May 12, 2022 |The API version. The current version of the API is `2022-05-12`. |
|ClusterId |String |Yes |ccbm7\*\*\*\* |Cluster ID.<br><br>You can call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to obtain cluster IDs. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST https://vke.cn-beijing.byteplusapi.com.cn?Action=CreateKubernetesObservability&Version=2022-05-12
Content-Type: application/json
{
    "ClusterId": "ccbm7****"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

This API has no API\-specific response parameters. For details about common response parameters, see [Response results](https://docs.byteplus.com/en/docs/vke/Response).

<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateKubernetesObservability",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This API has no API\-specific error codes. For details about common error codes, see [Common error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes).
