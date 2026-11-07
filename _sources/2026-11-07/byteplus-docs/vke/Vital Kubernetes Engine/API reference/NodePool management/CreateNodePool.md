---
title: "CreateNodePool"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/CreateNodePool"
---

Create a node pool in the specified cluster.

<span id=".5L2_55So6K-05piO"></span>
## Usage instructions


* Before you call this API, first call the [ListSupportedResourceTypes](https://docs.byteplus.com/en/docs/vke/ListSupportedResourceTypes) API to confirm whether the resources required for node pool creation are supported in the specified region and availability zone.

* This is an asynchronous API. When this API returns a success message, the ID of the node pool is included in the response, and the node pool enters the `{Creating, [Progressing]}` state, which stays until the creation is successful. You can call the [ListNodePools](https://docs.byteplus.com/en/docs/vke/ListNodePools) API to obtain the current status of the node pool, based on which you check whether the node pool has been created successfully.


<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point based on the region where your business is located.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=CreateNodePool&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateNodePool&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameter

The following table describes the API request parameters. You also need to provide public parameters when calling this API. For details about public request parameters, see [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters).


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |CreateNodePool |The API name. The name of the current API is `CreateNodePool`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|ClientToken |String |No |BC028527\-33B9\-4990\-A633\-84E9F9\*\*\*\*\*\* |A string used to ensure the idempotency of the request. This string is passed in by the caller and must be unique across different requests. ClientToken is case\-sensitive and can consist of 64 ASCII characters at most. |
|ClusterId |String |Yes |cc5silu\*\*\*\*\*\*\* |The ID of the cluster where the node pool is located.<br><br>You can call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to obtain cluster IDs.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The cluster must be in the <code>{Running,[Ok]}</code> or <code>{Updating,[Progressing]}</code> state. You can call the <a href="https://docs.byteplus.com/en/docs/vke/ListClusters">ListClusters</a> API to obtain the current status of the cluster.</div><br> |
|Name |String |Yes |test\-nodepool |The name of the node pool.<br><br><br>* The node pool name must be unique within the same cluster.<br><br>* It can contain uppercase and lowercase letters, Chinese characters, digits, and hyphens (\-). It can be 2 to 64 characters in length.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The default node pool name <code>vke-default-nodepool</code> cannot be used.</div><br> |
|KubernetesConfig |Object of [NodePoolKubernetesConfigRequest](https://docs.byteplus.com/en/docs/90/21159#nodepoolkubernetesconfigrequest) |No |\- |Kubernetes configuration for the node pool. |
|NodeConfig |Object of [NodePoolNodeConfigRequest](https://docs.byteplus.com/en/docs/90/21159#nodepoolnodeconfigrequest) |Yes |\- |The ECS instance configuration for the node pool. |
|AutoScaling |Object of [NodePoolAutoScalingRequest](https://docs.byteplus.com/en/docs/90/21159#nodepoolautoscalingrequest) |No |\- |Node pool scaling policy configuration. |
|Tags |Array of [Tag](https://docs.byteplus.com/en/docs/90/21159#tag) |No |\- |Custom tags for classifying, retrieving, and aggregating node pools with similar characteristics from different dimensions. Node pool tags enable you to manage node pools more flexibly and efficiently.<br><br><br>* Each **Key** in **Tags** must be unique.<br><br>* If the resource already has the same **Tags.Key**, an error will not occur if you bind the same **Tags.Key** again. Instead, the latest **Tags.Value** will be used.<br><br>* A resource can have up to 50 **tags**.<br><br>* The **Key** and **Value** in **Tags** cannot start or end with a space. |
|Management |Object of [NodePoolManagementRequest](https://docs.byteplus.com/en/docs/90/21159#nodepoolmanagementrequest) |No |\- |The management configuration of the node pool. |


<span id="nodepoolkubernetesconfigrequest"></span>
### NodePoolKubernetesConfigRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Labels |Array of [Label](https://docs.byteplus.com/en/docs/90/21159#label) |No |\- |The Kubernetes labels of the node pool or the node. Up to 20 labels can be provided.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The node pool manages the label configurations of nodes in a centralized manner. Therefore, the label information will be synchronized to all nodes in the node pool. When labels are changed, the original label configurations will be overwritten.</div><br> |
|Taints |Array of [Taint](https://docs.byteplus.com/en/docs/90/21159#taint) |No |\- |The Kubernetes taints of the node pool or the node. Up to 20 taints can be specified.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The node pool manages the taint configurations of nodes in a centralized manner. Therefore, the taint information will be synchronized to all nodes in the node pool. When taints are changed, the original taint configurations will be overwritten.</div><br> |
|Cordon |Boolean |No |false |Whether to cordon nodes. Valid values:<br><br><br>* **false**: Do not cordon nodes. This value is used by default.<br><br>* **true**: Cordon nodes.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When you update the configurations of a node pool, if you do not specify this parameter, the original parameter configurations are retained.</div><br> |
|NamePrefix |String |No |name\-prefix |The prefix of the metadata name for the node object in Kubernetes. This is disabled by default. If you specify this parameter, this option is enabled and will affect the prefix information shown in the `metadata.name` field of the Kubernetes node manifest file. The prefix is validated based on the following rules:<br><br><br>* It can contain lowercase letters, digits, hyphens (`-`), and periods (`.`).<br><br>* It can start only with a lowercase letter or digit.<br><br>* It can be 1 to 48 characters in length. |
|KubeletConfig |Object of [NodePoolKubeletConfig](https://docs.byteplus.com/en/docs/90/21159#nodepoolkubeletconfig) |No |\- |Specify custom kubelet parameters for nodes in the node pool to adjust node behavior. |
|AutoSyncDisabled |Boolean |No |false |Whether to disable automatic synchronization of labels and taints to existing nodes. Values:<br><br><br>* **true**: Disable automatic synchronization.<br><br>* **false**: (Default) Enable automatic synchronization. |
|Runtime |Object of [NodePoolRuntimeRequest](https://docs.byteplus.com/en/docs/90/21159#nodepoolruntimerequest) |No |\- |Container runtime configuration. |
|NameSuffix |String |No |\-demo |The suffix of the metadata name for the node object in Kubernetes. |
|NameUseHostname |Boolean |No |true |Specify whether the metadata name of the node object in Kubernetes uses the ECS hostname. Valid values:<br><br><br>* **true**: Use the ECS hostname as the node name.<br><br>* **false**: Do not use the ECS hostname as the node name.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This configuration has higher priority than <code>NamePrefix</code> and <code>NameSuffix</code>.</div><br> |
|ContainerdConfig |Object of [NodePoolContainerdConfig](https://docs.byteplus.com/en/docs/90/21159#nodepoolcontainerdconfig) |No |\- |Containerd configuration for the node pool. |


<span id="label"></span>
### Label


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Key |String |Yes |label\-key |The label key. The requirements are as follows. For more rules, see [Kubernetes label rules](https://kubernetes.io/zh/docs/concepts/overview/working-with-objects/labels/#%E8%AF%AD%E6%B3%95%E5%92%8C%E5%AD%97%E7%AC%A6%E9%9B%86).<br><br>A valid label key consists of <prefix\> and <Name\>, which are separated by a slash (/).<br><br><br>* <Name\> is required, which can contain uppercase or lowercase letters, digits, hyphens (\-), underscores (_), and periods (.). It must start and end with a letter or digit and can be up to 63 characters in length.<br><br>* <prefix\> is optional. If <prefix\> is specified, it must be a DNS subdomain. It is a series of DNS labels separated by periods (.), with a length not exceeding 253 characters.<br><br>* The total length of <prefix\> and <Name\> must not exceed 82 characters. |
|Value |String |No |label\-value |The label value. The requirements are as follows. For more rules, see [Kubernetes label rules](https://kubernetes.io/zh/docs/concepts/overview/working-with-objects/labels/#%E8%AF%AD%E6%B3%95%E5%92%8C%E5%AD%97%E7%AC%A6%E9%9B%86).<br><br><br>* The value cannot exceed 63 characters in length and can be left empty.<br><br>* The value can start and end with an uppercase or lowercase letter, or a digit.<br><br>* The value can contain the following special characters: hyphens (\-), underscores (_), and periods (.). |


<span id="taint"></span>
### Taint


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Key |String |Yes |taint\-key |The taint key. The requirements are as follows. For more rules, see [Kubernetes label rules](https://kubernetes.io/zh/docs/concepts/overview/working-with-objects/labels/#%E8%AF%AD%E6%B3%95%E5%92%8C%E5%AD%97%E7%AC%A6%E9%9B%86).<br><br>A valid taint key consists of a `prefix` and a `name`, which are separated by a slash (/).<br><br><br>* The `name` is required. It can contain uppercase and lowercase letters, digits, and the following special characters: `- _ .`. It must start and end with a letter or digit, and can be up to 63 characters in length.<br><br>* The `prefix` is optional. If you specify the `prefix`, it must be a DNS subdomain: a series of DNS labels separated by periods (`.`). It can be up to 253 characters in length.<br><br>* The total length of the `prefix` and `name` cannot exceed 82 characters.The prefix and name can consist of 82 characters in total. |
|Value |String |No |taint\-value |The taint value. The requirements are as follows. For more rules, see [Kubernetes label rules](https://kubernetes.io/zh/docs/concepts/overview/working-with-objects/labels/#%E8%AF%AD%E6%B3%95%E5%92%8C%E5%AD%97%E7%AC%A6%E9%9B%86).<br><br><br>* The value cannot exceed 63 characters in length and can be left empty.<br><br>* The value can start and end with an uppercase or lowercase letter, or a digit.<br><br>* The following special characters are supported: `- _ .` |
|Effect |String |No |NoSchedule |The taint effect. Valid values:<br><br><br>* **NoSchedule**: (Default) No scheduling is performed.<br><br>* **NoExecute**: Pods that do not tolerate the taint are evicted.<br><br>* **PreferNoSchedule**: Avoid scheduling if possible. |


<span id="nodepoolkubeletconfig"></span>
### NodePoolKubeletConfig


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|FeatureGates |Object of [FeatureGates](https://docs.byteplus.com/en/docs/90/21159#featuregates) |No |\- |The feature gates, which are a set of key\-value pairs that describe Kubernetes features. |
|TopologyManagerScope |String |No |container |The resource granularity of the topology management policy. Valid values:<br><br><br>* **container**: The resource alignment granularity is at the container level. |
|TopologyManagerPolicy |String |No |none |The topology management policy. Valid values:<br><br><br>* **none**: The topology management policy is disabled by default.<br><br>* **restricted**: kubelet accepts only pods that achieve optimal non\-uniform memory access (NUMA) alignment on the requested resources.<br><br>* **best\-effort**: Kubelet preferentially selects pods that achieve NUMA alignment on CPU and device resources.<br><br>* **single\-numa\-node**: Kubelet allows only pods that are aligned to the same NUMA node in terms of CPU and device resources. |
|MaxPods |Integer |No |110 |The maximum pods supported by the nodes. Default value: 110. |
|KubeApiQps |Integer |No |50 |The number of QPS for communication with the API server. <br><br><br>* The value is an integer. Valid values: 1 to 50.<br><br>* The default value is 50. |
|KubeApiBurst |Integer |No |100 |The maximum burst requests sent to the API server per second.<br><br><br>* The value is an integer. Valid values: 1 to 100.<br><br>* The default value is 100.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This value must be greater than or equal to the value of the <code>KubeApiQps</code> parameter.</div><br> |
|EvictionHard |Array of [EvictionHard](https://docs.byteplus.com/en/docs/90/21159#evictionhard) |No |\- |A set of hard eviction thresholds that trigger pod eviction. For detailed parameter descriptions, see the[ official documentation](https://kubernetes.io/docs/concepts/scheduling-eviction/node-pressure-eviction/).<br><br>To explicitly disable hard eviction, set the threshold to 0% or 100% on any resource.<br><br>Default values:<br><br><br>* memory.available: "100Mi"<br><br>* nodefs.available: "10%"<br><br>* nodefs.inodesFree: "5%"<br><br>* imagefs.available: "15%" |
|KubeReserved |Array of [ComputeResource](https://docs.byteplus.com/en/docs/90/21159#computeresource) |No |\- |The resources reserved by the node for Kubernetes system components. By default, resources are reserved based on half of the default value in the [node resource reservation policy](https://docs.byteplus.com/en/docs/vke/Node-resource-reservation-policies). |
|SystemReserved |Array of [ComputeResource](https://docs.byteplus.com/en/docs/90/21159#computeresource) |No |\- |The resources reserved for the operating system on the node. By default, resources are reserved based on half of the default value in the [node resource reservation policy](https://docs.byteplus.com/en/docs/vke/Node-resource-reservation-policies). |
|RegistryPullQps |Integer |No |5 |The QPS threshold for a cluster pulling images from Container Registry (CR).<br><br><br>* The value is an integer. Valid values: 1 to 50.<br><br>* Default value: 5. |
|RegistryBurst |Integer |No |10 |The maximum images concurrently pulled from CR.<br><br><br>* The value is an integer. Valid values: 1 to 100.<br><br>* Default value: 10.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You need to specify this parameter only when the value of the <code>RegistryPullQps</code> parameter is greater than 0. The value of this parameter must be greater than or equal to the value of the <code>RegistryPullQps</code> parameter.</div><br> |
|SerializeImagePulls |Boolean |No |true |Specify whether to serially pull images. Valid values:<br><br><br>* **true**: Serially pull images.<br><br>* **false**: (Default) Pull images in parallel to accelerate pod startup. |
|CpuManagerPolicy |String |No |none |The CPU manager policy. Valid values:<br><br><br>* **none**: The policy is the default policy.<br><br>* **static**: This policy allows pods with specific resource characteristics on the node to be granted enhanced CPU affinity and exclusivity. |
|FailSwapOn |Boolean |No |false |Specifies whether kubelet can run when swap is enabled on the node. Valid values:<br><br><br>* **true**: Prevents kubelet from running when swap is enabled on the node. This is the default value. This is the default protection mechanism in Kubernetes. Swap can interfere with precise memory limit control. As a result, containers may use more memory than expected, affecting the accuracy of Pod scheduling and out\-of\-memory (OOM) detection.<br><br>* **false**: Allows kubelet to run when swap is enabled on the node. This option applies when strict memory isolation is not required or when Kubernetes must run on existing nodes with swap configured. |
|ImageGcLowThresholdPercent |Integer |No |80 |The threshold for stopping Image garbage collection. During image garbage collection, collection stops when disk usage falls below this percentage.<br><br><br>* The value is an integer. Valid values: 0 to 100.<br><br>* Unit: percentage.<br><br>* Default value: 80.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">When configuring both <code>ImageGcHighThresholdPercent</code> and <code>ImageGcLowThresholdPercent</code>, ensure that <code>ImageGcLowThresholdPercent</code> is less than <code>ImageGcHighThresholdPercent</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">You can set this parameter to 100. However, this value triggers cleanup only when disk usage reaches 100%. This value is extremely conservative and not recommended in production environments.</div><br> |
|ImageGcHighThresholdPercent |Integer |No |85 |The threshold for triggering image garbage collection. When disk usage exceeds this value, the system starts cleaning up unused images.<br><br><br>* The value is an integer. Valid values: 0 to 100.<br><br>* Unit: percentage.<br><br>* Default value: 85.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">When configuring both <code>ImageGcHighThresholdPercent</code> and <code>ImageGcLowThresholdPercent</code>, ensure that <code>ImageGcLowThresholdPercent</code> is less than <code>ImageGcHighThresholdPercent</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">You can set this parameter to 0. However, this value stops cleanup only after disk usage reaches 0%, which is almost impossible and has no practical value.</div><br> |


<span id="featuregates"></span>
### FeatureGates


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|QoSResourceManager |Boolean |No |false |Specify whether to enable quality of service (QoS) Resource Manager to support micro\-topology scheduling. Valid values:<br><br><br>* **true**: Enable QoS Resource Manager.<br><br>* **false**: (Default) Disable QoS Resource Manager.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This configuration takes effect only in clusters of the following versions:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">v1.24.15\-vke.13 ≤ Cluster version < v1.26</div><br><br><br>* <div data-tips="true" data-tips-type="tip">v1.26.10\-vke.13 ≤ Cluster version < v1.28</div><br> |
|InPlacePodVerticalScaling |Boolean |No |true |Specify whether to enable the vertical scaling feature for pods. Valid values:<br><br><br>* **true**: Enable the vertical scaling feature for pods.<br><br>* **false**: Disable it.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This configuration is supported only by the following cluster versions. Attempting to configure it on clusters of other versions is not allowed and will result in an error:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">v1.28.3\-vke.17 ≤ Custer version < v1.36</div><br> |


<span id="evictionhard"></span>
### EvictionHard


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Key |String |Yes |memory.available |The name of the hard eviction threshold. Valid values:<br><br><br>* memory.available<br><br>* nodefs.available<br><br>* nodefs.inodesFree<br><br>* imagefs.available |
|Value |String |Yes |1Gi |The hard eviction threshold value. The value can be an integer or a percentage.<br><br><br>* If the value is an integer, it indicates the specific threshold value of the resource. Unit: bytes. For example: 100Mi.<br><br>* If the value is a percentage, it indicates the proportion of the resource threshold value. Valid values: 0% to 100%. For example: 20%. To explicitly disable hard eviction, set the threshold to 0% or 100% on any resource. |


<span id="computeresource"></span>
### ComputeResource


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Name |String |Yes |cpu |Resource name. The value is **cpu** or **memory**. |
|Quantity |String |Yes |1G |Specify the quantity of the resource.<br><br><br>* When the resource is **cpu**, the example value is 200m.<br><br>* When the resource is **memory**, the sample value is 1 GB. |


<span id="nodepoolruntimerequest"></span>
### NodePoolRuntimeRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Type |String |No |containerd |Container runtime type. Values:<br><br><br>* **containerd**: (Default) The containerd runtime. |
|Version |String |No |1.6.38 |Container runtime version in the `x.x.x` format.<br><br>For a list of containerd versions for VKE, see the [containerd release notes](https://docs.byteplus.com/en/docs/vke/Containerd_Runtime_release_notes). |


<span id="nodepoolcontainerdconfig"></span>
### NodePoolContainerdConfig


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|InsecureRegistries |Array of String |No |["example.com"] |Specify the URL of the CR instance for which certificate authentication will be skipped. The value format is a domain name or IP address followed by an optional port number, for example, `example.com` or `example.com:8080`. Note that no protocol precedes the domain or IP address.<br><br>You can enter up to 10 domain names or IP addresses. |
|RegistryProxyConfigs |Array of [RegistryProxyConfig](https://docs.byteplus.com/en/docs/90/21159#registryproxyconfig) |No |\- |The proxy configuration of the container image registry. |


<span id="registryproxyconfig"></span>
### RegistryProxyConfig


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Registry |String |Yes |example.com |The address of the container image registry. The address format is [domain_or_IP][:port], where the port number is optional. Note that no protocol is included. Examples: `example.com` and `example.com:8080` |
|ProxyEndpoints |Array of String |Yes |["https://example.com"] |The proxy address. The format is [protocol]://[domain_or_IP][:port], where the protocol prefix is required, and the port number is optional. Examples: `https://example.com` and `https://example.com:8080`<br><br>You can enter up to five domain names or IP addresses. |


<span id="nodepoolnodeconfigrequest"></span>
### NodePoolNodeConfigRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|InstanceTypeIds |Array of String |Yes |["ecs.g1ie.large"] |The IDs of the ECS instance specifications that correspond to nodes.<br><br>You can call the [ListSupportedResourceTypes](https://docs.byteplus.com/en/docs/vke/ListSupportedResourceTypes) API to query the supported resource types and scope for instances in a cluster.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Up to 10 array elements can be specified.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">All specification types must remain consistent. For example, all are GPU\-type specifications, or all are non\-GPU\-type specifications.</div><br> |
|SubnetIds |Array of String |Yes |["subnet\-3rf6vwb\*\*\*\*\*\*"] |The IDs of the subnets to which the node network belongs.<br><br>You can call the [VPC API](https://docs.byteplus.com/en/docs/vpc/API-overview-1) to obtain subnet IDs.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The subnets must be in the same VPC as the cluster.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">A node pool can be associated with up to eight subnet IDs.</div><br> |
|ImageId |String |No |image\-kd\*\*\*\*\*\*\*\* |The ID of the image used by the ECS instance that corresponds to the node.<br><br>Image IDs vary based on different types of images. For details, see [Public images supported by VKE](https://docs.byteplus.com/en/docs/vke/Overview-of-operating-system-images#.5a655Zmo5pyN5Yqh5pSv5oyB55qE5YWs5YWx6ZWc5YOP).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If this parameter is not specified, an image ID from the veLinux 2.0 series is preferentially allocated.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">This parameter is required when multiple specifications are provided.</div><br> |
|SystemVolume |Object of [SystemVolume](https://docs.byteplus.com/en/docs/90/21159#systemvolume) |No |\- |System volume configuration of the node.<br><br>You can call the [DescribeInstanceTypes](https://docs.byteplus.com/en/docs/ecs/DescribeInstanceTypes) API of ECS to obtain the mappings between ECS instance families and cloud disk specifications. |
|DataVolumes |Array of [DataVolume](https://docs.byteplus.com/en/docs/90/21159#datavolume) |No |\- |Data volume configuration for the node.<br><br>You can call the [DescribeInstanceTypes API](https://docs.byteplus.com/en/docs/ecs/DescribeInstanceTypes) of ECS to obtain the mappings between ECS instance families and cloud disk specifications. |
|InitializeScript |String |No |ZWNobyAid\*\*\*\*\*\* |The custom script that is executed after a node is created and initialized.<br><br>The script supports the shell format, and you need to Base64\-encode the script content before passing it in.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Base64\-encoded content can be up to 8 KB in length. If you specify both the <strong>InitializeScript</strong> and <strong>PreScript</strong> parameters, the total length of the two parameter values cannot exceed 8 KB.</div><br> |
|Security |Object of [NodeSecurityRequest](https://docs.byteplus.com/en/docs/90/21159#nodesecurityrequest) |Yes |\- |The node security configurations. |
|AdditionalContainerStorageEnabled |Boolean |No |false |Whether to format the first data volume of the node and mount it to the container and image storage directory `/var/lib/containerd`. Valid values:<br><br><br>* **false**: (Default) Disabled.<br><br>* **true**<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">At least one data volume must be configured. Otherwise, the node pool creation will fail.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If you enable this option, the first data volume of the node is formatted and a filesystem is created.</div><br> |
|InstanceChargeType |String |No |PostPaid |The billing type of ECS instances. Values:<br><br><br>* **PostPaid**: (Default) Pay\-as\-you\-go<br><br>* **PrePaid**: Subscription |
|Period |Integer |No |12 |The subscription duration of ECS instances. Unit: months. Valid values:<br><br>**1**, **2**, **3**, **4**, **5**, **6**, **7**, **8**, **9**, **12**, **24**, and **36**<br><br>This parameter is required only when `InstanceChargeType` is PrePaid. |
|AutoRenew |Boolean |No |true |Whether to automatically renew ECS instances upon expiration. Valid values:<br><br><br>* **true**: (Default value) Renew automatically<br><br>* **false**: Do not renew automatically<br><br>   This parameter is required only when `InstanceChargeType` is PrePaid. Otherwise, it can be omitted. |
|AutoRenewPeriod |Integer |No |1 |Auto\-renewal duration per cycle for ECS instances Unit: month. Valid values:<br><br>**1** (Default), **2**, **3**, **6**, and **12**<br><br>It is required only if `AutoRenew` is set to true. |
|NamePrefix |String |No |prefix\-name |The prefix of the node name. If this parameter is left empty, the node name prefix is not used. The prefix is disabled by default. The prefix is validated based on the following rules:<br><br><br>* It can contain uppercase and lowercase letters, digits, and hyphens (`-`).<br><br>* It can only start with a letter and end with a letter or digit.<br><br>* Consecutive hyphens (`-`) are not permitted.<br><br>* It can be 2 to 51 characters in length. |
|Tags |Array of [Tag](https://docs.byteplus.com/en/docs/90/21159#tag) |No |\- |The tags added to the ECS instances that correspond to nodes. The tags are used for filtering and managing ECS instances.<br><br><br>* Each **Key** in **Tags** must be unique.<br><br>* If the resource already has the same **Tags.Key**, an error will not occur if you bind the same **Tags.Key** again. Instead, the latest **Tags.Value** will be used.<br><br>* Up to 20 tags can be added to a single resource.<br><br>* The **Key** and **Value** in **Tags** cannot start or end with a space. |
|HpcClusterIds |Array of String |No |["hpcCluster\-1"] |The ID of the high\-performance compute (HPC) cluster.<br><br>If you create a node pool with **High Performance Computing Optimized** specifications, you need to specify the ID of the target HPC cluster. You can obtain the ID on the **Instances & Images** \> **HPC Cluster** page in the [ECS console](https://console.byteplus.com/ecs).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">You can enter only one HPC cluster ID. For more information, see <a href="https://docs.byteplus.com/en/docs/gpu/HPC-cluster-overview">HPC cluster overview</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Make sure that the specified HPC cluster and the subnets specified in <strong>SubnetIds</strong> are located in the same availability zone.</div><br> |
|SpotStrategy |String |No |NoSpot |The preemptive​ instance strategy for pay\-as\-you\-go billing. This parameter is valid only when `InstanceChargeType` is PostPaid. Valid values:<br><br><br>* **NoSpot**: (Default) Regular pay\-as\-you\-go billing.<br><br>* **SpotAsPriceGo**: The system automatically bids, following the current market price.<br><br>* **SpotWithPriceLimit**: Sets a maximum price by instance specification. |
|InstancesDistribution |Object of [InstancesDistribution](https://docs.byteplus.com/en/docs/90/21159#instancesdistribution) |No |\- |Configure the blending policy for preemptive​ instances and pay\-as\-you\-go instances. This policy takes effect when `SpotStrategy` is set to SpotAsPriceGo. |
|ProjectName |String |No |default |The project name of the ECS instances added to the node pool during scale\-out. Each ECS instance can only belong to one project.<br><br><br>* It can only contain letters, digits, underscores (`_`), dots (`.`), and hyphens (`-`).<br><br>* It can be up to 64 characters in length.<br><br>* Default value: default. |
|PublicAccessEnabled |Boolean |No |false |Specify whether to automatically bind EIPs to nodes. Valid values:<br><br><br>* **false**: This is the default value. The system does not automatically bind EIPs to nodes. If you need to access nodes over the public network later, see [Applying for an EIP and associating it with an ECS instance](https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP-and-associating-an-ECS-instance).<br><br>* **true**: Enabled The system automatically binds EIPs to nodes in the cluster. In this case, you also need to specify the **PublicAccessConfig** parameter to specify custom EIPs. |
|PublicAccessConfig |Object of [EipConfigRequest](https://docs.byteplus.com/en/docs/90/21159#eipconfigrequest) |No |\- |Automatic EIP binding configuration for nodes. |
|Hostname |String |No |test\-name |The hostname that corresponds to the node. The following two naming formats are supported: fixed growth sorting and dynamic expansion sorting. For details on the relevant naming format, see [Naming formats](https://docs.byteplus.com/en/docs/as/Setting-sequential-and-unique-names-or-hostnames-for-instances). |
|PreScript |String |No |ZWNoby\*\*\*\*\*\* |The script to execute before node deployment. Enter the Base64\-encoded shell script.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Base64\-encoded content can be up to 8 KB in length. If you specify both the <strong>InitializeScript</strong> and <strong>PreScript</strong> parameters, the total length of the two parameter values cannot exceed 8 KB.</div><br> |
|InstanceName |String |No |instance\-test |The node (instance) name. The following two naming formats are supported: fixed growth sorting and dynamic expansion sorting. For details on the relevant naming format, see [Naming formats](https://docs.byteplus.com/en/docs/as/Setting-sequential-and-unique-names-or-hostnames-for-instances). |
|NetworkTrafficMode |String |No |Standard |The network communication mode between nodes. Valid values:<br><br><br>* **HighPerformance**: A communication method for data transmission based on RDMA.<br><br>* **Standard**: A communication method for data transmission based on TCP. |
|DeploymentSetId |String |No |dps\-yc1\*\*\*\*\*\*\*\* |ID of the deployment set to which the nodes in the node pool are added.<br><br>You can call the [DescribeDeploymentSets](https://docs.byteplus.com/en/docs/ecs/DescribeDeploymentSets) API to obtain the deployment set ID. |
|DeploymentSetGroupNumber |Integer |No |1 |When the specified deployment set policy is high availability of deployment set groups, you can use this parameter. It specifies the ID of the Deployment set group that the instance belongs to.<br><br>Value range: 1–3. |
|GpuDriverConfig |Object of [GpuDriverConfig](https://docs.byteplus.com/en/docs/90/21159#gpudriverconfig) |No |\- |GPU driver configuration for the node. This configuration takes precedence over the `GpuDriverVersion` field.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If this parameter is not configured and the ECS instance in the node pool uses a GPU\-type model, the system automatically sets <code>InstallGpuDriver</code> to <code>true</code> and populates the recommended GPU driver version.</div><br> |
|SpotPriceLimits |Array of [InstanceTypeSpotPriceLimit](https://docs.byteplus.com/en/docs/90/21159#instancetypespotpricelimit) |No |\- |The maximum price for spot instances.<br><br><br>* This parameter takes effect only when `SpotStrategy` is set to `SpotWithPriceLimit`.<br><br>* The value is an array in which each item specifies an instance specification and its maximum price in USD/hour. |
|GpuDriverVersion |String |No |550.127.05 | **[This parameter is deprecated. Use GpuDriverConfig instead.]**  Specifies the GPU driver version to be installed on the node.<br><br>You can call the [ListSupportedGpuDriverVersions](https://docs.byteplus.com/en/docs/vke/ListSupportedGpuDriverVersions) API to obtain the list of GPU driver versions that can be installed for an image. |
|AffinityGroupConfig |Object of [AffinityGroupConfig](https://docs.byteplus.com/en/docs/90/21159#affinitygroupconfig) |No |\- |[[Beta - apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] Affinity group configuration for the node pool.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">To use this feature, you need to obtain beta access to both the VKE feature and ‌the ECS affinity group capabilities‌. Consult your BytePlus account manager for details.</div><br> |


<span id="systemvolume"></span>
### SystemVolume


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Type |String |No |ESSD_PL0 |Cloud disk type. Valid values:<br><br><br>* **ESSD_PL0**: ESSD of the PL0 specification. This value is used by default.<br><br>* **ESSD_FlexPL**: ESSD of the FlexPL specification.<br><br>* **Ultra_Disk**: Ultra disk.<br><br>* **TSSD_TL0**: Throughput SSD of the TL0 specification.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">This parameter is required when you update a node pool and has no default value.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">[Beta]: The ultra disk SSD (Ultra_Disk) is a beta feature of EBS and is available only in specific regions and for ECS instances. To request feature access, contact your account manager.</div><br> |
|Size |Integer |No |40 |Cloud disk capacity, in GiB. Valid values:<br><br><br>* Default value: 40.<br><br>* Valid values: 40 to 2048.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This parameter is required when you update a node pool and has no default value.</div><br> |
|BurstEnabled |Boolean |No |true |Whether to enable performance bursting. Valid values:<br><br><br>* **true**: Enabled<br><br>* **false**: (Default) Disable it.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is supported only when the cloud disk type is <strong>ESSD_FlexPL</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After you enable the performance bursting feature for ESSD FlexPL cloud disks, you will be charged based on the burst performance usage.</div><br> |
|SubgroupNumber |Integer |No |2 |The number of the storage placement sub\-group to which the system volume belongs.<br><br>You can call the [DescribePlacementGroupDetails](https://docs.byteplus.com/en/docs/ecs/Describeplacementgroupdetails) API to obtain the number of the placement sub\-group. |
|PlacementGroupId |String |No |pg\-bp67\*\*\*\*\*\*\* |The ID of the storage placement group to which the system volume belongs.<br><br>You can call the [DescribePlacementGroupDetails](https://docs.byteplus.com/en/docs/ecs/Describeplacementgroupdetails) API to obtain the placement group ID. |


<span id="datavolume"></span>
### DataVolume


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Type |String |No |ESSD_PL0 |The disk type. The cloud disk and local disk are supported.<br><br><br>* Cloud disks:<br><br>   * **ESSD_PL0**: ESSD of the PL0 specification. This value is used by default.<br><br>   * **ESSD_FlexPL**: ESSD of the FlexPL specification.<br><br>   * **Ultra_Disk**: Ultra disk.<br><br>   * **TSSD_TL0**: Throughput SSD of the TL0 specification.<br><br>   * **RSSD_PL0**: Remote elastic disk of the PL0 specification.<br><br>* Local disks:<br><br>   * **LOCAL_SSD**: Local SSD.<br><br>   * **LOCAL_HDD**: Local HDD.<br><br>   * **LOCAL_LVM_SSD**: Local LVM\-managed SSD.<br><br>   * **LOCAL_SSD_SRIOV**: Local SSD SRIOV<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">This parameter is required when you update a node pool and has no default value.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">[Beta]: Remote elastic disks (RSSD_PL0) and Ultra disks (Ultra_Disk) are EBS beta features. They are available only in some regions and for some ECS instances. To request feature access, contact your account manager.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When you configure local disks:</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">Local disks are provided along with ECS instances. When you specify a local disk type, no additional local disk will be created.</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">Confirm the local disk types that are supported by the instance specification configured for the node pool. For details, see <a href="https://docs.byteplus.com/en/docs/ecs/Local-volumes">Local disks</a>.</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">The number of local disks configured in the node pool cannot exceed that of those mounted to the ECS instances. You can call the <a href="https://docs.byteplus.com/en/docs/ecs/DescribeInstanceTypes">DescribeInstanceTypes</a> API to query the number of local disks mounted to instances.</div><br> |
|Size |Integer |No |20 |The disk capacity. Unit: GiB. Valid values:<br><br><br>* ESSD (ESSD_PL0 and ESSD_FlexPL): The default value is 20. The value range is 20 to 32768.<br><br>* Ultra disk (Ultra_Disk): The default value is 20. The value range is 20 to 32768.<br><br>* Throughput SSD (TSSD_TL0): The default value is 40. The value range is 40 to 32768.<br><br>* The valid values for remote elastic disk (RSSD_PL0) are 256 to 16384, with 256 used by default.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This parameter is required when you update a node pool and has no default value.</div><br> |
|MountPoint |String |No |/vke |The target mount directory after disk formatting. The value must meet the following requirements:<br><br><br>* It must start with a slash (`/`).<br><br>* It must be 1 to 255 characters in length.<br><br>* The mount directory for each data volume must be unique. |
|FileSystem |String |No |Ext4 |[[Beta - apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] The file system of the node pool data volume. Valid values:<br><br><br>* **Ext4** (Default)<br><br>* **Xfs** |
|SnapshotId |String |No |snap\-31ak\*\*\*\*\*\*\*\* |The ID of the snapshot that is used for creating the data volume. You can call the [DescribeSnapshots](https://docs.byteplus.com/en/docs/ecs/Describesnapshots) API to query the snapshot ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Only the ESSD and ultra disk types support the creation of cloud disks through snapshots.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Only snapshots in one of the following states support creating cloud disks:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">available</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">creating</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">rollbacking</div><br> |
|KmsKeyId |String |No |e91b2a39\-72\*\*\*\*\*\*\*\* |The ID of the KMS key used to encrypt the data volume. This parameter takes effect only when `Encrypted` is set to `true`.<br><br><br>* If this parameter is not specified or is empty, the default key is used.<br><br>* This parameter is required when you use a custom key. In this case, you need to specify the KMS key ID for encryption. |
|Encrypted |Boolean |No |true |Whether to enable data volume encryption. Valid values:<br><br><br>* **true**: Enable data volume encryption. After this feature is enabled, files on the data disk are stored in encrypted form, preventing unauthorized access to data at the storage layer and meeting data security compliance requirements.<br><br>* **false**: Disable data volume encryption. This is the default value. |
|BurstEnabled |Boolean |No |true |Whether to enable performance bursting. Valid values:<br><br><br>* **true**: Enabled<br><br>* **false**: (Default) Disable it.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is supported only when the cloud disk type is <strong>ESSD_FlexPL</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After you enable the performance bursting feature for ESSD FlexPL cloud disks, you will be charged based on the burst performance usage.</div><br> |
|SubgroupNumber |Integer |No |2 |The number of the storage placement sub\-group to which the data volume belongs.<br><br>You can call the [DescribePlacementGroupDetails](https://docs.byteplus.com/en/docs/ecs/Describeplacementgroupdetails) API to query the number of the storage placement sub\-group. |
|PlacementGroupId |String |No |pg\-bp67a\*\*\*\*\*\*\*\* |The number of the storage placement group to which the data volume belongs.<br><br>You can call the [DescribePlacementGroups](https://docs.byteplus.com/en/docs/ecs/Describeplacementgroups) API to query the storage placement group ID. |
|ExtraPerformanceIops |Integer |No |10 |The IOPS of extra performance for the cloud disk. This parameter takes effect only when the extra performance type is `IOPS` or `Balance`. The value is an integer within the range of 1 to 50000 and represents operations per second. |
|ExtraPerformanceTypeId |String |No |Bal\*\*\*\* |Extra performance type.<br><br><br>* This parameter can be configured only if the cloud disk specification is `ESSD_FlexPL`. Values:<br><br>   * **Balance**: The balance type.<br><br>   * **IOPS**: The IOPS type.<br><br>   * **Throughput**: The throughput type.<br><br>* This parameter can be configured only if the cloud disk specification is `TSSD_TL0`. Values:<br><br>   * **Throughput**: The throughput type. |
|ExtraPerformanceThroughputMb |Integer |No |10 |The throughput of the extra performance configuration for the cloud disk. This parameter takes effect only if the extra performance type is `Throughput`. The value is an integer. Unit: MB/s.<br><br><br>* When the cloud disk specification is `ESSD_FlexPL`, the value range is 1 to 650. For more details, see [ESSD FlexPL cloud disks](https://docs.byteplus.com/en/docs/ecs/essd_flexpl_volume).<br><br>* When the cloud disk specification is `TSSD_TL0`, the details are as follows: <br><br>   * The value range is related to the cloud disk capacity. The throughput performance is calculated through the following formula: `min {120 + 0.5 × Capacity (GiB), 1000}`, and the value cannot exceed the maximum throughput (1000 MB/s) of the cloud disk. For more details, see [Throughput SSD cloud disks](https://docs.byteplus.com/en/docs/ecs/Volume-specification-tssd-tl0-Volume).<br><br>   * For example, when the cloud disk capacity is 500 GiB, the base throughput is 370 MB/s, which is the calculation result of 120 + 0.5 × 500. In this case, the allowed range of extra performance is 1 to 630.<br><br>   * For example, when the cloud disk capacity is 2,000 GiB, the base throughput is 1,120 MB/s, which is the calculation result of 120 + 0.5 × 2,000. In this case, the maximum allowed throughput has been exceeded. Therefore, extra performance cannot be configured. |


<span id="nodesecurityrequest"></span>
### NodeSecurityRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Login |Object of [NodeLoginRequest](https://docs.byteplus.com/en/docs/90/21159#nodeloginrequest) |Yes |\- |The node access configurations.<br><br>You can use a password or key pair. If both are provided, the key pair takes precedence. |
|SecurityGroupIds |Array of String |No |["sg\-2byy13c\*\*\*\*\*\*"] |The IDs of security groups where the node network is located.<br><br>Call the [DescribeSecurityGroups](https://docs.byteplus.com/en/docs/vpc/DescribeSecurityGroups) API of VPC to obtain the security group IDs.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The security groups must be in the same VPC as the cluster.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If this parameter is left empty, the <strong>default security group for cluster nodes</strong> is used. The name of the security group is in the format of <ClusterID\>\-common. For details about the default security group, see <a href="https://docs.byteplus.com/en/docs/vke/Security-group-settings">Security group settings</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">A single node pool can be associated with up to five security groups, including the default security group for nodes.</div><br> |
|SecurityStrategies |Array of String |No |["Hids"] |The security policy for the node. Valid values:<br><br><br>* If the value is empty, security reinforcement is not enabled for the node.<br><br>* **Hids**: Host security reinforcement is used. |


<span id="nodeloginrequest"></span>
### NodeLoginRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Password |String |No |UHdkM\*\*\*\*\*\* |The login password of the root user. The value must be Base64\-encoded.<br><br>The password must meet the following ECS instance password requirements:<br><br><br>* It must be 8 to 30 characters in length.<br><br>* It cannot start with `/` or `$6$`.<br><br>* It needs to contain at least three of the following character types:<br><br>   * Lowercase letters `a` to `z`<br><br>   * Uppercase letters `A` to `Z`<br><br>   * Digits: `0` to `9`<br><br>   * Special characters: `( )`~! @ # $ % ^ & \* _ \- + = |
|SshKeyPairName |String |No |test\-key |The name of the SSH key pair. Make sure that the key pair has been created or managed in ECS. |


<span id="tag"></span>
### Tag


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Key |String |Yes |key |The tag key.<br><br><br>* It cannot start with `volc:` in ‌any case variation‌.<br><br>* It can only contain letters, digits, spaces, and special characters `_.:/=+-@`.<br><br>* The length is limited to 1 to 128 characters. |
|Value |String |No |value |The tag value, which can be left empty.<br><br><br>* It can only contain letters, digits, spaces, and the following special characters: `_.:/=+-@`.<br><br>* Its length does not exceed 256 characters. |


<span id="instancesdistribution"></span>
### InstancesDistribution


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|CapacityRebalance |Boolean |No |false |Specify whether to enable the feature to supplement preemptive​ instance capacity with pay\-as\-you\-go instances. Valid values:<br><br><br>* **true**: Enabled Before spot instances are reclaimed, new spot instances are proactively created for compensation.<br><br>* **false**: (Default) Disabled. A scale\-out is performed to replenish the instance count only after the preemptive​ instance has been reclaimed.<br><br>   For details, see [Node pools of preemptive​ instances](https://docs.byteplus.com/en/docs/vke/Preemptible_instance_node_pool). |
|OnDemandBaseCapacity |Integer |No |0 |The base capacity of pay\-as\-you\-go instances. When the number of pay\-as\-you\-go instances in the node pool is less than this value, pay\-as\-you\-go instances will be preferentially created.<br><br><br>* Default value: 0.<br><br>* Value range: It varies based on whether the node pool has the **autoscaling** feature enabled (i.e., `AutoScalingEnabled` is set to `true`). The maximum value does not exceed 500.<br><br>   The details are as follows:<br><br>   * When the autoscaler is not enabled, valid values are from 0 to the expected number of nodes in the node pool.<br><br>   * When the autoscaler is enabled, valid values are from 0 to the minimum number of nodes configured for the autoscaler. |
|CompensateWithOnDemand |Boolean |No |false |Specify whether to enable supplement of pay\-as\-you\-go instances. Valid values:<br><br><br>* **true**: Enabled When all preemptive​ instances fail to be purchased due to insufficient inventory or other reasons, the system attempts to purchase pay\-as\-you\-go instances.<br><br>* **false**: (Default) Disabled. During scale\-out, the system attempts to purchase configured preemptive​ instances only when they are required. |
|OnDemandPercentageAboveBaseCapacity |Integer |No |0 |Percentage of pay\-as\-you\-go instances in the node pool. When you calculate the number of pay\-as\-you\-go instances based on the percentage, you need to round up the value.<br><br><br>* Valid values: 0 to 100.<br><br>* Unit: %<br><br>* Default value: 0. This indicates that the portion exceeding the base capacity only consists of preemptive​ instances.<br><br>* A value of 100 indicates that the node pool only consists of pay\-as\-you\-go instances. |


<span id="eipconfigrequest"></span>
### EipConfigRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Isp |String |No |BGP |The line type of the EIP. Valid values:<br><br><br>* **BGP**: BGP (multi\-line) |
|Bandwidth |Integer |No |100 |The maximum bandwidth of the EIP. Unit: Mbit/s. Valid values:<br><br><br>* If `BillingType is set to 2`, the valid values of Bandwidth are 1 to 500, and the default value is 10.<br><br>* If `BillingType is set to 3`, the valid values of Bandwidth are 1 to 200, and the default value is 10. |
|BillingType |Integer |No |3 |The billing type of the EIP. Valid values:<br><br><br>* **3**: (Default) Pay\-as\-you\-go \- by actual traffic. This billing method requires a maximum bandwidth limit and incurs fees based on the actual outbound traffic over the Internet, regardless of the usage duration.<br><br>* **2**: Pay\-as\-you\-go \- by bandwidth limit. After you specify a maximum bandwidth, fees are calculated based on the usage duration, regardless of the actual traffic. |
|BandwidthPackageId |String |No |bwp\-2zeo\*\*\*\*\*\*\*\* |The ID of the shared bandwidth package. The EIP address is added to the shared bandwidth package.<br><br>You can call the [DescribeBandwidthPackages](https://docs.byteplus.com/en/docs/bandwidthpackage/DescribeBandwidthPackages) API to query the ID of the shared bandwidth package.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">An EIP address can be added to a shared bandwidth package only when all of the following conditions are met:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The line types are identical.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The shared bandwidth package is of type IPv4.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">No security protection is configured for the shared bandwidth package.</div><br> |


<span id="gpudriverconfig"></span>
### GpuDriverConfig


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|GpuDriverVersion |String |No |580.105.08 |Specifies the GPU driver version to be installed on the node.<br><br><br>* You can call the [ListSupportedGpuDriverVersions](https://docs.byteplus.com/en/docs/vke/ListSupportedGpuDriverVersions) API to obtain the list of GPU driver versions that can be installed for an image.<br><br>* When the configuration is empty, the system automatically populates the recommended GPU driver version based on the GPU model.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If you specify multiple ECS instance specifications in the node pool, the supported GPU drivers may vary with instance specifications. You need to specify a GPU driver supported by all instance specifications. Otherwise, an error will occur.</div><br> |
|InstallGpuDriver |Boolean |No |true |Specifies whether to automatically install the GPU driver when the node is a GPU\-type ECS instance that uses a public base image (for example, veLinux 1.0 or Ubuntu 22.04). Valid values:<br><br><br>* **true**: Automatically installs the GPU driver. If you set the parameter to this value, you can use the `GpuDriverVersion` parameter to specify a GPU driver.<br><br>* **false**: Does not automatically install the GPU driver.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When the ECS instance is a GPU\-type model, this parameter defaults to <strong>true</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the ECS instance is a non\-GPU model, this configuration does not take effect.</div><br> |


<span id="instancetypespotpricelimit"></span>
### InstanceTypeSpotPriceLimit


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|InstanceTypeId |String |Yes |ecs.g1i\*\*\*\*\*\*\* |Instance specification ID. The specified instance specification must be included in the list of ECS instance specification IDs for the nodes. This applies even if the specification is specified by the `InstanceTypeIds` parameter. |
|SpotPriceLimit |Double |Yes |0.321 |The maximum price for spot instances of this instance specification. Unit: USD/hour. Up to three decimal places are supported. |


<span id="affinitygroupconfig"></span>
### AffinityGroupConfig


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Size |Integer |No |2 |[[Beta - apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] Affinity group size used by the node pool. To query the affinity group size, call the [DescribeInstanceTypes](https://docs.byteplus.com/en/docs/ecs/DescribeInstanceTypes) API. |
|Enabled |Boolean |No |false |[[Beta - apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] Whether to enable affinity group configuration for the node pool. Valid values:<br><br><br>* **true**: Enables affinity group\-based node purchases in the node pool.<br><br>* **false**: (Default) Disables affinity groups and uses standard node purchasing. |


<span id="nodepoolautoscalingrequest"></span>
### NodePoolAutoScalingRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Enabled |Boolean |No |false |Specify whether to enable the autoscaler feature for the node pool. Valid values:<br><br><br>* **false**: The autoscaler feature is disabled by default.<br><br>* **true**: Enabled |
|Priority |Integer |No |10 |The priority. Valid values:<br><br><br>* Default value: 10.<br><br>* Valid values: 0 to 100.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This configuration takes effect only after the autoscaler feature is enabled for the node pool and the scale\-out algorithm is priority.</div><br> |
|MaxReplicas |Integer |No |10 |Specify the maximum nodes in the node pool. Valid values:<br><br><br>* Default value: 10.<br><br>* Valid values: 1 to 2000<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This configuration takes effect only after the autoscaler feature is enabled for the node pool.</div><br> |
|MinReplicas |Integer |No |0 |Specify the minimum number of nodes in the node pool. Valid values:<br><br><br>* Default value: 0<br><br>* Minimum value: 0<br><br>* Maximum value: The maximum value is less than the value of the **MaxReplicas** parameter.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This configuration takes effect only after the autoscaler feature is enabled for the node pool.</div><br> |
|SubnetPolicy |String |No |ZoneBalance |The scheduling policy for multiple subnets of the node pool. Worker nodes are scheduled based on the subnet priority during scale\-out. Valid values:<br><br><br>* **ZoneBalance**: (Default) Balancing across availability zones. For a node scale\-out, new nodes are distributed across subnets in multiple availability zones to ensure a relatively balanced number of nodes in each availability zone.<br><br>* **Priority**: Subnet priority\-based scheduling. Scheduling is performed according to the order of the subnets in the list. If the highest\-priority subnet is available for successful creation, new nodes will always be added to that subnet. |
|DesiredReplicas |Integer |No |0 |The expected number of nodes in the node pool. Valid values:<br><br><br>* Default value: 0.<br><br>* Valid values: 0 to 2000<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When you enable the autoscaler feature for the node pool, the value of the <strong>DesiredReplicas</strong> parameter must be greater than or equal to the value of the <strong>MinReplicas</strong> parameter, and must be less than or equal to the value of the <strong>MaxReplicas</strong> parameter.</div><br> |


<span id="nodepoolmanagementrequest"></span>
### NodePoolManagementRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Enabled |Boolean |No |false |Specify whether to enable the managed mode for the node pool. Valid values:<br><br><br>* **true**: Enabled<br><br>* **false**: This mode is disabled by default.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After you enable the managed mode for the node pool, the cloud assistant Agent will be installed for newly added instances by default.</div><br> |
|RemedyConfig |Object of [RemedyConfigRequest](https://docs.byteplus.com/en/docs/90/21159#remedyconfigrequest) |No |\- |The check and self\-healing rule configuration of the node pool. |


<span id="remedyconfigrequest"></span>
### RemedyConfigRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Enabled |Boolean |No |false |Specify whether to enable node check and self\-healing after you enable the managed mode for the node pool. Valid values:<br><br><br>* **true**: Enabled<br><br>* **false**: (Default) Disable it. |
|Id |String |No |R2025091\*\*\*\*\*\*\*\* |The ID of the node self\-healing rule to be associated after you enable check and self\-healing for the node pool. If you do not specify this parameter, the node pool will automatically create and bind the rule.<br><br>View the self\-healing rule ID on the **Health check & auto recovery** page of the target cluster in the [VKE console](https://console.byteplus.com/vke). |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vke.cn-beijing.byteplusapi.com.cn?Action=CreateNodePool&Version=2022-05-12
Content-Type: application/json
{
    "ClientToken": "BC028527-33B9-4990-A633-84E9F9******",
    "ClusterId": "cc5silu*******",
    "Name": "test-nodepool",
    "KubernetesConfig": {
        "Labels": [
            {
                "Key": "label-key",
                "Value": "label-value"
            }
        ],
        "Taints": [
            {
                "Key": "taint-key",
                "Value": "taint-value",
                "Effect": "NoSchedule"
            }
        ],
        "Cordon": false,
        "NamePrefix": "name-prefix",
        "NameSuffix": "-demo",
        "NameUseHostname": true,
        "AutoSyncDisabled": false
    },
    "NodeConfig": {
        "InstanceTypeIds": [
            "ecs.**.**"
        ],
        "SubnetIds": [
            "subnet-3rf6vwb******"
        ],
        "ImageId": "image-kd********",
        "SystemVolume": {
            "Type": "ESSD_PL0",
            "Size": 40
        },
        "DataVolumes": [
            {
                "Type": "ESSD_PL0",
                "Size": 20,
                "MountPoint": "/vke",
                "FileSystem": "Ext4"
            }
        ],
        "InitializeScript": "ZWNoby******",
        "Security": {
            "SecurityGroupIds": [
                "sg-2byy13c******"
            ],
            "SecurityStrategies": [
                "Hids"
            ],
            "Login": {
                "Password": "UHdkMT******",
                "SshKeyPairName": "test-key"
            }
        },
        "AdditionalContainerStorageEnabled": false,
        "InstanceChargeType": "PostPaid",
        "Period": 12,
        "AutoRenew": true,
        "AutoRenewPeriod": 1,
        "NamePrefix": "prefix-name",
        "Tags": [
            {
                "Key": "key",
                "Value": "value"
            }
        ],
        "HpcClusterIds": [
            "hpcCluster-1"
        ],
        "SpotStrategy": "NoSpot",
        "ProjectName": "default",
        "PublicAccessConfig": {
            "BillingType": 3,
            "Bandwidth": 100,
            "Isp": "BGP"
        },
        "PublicAccessEnabled": false,
        "Hostname": "test-name",
        "PreScript": "ZWNoby******",
        "InstanceName": "instance-test",
        "NetworkTrafficMode": "Standard",
        "DeploymentSetId": "dps-yc1********",
        "DeploymentSetGroupNumber": 1,
        "GpuDriverConfig": {
            "GpuDriverVersion": "580.105.08",
            "InstallGpuDriver": true
        }
    },
    "AutoScaling": {
        "Enabled": false,
        "Priority": 10,
        "MaxReplicas": 10,
        "MinReplicas": 0,
        "SubnetPolicy": "ZoneBalance",
        "DesiredReplicas": 0
    },
    "Tags": [
        {
            "Key": "key",
            "Value": "value"
        }
    ],
    "Management": {
        "Enabled": false,
        "RemedyConfig": {
            "Id": "R202509152********",
            "Enabled": false
        }
    }
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

The following table contains the response parameters of this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Id |String |pc51i0\*\*\*\*\*\*\* |The node pool ID. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041********",
        "Action": "CreateNodePool",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {
        "Id": "pc51i0*******"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for this API are listed in the table below. For public error codes, see [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes).


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|409 |Conflict.Name |The specified name conflicts with existing {{resourceType}}. |A resource with the same name exists in the specified region. Update the resource name and try again. |
|400 |NotSupported.{{parameter}} |The specified {{resourceType}} {{resourceContent}} is not supported. |The specified parameter (such as InstanceType or ImageId) is not supported. Check the parameter and try again. |
|400 |QuotaExceeded.NodePool |The number of node pools in the cluster has reached the limit. |The number of node pools in the cluster has reached the upper limit. You can select another region or [submit a ticket](https://console.byteplus.com/ticket/createTicketV2/?step=2&Service=vke) to apply for a quota increase. |
|400 |LimitExceeded.MaximumVolumes |You have reached the limit of the number of volumes that you can create. |The number of cloud disks exceeds the maximum cloud disks that can be mounted to a single ECS instance. For the usage restrictions on ECS, see [Constraints](https://docs.byteplus.com/en/docs/ecs/Limits). |
|400 |LimitExceeded.DataVolumeSize |You have reached the limit of the size of data volume that you can create. |The data volume capacity exceeds the upper limit. For ECS limits, see [Limits](https://docs.byteplus.com/en/docs/ecs/Limits). |
|400 |LimitExceeded.SystemVolumeSize |You have reached the limit of the size of the system volume that you can create. |The system volume capacity exceeds the upper limit. For ECS limits, see [Limits](https://docs.byteplus.com/en/docs/ecs/Limits). |
|400 |ClusterVpcMismatch.{{parameter}} |The specified {{resourceType}} {{resourceId}} is not in the VPC of cluster. |The specified subnets, security groups, and HPC cluster belong to different VPCs from the cluster. Make sure that they are in the same VPC as the cluster. |
|400 |Mismatch.Replicas |The specified DesiredReplicas, MinReplicas and MaxReplicas are mismatched. |The specified minimum, maximum, and desired number of nodes​ in the node pool are logically inconsistent. Check the parameter and try again. |
|400 |OperationDenied.ClusterStatus |The action is forbidden due to cluster status {{statusPhase}} and {{statusConditions}}. |The current status of the specified cluster does not support this operation. Confirm the required cluster status for this API and try again. |
|400 |QuotaExceeded.Node |The number of nodes in the cluster has reached the limit. |The number of nodes in the current cluster has reached the limit. You can select another region or [submit a ticket](https://console.byteplus.com/ticket/createTicketV2/?step=2&Service=vke) to apply for a quota increase. |
|400 |LimitExceeded.NodeInCluster |The number of nodes exceeds the cluster\-defined pods config limit. |The maximum nodes specified for the node pool exceeds the maximum nodes supported by the Flannel cluster. For limits on various resources of VKE, see [Resource limits](https://docs.byteplus.com/en/docs/vke/Limits).<br><br>The supported maximum nodes depend on **PodsConfig.FlannelConfig.PodCidrs** and **MaxPodsPerNode**. After a cluster is created, it cannot be modified. You need to plan cluster settings based on your business requirements. |
|400 |InstanceTypeMismatch.VolumeType |The specified VolumeType {{volumeType}} and InstanceType {{instanceType}} are mismatched. |The specified instance specification and cloud disk specification do not match. Call the [DescribeInstanceTypes](https://docs.byteplus.com/en/docs/ecs/DescribeInstanceTypes) API of ECS to obtain the matching relationship between ECS instance specifications and cloud disk specifications, update the parameter, and then try again. |
|400 |ZoneMismatch.InstanceType |The specified InstanceType {{instanceType}} and subnet zones are mismatched. |The availability zone of the subnet does not support the instance specification. Call the [DescribeAvailableResource](https://docs.byteplus.com/en/docs/ecs/DescribeAvailableResource) API of ECS to obtain the instance specifications supported in each availability zone. Then, update the parameters and try again. |
|400 |OutOfRange.DataVolumes |There is no data volume for additional container storage enabling. |The first data volume of the node is specified as the storage for container images and logs (namely, AdditionalContainerStorageEnabled=true), but no data volume has been specified in the **DataVolume** parameter. Specify the parameter and try again. |
|400 |ZoneMismatch.Subnet |The specified Subnet {{subnetId}} is not in the cluster\-defined zones. |The availability zone to which the specified subnet belongs is not supported by the cluster. Use a subnet that is deployed in the availability zones of the cluster. |
|400 |QuotaExceeded.{{ResourceType}} |The quota of {{ResourceType}} has reached the limit. |The quota for the specified resource (such as EIPs, ECS instances, tags, ECS tags, and EBS) has reached the upper limit. Increase the relevant resource quota or delete unused resources. When the available quota is sufficient, try again later. |
|400 |ZoneMismatch.HpcCluster |The specified HpcCluster {{hpcClusterID}} and subnet zones are mismatched. |The specified availability zone of the HPC cluster does not match that of the node subnet. Make sure that both availability zones are consistent and try again. |
|400 |ClusterVersionMismatch.ImageId |The specified ImageId {{imageId}} and KubernetesVersion {{kubernetesVersion}} are mismatched. |The specified image ID (**ImageId**) does not match the cluster Kubernetes version. Please specify a proper value according to the parameter description and try again later. |
|400 |ReplicasMismatch.OnDemandBaseCapacity |The specified DesiredReplicas, MinReplicas and OnDemandBaseCapacity are mismatched. |In the preemptive​ node pool, **OnDemandBaseCapacity** does not match **DesiredReplicas** and **MinReplicas**. Check the parameter and try again. |
|400 |InstanceChargeTypeMismatch.SpotStrategy |The specified SpotStrategy {{spotStrategy}} and InstanceChargeType {{instanceChargeType}} are mismatched. |The specified preemption policy and billing type do not match. Subscription node pools do not support preemption policies. Specify the parameter and try again. |
|400 |SpotStrategyMismatch.InstanceType |The specified InstanceType {{instanceType}} and SpotStrategy {{spotStrategy}} are mismatched. |The specified instance specification and preemption policy do not match. Specify the instance specification and try again. |
|400 |Insufficient.Balance |Your account has run out of balance. |The balance of the current account is insufficient. Top up your account and try again. |
|400 |InstanceTypeMismatch.ImageId |The specified ImageId {{imageId}} and InstanceType {{instanceType}} are mismatched. |The specified image ID (**ImageId**) does not match the ECS instance specification (**InstanceTypeIds**). Specify appropriate parameter values based on the parameter descriptions and try again. |
|400 |IpFamilyMismatch.{{parameter}} |The specified {{resourceType}} {{resourceContent}} and IpFamily {{ipFamily}} are mismatched. |The specified resources do not match the network protocol stack. Confirm the network protocol stack supported by the resources and try again. |
|400 |LimitExceeded.LocalVolumes |You have reached the limit of the number of local volumes that you can use. |The quantity of local disks exceeds the limit. Specify appropriate parameter values based on the parameter descriptions and try again. |
|400 |KubernetesVersionMismatch.{{parameter}} |The specified config and kubernetes version are mismatched. |The specified parameter does not match the Kubernetes version. Confirm the Kubernetes version supported by the parameter and try again. |
|400 |ImageSizeMismatch.SystemVolumeSize |The specified system volume size and image size are mismatched. |The specified system volume size does not match the image size. The system volume must be at least 10 GiB larger than the image. Specify appropriate parameter values based on the parameter descriptions and try again. |
|400 |SnapshotIdMismatch.DataVolumeType |The specified data volume type {{volumeType}} and SnapshotId are mismatched. |The specified data volume type does not match SnapshotId. Configure the correct parameter values based on the parameter description and try again. |
|400 |SnapshotIdMismatch.DataVolumeSize |The specified data volume size and data SnapshotId are mismatched. |The disk size specified for the data volume must be greater than the cloud disk size that corresponds to SnapshotId. Specify appropriate parameter values based on the parameter descriptions and try again. |
|400 |PlacementGroupMismatch.SubgroupNumber |The specified SubgroupNumber {{subgroupNumber}} and PlacementGroup {{placementGroupId}} are mismatched. |The specified placement sub\-group does not match the placement group. Specify appropriate parameter values based on the parameter descriptions and try again. |
|400 |InstanceTypeMismatch.HpcCluster |The specified HpcCluster {{hpcClusterID}} and InstanceType {{instanceType}} are mismatched. |The specified high\-performance cluster does not match the instance specification. Specify appropriate parameter values based on the parameter descriptions and try again. |
|400 |Mismatch.InstanceTypeIds |The specified InstanceTypeIds are mismatched. |The ECS instance specifications for the node pool do not match. A valid set of allowed instance specifications cannot span the CPU, GPU, Bare Metal categories or different GPU vendors. Please specify a proper value according to the parameter description and try again later. |
|400 |OperationDenied.DeploymentSetGroupNumber |The operation has been denied due to the specified DeploymentSetGroupNumber. |The specified deployment set group does not support this action. Specify appropriate parameter values based on the parameter descriptions and try again. |
|400 |DeploymentSetMismatch.InstanceType |The specified InstanceType {{instanceType}} and DeploymentSet {{deploymentSetId}} are mismatched. |The specified instance specification does not match the deployment set. Update the parameter and try again. |
|400 |ZoneMismatch.VolumeType |The specified volume type {{volumeType}} and subnet zones are mismatched. |The specified cloud disk type does not match the availability zone of the subnet. Specify a cloud disk that matches the availability zone of the subnet and try again. |
|400 |NetworkTrafficModeMismatch.InstanceType |The specified InstanceType {{instanceType}} and NetworkTrafficMode {{networkTrafficMode}} are mismatched. |The specified instance specification does not match the network communication mode. Please specify a proper value according to the parameter description and try again later. |
|400 |IpFamilyMismatch.PublicAccessEnabled |The specified Config PublicAccessEnabled and cluster IpFamily {{ipFamily}} are mismatched. |The cluster network stack does not match with automatic EIP binding for the nodes. Specify appropriate parameter values based on the parameter descriptions and try again. |
|400 |InstanceChargeTypeMismatch.AutoScalingEnabled |The specified AutoScalingEnabled and InstanceChargeType {{instanceChargeType}} are mismatched. |The specified autoscaler switch and billing type do not match. You cannot enable the autoscaler for subscription node pools. |
|400 |KubernetesVersionMismatch.RuntimeVersion |The specified runtime version {{runtimeVersion}} and kubernetes version {{kubernetesVersion}} are mismatched. |The specified container runtime version does not match the cluster Kubernetes version. For example, containerd 2.1.x is only supported in clusters with Kubernetes v1.34 or later. Specify another container runtime version and try again later. For more information, see the [containerd release notes](https://docs.byteplus.com/en/docs/vke/Containerd_Runtime_release_notes). |
|400 |LimitExceeded.ScriptLength |The InitializeScript and PreScript total length exceeds maximum allowed length. |The total length of the pre\-script and post\-script exceeds the limit. Specify appropriate parameter values based on the parameter descriptions and try again. |
|400 |PublicAccessConfigMismatch.BandwidthPackageId |The specified BandwidthPackage {{bandwidthPackageId}} does not match the PublicAccessConfig. |The specified shared bandwidth package does not match the public access configuration. Specify appropriate parameter values based on the parameter descriptions and try again. |
|400 |UnsupportedVolumeType.BurstEnabled |The specified VolumeType {{volumeType}} does not support BurstEnabled. |The specified cloud disk type does not support performance bursting. Change the cloud disk type and try again later. |
|400 |UnsupportedInstanceChargeType.BurstEnabled |The specified InstanceChargeType {{instanceChargeType}} does not support BurstEnabled. |The specified instance billing type does not support performance bursting. Change the cloud disk billing type and try again later. |
