---
title: "ScaleNodePool"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/ScaleNodePool"
---

Scale out the specified node pool.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This OpenAPI interface can only scale out nodes in the specified node pool and does not support scaling in nodes. To scale in nodes, use the <a href="https://docs.byteplus.com/en/docs/vke/UpdateNodePoolConfig">UpdateNodePoolConfig</a> or <a href="https://docs.byteplus.com/en/docs/vke/DeleteNodes">DeleteNodes</a> API.</div>


<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point for your business region.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=ScaleNodePool&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ScaleNodePool&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table describes the API request parameters. You also need to provide public parameters when calling this API. See [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters) for details.


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ScaleNodePool |The API name. The API name is `ScaleNodePool`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|ClusterId |String |Yes |cc5silu\*\*\*\*\*\*\* |The ID of the cluster where the node pool is located.<br><br>Cluster IDs can be obtained by calling the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The cluster must be in the <code>{Running,[Ok]}</code> or <code>{Updating,[Progressing]}</code> state. You can call the <a href="https://docs.byteplus.com/en/docs/vke/ListClusters">ListClusters</a> API to view the current status of the cluster.</div><br> |
|Id |String |Yes |pc51i0\*\*\*\*\*\*\* |The node pool ID.<br><br>You can call the [ListNodePools](https://docs.byteplus.com/en/docs/vke/ListNodePools) API to obtain the node pool ID.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The node pool must be in the <code>{Running,[*]}</code> or <code>{Scaling,[Progressing]}</code> state. You can call the <a href="https://docs.byteplus.com/en/docs/vke/ListNodePools">ListNodePools</a> API to obtain the current status of the node pool.</div><br> |
|Count |Integer |Yes |2 |Number of nodes to scale out. The value must be an integer greater than 0.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The maximum value of this parameter depends on the desired node count configuration for the node pool.</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The sum of the ‌desired node count (<code>DesiredReplicas‌</code>) and scale\-out node count (‌<code>Count‌</code>) for a node pool must not exceed the maximum node count (2,000) of the node pool.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When autoscaling is enabled for the node pool, the total node count after scaling must not exceed the ‌value of the <code>MaxReplicas‌</code> parameter.</div><br><br><br>* <div data-tips="true" data-tips-type="default">For information about how to configure <code>DesiredReplicas</code> and <code>MaxReplicas</code>, see <a href="https://docs.byteplus.com/en/docs/vke/CreateNodePool">CreateNodePool</a>.</div><br> |
|ClientToken |String |No |BC028527\-33\*\*\* |A string used to ensure the idempotency of the request. This string is passed in by the caller and must be unique across different requests. ClientToken is case\-sensitive and can consist of 64 ASCII characters at most. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST https://vke.cn-beijing.byteplusapi.com.cn?Action=ScaleNodePool&Version=2022-05-12
Content-Type: application/json
{
    "ClusterId": "cc5silu*******",
    "Id": "pc51i0*******",
    "Count": 2,
    "ClientToken": "BC028527-33***"
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
        "Action": "ScaleNodePool",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for this API are listed in the table below. For public error codes, see [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes).


|**HTTP status code** |**Error code** |**Error message** |**Description** |
|---|---|---|---|
|400 |OperationDenied.ClusterStatus |The action is forbidden due to cluster status {{statusPhase}} and {{statusConditions}}. |The current status of the specified cluster does not support this operation. Please confirm the required cluster status for this API and try again. |
|400 |OperationDenied.NodePoolStatus |The action is forbidden on node pool {{nodePoolId}} due to node pool status {{statusPhase}} and {{statusConditions}}. |The current status of the specified node pool does not support this operation. Please confirm the required node pool status for this API and try again. |
|400 |Mismatch.Replicas |The specified DesiredReplicas, MinReplicas and MaxReplicas are mismatched. |The specified minimum, maximum, and desired number of nodes​ in the node pool are logically inconsistent. Check the parameter and try again. |
|400 |QuotaExceeded.Node |The number of nodes in the cluster has reached the limit. |The number of nodes in the current cluster has reached the limit. You can select another region or [submit a ticket](https://console.byteplus.com/ticket/createTicketV2/?step=2&Service=vke) to apply for a quota increase. |
|400 |LimitExceeded.NodeInCluster |The number of nodes exceeds the cluster\-defined pods config limit. |The maximum nodes specified for the node pool exceeds the maximum nodes supported by the Flannel cluster. For limits on various resources of VKE, see [Resource limits](https://docs.byteplus.com/en/docs/vke/Limits).<br><br>The supported maximum nodes depend on **PodsConfig.FlannelConfig.PodCidrs** and **MaxPodsPerNode**. After a cluster is created, it cannot be modified. You need to plan cluster settings based on your business requirements. |
|400 |UpdateNotAllowed.{{parameter}} |The update to the specified parameter {{parameter}} is not allowed due to {{resourceType}}. |Certain attributes of the specified object cannot be updated due to its resource type. |
|400 |QuotaExceeded.{{ResourceType}} |The quota of {{ResourceType}} has reached the limit. |The quota for the specified resource (such as EIP or EBS) has reached its upper limit. Increase the relevant resource quota or delete unused resources. When the available quota is sufficient, try again later. |
|400 |Insufficient.Balance |Your account has run out of balance. |The balance of the current account is insufficient. Top up your account and try again. |
