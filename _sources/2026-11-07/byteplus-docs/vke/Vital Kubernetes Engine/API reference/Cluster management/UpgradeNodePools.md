---
title: "UpgradeNodePools"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/UpgradeNodePools"
---

Upgrade the VKE cluster data plane, i.e., upgrade the nodes.

<span id="7223da52"></span>
## Considerations


* The target Kubernetes version to which the node is upgraded cannot exceed the Kubernetes version of the cluster's control plane where the node resides.

* Kubernetes node upgrades can affect running applications. During the upgrade, pod probers and lifecycle hooks may fail, and in\-place restarts of pods may occur. Therefore, before the upgrade, you need to check whether the cluster is in a healthy state and whether applications are at off\-peak hours. This helps you determine whether to start upgrading nodes.

* You cannot roll back the upgrade of the node Kubernetes version. Proceed with caution.

* If you have modified the kubelet or containerd parameter configuration on the nodes, only compatible parameters will be retained during the node upgrade, and incompatible parameters will be removed. After the nodes are upgraded, you need to check the configuration again.

* When upgrading nodes to v1.28 or later, the system will update the default values of kubelet parameters to the latest values. For details, see [Configuring Kubelet parameters for node pools](https://docs.byteplus.com/en/docs/vke/Configuring-kubelet-parameters-for-a-NodePool).

* For more precautions regarding node upgrades, see [Cluster upgrade operations](https://docs.byteplus.com/en/docs/vke/Upgrading-a-cluster).


<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point based on the region where your business is located.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=UpgradeNodePools&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=UpgradeNodePools&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameter

The following table describes the API request parameters. You also need to provide public parameters when calling this API. For details about public request parameters, see [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters).


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |UpgradeNodePools |The API name. The current API name is `UpgradeNodePools`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|ClusterId |String |Yes |cc8oo\*\*\*\*\*\* |Cluster ID.<br><br>You can call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to obtain cluster IDs.<br><br><div data-tips="true" data-tips-type="warning">Note</div><br><br><br><div data-tips="true" data-tips-type="warning">The cluster to be updated must be in the <code>{Running,[*]}</code> state. You can call the <a href="https://docs.byteplus.com/en/docs/vke/ListClusters">ListClusters</a> API to view the current status of the cluster.</div><br> |
|Operation |String |No |Precheck |The specific operation to be performed. Valid values:<br><br><br>* **Precheck**: (Default value) Only perform the upgrade precheck operation.<br><br>* **Upgrade**: Directly execute the upgrade task. The upgrade task includes a precheck, and after the check passes, the upgrade operation continues. |
|NodePools |Array of [UpgradeNodePoolConfig](https://docs.byteplus.com/en/docs/90/120402#upgradenodepoolconfig) |No |\- |Information about the node pool where the nodes to be upgraded reside. |
|IgnorePrecheckWarning |Boolean |No |true |Whether to stop the upgrade process when a **Warning** occurs during the upgrade precheck. Valid values:<br><br><br>* **true**: When the upgrade precheck result is **Warning**, the node upgrade operation will not be stopped.<br><br>* **false**: (Default value) When the upgrade precheck result is **Warning**, the node upgrade operation will be stopped. |
|Runtime |Object of [Runtime](https://docs.byteplus.com/en/docs/90/120402#runtime) |No |\- |Container runtime configuration. |
|KubernetesVersion |String |No |v1.36.1\-vke.2 |The Kubernetes version of the node, in the format `<Kubernetes version>-<VKE patch version>`.<br><br>For the release notes for Kubernetes versions supported by VKE, see [Kubernetes version release notes](https://docs.byteplus.com/en/docs/vke/Kubernetes-version-release-notes). |
|UpgradePolicy |Object of [UpgradePolicy](https://docs.byteplus.com/en/docs/90/120402#upgradepolicy) |No |\- |The batching policy for node upgrades. |
|ClientToken |String |No |BC028527\-33B9\-4990\-A633\-\*\*\*\*\*\* |A string used to ensure the idempotency of the request. This string is passed in by the caller and must be unique across different requests. ClientToken is case\-sensitive and can consist of 64 ASCII characters at most. |


<span id="upgradenodepoolconfig"></span>
### UpgradeNodePoolConfig


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|NodeIds |Array of String |No |["nd6ptkl0f9t\*\*\*\*", "nd6ptkl0f9t\*\*\*\*"] |List of node IDs to be upgraded. You can call the [ListNodes](https://docs.byteplus.com/en/docs/vke/ListNodes) API to obtain the node ID. A single call can include at most 2000 node IDs.<br><br><br>* Pass a parameter value: It indicates a node\-level upgrade, and the specified nodes will be upgraded.<br><br>* Parameter value is empty: It indicates a node pool\-level upgrade, and all nodes under the specified node pool will be upgraded.<br><br><br><div data-tips="true" data-tips-type="warning">Note</div><br><br><br><div data-tips="true" data-tips-type="warning">The nodes must be in the <code>{Running,[OK]}</code> status.</div><br><br><br><div data-tips="true" data-tips-type="warning">You can call the <a href="https://docs.byteplus.com/en/docs/vke/ListNodes">ListNodes</a> API to obtain the current status of nodes.</div><br> |
|NodePoolId |String |Yes |pd6l4v8e\*\*\*\* |The ID of the node pool where the nodes to be upgraded reside.<br><br>You can call the [ListNodePools](https://docs.byteplus.com/en/docs/vke/ListNodePools) API to obtain node pool IDs.<br><br><div data-tips="true" data-tips-type="warning">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The node pool must be in one of the following states:</div><br><br><br>   * <div data-tips="true" data-tips-type="warning"><code>{Running,[*]}</code></div><br><br><br>   * <div data-tips="true" data-tips-type="warning"><code>{Scaling,[*]}</code></div><br><br><br>* <div data-tips="true" data-tips-type="warning">When nodes in the node pool are in the following statuses, the corresponding node upgrades will be blocked. Nodes in other statuses will complete the upgrade.</div><br><br><br>   * <div data-tips="true" data-tips-type="warning"><code>{Running,[Unschedulable]}</code></div><br><br><br>   * <div data-tips="true" data-tips-type="warning"><code>{Updating,[*]}</code></div><br><br><br>   * <div data-tips="true" data-tips-type="warning"><code>{Failed,[NotReady]}</code></div><br><br><br>   * <div data-tips="true" data-tips-type="warning"><code>{Failed,[Balance]}</code></div><br><br><br><br><div data-tips="true" data-tips-type="warning">You can call the <a href="https://docs.byteplus.com/en/docs/vke/ListNodePools">ListNodePools</a> API to obtain the node pool status, and call the <a href="https://docs.byteplus.com/en/docs/vke/ListNodes">ListNodes</a> API to obtain the node status.</div><br> |


<span id="runtime"></span>
### Runtime


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Type |String |No |containerd |Container runtime type. Values:<br><br><br>* **containerd**: (Default) The containerd runtime. |
|Version |String |Yes |v2.1.9\-vke.1 |Container runtime version, in the format `<scontainerd Version>-<VKE patch Version>`.<br><br>For a list of containerd versions for VKE, see the [containerd release notes](https://docs.byteplus.com/en/docs/vke/Containerd_Runtime_release_notes). |


<span id="upgradepolicy"></span>
### UpgradePolicy


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|MaxFailed |Integer |No |0 |The maximum number of node failures allowed during the upgrade process. If the number of failed nodes does not exceed this setting, the upgrade continues. If it exceeds this value, the upgrade stops.<br><br><br>* Value range: [0, 2000]<br><br>* Default value: 0 |
|MaxUnavailable |Integer |No |100 |The maximum number of concurrent nodes during a node pool upgrade.<br><br><br>* Value range: [0, 20]<br><br>* Default value:<br><br>   * For node\-level upgrade: 10<br><br>   * For node pool\-level upgrade: 20 |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST https://vke.cn-beijing.byteplusapi.com.cn?Action=UpgradeNodePools&Version=2022-05-12
Content-Type: application/json
{
    "ClusterId": "cc8oo******",
    "Operation": "Precheck",
    "NodePools": [
        {
            "NodeIds": [
                "nd6ptkl0f9t****"
            ],
            "NodePoolId": "pd6l4v******"
        }
    ],
    "IgnorePrecheckWarning": true,
    "Runtime": {
        "Type": "containerd",
        "Version": "v2.1.9-vke.1"
    },
    "KubernetesVersion": "v1.36.1-vke.2",
    "UpgradePolicy": {
        "MaxFailed": 0,
        "MaxUnavailable": 100
    },
    "ClientToken": "BC028527-33B9-4990-A633-******"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

The following table contains the response parameters of this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|TaskId |String |tdaa4i21v7p3\*\*\*\* |Task ID. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420**********",
        "Action": "UpgradeNodePools",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {
        "TaskId": "tdaa4i21********"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for this API are listed in the table below. For public error codes, see [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes).


|**HTTP status code** |**Error code** |**Error message** |**Description** |
|---|---|---|---|
|400 |OperationDenied.UpgradeNodesAndNodePools |UpgradeNodePools cannot be performed on both nodes and node pools at the same time. |Upgrading at both the node level and the node pool level is not allowed. When multiple arrays are passed in **NodePools**, if some arrays are upgraded at the node pool level and some at the node level, this error code will appear. Please update the corresponding parameter values and try again. |
|400 |LimitExceeded.UpgradeNodesNumber |The number of nodes for upgrade exceeds the maximum limit of {{UpgradeNodesMaxNum}}. |The total number of nodes to be upgraded exceeds the limit. A single call supports upgrading at most 2000 nodes. Please update the relevant parameters and try again. |
|400 |OperationDenied.ClusterStatus |The action is forbidden due to cluster status {{statusPhase}} and {{statusConditions}}. |The current status of the specified cluster does not support this operation. Confirm the required cluster status for this API and try again. |
|400 |OperationDenied.NodeStatus |The action is forbidden on node {{nodeId}} due to node status {{statusPhase}} and {{statusConditions}}. |The current node status does not support this operation. Please confirm the required node status for this API and try again. |
|400 |OperationDenied.NodePoolStatus |The action is forbidden on node pool {{nodePoolId}} due to node pool status {{statusPhase}} and {{statusConditions}}. |The current status of the specified node pool does not support this operation. Please confirm the required node pool status for this API and try again. |
|400 |KubernetesVersionMismatch.RuntimeVersion |The specified runtime version {{runtimeVersion}} and Kubernetes version {{kubernetesVersion}} are mismatched. |The specified container runtime version does not match the cluster Kubernetes version. For example, containerd 2.1.x is only supported in clusters with Kubernetes v1.34 or later. Specify another container runtime version and try again later. For more information, see the [containerd release notes](https://docs.byteplus.com/en/docs/vke/Containerd_Runtime_release_notes). |
