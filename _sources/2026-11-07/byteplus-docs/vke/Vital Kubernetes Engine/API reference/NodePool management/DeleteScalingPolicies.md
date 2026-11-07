---
title: "DeleteScalingPolicies"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/DeleteScalingPolicies"
---

Delete the elastic scheduled scaling rules of a node pool.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point for your business region.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=DeleteScalingPolicies&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteScalingPolicies&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table contains the request parameters for the API. You also need to provide public parameters when calling this API.  See [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters) for details.


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |DeleteScalingPolicies |The API name. The name of the current API is `DeleteScalingPolicies`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|ClusterId |String |Yes |cc5silumrsfeqxxxx |Cluster ID.<br><br>Cluster IDs can be queried by calling the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The cluster must be in the <code>{Running,[Ok]}</code> or <code>{Updating,[Progressing]}</code> state. You can call the <a href="https://docs.byteplus.com/en/docs/vke/ListClusters">ListClusters</a> API to obtain the current status of the cluster.</div><br> |
|NodePoolId |String |Yes |pc51i0m6rsfenxxxx |Node pool ID.<br><br><div data-tips="true" data-tips-type="warning">Note</div><br><br><br><div data-tips="true" data-tips-type="warning">The node pool must be in the <code>{Running,[*]}</code> state. You can call the <a href="https://docs.byteplus.com/en/docs/vke/ListNodePools">ListNodePools</a> API to obtain the current status of the node pool.</div><br> |
|Ids |Array of String |Yes |["spco2o8q2nvp211bm\*\*\*"] |A list of scaling policy IDs. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST https://open.volcengineapi.com/?Action=DeleteScalingPolicies&Version=2022-05-12
Content-Type: application/json
{
    "ClusterId": "cc5silumrsfeqxxxx",
    "NodePoolId": "pc51i0m6rsfenxxxx",
    "Ids": [
        "spco2o8q2nvp211bm***"
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

There are no proprietary response parameters for this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.

<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteScalingPolicies",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for this API are listed in the table below. Refer to the [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes) topic for details.


|**HTTP status code** |**Error code** |**Error message** |**Description** |
|---|---|---|---|
|400 |OperationDenied.ClusterStatus |The action has been denied due to wrong cluster status {{statusPhase}} and [{{statusConditions}}]. |The current status of the specified cluster does not support this operation. Please confirm the required cluster status for this API and try again. |
|400 |OperationDenied.NodePoolStatus |The action has been forbidden due to wrong node pool status {{statusPhase}} and [{{statusConditions}}]. |The current status of the specified node pool does not support this operation. Please confirm the required node pool status for this API and try again. |
