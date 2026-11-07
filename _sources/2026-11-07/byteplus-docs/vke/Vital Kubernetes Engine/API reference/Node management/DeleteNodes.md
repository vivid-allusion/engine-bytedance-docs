---
title: "DeleteNodes"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/DeleteNodes"
---

Delete one or more nodes from the cluster.

<span id=".5L2_55So6K-05piO"></span>
## Usage instructions

This is an asynchronous API. When this API returns a success message, the node will be in the `{Deleting, [Progressing]}` state. However, the return of a success message does not indicate that the node will be deleted ultimately. You need to call the [ListNodes](https://docs.byteplus.com/en/docs/vke/ListNodes) API to check whether the node exists. If the node cannot be found, it has been deleted successfully.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point based on the region where your business is located.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=DeleteNodes&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteNodes&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameter

The following table describes the API request parameters. You also need to provide public parameters when calling this API. For details about public request parameters, see [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters).


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |DeleteNodes |The API name. The name of the current API is `DeleteNodes`. |
|Version |String |Yes |May 12, 2022 |The API version. The API version is `2022-05-12`. |
|ClusterId |String |Yes |cc5sil\*\*\*\*\*\* |Cluster ID.<br><br>You can call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to obtain cluster IDs.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The cluster must be in one of the following states:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning"><code>{Running,[*]}</code></div><br><br><br>* <div data-tips="true" data-tips-type="warning"><code>{Updating, [Progressing]}</code></div><br><br><br>* <div data-tips="true" data-tips-type="warning"><code>{Stopped, [Balance]}</code></div><br><br><br>   <div data-tips="true" data-tips-type="warning">You can call the <a href="https://docs.byteplus.com/en/docs/vke/ListClusters">ListClusters</a> API to obtain the current status of the cluster.   </div><br>    |
|NodePoolId |String |No |pc8oah9\*\*\*\*\*\*\*\* |The node pool ID.<br><br>You can call the [ListNodePools](https://docs.byteplus.com/en/docs/vke/ListNodePools) API to obtain the node pool ID.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The node pool must be in one of the following states:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning"><code>{Running,[*]}</code></div><br><br><br>* <div data-tips="true" data-tips-type="warning"><code>{Scaling,[Progressing]}</code></div><br><br><br>* <div data-tips="true" data-tips-type="warning"><code>{Failed, [ClusterNotRunning, ResourceCleanupFailed]}</code></div><br><br><br>   <div data-tips="true" data-tips-type="warning">You can call the <a href="https://docs.byteplus.com/en/docs/vke/ListNodePools">ListNodePools</a> API to obtain the current status of the node pool.   </div><br>    |
|Ids |Array of String |Yes |["nc5t5epm\*\*\*\*\*\*"] |A list of node IDs.<br><br>You can call the [ListNodes](https://docs.byteplus.com/en/docs/vke/ListNodes) API to obtain the node ID. At most 100 node IDs can be specified per call.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">A node must be in one of the following states:</div><br><br><br>   * <div data-tips="true" data-tips-type="warning"><code>{Running,[*]}</code></div><br><br><br>   * <div data-tips="true" data-tips-type="warning"><code>{Stopped, [*]}</code></div><br><br><br>   * <div data-tips="true" data-tips-type="warning"><code>{Failed, [InitilizeFailed, NotReady, ResourceCleanupFailed, Balance, Unknown]}</code></div><br><br><br>      <div data-tips="true" data-tips-type="warning">You can call the <a href="https://docs.byteplus.com/en/docs/vke/ListNodes">ListNodes</a> API to obtain the current status of the node.      </div><br>      <br><br>* <div data-tips="true" data-tips-type="warning">When taking <a href="https://docs.byteplus.com/en/docs/ecs/General-purpose-EBM">Bare Metal</a> nodes offline, ECS will attempt a normal shutdown based on the node status. If a normal shutdown is not possible, a forced shutdown will be performed. For more details, see <a href="https://docs.byteplus.com/en/docs/ecs/StopInstance">StopInstance</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If the specified node pool has <strong>AffinityGroupConfig</strong> (beta) enabled, ensure that the remaining node count after node removal is an integer multiple of the affinity group size. You can also delete all nodes in the node pool.</div><br> |
|CascadingDeleteResources |Array of String |No |["Ecs"] |Synchronously delete the associated resources of the specified nodes. Values:<br><br><br>* This parameter is left empty by default, which indicates that associated resources will not be deleted.<br><br>* **Ecs**: Delete non\-subscription ECS instances.<br><br>   Subscription ECS instances are only removed from the cluster and will not be deleted. You can query the instances by using the [ECS console](https://console.byteplus.com/ecs) or [ECS API](https://docs.byteplus.com/en/docs/ecs/Elastic-Compute-Service-API-overview) and perform operations on these instances based on your business requirements.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">During deletion, resources cannot be deleted if deletion protection is enabled for these resources. Otherwise, they will continue to be deleted. We recommend that you adjust the deletion protection settings based on your business requirements before calling the API.</div><br> |
|RetainResources |Array of String |No |["Ecs"] |The resources to be retained after node deletion. Valid values:<br><br><br>* An empty value (default) deletes all associated resources.<br><br>   If the node is a Subscription ECS instance, this API only removes the ECS instance from the cluster and does not delete the instance. You can query the instances by using the [ECS console](https://console.byteplus.com/ecs) or [ECS API](https://docs.byteplus.com/en/docs/ecs/Elastic-Compute-Service-API-overview) and perform operations on these instances based on your business requirements.<br><br>* **ECS**: Retain the ECS instance corresponding to the node.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">During deletion, resources cannot be deleted if deletion protection is enabled for these resources. Otherwise, they will continue to be deleted. We recommend that you adjust the deletion protection settings based on your business requirements before calling the API.</div><br> |
|Drain |Boolean |No |false |Whether to drain the node before it is deleted. Valid values:<br><br><br>* **true**: Yes.<br><br>* **false**: (Default) No. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vke.cn-beijing.byteplusapi.com.cn?Action=DeleteNodes&Version=2022-05-12
Content-Type: application/json
{
    "ClusterId": "cc5sil******",
    "NodePoolId": "pc8oah9********",
    "Ids": [
        "nc5t5epm******"
    ],
    "CascadingDeleteResources": [
        "Ecs"
    ],
    "RetainResources": [
        "Ecs"
    ],
    "Drain": true
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

This API has no API\-specific response parameters. For details about common response parameters, see [Response results](https://docs.byteplus.com/en/docs/vke/Response).

<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104********",
        "Action": "DeleteNodes",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for this API are listed in the table below. For public error codes, see [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes).


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |OperationDenied.ClusterStatus |The action is forbidden due to cluster status {{statusPhase}} and {{statusConditions}}. |The current status of the specified cluster does not support this operation. Confirm the required cluster status for this API and try again. |
|400 |OperationDenied.NodePoolStatus |The action is forbidden on node pool {{nodePoolId}} due to node pool status {{statusPhase}} and {{statusConditions}}. |The current status of the specified node pool does not support this operation. Please confirm the required node pool status for this API and try again. |
|400 |OperationDenied.NodeStatus |The action is forbidden on node {{nodeId}} due to node status {{statusPhase}} and {{statusConditions}}. |The current node status does not support this operation. Please confirm the required node status for this API and try again. |
|400 |OperationDenied.NodePoolReplicas |The operation has been denied due to the node pool min/max replicas limit. |The maximum node count for this node pool has been reached. Please reduce the number of ECS instance IDs to be added and try again later.<br><br>If autoscaling is enabled for the target node pool, you can update the maximum number of nodes (MaxReplicas) in the target node pool. Then, call this API again to add existing nodes. Call the [UpdateNodePoolConfig](https://docs.byteplus.com/en/docs/vke/UpdateNodePoolConfig) API to update the node pool. |
|400 |AffinityGroupMismatch.InstanceIds |The specified InstanceIds and AffinityGroup {{AffinityGroupId}} are mismatched. |The specified ECS instances do not match the affinity group configuration. The number of nodes in the affinity group\-based node pool must be an integer multiple of the affinity group size. Check the specified nodes and node pools, confirm the relevant parameters, and try again later. |
