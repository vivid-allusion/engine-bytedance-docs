---
title: "UpdateNodePoolNodesConfig"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/UpdateNodePoolNodesConfig"
---

Updates the configurations of nodes in a node pool, including kubelet and containerd parameter settings.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">This API supports only updating the kubelet and containerd parameters of nodes in a node pool and does not support modifying other node pool configurations.</div>


* <div data-tips="true" data-tips-type="warning">When node configurations are modified, the system applies the configuration changes in batches. Modifying the kubelet configuration restarts kubelet, and modifying the containerd configuration restarts containerd. During the service restart, the nodes and the workloads running on the nodes may be affected. Perform this operation during off\-peak hours.</div>



<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. See [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) and select the most suitable endpoint for the region where your business operates.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=UpdateNodePoolNodesConfig&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=UpdateNodePoolNodesConfig&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table describes the API request parameters. You also need to provide public parameters when calling this API. For details about public request parameters, see [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters).


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |UpdateNodePoolNodesConfig |The API name. The API name is `UpdateNodePoolNodesConfig`. |
|Version |String |Yes |May 12, 2022 |The API version. The API version is `2022-05-12`. |
|ClusterId |String |Yes |cc5silumrsfeq\*\*\*\* |The ID of the cluster where the node pool is located.<br><br>You can call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to obtain cluster IDs.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The cluster must be in the <code>{Running,[Ok]}</code> or <code>{Updating,[Progressing]}</code> state. You can call the <a href="https://docs.byteplus.com/en/docs/vke/ListClusters">ListClusters</a> API to view the current status of the cluster.</div><br> |
|NodePoolId |String |Yes |pc51i0m6rsfen\*\*\*\* |The node pool ID.<br><br>You can call the [ListNodePools](https://docs.byteplus.com/en/docs/vke/ListNodePools) API to obtain the node pool ID.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The node pool must be in the <code>{Running,[*]}</code> or <code>{Scaling,[Progressing]}</code> state. You can call the <a href="https://docs.byteplus.com/en/docs/vke/ListNodePools">ListNodePools</a> API to obtain the current status of the node pool.</div><br> |
|KubeletConfig |Object of [NodePoolKubeletConfig](https://docs.byteplus.com/en/docs/90/121842#nodepoolkubeletconfig) |No |\- |The kubelet configuration for the node. |
|ContainerdConfig |Object of [NodePoolContainerdConfig](https://docs.byteplus.com/en/docs/90/121842#nodepoolcontainerdconfig) |No |\- |The containerd configuration for the node.<br><br><div data-tips="true" data-tips-type="default">Description</div><br><br><br><div data-tips="true" data-tips-type="default">At least one of <code>KubeletConfig</code> and <code>ContainerdConfig</code> must be specified.</div><br> |
|NodeIds |Array of String |No |["nc5t5epmrsf\*\*\*"，"ndao9ti534q5ge6\*\*\*"] |The IDs of the nodes whose configurations are to be synchronized.<br><br>If this field is not configured or an empty list `[]` is passed in, the configurations of all existing nodes in the node pool are synchronized. |
|ClientToken |String |Yes |BC028527\-33B9\-4990\-A633\-84E9F9\*\*\*\* |A string used to ensure the idempotency of the request. This string is passed in by the caller and must be unique across different requests. ClientToken is case\-sensitive and can consist of 64 ASCII characters at most. |


<span id="nodepoolkubeletconfig"></span>
### NodePoolKubeletConfig


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|FeatureGates |Object of [FeatureGates](https://docs.byteplus.com/en/docs/90/121842#featuregates) |No |\- |The feature gates, which are a set of key\-value pairs that describe Kubernetes features. |
|TopologyManagerScope |String |No |container |The resource granularity of the topology management policy. Valid values:<br><br><br>* **container**: The resource alignment granularity is at the container level. |
|TopologyManagerPolicy |String |No |none |The topology management policy. Valid values:<br><br><br>* **none**: The topology management policy is disabled by default.<br><br>* **restricted**: kubelet accepts only pods that achieve optimal non\-uniform memory access (NUMA) alignment on the requested resources.<br><br>* **best\-effort**: Kubelet preferentially selects pods that achieve NUMA alignment on CPU and device resources.<br><br>* **single\-numa\-node**: Kubelet allows only pods that are aligned to the same NUMA node in terms of CPU and device resources. |
|MaxPods |Integer |No |110 |The maximum pods supported by the nodes. Default value: 110. |
|KubeApiQps |Integer |No |50 |The number of QPS for communication with the API server. <br><br><br>* The value is an integer. Valid values: 1 to 500.<br><br>* The default value is 50. |
|KubeApiBurst |Integer |No |100 |The maximum burst requests sent to the API server per second.<br><br><br>* Enter an integer from 1 to 1000.<br><br>* The default value is 100.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This value must be greater than or equal to the value of the <code>KubeApiQps</code> parameter.</div><br> |
|EvictionHard |Array of [EvictionHard](https://docs.byteplus.com/en/docs/90/121842#evictionhard) |No |\- |A set of hard eviction thresholds that trigger pod eviction. For detailed parameter descriptions, see the[ official documentation](https://kubernetes.io/docs/concepts/scheduling-eviction/node-pressure-eviction/).<br><br>To explicitly disable hard eviction, set the threshold to 0% or 100% on any resource.<br><br>Default values:<br><br><br>* memory.available: "300Mi"<br><br>* nodefs.available: "10%"<br><br>* nodefs.inodesFree: "5%"<br><br>* imagefs.available: "15%" |
|KubeReserved |Array of [ComputeResource](https://docs.byteplus.com/en/docs/90/121842#computeresource) |No |\- |The resources reserved by the node for Kubernetes system components. By default, resources are reserved based on half of the default value in the [node resource reservation policy](https://docs.byteplus.com/en/docs/vke/Node-resource-reservation-policies). |
|SystemReserved |Array of [ComputeResource](https://docs.byteplus.com/en/docs/90/121842#computeresource) |No |\- |The resources reserved for the operating system on the node. By default, resources are reserved based on half of the default value in the [node resource reservation policy](https://docs.byteplus.com/en/docs/vke/Node-resource-reservation-policies). |
|RegistryPullQps |Integer |No |5 |The QPS threshold for a cluster pulling images from Container Registry (CR).<br><br><br>* The value is an integer. Valid values: 1 to 50.<br><br>* Default value: 5. |
|RegistryBurst |Integer |No |10 |The maximum images concurrently pulled from CR.<br><br><br>* The value is an integer. Valid values: 1 to 100.<br><br>* Default value: 10.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You need to specify this parameter only when the value of the <code>RegistryPullQps</code> parameter is greater than 0. The value of this parameter must be greater than or equal to the value of the <code>RegistryPullQps</code> parameter.</div><br> |
|SerializeImagePulls |Boolean |No |true |Specify whether to serially pull images. Valid values:<br><br><br>* **true**: Serially pull images.<br><br>* **false**: (Default) Pull images in parallel to accelerate pod startup. |
|CpuManagerPolicy |String |No |none |The CPU manager policy. Valid values:<br><br><br>* **none**: The policy is the default policy.<br><br>* **static**: This policy allows pods with specific resource characteristics on the node to be granted enhanced CPU affinity and exclusivity. |
|FailSwapOn |Boolean |No |false |Specifies whether kubelet can run when swap is enabled on the node. Valid values:<br><br><br>* **true**: Prevents kubelet from running when swap is enabled on the node. This is the default value. This is the default protection mechanism in Kubernetes. Swap can interfere with precise memory limit control. As a result, containers may use more memory than expected, affecting the accuracy of Pod scheduling and out\-of\-memory (OOM) detection.<br><br>* **false**: Allows kubelet to run when swap is enabled on the node. This option applies when strict memory isolation is not required or when Kubernetes must run on existing nodes with swap configured. |
|PodPidsLimit |Integer |No |4096 |This parameter limits the maximum number of process IDs (PIDs) that all containers in a single Pod can use. This prevents a single Pod from creating excess processes and exhausting the PID resources of the node.<br><br><br>* The value is an integer. Valid values: \-1 or a positive integer. Unit: count.<br><br>* When the value is set to \-1, it indicates that the number of PIDs that a single Pod can use is not limited.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This configuration only limits the number of PIDs that a single Pod can use. The actual number of PIDs available to a Pod is also affected by the PID limit of the node kernel and the PID usage of other processes on the node.</div><br><br><br>* <div data-tips="true" data-tips-type="default">We do not recommend setting the value to \-1. We recommend setting the value based on the PID capacity of the node, the number of processes required by each Pod, and the number of Pods the node can run. This prevents a single Pod from exhausting the PID resources of the node. In addition, do not set a value that is too low. Otherwise, the Pod cannot create processes as expected.</div><br> |
|ImageMaximumGcAge |String |No |24h |The maximum retention duration for unused images before they are garbage collected. Images that have remained unused for longer than this period will be cleaned up during the next garbage collection cycle.<br><br><br>* The Kubernetes duration. The value is a string. It supports time units, such as 48h and 168h.<br><br>* The default value is 0s, which indicates that images are not cleaned up based on time limits and are garbage collected only based on disk utilization (ImageGcHighThresholdPercent).<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">When this parameter is set to a non\-zero value, it must be greater than <code>ImageMinimumGcAge</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">This parameter is supported only in clusters running on Kubernetes v1.30 or later.</div><br> |
|ImageMinimumGcAge |String |No |5m |The minimum retention duration for unused images before they are garbage collected. During this time, the image will not be garbage collected even if disk utilization exceeds the garbage collection threshold.<br><br><br>* The Kubernetes duration. The value is a string. It supports time units, such as 2m and 30m.<br><br>* The default value is 2m.<br><br>* This parameter prevents a newly pulled image from being garbage collected immediately. This keeps the image available during the window between the pull and container startup.<br><br><br><div data-tips="true" data-tips-type="default">Description</div><br><br><br><div data-tips="true" data-tips-type="default">Do not set a value that is too high. Otherwise, newly downloaded images that are not used in the short term cannot be cleaned up in time when disk space is tight. This potentially increases disk pressure.</div><br> |
|ImageGcLowThresholdPercent |Integer |No |80 |The threshold for stopping Image garbage collection. During image garbage collection, collection stops when disk usage falls below this percentage.<br><br><br>* The value is an integer. Valid values: 0 to 100.<br><br>* Default value: 80.<br><br>* Unit: percentage.<br><br><br><div data-tips="true" data-tips-type="warning">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">When specifying this parameter, make sure that <code>ImageGcLowThresholdPercent</code> is less than <code>ImageGcHighThresholdPercent</code>. Even if only one of the parameters is modified, the system validates it against the default value or the original configuration of the other parameter.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">You can set this parameter to 0. However, this value stops cleanup only after disk usage reaches 0%, which is almost impossible and has no practical value.</div><br> |
|ImageGcHighThresholdPercent |Integer |No |85 |The threshold for triggering image garbage collection. When disk utilization exceeds this value, garbage collection will be triggered. Unused images will be cleaned up to release disk space.<br><br><br>* The value is an integer. Valid values: 0 to 100.<br><br>* Default value: 85.<br><br>* Unit: percentage.<br><br><br><div data-tips="true" data-tips-type="warning">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">When specifying this parameter, make sure that <code>ImageGcLowThresholdPercent</code> is less than <code>ImageGcHighThresholdPercent</code>. Even if only one of the parameters is modified, the system validates it against the default value or the original configuration of the other parameter.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">You can set this parameter to 100. However, this value triggers cleanup only when disk usage reaches 100%. This value is extremely conservative and not recommended in production environments.</div><br> |


<span id="featuregates"></span>
### FeatureGates


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|QoSResourceManager |Boolean |No |false |Specify whether to enable quality of service (QoS) Resource Manager to support micro\-topology scheduling. Valid values:<br><br><br>* **true**: Enable QoS Resource Manager.<br><br>* **false**: (Default) Disable QoS Resource Manager.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This configuration takes effect only in clusters of the following versions:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">v1.24.15\-vke.13 ≤ Cluster version < v1.26</div><br><br><br>* <div data-tips="true" data-tips-type="default">v1.26.10\-vke.13 ≤ Cluster version < v1.28</div><br> |
|InPlacePodVerticalScaling |Boolean |No |true |Specify whether to enable the vertical scaling feature for pods. Valid values:<br><br><br>* **true**: Enable the vertical scaling feature for pods.<br><br>* **false**: Disable it.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This configuration is supported only by the following cluster versions. Attempting to configure it on clusters of other versions is not allowed and will result in an error:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">v1.28.3\-vke.17 ≤ Custer version < v1.36</div><br> |


<span id="evictionhard"></span>
### EvictionHard


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Key |String |Yes |memory.available |The name of the hard eviction threshold. Valid values:<br><br><br>* memory.available<br><br>* nodefs.available<br><br>* nodefs.inodesFree<br><br>* imagefs.available |
|Value |String |Yes |1Gi |The hard eviction threshold value. The value can be an integer or a percentage.<br><br><br>* If the value is an integer, it indicates the specific threshold value of the resource. Unit: bytes. For example: 100Mi.<br><br>* If the value is a percentage, it indicates the proportion of the resource threshold value. Valid values: 0% to 100%. For example: 20%. To explicitly disable hard eviction, set the threshold to 0% or 100% on any resource. |


<span id="computeresource"></span>
### ComputeResource


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Name |String |Yes |cpu |The resource name. Set the value to **cpu** or **memory**. |
|Quantity |String |Yes |1G |Specify the quantity of the resource.<br><br><br>* When the resource is **cpu**, the example value is 200m.<br><br>* When the resource is **memory**, the sample value is 1 GB. |


<span id="nodepoolcontainerdconfig"></span>
### NodePoolContainerdConfig


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|ConcurrentLayerFetchBuffer |Integer |No |512 |The buffer size used when a single image layer is concurrently pulled in chunks. The value is a positive integer. Unit: bytes.<br><br><div data-tips="true" data-tips-type="default">Description</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is supported only if the containerd version is v2.1.0 or later.</div><br> |
|MaxConcurrentUnpacks |Integer |No |8 |The maximum number of image layers that containerd can decompress simultaneously.<br><br><br>* The value is a positive integer. Default value: 1.<br><br>* This parameter takes effect only if `UseLocalImagePull` is set to `false`.<br><br><br><div data-tips="true" data-tips-type="default">Description</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is supported only if the containerd version is v2.2.0 or later.</div><br> |
|MaxConcurrentDownloads |Integer |No |10 |The maximum number of image layers that containerd can download concurrently when pulling images at a time.<br><br><br>* The value is a positive integer. Default value: 3.<br><br>* If you do not specify this parameter, the default value is used.<br><br><br><div data-tips="true" data-tips-type="default">Description</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is supported only if the containerd version is v2.1.0 or later.</div><br> |
|UseLocalImagePull |Boolean |No |true |The image pull mode of containerd. Valid values:<br><br><br>* **true**: (Default) Use a local client to pull images.<br><br>* **false**: Use Transfer Service to pull images.<br><br><br><div data-tips="true" data-tips-type="default">Description</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is supported only if the containerd version is v2.1.0 or later.</div><br> |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST https://vke.cn-beijing.byteplusapi.com.cn?Action=UpdateNodePoolNodesConfig&Version=2022-05-12
Content-Type: application/json
{
    "ClusterId": "cc5silum********",
    "NodePoolId": "pc51i0m6********",
    "KubeletConfig": {
        "MaxPods": 110,
        "FailSwapOn": true,
        "KubeApiQps": 50,
        "EvictionHard": [
            {
                "Key": "memory.available",
                "Value": "1Gi"
            }
        ],
        "FeatureGates": {
            "QoSResourceManager": false
        },
        "KubeApiBurst": 100,
        "KubeReserved": [
            {
                "Name": "cpu",
                "Quantity": "1G"
            }
        ],
        "PodPidsLimit": 4096,
        "RegistryBurst": 10,
        "SystemReserved": [
            {
                "Name": "cpu",
                "Quantity": "1G"
            }
        ],
        "RegistryPullQps": 5,
        "CpuManagerPolicy": "none",
        "ImageMaximumGcAge": "24h",
        "ImageMinimumGcAge": "5m",
        "SerializeImagePulls": true,
        "TopologyManagerScope": "container",
        "TopologyManagerPolicy": "none",
        "ImageGcLowThresholdPercent": 80,
        "ImageGcHighThresholdPercent": 85
    },
    "ContainerdConfig": {
        "UseLocalImagePull": false,
        "MaxConcurrentUnpacks": 8,
        "MaxConcurrentDownloads": 10,
        "ConcurrentLayerFetchBuffer": 512
    },
    "NodeIds": [
        "nc5t5epmrsf***"
    ],
    "ClientToken": "BC028527-33B9-4990-A633-84E9F9****"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

The following table contains the response parameters of this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|TaskId |String |tcax\*\*\*\*\*\* |Task ID. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateNodePoolNodesConfig",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {
        "TaskId": "tcax******"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for this API are listed in the table below. For public error codes, see [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes).


|**HTTP status code** |**Error code** |**Error message** |**Description** |
|---|---|---|---|
|400 |InvalidParameter.{{parameter}} |The specified parameter {{parameter}} is invalid. |The request parameters are invalid, such as incorrect parameter types, invalid lengths, invalid enumeration values, and failure to satisfy regular expression rules. For example, `InvalidParameter.MaxPods` and `InvalidParameter.KubeApiQps`. |
|400 |OperationDenied.ClusterStatus |The action is forbidden due to cluster status {{statusPhase}} and {{statusConditions}}. |The current status of the specified cluster does not support this operation. Confirm the required cluster status for this API and try again. |
|400 |OperationDenied.NodePoolStatus |The action is forbidden on node pool {{nodePoolId}} due to node pool status {{statusPhase}} and {{statusConditions}}. |The current status of the specified node pool does not support this operation. Please confirm the required node pool status for this API and try again. |
|400 |OperationDenied.NodeStatus |The action is forbidden on node {{nodeId}} due to node status {{statusPhase}} and {{statusConditions}}. |The current node status does not support this operation. Please confirm the required node status for this API and try again. |
|400 |NotSupported.{{parameter}} |The specified {{resourceType}} {{resourceContent}} is not supported. |The specified resources cannot be installed. |
