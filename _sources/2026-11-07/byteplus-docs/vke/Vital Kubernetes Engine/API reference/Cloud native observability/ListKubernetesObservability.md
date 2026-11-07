---
title: "ListKubernetesObservability"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/ListKubernetesObservability"
---

Queries whether basic observability is enabled for a cluster.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. See [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) and select the most suitable endpoint for the region where your business operates.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=ListKubernetesObservability&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListKubernetesObservability&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table describes the API request parameters. You also need to provide public parameters when calling this API. For details about public request parameters, see [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters).


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListKubernetesObservability |The API name. The API name is `ListKubernetesObservability`. |
|Version |String |Yes |May 12, 2022 |The API version. The API version is `2022-05-12`. |
|Filter |Object of [ClusterFilter](https://docs.byteplus.com/en/docs/90/121826#clusterfilter) |Yes |\- |The query filters. |
|PageNumber |Integer |No |1 |The starting page number for paginated queries. The value starts at 1 and defaults to 1. |
|PageSize |Integer |No |10 |The number of results per page:<br><br><br>* Minimum value: 1<br><br>* Maximum value: 100<br><br>* Default value: 10 |


<span id="clusterfilter"></span>
### ClusterFilter


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|ClusterIds |Array of String |No |["ccbm7\*\*\*\*", "ccdhm\*\*\*\*"] |Cluster ID.<br><br>You can call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to obtain cluster IDs. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST https://vke.cn-beijing.byteplusapi.com.cn?Action=ListKubernetesObservability&Version=2022-05-12
Content-Type: application/json
{
    "Filter": {
        "ClusterIds": [
            "ccbm7****",
            "ccdhm****"
        ]
    },
    "PageNumber": 1,
    "PageSize": 10
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

The following table contains the response parameters of this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Items |Array of [KubernetesObservabilityConfig](https://docs.byteplus.com/en/docs/90/121826#kubernetesobservabilityconfig) |\- |The cluster observability configuration. |
|PageNumber |Integer |1 |The current page number. |
|PageSize |Integer |10 |Number of tasks displayed per page. |
|TotalCount |Integer |2 |The total number of data entries that match the query conditions. |


<span id="kubernetesobservabilityconfig"></span>
### KubernetesObservabilityConfig


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Enabled |Boolean |true |Whether basic observability is enabled for the cluster. Valid values:<br><br><br>* **true**: Yes<br><br>* **false**: No |
|ClusterId |String |ccbm7\*\*\*\* |Cluster ID. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420**********",
        "Action": "ListKubernetesObservability",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {
        "Items": [
            {
                "Enabled": true,
                "ClusterId": "ccbm*****"
            }
        ],
        "PageNumber": 1,
        "PageSize": 10,
        "TotalCount": 2
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no error codes proprietary to this API. See [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes) for details about public error codes.
