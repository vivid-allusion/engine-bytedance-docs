---
title: "DeleteNodePool"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/DeleteNodePool"
---

Delete a node pool in a specified cluster.

<span id=".5L2_55So6K-05piO"></span>
## Usage instructions

This is an asynchronous API. When this API returns a success message, the node pool will be in the `{Deleting, [Progressing]}` state. A returned success message does not mean the node pool has been deleted. You need to call the [ListNodePools](https://docs.byteplus.com/en/docs/vke/ListNodePools) API to check whether the node pool still exists. If it is not found in the query results, the node pool has been deleted.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point for your business region.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=DeleteNodePool&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteNodePool&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table describes the API request parameters. You also need to provide public parameters when calling the API. For details, see [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters).


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |DeleteNodePool |The API name. The name of the current API is `DeleteNodePool`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|ClusterId |String |Yes |cc5silumrsfeqxxxx |The ID of the cluster where the node pool is located.<br><br>Cluster IDs can be queried by calling the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The cluster where the node pool to be deleted is located must be in one of the following states:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning"><code>{Running,[*]}</code></div><br><br><br>* <div data-tips="true" data-tips-type="warning"><code>{Updating, [Progressing]}</code></div><br><br><br>* <div data-tips="true" data-tips-type="warning"><code>{Stopped, [Balance]}</code></div><br><br><br><br>You can call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to view the current status of the cluster. |
|Id |String |Yes |pc51i0m6rsfenxxxx |Node pool ID.<br><br>You can call the [ListNodePools](https://docs.byteplus.com/en/docs/vke/ListNodePools) API to obtain the node pool ID.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The node pool must be in one of the following states:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning"><code>{Running,[*]}</code></div><br><br><br>* <div data-tips="true" data-tips-type="warning"><code>{Failed, [*]}</code></div><br><br><br><br>You can call the [ListNodePools](https://docs.byteplus.com/en/docs/vke/ListNodePools) API to obtain the current status of the node pool. |
|RetainResources |Array of String |no |["Ecs"] |The resources to be retained when the node pool is being deleted. Valid values:<br><br><br>* An empty value (default) deletes all associated resources.<br><br>   If subscription ECS instances exist in the node pool, this API only removes the ECS instances from the node pool and does not delete them. You can query the instances by using the [ECS console](https://console.byteplus.com/ecs) or [ECS API](https://docs.byteplus.com/en/docs/ecs/Elastic-Compute-Service-API-overview) and perform operations on these instances based on your business requirements.<br><br>* **Ecs**: Retain ECS instances in the node pool.<br><br><br>  |


&nbsp;


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |DeleteNodePool |The API name. The name of the current API is `DeleteNodePool`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|ClusterId |String |Yes |cc5silumrsfeqxxxx |The ID of the cluster where the node pool is located.<br><br>Cluster IDs can be queried by calling the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The cluster where the node pool to be deleted is located must be in one of the following states:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning"><code>{Running,[*]}</code></div><br><br><br>* <div data-tips="true" data-tips-type="warning"><code>{Updating, [Progressing]}</code></div><br><br><br>* <div data-tips="true" data-tips-type="warning"><code>{Stopped, [Balance]}</code></div><br><br><br><br>You can call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to view the current status of the cluster. |
|Id |String |Yes |pc51i0m6rsfenxxxx |Node pool ID.<br><br>You can call the [ListNodePools](https://docs.byteplus.com/en/docs/vke/ListNodePools) API to obtain the node pool ID.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The node pool must be in one of the following states:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning"><code>{Running,[*]}</code></div><br><br><br>* <div data-tips="true" data-tips-type="warning"><code>{Failed, [*]}</code></div><br><br><br><br>You can call the [ListNodePools](https://docs.byteplus.com/en/docs/vke/ListNodePools) API to obtain the current status of the node pool. |
|RetainResources |Array of String |no |["Ecs"] |The resources to be retained when the node pool is being deleted. Valid values:<br><br><br>* An empty value (default) deletes all associated resources.<br><br>   If subscription ECS instances exist in the node pool, this API only removes the ECS instances from the node pool and does not delete them. You can query the instances by using the [ECS console](https://console.byteplus.com/ecs) or [ECS API](https://docs.byteplus.com/en/docs/ecs/Elastic-Compute-Service-API-overview) and perform operations on these instances based on your business requirements.<br><br>* **Ecs**: Retain ECS instances in the node pool.<br><br><br>  |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST /?Action=DeleteNodePool&Version=2022-05-12 HTTP/1.1
Content-Type:application/json
{
    "ClusterId": "cc5silumrsfeq****",
    "Id": "pc51i0m6rsfen****",
    "RetainResources": ["Ecs"]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

There are no proprietary response parameters for this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.

<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```JSON
HTTP/1.1 200 OK
Content-Type:application/json
{
    "ResponseMetadata": {
        "RequestId": "021635330810134****",
        "Action": "DeleteNodePool",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for this API are listed in the table below. Refer to the [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes) topic.


|**HTTP status code** |**Error code** |**Error message** |**Description** |
|---|---|---|---|
|400 |OperationDenied.ClusterStatus |The action has been denied due to wrong cluster status {{statusPhase}} and [{{statusConditions}}]. |The current status of the specified cluster does not support this operation. Please confirm the required cluster status for this API and try again. |
|400 |OperationDenied.NodePoolStatus |The action has been forbidden due to wrong node pool status {{statusPhase}} and [{{statusConditions}}]. |The current status of the specified node pool does not support this operation. Please confirm the required node pool status for this API and try again. |
|400 |OperationDenied.ScheduledInstanceId |The operation has been denied due to the ScheduledInstanceId {{scheduledInstanceId}}. |The node pool cannot be deleted because an elastic scheduled order to be delivered exists. |
