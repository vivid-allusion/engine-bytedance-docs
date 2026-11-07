---
title: "DeleteCluster"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/DeleteCluster"
---

Delete a VKE cluster.

<span id=".5L2_55So6K-05piO"></span>
## Usage instructions

This API is asynchronous. When this API returns success, the cluster is in the `{Deleting, [Progressing]}` state and is no longer managed and charged. In this case, it does not mean the cluster has been deleted. You need to call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to check whether the cluster exists. If it is not found in the query results, the cluster has been deleted.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point for your business region.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=DeleteCluster&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteCluster&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table describes the API request parameters. You also need to provide public parameters when calling this API. See [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters) for details.


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |DeleteCluster |The API name. The name of the current API is `DeleteCluster`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Id |String |Yes |cc9l74mvqtofjnoj5xxxx |The ID of the cluster to be deleted.<br><br>Cluster IDs can be queried by calling the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The cluster to be deleted must be in one of the following states:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning"><code>{Running,[*]}</code></div><br><br><br>* <div data-tips="true" data-tips-type="warning"><code>{Failed, [*]}</code></div><br><br><br>* <div data-tips="true" data-tips-type="warning"><code>{Stopped, [Ok, Balance]}</code></div><br><br><br><br>You can call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to view the current status of the cluster. |
|Force |Boolean |No |false |Specify whether to forcibly delete the cluster. Valid values:<br><br><br>* **false**: (Default) Disable the feature.<br><br>* **true**: If you set the parameter to this value, even clusters with deletion protection enabled (`DeleteProtection=true`) can be forcibly deleted. |
|RetainResources |Array of String |No |["Nat"] |The resources to be retained in the cluster when the cluster is being deleted. Valid values:<br><br><br>* If this parameter is left empty, which is the default value, all resources associated with the cluster, as well as non\-subscription ECS instances added to node pools, will be deleted.<br><br>* **DefaultNodePoolResource**: Retain ECS instances in the default node pool of the cluster and their associated resources, such as EBS devices and EIPs.<br><br>* **NodePoolResource**: Retain ECS instances in all custom node pools in the cluster and their associated resources, such as EBS devices and EIPs.<br><br>* **Clb**: Retain CLB instances created by the Ingresses and Services in the cluster.<br><br>* **Alb**: Retain ALB instances created by the Ingresses and Services in the cluster.<br><br>* **Nat**: Retain NAT gateways associated with the cluster.<br><br>* **SecurityGroup**: Retain security groups associated with the cluster.<br><br>* **All**: Retain all resources associated with the cluster.<br><br><br>  |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST /?Action=DeleteCluster&Version=2022-05-12 HTTP/1.1
Content-Type:application/json
{
    "Id": "cc9l74mvqtofjnoj5****",
    "Force": true,
    "RetainResources": ["DefaultNodePoolResource"]
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
        "Action": "DeleteCluster",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for this API are listed in the table below. Refer to the [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes) topic for details.


|**HTTP status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |OperationDenied.DeleteProtection |The deletion protection of specified {{resourceType}} is enabled. |The deletion failed because deletion protection is enabled for the specified resources. You can forcibly delete the cluster or disable deletion protection and try again. |
|400 |OperationDenied.ClusterStatus |The action has been denied due to wrong cluster status {{statusPhase}} and [{{statusConditions}}]. |The current status of the specified cluster does not support this operation. Please confirm the required cluster status for this API and try again. |
