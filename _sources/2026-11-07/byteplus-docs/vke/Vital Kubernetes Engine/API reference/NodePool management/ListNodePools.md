---
title: "ListNodePools"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/ListNodePools"
---

Return a list of node pools that meet the specified conditions.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point based on the region where your business is located.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=ListNodePools&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListNodePools&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameter

The following table describes the API request parameters. You also need to provide public parameters when calling this API. For details about public request parameters, see [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters).


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListNodePools |The API name. The name of the current API is `ListNodePools`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Filter |Object of [ListNodePoolsFilter](https://docs.byteplus.com/en/docs/90/21161#listnodepoolsfilter) |No |\- |Node pool filter. |
|Tags |Array of [ListTagFilter](https://docs.byteplus.com/en/docs/90/21161#listtagfilter) |No |\- |Query node pools based on tags.<br><br><br>* Each **Key** in **Tags** must be unique.<br><br>* The **Key** and **Value** in **Tags** cannot start or end with a space.<br><br>* Up to 10 tags are supported per call. |
|PageNumber |Integer |No |1 |The starting page number of the pagination query, starting from 1. |
|PageSize |Integer |No |10 |The number of results per page:<br><br><br>* Minimum value: 1<br><br>* Maximum value: 100 |


<span id="listnodepoolsfilter"></span>
### ListNodePoolsFilter


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Ids |Array of String |No |["pc51i0m\*\*\*\*\*\*"] |A list of node pool IDs.<br><br>At most 100 node pool IDs can be specified per call. |
|Name |String |No |test\-nodepool |The name of the node pool.<br><br>Fuzzy matching is supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If this parameter is left empty, all node pools within the specified cluster will be returned.</div><br> |
|Statuses |Array of [NodePoolStatusFilter](https://docs.byteplus.com/en/docs/90/21161#nodepoolstatusfilter) |No |\- |Node pool status.<br><br>Up to 15 array elements can be provided at a time. If multiple statuses are provided, they have a logical **OR** relationship. |
|ClusterIds |Array of String |No |["cc5silumr\*\*\*\*\*\*"] |A list of cluster IDs.<br><br>You can call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to obtain cluster IDs. Up to 100 cluster IDs can be included in a single query.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If this parameter is an empty array, filtering is performed based on all clusters in the specified region within the account.</div><br> |
|CreateClientToken |String |No |BC028527\-33B9\-4990\-A633\-84E9F9\*\*\*\*\*\* |The ClientToken generated upon successful creation.<br><br>The ClientToken is a string that ensures request idempotency. This string is provided by the caller. |
|UpdateClientToken |String |No |BC028527\-33B9\-4990\-A633\-84E9F9\*\*\*\*\*\* |The ClientToken generated for the last successful update.<br><br>The ClientToken is a string that ensures request idempotency. This string is provided by the caller. |
|AutoScaling.Enabled |Boolean |No |true |Autoscaling switch for the node pool. Valid values:<br><br><br>* **true**: Enable autoscaling.<br><br>* **false**: Disable autoscaling. |


<span id="nodepoolstatusfilter"></span>
### NodePoolStatusFilter


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Phase |String |No |Running |Filter by node pool status. Values:<br><br><br>* **Creating**: It is being created.<br><br>* **Running**: It is running.<br><br>* **Updating**: It is being updated.<br><br>* **Deleting**: It is being deleted.<br><br>* **Scaling**: Being scaled<br><br>* **Failed**: It is experiencing an anomaly.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">At least one of <strong>Phase</strong> and <strong>Conditions.Type</strong> must be provided. Otherwise, it is an invalid array element. For valid combinations of <strong>Phase</strong> and <strong>Conditions.Type</strong>, see <a href="https://docs.byteplus.com/en/docs/vke/Resource-status-description">Resource status description</a>.</div><br> |
|Conditions.Type |String |No |Ok |Filter by the current node pool status. Values:<br><br><br>* **Progressing**<br><br>* **Ok**: The status is normal.<br><br>* **ResourceCleanupFailed**: Resource cleanup failed.<br><br>* **Unknown**: Creation failure due to unknown reasons<br><br>* **ClusterNotRunning**: The cluster is not running as expected.<br><br>* **ScalingFailed**: Scaling failed.<br><br>* **ClusterVersionUpgrading**: The cluster node version is being upgraded.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">At least one of <strong>Phase</strong> and <strong>Conditions.Type</strong> must be provided. Otherwise, it is an invalid array element. For valid combinations of <strong>Phase</strong> and <strong>Conditions.Type</strong>, see <a href="https://docs.byteplus.com/en/docs/vke/Resource-status-description">Resource status description</a>.</div><br> |


<span id="listtagfilter"></span>
### ListTagFilter


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Key |String |Yes |key |The tag key.<br><br><br>* It cannot start with volc: in ‌any case variation‌.<br><br>* It can contain only letters, digits, spaces, and the following special characters: `_ .` `: / = + - @`。<br><br>* The length is limited to 1 to 128 characters. |
|Value |String |No |value |A single tag value. It is used to match one candidate value under the same tag key.<br><br><br>* It can contain only letters, digits, spaces, and the following special characters: `_ .` `: / = + - @`。<br><br>* Its length does not exceed 256 characters.<br><br>* This can be left blank.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When both Value and <strong>Values</strong> are provided, the label values are merged into the same candidate set for matching. They are neither mutually exclusive nor deduplicated.</div><br> |
|Values |Array of String |No |["value1","value2"] |The list of tag values. It is used to match multiple candidate values under the same tag key.<br><br><br>* Each tag value needs to meet the following conditions:<br><br>   * It can contain only letters, digits, spaces, and the following special characters: `_ .` `: / = + - @`。<br><br>   * Its length does not exceed 256 characters.<br><br>* Multiple tag values are separated with commas (,).<br><br>* This can be left blank.<br><br>* After you specify the parameter values, clusters matching any tag value in this list will be filtered.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When both <strong>Value</strong> and Values are provided, the label values are merged into the same candidate set for matching. They are neither mutually exclusive nor deduplicated.</div><br> |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vke.cn-beijing.byteplusapi.com.cn?Action=ListNodePools&Version=2022-05-12 HTTP/1.1
Content-Type:application/json
{
    "PageNumber": 1,
    "PageSize": 10,
    "Filter": {
        "ClusterIds": [
            "cc5silum******"
        ],
        "Statuses": [
            {
                "Phase": "Running",
                "Conditions.Type": "Ok"
            }
        ]
    },
    "Tags": [
        {
            "Key": "key",
            "Value": "value"
        }
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

The following table contains the response parameters of this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Items |Array of [NodePool](https://docs.byteplus.com/en/docs/90/21161#nodepool) |\- |A list of node pools. |
|TotalCount |Integer |100 |Total number of node pools that meet the conditions. |
|PageNumber |Integer |1 |The current page number. |
|PageSize |Integer |10 |Number of node pools displayed per page. |


<span id="nodepool"></span>
### NodePool


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Id |String |pc51i0\*\*\*\*\*\*\* |The node pool ID. |
|Name |String |test\-nodepool |The name of the node pool. |
|Tags |Array of [TagResponse](https://docs.byteplus.com/en/docs/90/21161#tagresponse) |\- |Tags added to the node pool. |
|Status |Object of [NodePoolStatus](https://docs.byteplus.com/en/docs/90/21161#nodepoolstatus) |\- |Node pool status. |
|ClusterId |String |cc5silu\*\*\*\*\*\*\* |Cluster ID. |
|CreateTime |String |2021\-10\-27T10:33:30Z |Time when the node pool was created.<br><br>UTC+0 time in standard [RFC3339](https://tools.ietf.org/html/rfc3339) format. |
|Management |Object of [NodePoolManagementResponse](https://docs.byteplus.com/en/docs/90/21161#nodepoolmanagementresponse) |\- |The management configuration of the node pool. |
|NodeConfig |Object of [NodePoolNodeConfigResponse](https://docs.byteplus.com/en/docs/90/21161#nodepoolnodeconfigresponse) |\- |The ECS instance configuration for the node pool. |
|UpdateTime |String |2021\-10\-29T10:33:30Z |The time when the node pool was updated.<br><br>UTC+0 time in standard [RFC3339](https://tools.ietf.org/html/rfc3339) format. |
|AutoScaling |Object of [NodePoolAutoScalingResponse](https://docs.byteplus.com/en/docs/90/21161#nodepoolautoscalingresponse) |\- |Node pool scaling policy configuration. |
|NodeStatistics |Object of [NodeStatistics](https://docs.byteplus.com/en/docs/90/21161#nodestatistics) |\- |Statistics of nodes in the node pool. |
|KubernetesConfig |Object of [NodePoolKubernetesConfigResponse](https://docs.byteplus.com/en/docs/90/21161#nodepoolkubernetesconfigresponse) |\- |The Kubernetes configuration of the node pool. |
|CreateClientToken |String |BC028527\-33B9\-4990\-A633\-84E9F9\*\*\*\*\*\* |The ClientToken generated upon successful creation.<br><br>The ClientToken is a string that ensures request idempotency. This string is provided by the caller. |
|UpdateClientToken |String |BC028527\-33B9\-4990\-A633\-84E9F9\*\*\*\*\*\* |The ClientToken generated for the last successful update.<br><br>The ClientToken is a string that ensures request idempotency. This string is provided by the caller. |


<span id="tagresponse"></span>
### TagResponse


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Key |String |key |The tag key. |
|Type |String |Custom |Tag type. Valid values:<br><br><br>* **System:**  System tag<br><br>* **Custom**: User\-defined tag |
|Value |String |value |The label value. |


<span id="nodepoolstatus"></span>
### NodePoolStatus


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Phase |String |Running |The status of the node pool. Values:<br><br><br>* **Creating**: It is being created.<br><br>* **Running**: It is running.<br><br>* **Updating**: It is being updated.<br><br>* **Deleting**: It is being deleted.<br><br>* **Failed**: An abnormality has occurred.<br><br>* **Scaling**: Being scaled<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For valid combinations of <strong>Phase</strong> and <strong>Conditions.Type</strong>, see <a href="https://docs.byteplus.com/en/docs/vke/Resource-status-description">Resource status description</a>.</div><br> |
|Conditions |Array of [NodePoolStatusCondition](https://docs.byteplus.com/en/docs/90/21161#nodepoolstatuscondition) |\- |The condition under which the node pool enters the primary status. |


<span id="nodepoolstatuscondition"></span>
### NodePoolStatusCondition


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Type |String |Ok |The condition under which the node pool enters the primary status. Multiple conditions are possible. Values:<br><br><br>* **Progressing**<br><br>* **Ok**: The status is normal.<br><br>* **ResourceCleanupFailed**: Resource cleanup failed.<br><br>* **Unknown**: Creation failure due to unknown reasons<br><br>* **ClusterNotRunning**: The cluster is not running as expected.<br><br>* **ScalingFailed**: Scaling failed.<br><br>* **ClusterVersionUpgrading**: Cluster node versions are being upgraded.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For valid combinations of <strong>Phase</strong> and <strong>Conditions.Type</strong>, see <a href="https://docs.byteplus.com/en/docs/vke/Resource-status-description">Resource status description</a>.</div><br> |


<span id="nodepoolmanagementresponse"></span>
### NodePoolManagementResponse


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Enabled |Boolean |false |Whether the node pool is managed. Valid values:<br><br><br>* **true**: Enable it.<br><br>* **false**: Disable it. |
|RemedyConfig |Object of [RemedyConfigResponse](https://docs.byteplus.com/en/docs/90/21161#remedyconfigresponse) |\- |The check and self\-healing rule configuration of the node pool. |


<span id="remedyconfigresponse"></span>
### RemedyConfigResponse


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Enabled |Boolean |false |Whether check and self\-healing are enabled for a managed node pool. Values:<br><br><br>* **true**: Enable it.<br><br>* **false**: Disable it. |
|Id |String |R202\*\*\*\* |ID of the self\-healing rule that is associated with the node pool that has checking and self\-healing enabled. |


<span id="nodepoolnodeconfigresponse"></span>
### NodePoolNodeConfigResponse


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|InstanceTypeIds |Array of String |["ecs.g1ie.large"] |Specification IDs of instances that correspond to the nodes.<br><br>For a detailed description of the specifications, see [Instance types and specifications](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types). |
|SubnetIds |Array of String |["subnet\-3rf6g\*\*\*\*"] |The IDs of the subnets to which the node network belongs. |
|ImageId |String |image\-kd\*\*\*\*\*\*\*\* |ID of the image used by the ECS instance corresponding to the node. |
|SystemVolume |Object of [SystemVolume](https://docs.byteplus.com/en/docs/90/21161#systemvolume) |\- |System volume configuration of the node. |
|DataVolumes |Array of [DataVolume](https://docs.byteplus.com/en/docs/90/21161#datavolume) |\- |Data volume configuration for the node. |
|InitializeScript |String |ZWNobyAidG\*\*\*\*\*\* |The Base64\-encoded custom script that is executed after the node is created and initialized. |
|Security |Object of [NodeSecurityResponse](https://docs.byteplus.com/en/docs/90/21161#nodesecurityresponse) |\- |The node security configurations. |
|AdditionalContainerStorageEnabled |Boolean |false |Whether the first data volume of the node is configured and formatted to be mounted as the storage directory for container images and logs. Value description:<br><br><br>* **false**: Not configured and formatted.<br><br>* **true**: Configured and formatted. |
|InstanceChargeType |String |PostPaid |Billing type of ECS instances. Valid values:<br><br><br>* **PostPaid**: Pay\-as\-you\-go<br><br>* **PrePaid**: Subscription |
|Period |Integer |12 |The subscription duration of ECS instances. Unit: months.<br><br>This parameter is returned only when `InstanceChargeType` is PrePaid. |
|AutoRenew |Boolean |true |Whether automatic renewal is enabled for the ECS instance upon expiration. Values:<br><br><br>* **true**: Enables automatic renewal.<br><br>* **false**: Does not enable automatic renewal.<br><br>   This parameter is returned only when `InstanceChargeType` is PrePaid. |
|AutoRenewPeriod |Integer |1 |The automatic renewal duration in months for the ECS instance.<br><br>This parameter is returned only when `AutoRenew` is true. |
|NamePrefix |String |prefix\-name |The prefix of node names. An empty string or **nil** indicates that no node name prefix is applied. |
|HpcClusterIds |Array of String |["hpcCluster\-1"] |The ID of the high\-performance compute (HPC) cluster.<br><br>IDs of the high\-performance compute clusters. This parameter is returned if the node specification type for the node pool is High Performance Computing Optimized. |
|Tags |Array of [Tag](https://docs.byteplus.com/en/docs/90/21161#tag) |\- |Tags bound to the ECS instance corresponding to the node. |
|SpotStrategy |String |NoSpot |Spot strategy for pay\-as\-you\-go billing. Values:<br><br><br>* **NoSpot**: Regular pay\-as\-you\-go billing.<br><br>* **SpotAsPriceGo**: The system automatically bids, following the current market price.<br><br>* **SpotWithPriceLimit**: Sets a maximum price by instance specification. |
|InstancesDistribution |Object of [InstancesDistribution](https://docs.byteplus.com/en/docs/90/21161#instancesdistribution) | |Configure the blending policy for preemptive​ instances and pay\-as\-you\-go instances. This policy takes effect when `SpotStrategy` is set to SpotAsPriceGo. |
|ProjectName |String |default |The project to which ECS instances in the node pool belong. |
|PublicAccessConfig |Object of [EipConfigResponse](https://docs.byteplus.com/en/docs/90/21161#eipconfigresponse) | |Automatic EIP binding configuration for the node. |
|PublicAccessEnabled |Boolean |false |Whether to automatically bind EIPs to nodes. Valid values:<br><br><br>* **false**: Disable it.<br><br>* **true**: Enable this option. |
|Hostname |String |test\-name |Hostname corresponding to the node. |
|PreScript |String |ZWNobyAi\*\*\*\*\* |The Base64\-encoded content of the script to execute before node deployment. |
|InstanceName |String |instance\-test |Name of the node (instance). |
|DeploymentSetId |String |dps\-yc1o9aah\*\*\*\*\*\*\*\* |ID of the deployment set to which the nodes in the node pool belong. |
|SpotPriceLimits |Array of [InstanceTypeSpotPriceLimit](https://docs.byteplus.com/en/docs/90/21161#instancetypespotpricelimit) |\- |The maximum price for spot instances. |
|GpuDriverVersion |String |550.127.05 |The version of the GPU driver installed on the node. |
|NetworkTrafficMode |String |Standard |The network communication mode between nodes. Values:<br><br><br>* **HighPerformance**: A communication method for data transmission based on RDMA.<br><br>* **Standard**: A communication method for data transmission based on TCP. |
|AffinityGroupConfig |Object of [AffinityGroupConfig](https://docs.byteplus.com/en/docs/90/21161#affinitygroupconfig) |\- |[[Beta - apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] Affinity group configuration for the node pool.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The affinity group configuration for node pools is <strong>in beta</strong>. <strong>AffinityGroupConfig</strong> and its related sub\-parameters listed in this topic are returned only if you have obtained beta access to and used the feature.</div><br> |
|DeploymentSetGroupNumber |Integer |1 |Group number of the node in the deployment set. A value of 0 means that this setting is not configured. |


<span id="systemvolume"></span>
### SystemVolume


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Type |String |ESSD_PL0 |The cloud disk type. Valid values:<br><br><br>* **ESSD_PL0**: ESSD of the PL0 specification.<br><br>* **ESSD_FlexPL**: ESSD of the FlexPL specification.<br><br>* **Ultra_Disk**: [EBS beta] High performance SSD.<br><br>* **TSSD_TL0**: Throughput SSD of the TL0 specification. |
|Size |Integer |40 |Volume capacity, unit: GiB. |
|BurstEnabled |Boolean |true |Whether to enable performance bursting. |
|SubgroupNumber |Integer |2 |The number of the placement sub\-group to which the system volume belongs. |
|PlacementGroupId |String |pg\-bp67\*\*\*\*\*\*\* |The ID of the storage placement group to which the system volume belongs. |


<span id="datavolume"></span>
### DataVolume


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Type |String |ESSD_PL0 |The disk type:<br><br><br>* Cloud disks:<br><br>   * **ESSD_PL0**: ESSD of the PL0 specification.<br><br>   * **ESSD_FlexPL**: ESSD of the FlexPL specification.<br><br>   * **Ultra_Disk**: [EBS beta] High performance SSD.<br><br>   * **TSSD_TL0**: Throughput SSD of the TL0 specification.<br><br>   * **RSSD_PL0**: [EBS beta] Remote elastic disk of the PL0 specification.<br><br>* Local disks:<br><br>   * **LOCAL_SSD**: Local SSD.<br><br>   * **LOCAL_HDD**: Local HDD.<br><br>   * **LOCAL_LVM_SSD**: Local LVM\-managed SSD.<br><br>   * **LOCAL_SSD_SRIOV**: Local SSD SRIOV |
|Size |Integer |20 |Disk capacity in GiB. |
|MountPoint |String |/vke |The target mount point after disk formatting. |
|FileSystem |String |Ext4 |[[Beta - apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] The file system of data volumes for the node pool. |
|SnapshotId |String |snap\-31ak\*\*\*\*\*\*\*\* |The ID of the snapshot that is used for creating the data volume. |
|KmsKeyId |String |e91b2a39\-72\*\*\*\*\*\*\*\* |The ID of the KMS key used to encrypt the data volume. |
|Encrypted |Boolean |true |Whether to enable data volume encryption. Values:<br><br><br>* **true**: Enables data volume encryption.<br><br>* **false**: Disables data volume encryption. This is the default value. |
|BurstEnabled |Boolean |true |Whether to enable performance bursting. |
|SubgroupNumber |Integer |2 |The number of the storage placement sub\-group to which the data volume belongs. |
|PlacementGroupId |String |pg\-bp67a\*\*\*\*\*\*\*\* |The number of the storage placement group to which the data volume belongs. |
|ExtraPerformanceIops |Integer |10 |IOPS in the extra performance configuration for the cloud disk. |
|ExtraPerformanceTypeId |String |Bal\*\*\*\* |Extra performance type. |
|ExtraPerformanceThroughputMb |Integer |10 |The throughput of the extra performance configuration for the cloud disk. |


<span id="nodesecurityresponse"></span>
### NodeSecurityResponse


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Login |Object of [NodeLoginResponse](https://docs.byteplus.com/en/docs/90/21161#nodeloginresponse) |\- |The node access configurations. |
|SecurityGroupIds |Array of String |["sg\-2byy13cn\*\*\*\*\*\*"] |The IDs of security groups where the node network is located. |
|SecurityStrategies |Array of String |["Hids"] |The security policy for the node. Value description:<br><br>**Hids**: Host security reinforcement |
|SecurityStrategyEnabled |Boolean |true |Whether the node has security reinforcement enabled. Values:<br><br><br>* **true**: It is enabled.<br><br>* **false**: It is disabled. |


<span id="nodeloginresponse"></span>
### NodeLoginResponse


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Type |String |Password |The node login method. Valid values:<br><br><br>* **Password**: Use the password.<br><br>* **SshKeyPair**: Use the SSH key pair. |
|SshKeyPairName |String |test\-key |The name of the SSH key pair. |


<span id="tag"></span>
### Tag


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Key |String |key |The tag key. |
|Value |String |value |The label value. |


<span id="instancesdistribution"></span>
### InstancesDistribution


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|CapacityRebalance |Boolean |false |Whether it is allowed to supplement preemptive​ instance capacity with pay\-as\-you\-go instances. Values:<br><br><br>* **true**: Enabled Before preemptive​ instances are reclaimed, new preemptive​ instances are proactively created for compensation.<br><br>* **false**: Disabled. A scale\-out is performed to replenish the instance count only after the preemptive​ instance has been reclaimed.<br><br>   For details, see [Node pools of preemptive​ instances](https://docs.byteplus.com/en/docs/vke/Preemptible_instance_node_pool). |
|OnDemandBaseCapacity |Integer |0 |The base capacity of pay\-as\-you\-go instances. |
|CompensateWithOnDemand |Boolean |false |Whether to enable supplement of pay\-as\-you\-go instances. Values:<br><br><br>* **true**: Enabled When all preemptive instances fail to be purchased due to insufficient inventory or other reasons, the system attempts to purchase pay\-as\-you\-go instances.<br><br>* **false**: Disabled. During scale\-out, the system attempts to purchase configured preemptive​ instances only when they are required. |
|OnDemandPercentageAboveBaseCapacity |Integer |0 |Percentage of pay\-as\-you\-go instances in the node pool. |


<span id="eipconfigresponse"></span>
### EipConfigResponse


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Isp |String |BGP |The line type of the EIP. Valid values:<br><br>**BGP**: BGP (multipath) |
|Bandwidth |Integer |100 |The maximum bandwidth of the EIP. Unit: Mbit/s. |
|BillingType |Integer |3 |The billing type of the EIP. Valid values:<br><br><br>* **2**: Pay\-as\-you\-go \- by bandwidth limit<br><br>* **3**: Pay\-as\-you\-go \- by actual traffic |
|BandwidthPackageId |String |bwp\-2ze\*\*\*\*\*\*\*\* |The ID of the shared bandwidth package. This parameter indicates that the EIP has been added to this shared bandwidth package. |


<span id="instancetypespotpricelimit"></span>
### InstanceTypeSpotPriceLimit


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|InstanceTypeId |String |ecs.g1i\*\*\*\*\*\*\* |The instance specification ID. |
|SpotPriceLimit |Double |0.321 |The maximum price for spot instances of this instance specification. Unit: USD/hour. |


<span id="affinitygroupconfig"></span>
### AffinityGroupConfig


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Size |Integer |3 |[[Beta - apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] Affinity group size specified for the node pool. |
|Enabled |Boolean |false |[[Beta - apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] Whether the affinity group configuration is enabled for the node pool. Valid values:<br><br><br>* **true**: Enables affinity group\-based node purchases in the node pool.<br><br>* **false**: Disables affinity group configuration and uses standard node purchasing. |


<span id="nodepoolautoscalingresponse"></span>
### NodePoolAutoScalingResponse


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Enabled |Boolean |false |Configuration switch for node pool autoscaling. Values:<br><br><br>* **false**: Disabled.<br><br>* **true**: Enabled. |
|Priority |Integer |10 |Priority. |
|MaxReplicas |Integer |10 |Maximum number of nodes in the node pool. |
|MinReplicas |Integer |0 |Minimum number of nodes in the node pool. |
|SubnetPolicy |String |ZoneBalance |The scheduling policy for a multi\-subnet node pool. Valid values:<br><br><br>* **ZoneBalance**: Balanced scheduling across availability zones.<br><br>* **Priority**: Subnet priority\-based scheduling. |
|ScalingGroupId |String |scg\-ycf\*\*\*\*\*\*\* |The scaling group ID. |
|DesiredReplicas |Integer |0 |The desired number of nodes in the node pool. |


<span id="nodestatistics"></span>
### NodeStatistics


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|TotalCount |Integer |8 |The total number of nodes. |
|FailedCount |Integer |1 |The total number of nodes in the `Failed phase`. |
|RunningCount |Integer |1 |The total number of nodes in the `Running phase`. |
|CreatingCount |Integer |1 |The total number of nodes in the `Creating phase`. |
|DeletingCount |Integer |1 |The total number of nodes in the `Deleting` phase. |
|UpdatingCount |Integer |1 |The total number of nodes in the `Updating phase`. |


<span id="nodepoolkubernetesconfigresponse"></span>
### NodePoolKubernetesConfigResponse


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Labels |Array of [Label](https://docs.byteplus.com/en/docs/90/21161#label) |\- |Kubernetes labels of the node pool or node. |
|Taints |Array of [Taint](https://docs.byteplus.com/en/docs/90/21161#taint) |\- |The Kubernetes taints of the node pool or the node. |
|Cordon |Boolean |false |Node cordon configuration switch. Value description:<br><br><br>* **false**: Disable node cordoning.<br><br>* **true**: Enable node cordoning. |
|NamePrefix |String |xxx\- |The prefix of the metadata name for the node object in Kubernetes. |
|KubeletConfig |Object of [NodePoolKubeletConfig](https://docs.byteplus.com/en/docs/90/21161#nodepoolkubeletconfig) |\- |The kubelet settings for the node. |
|AutoSyncDisabled |Boolean |false |Specify whether to disable automatic synchronization of labels and taints to existing nodes. Valid values:<br><br><br>* **true**: Disable automatic synchronization.<br><br>* **false**: Enable automatic synchronization. |
|Runtime |Object of [NodePoolRuntimeResponse](https://docs.byteplus.com/en/docs/90/21161#nodepoolruntimeresponse) |\- |Container runtime configuration. |
|NameSuffix |String |\-xxx |The suffix of the metadata name for the node object in Kubernetes. |
|NameUseHostname |Boolean |true |Specify whether the metadata name of the node object in Kubernetes uses the ECS hostname. Valid values:<br><br><br>* **true**: Use the ECS hostname as the node name.<br><br>* **false**: Do not use the ECS hostname as the node name. |
|ContainerdConfig |Object of [NodePoolContainerdConfig](https://docs.byteplus.com/en/docs/90/21161#nodepoolcontainerdconfig) |\- |Containerd configuration. |


<span id="label"></span>
### Label


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Key |String |label\-key |The tag key. |
|Value |String |label\-value |The label value. |


<span id="taint"></span>
### Taint


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Key |String |taint\-key |The taint key. |
|Value |String |taint\-value |The taint value. |
|Effect |String |NoSchedule |The taint effect. Valid values:<br><br><br>* **NoSchedule**: No scheduling is performed.<br><br>* **NoExecute**: Pods that do not tolerate the taint are evicted.<br><br>* **PreferNoSchedule**: Avoid scheduling if possible. |


<span id="nodepoolkubeletconfig"></span>
### NodePoolKubeletConfig


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|FeatureGates |Object of [FeatureGates](https://docs.byteplus.com/en/docs/90/21161#featuregates) |\- |The feature gates, which are a set of key\-value pairs that describe Kubernetes features. |
|TopologyManagerScope |String |container |The resource granularity of the topology management policy. Valid values:<br><br><br>* **container**: The resource alignment granularity is at the container level. |
|TopologyManagerPolicy |String |none |Topology management policy. Values:<br><br><br>* **none**: No topology management policy is enabled.<br><br>* **restricted**: The kubelet only accepts Pods that achieve optimal NUMA alignment for the requested resources.<br><br>* **best\-effort**: Kubelet preferentially selects pods that achieve NUMA alignment on CPU and device resources.<br><br>* **single\-numa\-node**: Kubelet allows only pods that are aligned to the same NUMA node in terms of CPU and device resources. |
|MaxPods |Integer |110 |The maximum number of pods supported by the node. |
|KubeApiQps |Integer |50 |The number of QPS for communication with the API server.  |
|KubeApiBurst |Integer |100 |The maximum burst requests sent to the API server per second. |
|CpuCfsQuota |Boolean |false |Whether to enable CPU CFS quota guarantee for containers with CPU limits.<br><br><br>* **true**: Enable this feature.<br><br>* **false**: Disable this feature. |
|EvictionHard |Array of [EvictionHard](https://docs.byteplus.com/en/docs/90/21161#evictionhard) |\- |A set of hard eviction thresholds that trigger pod eviction. For detailed parameter descriptions, see the[ official documentation](https://kubernetes.io/docs/concepts/scheduling-eviction/node-pressure-eviction/). |
|KubeReserved |Array of [ComputeResource](https://docs.byteplus.com/en/docs/90/21161#computeresource) |\- |The resources reserved by the node for Kubernetes system components. |
|SystemReserved |Array of [ComputeResource](https://docs.byteplus.com/en/docs/90/21161#computeresource) |\- |The resources reserved for the operating system on the node. |
|RegistryPullQps |Integer |5 |The QPS threshold for a cluster pulling images from Container Registry (CR). |
|RegistryBurst |Integer |10 |The maximum images concurrently pulled from CR. |
|SerializeImagePulls |Boolean |true |Whether to serially pull images. Values:<br><br><br>* **true**: Serially pull images.<br><br>* **false**: Serially pull images. |
|CpuManagerPolicy |String |none |The CPU manager policy. Valid values:<br><br><br>* **none**: The policy is the default policy.<br><br>* **static**: This policy allows pods with specific resource characteristics on the node to be granted enhanced CPU affinity and exclusivity. |
|FailSwapOn |Boolean |false |Specifies whether kubelet can run when swap is enabled on the node. Valid values:<br><br><br>* **true**: Prevents kubelet from running when swap is enabled on the node.<br><br>* **false**: Allows kubelet to run when swap is enabled on the node. |
|ImageGcLowThresholdPercent |Integer |80 |The threshold for stopping Image garbage collection. During image garbage collection, collection stops when disk usage falls below this percentage. |
|ImageGcHighThresholdPercent |Integer |85 |The threshold for triggering image garbage collection. When disk usage exceeds this value, the system starts cleaning up unused images. |


<span id="featuregates"></span>
### FeatureGates


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|QoSResourceManager |Boolean |false |Specify whether to enable quality of service (QoS) Resource Manager to support micro\-topology scheduling. Valid values:<br><br><br>* **true**: Enable QoS Resource Manager.<br><br>* **false**: Do not enable QoS Resource Manager. |
|InPlacePodVerticalScaling |Boolean |true |Whether to enable vertical pod scaling. Value description:<br><br><br>* **true**: Enable it.<br><br>* **false**: Disable it. |


<span id="evictionhard"></span>
### EvictionHard


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Key |String |memory.available |The name of the hard eviction threshold. Valid values:<br><br><br>* memory.available<br><br>* nodefs.available<br><br>* nodefs.inodesFree<br><br>* imagefs.available |
|Value |String |1Gi |The hard eviction threshold value. |


<span id="computeresource"></span>
### ComputeResource


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Name |String |cpu |Resource name. The value is **cpu** or **memory**. |
|Quantity |String |1G |The quantity of the resource. |


<span id="nodepoolruntimeresponse"></span>
### NodePoolRuntimeResponse


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Type |String |containerd |Container runtime type. Values:<br><br>**containerd**: The containerd runtime. |
|Version |String |v1.6.38\-vke.17 |Container runtime version. This includes the major version of the container runtime and the patch version of VKE. |


<span id="nodepoolcontainerdconfig"></span>
### NodePoolContainerdConfig


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|InsecureRegistries |Array of String |["example.com"] |Specify the URL of the CR instance for which certificate authentication will be skipped. |
|RegistryProxyConfigs |Array of [RegistryProxyConfig](https://docs.byteplus.com/en/docs/90/21161#registryproxyconfig) |\- |The proxy configuration of the container image registry. |


<span id="registryproxyconfig"></span>
### RegistryProxyConfig


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Registry |String |example.com |The address of the container image registry. |
|ProxyEndpoints |Array of String |["https://example.com"] |The proxy address. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1 200 OK
Content-Type:application/json

{
    "ResponseMetadata": {
        "RequestId": "021635330********",
        "Action": "ListNodePools",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {
        "Items": [
            {
                "Id": "pc51i0m6********",
                "Name": "test-nodepool",
                "ClusterId": "cc5silu*******",
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
                    "InstanceTypeIds": [
                        "ecs.g1.large"
                    ],
                    "SubnetIds": [
                        "subnet-3rf6vwbgkg****"
                    ],
                    "ImageId": "image-kd********",
                    "GpuDriverVersion": "550.127.05",
                    "SystemVolume": {
                        "Type": "ESSD_PL0",
                        "Size": 40
                    },
                    "DataVolumes": [
                        {
                            "Type": "ESSD_PL0",
                            "Size": 20
                        }
                    ],
                    "AdditionalContainerStorageEnabled": true,
                    "InitializeScript": "ZWNoby******",
                    "Security": {
                        "SecurityGroupIds": [
                            "sg-2byy13****"
                        ],
                        "SecurityStrategyEnabled": true,
                        "SecurityStrategies": [
                            "Hids"
                        ],
                        "Login": {
                            "Type": "Password",
                            "SshKeyPairName": ""
                        }
                    },
                    "InstanceChargeType": "PostPaid",
                    "Period": 0,
                    "AutoRenew": false,
                    "AutoRenewPeriod": 0,
                    "NamePrefix": "name-prefix"
                },
                "AutoScaling": {
                    "Enabled": true,
                    "DesiredReplicas": 1,
                    "MinReplicas": 0,
                    "MaxReplicas": 10,
                    "Priority": 10,
                    "SubnetPolicy": "Priority"
                },
                "Status": {
                    "Phase": "Running",
                    "Conditions": [
                        {
                            "Type": "Ok"
                        }
                    ]
                },
                "NodeStatistics": {
                    "TotalCount": 1,
                    "CreatingCount": 0,
                    "RunningCount": 1,
                    "UpdatingCount": 0,
                    "DeletingCount": 0,
                    "FailedCount": 0
                },
                "Tags": [
                    {
                        "Key": "key",
                        "Value": "value",
                        "Type": "Custom"
                    }
                ],
                "CreateClientToken": "BB928624-11C0-4856-A233-84F9F9******",
                "UpdateClientToken": "BC028527-33B9-4990-A633-54A859******",
                "CreateTime": "2022-05-11T17:01:23+08:00",
                "UpdateTime": "2022-05-12T17:01:23+08:00"
            }
        ],
        "PageNumber": 1,
        "PageSize": 10,
        "TotalCount": 1
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no proprietary error codes for this API. See [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes) for details about public error codes.
