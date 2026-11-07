---
title: "CreateDefaultNodePool"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/CreateDefaultNodePool"
---

Create a default node pool in the specified cluster.

<span id=".5L2_55So6K-05piO"></span>
## Usage instructions


* In addition to standard custom node pools, VKE supports the **default node pool** with the fixed name `vke-default-nodepool`, which is used to manage existing ECS instances. After you create the default node pool, you can add existing ECS instances to it by calling the [CreateNodes](https://docs.byteplus.com/en/docs/vke/CreateNodes) API.

* Before you call this API, first call the [ListSupportedResourceTypes](https://docs.byteplus.com/en/docs/vke/ListSupportedResourceTypes) API to confirm whether the resources required for default node pool creation are supported in the specified region and availability zone.

* This is an asynchronous API. When this API returns a success message, the ID of the default node pool is included in the response, and the node pool enters the `{Creating, [Progressing]}` state, which stays until the creation is successful. You can call the [ListNodePools](https://docs.byteplus.com/en/docs/vke/ListNodePools) API to obtain the current status of the node pool, based on which you check whether the node pool has been created successfully.

* The default node pool does not consume your node pool quota. For details about quota, see [Limit](https://docs.byteplus.com/en/docs/vke/Limits).


<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point for your business region.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=CreateDefaultNodePool&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateDefaultNodePool&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table describes the API request parameters. You also need to provide public parameters when calling this API. See [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters) for details.


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |CreateDefaultNodePool |The API name. The name of the current API is `CreateDefaultNodePool`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|ClientToken |String |No |BC028527\-33B9\-4990\-A633\-84E9F9\*\*\*\*\*\* |A string used to ensure the idempotency of the request. This string is passed in by the caller and must be unique across different requests. ClientToken is case\-sensitive and can consist of 64 ASCII characters at most. |
|ClusterId |String |Yes |cc5silu\*\*\*\*\*\*\* |The ID of the cluster where the default node pool is located.<br><br>Cluster IDs can be obtained by calling the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The cluster must be in the <code>{Running,[Ok]}</code> or <code>{Updating,[Progressing]}</code> state. You can call the <a href="https://docs.byteplus.com/en/docs/vke/ListClusters">ListClusters</a> API to obtain the current status of the cluster.</div><br> |
|KubernetesConfig |Object of [NodePoolKubernetesConfigRequest](https://docs.byteplus.com/en/docs/90/21158#nodepoolkubernetesconfigrequest) |No |\- |The Kubernetes configuration of the default node pool. |
|NodeConfig |Object of [DefaultNodePoolNodeConfigRequest](https://docs.byteplus.com/en/docs/90/21158#defaultnodepoolnodeconfigrequest) |Yes |\- |The ECS instance configurations for the default node pool. |
|Tags |Array of [Tag](https://docs.byteplus.com/en/docs/90/21158#tag) |No |\- |Default tags for classifying, retrieving, and aggregating node pools with similar characteristics from different dimensions. Node pool tags enable you to manage node pools more flexibly and efficiently.<br><br><br>* Each **Key** of **Tags** must be unique.<br><br>* If the resource already has the same **Tags.Key**, an error will not occur if you bind the same **Tags.Key** again. Instead, the latest **Tags.Value** will be used.<br><br>* You can add up to 50 **labels** for each resource.<br><br>* The **Key** and **Value** in **Tags** cannot start or end with a space. |


<span id="nodepoolkubernetesconfigrequest"></span>
### NodePoolKubernetesConfigRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Labels |Array of [Label](https://docs.byteplus.com/en/docs/90/21158#label) |No |\- |The Kubernetes labels of the node pool or the node. Up to 20 labels can be provided.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The node pool manages the label configurations of nodes in a centralized manner. Therefore, the label information will be synchronized to all nodes in the node pool. When labels are changed, the original label configurations will be overwritten.</div><br> |
|Taints |Array of [Taint](https://docs.byteplus.com/en/docs/90/21158#taint) |No |\- |The Kubernetes taints of the node pool or the node. Up to 20 taints can be specified.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The node pool manages the taint configurations of nodes in a centralized manner. Therefore, the taint information will be synchronized to all nodes in the node pool. When taints are changed, the original taint configurations will be overwritten.</div><br> |
|Cordon |Boolean |No |false |Whether to cordon nodes. Valid values:<br><br><br>* **false**: Do not cordon nodes. This value is used by default.<br><br>* **true**: Cordon nodes.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When you update the configurations of a node pool, if you do not specify this parameter, the original parameter configurations are retained.</div><br> |
|NamePrefix |String |No |name\-prefix |The prefix of the metadata name for the node object in Kubernetes. This is disabled by default. If you specify this parameter, this option is enabled and will affect the prefix information shown in the `metadata.name` field of the Kubernetes node manifest file. The prefix is validated based on the following rules:<br><br><br>* It can contain lowercase letters, digits, hyphens (`-`), and periods (`.`).<br><br>* It can start only with a lowercase letter or digit.<br><br>* It can be 1 to 48 characters in length. |
|KubeletConfig |Object of [NodePoolKubeletConfig](https://docs.byteplus.com/en/docs/90/21158#nodepoolkubeletconfig) |No |\- |Specify custom kubelet parameters for nodes in the node pool.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The default node pool does not support custom kubelet configuration, and the related sub\-parameters that have been specified do not take effect.</div><br> |
|AutoSyncDisabled |Boolean |No |false |Whether to disable automatic synchronization of labels and taints to existing nodes. Values:<br><br><br>* **true**: Disable automatic synchronization.<br><br>* **false**: (Default) Enable automatic synchronization. |
|Runtime |Object of [NodePoolRuntimeRequest](https://docs.byteplus.com/en/docs/90/21158#nodepoolruntimerequest) |No |\- |Container runtime configuration. |
|NameSuffix |String |No |\-demo |The suffix of the metadata name for the node object in Kubernetes. |
|NameUseHostname |Boolean |No |true |Specify whether the metadata name of the node object in Kubernetes uses the ECS hostname. Valid values:<br><br><br>* **true**: Use the ECS hostname as the node name.<br><br>* **false**: Do not use the ECS hostname as the node name.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This configuration has higher priority than <code>NamePrefix</code> and <code>NameSuffix</code>.</div><br> |
|ContainerdConfig |Object of [NodePoolContainerdConfig](https://docs.byteplus.com/en/docs/90/21158#nodepoolcontainerdconfig) |No |\- |The containerd\-related configurations of the node pool.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The default node pool does not support containerd configuration, and the related sub\-parameters that have been specified do not take effect.</div><br> |


<span id="label"></span>
### Label


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Key |String |Yes |label\-key |The label key. |
|Value |String |No |label\-value |The label value. |


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
|FeatureGates |Object of [FeatureGates](https://docs.byteplus.com/en/docs/90/21158#featuregates) |No |\- |The feature gates, which are a set of key\-value pairs that describe Kubernetes features. |
|TopologyManagerScope |String |No |container |The resource granularity of the topology management policy. Valid values:<br><br><br>* **container**: The resource alignment granularity is at the container level. |
|TopologyManagerPolicy |String |No |none |The topology management policy. Valid values:<br><br><br>* **none**: The topology management policy is disabled by default.<br><br>* **restricted**: kubelet accepts only pods that achieve optimal non\-uniform memory access (NUMA) alignment on the requested resources.<br><br>* **best\-effort**: Kubelet preferentially selects pods that achieve NUMA alignment on CPU and device resources.<br><br>* **single\-numa\-node**: Kubelet allows only pods that are aligned to the same NUMA node in terms of CPU and device resources. |
|MaxPods |Integer |No |110 |The maximum pods supported by the nodes. Default value: 110. |
|KubeApiQps |Integer |No |50 |The number of QPS for communication with the API server. <br><br><br>* The value is an integer. Valid values: 1 to 50.<br><br>* The default value is 50. |
|KubeApiBurst |Integer |No |100 |The maximum burst requests sent to the API server per second.<br><br><br>* The value is an integer. Valid values: 1 to 100.<br><br>* The default value is 100.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This value must be greater than or equal to the value of the <code>KubeApiQps</code> parameter.</div><br> |
|EvictionHard |Array of [EvictionHard](https://docs.byteplus.com/en/docs/90/21158#evictionhard) |No |\- |A set of hard eviction thresholds that trigger pod eviction. For detailed parameter descriptions, see the[ official documentation](https://kubernetes.io/docs/concepts/scheduling-eviction/node-pressure-eviction/).<br><br>To explicitly disable hard eviction, set the threshold to 0% or 100% on any resource.<br><br>Default values:<br><br><br>* memory.available: "100Mi"<br><br>* nodefs.available: "10%"<br><br>* nodefs.inodesFree: "5%"<br><br>* imagefs.available: "15%" |
|KubeReserved |Array of [ComputeResource](https://docs.byteplus.com/en/docs/90/21158#computeresource) |No |\- |The resources reserved by the node for Kubernetes system components. By default, resources are reserved based on half of the default value in the [node resource reservation policy](https://docs.byteplus.com/en/docs/vke/Node-resource-reservation-policies). |
|SystemReserved |Array of [ComputeResource](https://docs.byteplus.com/en/docs/90/21158#computeresource) |No |\- |The resources reserved for the operating system on the node. By default, resources are reserved based on half of the default value in the [node resource reservation policy](https://docs.byteplus.com/en/docs/vke/Node-resource-reservation-policies). |
|RegistryPullQps |Integer |No |5 |The QPS threshold for a cluster pulling images from Container Registry (CR).<br><br><br>* The value is an integer. Valid values: 1 to 50.<br><br>* Default value: 5. |
|RegistryBurst |Integer |No |10 |The maximum images concurrently pulled from CR.<br><br><br>* The value is an integer. Valid values: 1 to 100.<br><br>* Default value: 10.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You need to specify this parameter only when the value of the <code>RegistryPullQps</code> parameter is greater than 0. The value of this parameter must be greater than or equal to the value of the <code>RegistryPullQps</code> parameter.</div><br> |
|SerializeImagePulls |Boolean |No |true |Specify whether to serially pull images. Valid values:<br><br><br>* **true**: Serially pull images.<br><br>* **false**: (Default) Pull images in parallel to accelerate pod startup. |
|CpuManagerPolicy |String |No |none |The CPU manager policy. Valid values:<br><br><br>* **none**: The policy is the default policy.<br><br>* **static**: This policy allows pods with specific resource characteristics on the node to be granted enhanced CPU affinity and exclusivity. |


<span id="featuregates"></span>
### FeatureGates


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|QoSResourceManager |Boolean |No |false |Specify whether to enable quality of service (QoS) Resource Manager to support micro\-topology scheduling. Valid values:<br><br><br>* **true**: Enable QoS Resource Manager.<br><br>* **false**: (Default) Disable QoS Resource Manager.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This configuration takes effect only in clusters of the following versions:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">v1.24.15\-vke.13 ≤ Cluster version < v1.26</div><br><br><br>* <div data-tips="true" data-tips-type="tip">v1.26.10\-vke.13 ≤ Cluster version < v1.28</div><br> |
|InPlacePodVerticalScaling |Boolean |No |true |Specify whether to enable the vertical scaling feature for pods. Valid values:<br><br><br>* **true**: Enable the vertical scaling feature for pods.<br><br>* **false**: Disable.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This configuration is supported only by the following cluster versions. Attempting to configure it on clusters of other versions is not allowed and will result in an error:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">v1.28.3\-vke.17 ≤ Custer version < v1.36</div><br> |


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
|Type |String |No |containerd |Container runtime type. Values:<br><br>**containerd**: (Default) The containerd runtime. |
|Version |String |No |1.6.38 |Container runtime version in the `x.x.x` format.<br><br>For a list of containerd versions for VKE, see the [containerd release notes](https://docs.byteplus.com/en/docs/vke/Containerd_Runtime_release_notes). |


<span id="nodepoolcontainerdconfig"></span>
### NodePoolContainerdConfig


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|InsecureRegistries |Array of String |No |["example.com"] |Specify the URL of the CR instance for which certificate authentication will be skipped. The value format is a domain name or IP address followed by an optional port number, for example, `example.com` or `example.com:8080`. Note that no protocol precedes the domain or IP address.<br><br>You can enter up to 10 domain names or IP addresses. |
|RegistryProxyConfigs |Array of [RegistryProxyConfig](https://docs.byteplus.com/en/docs/90/21158#registryproxyconfig) |No |\- |The proxy configuration of the container image registry. |


<span id="registryproxyconfig"></span>
### RegistryProxyConfig


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Registry |String |Yes |example.com |The address of the container image registry. The address format is [domain_or_IP][:port], where the port number is optional. Note that no protocol is included. Examples: `example.com` and `example.com:8080` |
|ProxyEndpoints |Array of String |Yes |["https://example.com"] |The proxy address. The format is [protocol]://[domain_or_IP][:port], where the protocol prefix is required, and the port number is optional. Examples: `https://example.com` and `https://example.com:8080`<br><br>You can enter up to five domain names or IP addresses. |


<span id="defaultnodepoolnodeconfigrequest"></span>
### DefaultNodePoolNodeConfigRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Tags |Array of [Tag](https://docs.byteplus.com/en/docs/90/21158#tag) |No |\- |The tags added to the ECS instances that correspond to nodes. The tags are used for filtering and managing ECS instances.<br><br><br>* Each **Key** of **Tags** must be unique.<br><br>* If the resource already has the same **Tags.Key**, an error will not occur if you bind the same **Tags.Key** again. Instead, the latest **Tags.Value** will be used.<br><br>* Up to 20 tags can be added to a single resource.<br><br>* The **Key** and **Value** in **Tags** cannot start or end with a space. |
|Security |Object of [NodeSecurityRequest](https://docs.byteplus.com/en/docs/90/21158#nodesecurityrequest) |Yes |\- |The node security configurations. |
|PreScript |String |No |ZWNoby\*\*\*\*\*\* |[[Beta - apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] The script to execute before node deployment. Enter the Base64\-encoded shell script.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Base64\-encoded content can be up to 8 KB in length. If you specify both the <strong>InitializeScript</strong> and <strong>PreScript</strong> parameters, the total length of the two parameter values cannot exceed 8 KB.</div><br> |
|NamePrefix |String |No |prefix\-name |The prefix of the node name. If this parameter is left empty, the node name prefix is not used. The prefix is disabled by default. The prefix is validated based on the following rules:<br><br><br>* The prefix can contain uppercase and lowercase letters, digits, and hyphens (\-).<br><br>* The prefix can only start with a letter and end with a letter or digit.<br><br>* Hyphens (\-) cannot be used consecutively.<br><br>* The prefix can be 2 to 51 characters in length. |
|InitializeScript |String |No |ZWNoby\*\*\*\*\*\* |The custom script that is executed after a node is created and initialized.<br><br>The script supports the shell format, and you need to Base64\-encode the script content before passing it in.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Base64\-encoded content can be up to 8 KB in length. If you specify both the <strong>InitializeScript</strong> and <strong>PreScript</strong> parameters, the total length of the two parameter values cannot exceed 8 KB.</div><br> |


<span id="tag"></span>
### Tag


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Key |String |Yes |key |The label key.<br><br><br>* It cannot start with `volc:` in ‌any case variation‌.<br><br>* It can only contain characters, digits, spaces, and special characters `_.:/=+-@`.<br><br>* The length is limited to 1 to 128 characters. |
|Value |String |No |value |The tag value, which can be left empty.<br><br><br>* It can only contain language characters, digits, spaces, and the following special characters: `_.:/=+-@`.<br><br>* Its length does not exceed 256 characters. |


<span id="nodesecurityrequest"></span>
### NodeSecurityRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Login |Object of [NodeLoginRequest](https://docs.byteplus.com/en/docs/90/21158#nodeloginrequest) |Yes |\- |The node access configurations.<br><br>You can use a password or key pair. If both are provided, the key pair takes precedence. |
|SecurityGroupIds |Array of String |No |["sg\-2byy13c\*\*\*\*\*\*"] |The IDs of security groups where the node network is located.<br><br>Call the [DescribeSecurityGroups](https://docs.byteplus.com/en/docs/vpc/DescribeSecurityGroups) API of VPC to obtain the security group IDs.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The security groups must be in the same VPC as the cluster.</div><br><br><br><div data-tips="true" data-tips-type="warning">If this parameter is left empty, the <strong>default security group for cluster nodes</strong> is used. The name of the security group is in the format of <ClusterID\>\-common. For details about the default security group, see <a href="https://docs.byteplus.com/en/docs/vke/Security-group-settings">Security group settings</a>.</div><br><br><br><div data-tips="true" data-tips-type="warning">A single node pool can be associated with up to five security groups, including the default security group for nodes.</div><br> |
|SecurityStrategies |Array of String |No |["Hids"] |The security policy for the node. Valid values:<br><br><br>* If the value is empty, security reinforcement is not enabled for the node.<br><br>* **Hids**: Host security reinforcement is used. |


<span id="nodeloginrequest"></span>
### NodeLoginRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Password |String |No |UHdkM\*\*\*\*\*\* |The login password of the root user. The value must be Base64\-encoded.<br><br>The password must meet the following ECS instance password requirements:<br><br><br>* It must be 8 to 30 characters in length.<br><br>* It cannot start with `/` or `$6$`.<br><br>* It needs to contain at least three of the following character types:<br><br>   * Lowercase letters `a` to `z`<br><br>   * Uppercase letters `A` to `Z`<br><br>   * Digits: `0` to `9`<br><br>   * Special characters: `( )`~! @ # $ % ^ & \* _ \- + = |
|SshKeyPairName |String |No |test\-key |The name of the SSH key pair. Make sure that the key pair has been created or managed in ECS. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vke.cn-beijing.byteplusapi.com.cn?Action=CreateDefaultNodePool&Version=2022-05-12 HTTP/1.1
Content-Type:application/json
{
    "ClusterId": "cc5silum********",
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
        "Cordon": false
    },
    "NodeConfig": {
        "InitializeScript": "ZWNobyAidG******",
        "Security": {
            "SecurityGroupIds": [
                "sg-2byy13cnsc******"
            ],
            "SecurityStrategies": [
                "Hids"
            ],
            "Login": {
                "Password": "UHdkM******"
            }
        },
        "NamePrefix": "name-prefix",
        "Tags": [
            {
                "Key": "key",
                "Value": "value"
            }
        ]
    },
    "Tags": [
        {
            "Key": "key",
            "Value": "value"
        }
    ],
    "ClientToken": "BC028527-33B9-4990-A633-84E9F9******"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following table contains the response parameters of this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Id |String |pc51i0m\*\*\*\*\*\*\* |The default node pool ID. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1 200 OK
Content-Type:application/json

{
    "ResponseMetadata": {
        "RequestId": "021635330********",
        "Action": "CreateDefaultNodePool",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {
        "Id": "pc51i0m*******"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for this API are listed in the table below. For public error codes, see [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes).


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|409 |AlreadyExists.DefaultNodePool |The default node pool already exists. |The default node pool already exists and you do not need to create one. |
|400 |ClusterVpcMismatch.{{parameter}} |The specified {{resourceType}} {{resourceId}} is not in the VPC of cluster. |The specified subnets, security groups, and HPC cluster belong to different VPCs from the cluster. Make sure that they are in the same VPC as the cluster. |
|400 |OperationDenied.ClusterStatus |The action is forbidden due to cluster status {{statusPhase}} and {{statusConditions}}. |The current status of the specified cluster does not support this operation. Please confirm the required cluster status for this API and try again. |
|400 |QuotaExceeded.{{ResourceType}} |The quota of {{ResourceType}} has reached the limit. |The quota for the specified resource has reached the upper limit, such as tags and ECS tags. Increase the relevant resource quota or delete unused resources. When the available quota is sufficient, try again later. |
|400 |NotSupported.{{parameter}} |The specified {{resourceType}} {{resourceContent}} is not supported. |The specified parameter is not supported, such as **SecurityGroupIds**. Check the parameter and try again. |
|400 |KubernetesVersionMismatch.RuntimeVersion |The specified runtime version {{runtimeVersion}} and kubernetes version {{kubernetesVersion}} are mismatched. |The specified container runtime version does not match the cluster Kubernetes version. For example, containerd 2.1.x is only supported in clusters with Kubernetes v1.34 or later. Specify another container runtime version and try again later. For more information, see the [containerd release notes](https://docs.byteplus.com/en/docs/vke/Containerd_Runtime_release_notes). |
|400 |LimitExceeded.ScriptLength |The InitializeScript and PreScript total length exceeds maximum allowed length. |The total length of the pre\-script and post\-script exceeds the limit. Specify appropriate parameter values based on the parameter descriptions and try again. |
