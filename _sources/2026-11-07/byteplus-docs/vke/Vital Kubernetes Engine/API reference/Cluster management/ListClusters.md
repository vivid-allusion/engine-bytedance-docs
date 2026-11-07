---
title: "ListClusters"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/ListClusters"
---

Query the details of clusters that meet the criteria.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point for your business region.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=ListClusters&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListClusters&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table describes the API request parameters. You also need to provide public parameters when calling this API. See [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters) for details.


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListClusters |The API name. The name of the current API is `ListClusters`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Filter |Object of [ListClustersFilter](https://docs.byteplus.com/en/docs/90/21187#listclustersfilter) |No |\- |The filter conditions for the cluster to be queried. |
|Tags |Array of [ListTagFilter](https://docs.byteplus.com/en/docs/90/21187#listtagfilter) |No |\- |Query the cluster list based on tags.<br><br><br>* Each **Key** of **Tags** must be unique.<br><br>* The **Key** and **Value** in **Tags** cannot start or end with a space.<br><br>* Up to 10 tags are supported per call. |
|PageNumber |Integer |No |1 |The starting page number of the pagination query, starting from 1. Default value: 1. |
|PageSize |Integer |No |10 |The number of results per page:<br><br><br>* Minimum value: 1<br><br>* Maximum value: 100<br><br>* Default value: 10 |
|ProjectName |String |No |default |The project name. You can filter clusters by the project to which the clusters belong. |


<span id="listclustersfilter"></span>
### ListClustersFilter


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Ids |Array of String |No |["cc9q8p\*\*\*\*\*\*"] |A list of cluster IDs.<br><br>100 IDs can be included at most in a single query.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you leave this parameter empty, filtering is performed on all clusters in the region specified in the public parameters within the current account.</div><br> |
|Name |String |No |TestCluster |Cluster name. Fuzzy query is supported. |
|DeleteProtectionEnabled |Boolean |No |false |Specify whether to enable cluster deletion protection. Valid values:<br><br><br>* **true**: Enable it.<br><br>* **false**: Disable it. |
|PodsConfig.PodNetworkMode |String |No |Flannel |The Pod network model (CNI). Valid values:<br><br><br>* **Flannel**: an independent underlay network solution, based on which a high\-performance network for clusters can be built along with the global routing capabilities of VPCs.<br><br>* **VpcCniShared**: VPC\-CNI, an Underlay container network solution implemented based on the ENI of private networks. |
|Statuses |Array of [ClusterStatusFilter](https://docs.byteplus.com/en/docs/90/21187#clusterstatusfilter) |No |\- |An array of cluster statuses to filter.<br><br>The logic OR relationship is applied to the elements in the array. Up to 15 status array elements can be provided at a time. |
|CreateClientToken |String |No |BB928624\-11C0\-4856\-\*\*\*\*\*\* |The ClientToken generated upon cluster creation.<br><br>The ClientToken is a string that ensures request idempotency. This string is provided by the caller. |
|UpdateClientToken |String |No |BB928624\-11C0\-4856\-\*\*\*\*\*\* |The ClientToken generated for the last successful cluster update.<br><br>The ClientToken is a string that ensures request idempotency. This string is provided by the caller. |
|Types |Array of String |No |Managed |The cluster type (exact matching). Valid values:<br><br><br>* **Managed**: Managed cluster<br><br>* **Registered**: [[Beta - apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] Registered cluster |


<span id="clusterstatusfilter"></span>
### ClusterStatusFilter


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Phase |String |No |Creating |The cluster status. Valid values:<br><br><br>* **Creating**: It is being created.<br><br>* **Running**: It is running.<br><br>* **Updating**: It is being updated.<br><br>* **Stopped**<br><br>* **Deleting**: It is being deleted.<br><br>* **Failed**<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">At least one of <strong>Phase</strong> and <strong>Conditions.Type</strong> must be provided. Otherwise, it is an invalid array element. For valid combinations of <strong>Phase</strong> and <strong>Conditions.Type</strong>, see <a href="https://docs.byteplus.com/en/docs/vke/Resource-status-description">Resource status description</a>.</div><br> |
|Conditions.Type |String |No |Ok |The condition under which the cluster enters the current status. Valid values:<br><br><br>* **Ok**: The cluster is in a normal status.<br><br>* **CreateError**: The cluster fails to be created.<br><br>* **Progressing**: The cluster is being processed.<br><br>* **Balance**: Overdue payments exist in the account.<br><br>* **ResourceCleanupFailed**: The cluster fails to be deleted.<br><br>* **Unknown**: An unknown error occurs.<br><br>* **UpdatingCluster**: The configurations of the cluster are being updated.<br><br>* **SyncingAddon**: The add\-on is being updated.<br><br>* **SyncingNodePool**: The node pool is being updated.<br><br>* **ClusterVersionUpgrading**: The cluster version is being upgraded.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">At least one of <strong>Phase</strong> and <strong>Conditions.Type</strong> must be provided. Otherwise, it is an invalid array element. For valid combinations of <strong>Phase</strong> and <strong>Conditions.Type</strong>, see <a href="https://docs.byteplus.com/en/docs/vke/Resource-status-description">Resource status description</a>.</div><br> |


<span id="listtagfilter"></span>
### ListTagFilter


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Key |String |Yes |key |The label key.<br><br><br>* It cannot start with volc: in ‌any case variation‌.<br><br>* It can only contain language characters, digits, spaces, and the following special characters: `_ .` `: / = + - @`。<br><br>* The length is limited to 1 to 128 characters. |
|Value |String |No |value |A single tag value. It is used to match one candidate value under the same tag key.<br><br><br>* It can contain only letters, digits, spaces, and the following special characters: `_ .` `: / = + - @`。<br><br>* Its length does not exceed 256 characters.<br><br>* This can be left blank.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When both Value and <strong>Values</strong> are provided, the label values are merged into the same candidate set for matching. They are neither mutually exclusive nor deduplicated.</div><br> |
|Values |Array of String |No |["value1","value2"] |The list of tag values. It is used to match multiple candidate values under the same tag key.<br><br><br>* Each tag value needs to meet the following conditions:<br><br>   * It can only contain language characters, digits, spaces, and the following special characters: `_ .` `: / = + - @`。<br><br>   * Its length does not exceed 256 characters.<br><br>* Multiple tag values are separated with commas (,).<br><br>* This can be left blank.<br><br>* After you specify the parameter values, clusters matching any tag value in this list will be filtered.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When both <strong>Value</strong> and Values are provided, the label values are merged into the same candidate set for matching. They are neither mutually exclusive nor deduplicated.</div><br> |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vke.cn-beijing.byteplusapi.com.cn?Action=ListClusters&Version=2022-05-12 HTTP/1.1
Content-Type:application/json
{
    "PageNumber": 1,
    "PageSize": 10,
    "Filter": {
        "Name": "test",
        "Ids": [
            "cc9q8pbfqtofn8j******"
        ],
        "DeleteProtectionEnabled": true,
        "Statuses": [
            {
                "Phase": "Running"
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
## Response parameters

The following table contains the response parameters of this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Items |Array of [ClusterResponse](https://docs.byteplus.com/en/docs/90/21187#clusterresponse) |\- |The list of detailed information about clusters. |
|PageNumber |Integer |1 |The current page number. |
|PageSize |Integer |10 |The number of clusters displayed per page. |
|TotalCount |Integer |100 |The total number of clusters that meet the conditions. |


<span id="clusterresponse"></span>
### ClusterResponse


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Id |String |cc9q8p\*\*\*\*\*\*\* |Cluster ID. |
|CreateClientToken |String |BC028527\-33B9\-4990\-A633\-\*\*\*\*\*\* |The ClientToken generated upon successful creation. The ClientToken is a string that ensures request idempotency. This string is provided by the caller. |
|UpdateClientToken |String |BC028527\-33B9\-4990\-A633\-\*\*\*\*\*\* |The ClientToken generated for the last successful update. The ClientToken is a string that ensures request idempotency. This string is provided by the caller. |
|CreateTime |String |2022\-05\-06T02:49:19Z |The time when the cluster was created.<br><br>UTC+0 time in standard [RFC3339](https://tools.ietf.org/html/rfc3339) format. |
|UpdateTime |String |2022\-05\-15T03:13:20Z |The time when the cluster was last updated.<br><br>UTC+0 time in standard [RFC3339](https://tools.ietf.org/html/rfc3339) format. |
|KubernetesVersion |String |v1.36.1\-vke.2 |The Kubernetes version that corresponds to the cluster. |
|Name |String |TestCluster |Cluster name. |
|Description |String |A Kubernetes Cluster Managed by VKE |The cluster description. |
|Status |Object of [ClusterStatus](https://docs.byteplus.com/en/docs/90/21187#clusterstatus) |\- |The cluster status. |
|DeleteProtectionEnabled |Boolean |false |Specify whether to enable cluster deletion protection. Valid values:<br><br><br>* **true**: Enable deletion protection.<br><br>* **false**: Disable deletion protection. |
|ClusterConfig |Object of [ClusterConfigResponse](https://docs.byteplus.com/en/docs/90/21187#clusterconfigresponse) |\- |The network configurations of the cluster control plane and some nodes. |
|PodsConfig |Object of [PodsConfigResponse](https://docs.byteplus.com/en/docs/90/21187#podsconfigresponse) |\- |The pod network configurations. |
|ServicesConfig |Object of [ServicesConfigResponse](https://docs.byteplus.com/en/docs/90/21187#servicesconfigresponse) |\- |The service network configurations. |
|NodeStatistics |Object of [NodeStatistics](https://docs.byteplus.com/en/docs/90/21187#nodestatistics) |\- |The statistics on the number of nodes when the cluster is in each primary status. |
|Tags |Array of [TagResponse](https://docs.byteplus.com/en/docs/90/21187#tagresponse) |\- |The tags added to the cluster. |
|LoggingConfig |Object of [ClusterLoggingConfigResponse](https://docs.byteplus.com/en/docs/90/21187#clusterloggingconfigresponse) |\- |Log configuration for the cluster. |
|Type |String |\- |The cluster type. Valid values:<br><br><br>* **Managed**: Managed cluster<br><br>* **Registered**: [[Beta - apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] Registered cluster |
|IrsaConfig |Object of [IrsaConfigResponse](https://docs.byteplus.com/en/docs/90/21187#irsaconfigresponse) |\- |The configurations related to the IRSA capability. |
|ProjectName |String |default |The project to which the cluster belongs. |
|ConnectorConfig |Object of [ClusterConnectorConfigResponse](https://docs.byteplus.com/en/docs/90/21187#clusterconnectorconfigresponse) |\- |[[Beta - apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] The connection configurations of the registered cluster.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The registered cluster is currently in <strong>beta</strong>. The <strong>ConnectorConfig</strong> parameter and its related sub\-parameters described in this topic are returned only after you obtain beta access and use the feature.</div><br> |
|KubernetesConfig |Object of [ClusterKubernetesConfigResponse](https://docs.byteplus.com/en/docs/90/21187#clusterkubernetesconfigresponse) |\- |Kubernetes\-related parameter configuration. |
|MonitoringConfig |Object of [ClusterMonitoringConfigResponse](https://docs.byteplus.com/en/docs/90/21187#clustermonitoringconfigresponse) |\- |The monitoring configurations of the managed cluster. |
|MaintenanceWindowConfig |Object of [ClusterMaintenanceWindowConfigResponse](https://docs.byteplus.com/en/docs/90/21187#clustermaintenancewindowconfigresponse) |\- |The O&M configurations of the cluster. |
|Message |String |CLB clb\-rrgk\*\*\*\* deletion failed |The cluster error message. |
|RegisterMonitoringConfig |Object of [RegisterClusterMonitoringConfigResponse](https://docs.byteplus.com/en/docs/90/21187#registerclustermonitoringconfigresponse) |\- |[[Beta - apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] The monitoring configurations of the registered cluster.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The registered cluster is currently in <strong>beta</strong>. The <strong>RegisterMonitoringConfig</strong> parameter and its related sub\-parameters described in this topic are returned only after you obtain beta access and use the feature.</div><br> |


<span id="clusterstatus"></span>
### ClusterStatus


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Phase |String |Creating |The cluster status. Valid values:<br><br><br>* **Creating**: It is being created.<br><br>* **Running**: It is running.<br><br>* **Updating**: It is being updated.<br><br>* **Stopped**<br><br>* **Deleting**: It is being deleted.<br><br>* **Failed**: An abnormality has occurred.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For valid combinations of <strong>Phase</strong> and <strong>Conditions.Type</strong>, see <a href="https://docs.byteplus.com/en/docs/vke/Resource-status-description">Resource status description</a>.</div><br> |
|Conditions |Array of [ClusterStatusCondition](https://docs.byteplus.com/en/docs/90/21187#clusterstatuscondition) |\- |The condition under which the cluster enters the primary status. |


<span id="clusterstatuscondition"></span>
### ClusterStatusCondition


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Type |String |Ok |The condition under which the cluster enters the primary status. You can specify multiple conditions. Valid values:<br><br><br>* **Ok**: The cluster is in a normal status.<br><br>* **CreateError**: The cluster fails to be created.<br><br>* **Progressing**: The cluster is being processed.<br><br>* **Balance**: Overdue payments exist in the account.<br><br>* **ResourceCleanupFailed**: The cluster fails to be deleted.<br><br>* **Unknown**: An unknown error occurs.<br><br>* **UpdatingCluster**: The configurations of the cluster are being updated.<br><br>* **SyncingAddon**: The add\-on is being updated.<br><br>* **SyncingNodePool**: The node pool is being updated.<br><br>* **ClusterVersionUpgrading**: The cluster version is being upgraded.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For valid combinations of <strong>Phase</strong> and <strong>Conditions.Type</strong>, see <a href="https://docs.byteplus.com/en/docs/vke/Resource-status-description">Resources status description</a>.</div><br> |


<span id="clusterconfigresponse"></span>
### ClusterConfigResponse


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|VpcId |String |vpc\-2d\*\*\*\*\*\*\* |The ID of the VPC where the network of the cluster control plane and some nodes is located. |
|SubnetIds |Array of String |["subnet\-2d73\*\*\*\*"] |The IDs of subnets within the VPC for the control plane of the cluster. |
|SecurityGroupIds |Array of String |["sg\-3re8ff\*\*\*\*"] |A list of IDs of security groups used by the control plane and nodes of the cluster. |
|ApiServerPublicAccessEnabled |Boolean |false |Specify whether to enable public access to the API server of the cluster. Valid values:<br><br><br>* **false**: Disable it.<br><br>* **true**: Enable it. |
|ApiServerPublicAccessConfig |Object of [PublicAccessConfigResponse](https://docs.byteplus.com/en/docs/90/21187#publicaccessconfigresponse) |\- |The public access configurations of the API server of the cluster.<br><br>This parameter is returned only if `ApiServerPublicAccessEnable is set to true`. |
|ResourcePublicAccessDefaultEnabled |Boolean |false |The public node access configuration. Valid values:<br><br><br>* **false**: Disable it.<br><br>* **true**: Enable it. |
|ApiServerEndpoints |Object of [ClusterApiServerEndpointsResponse](https://docs.byteplus.com/en/docs/90/21187#clusterapiserverendpointsresponse) |\- |The endpoint used for accessing the API server of the registered cluster. |
|IpFamily |String |Ipv4 |The cluster network protocol stack. Valid values:<br><br><br>* **Ipv4**: Single\-stack IPv4<br><br>* **Ipv6**: [[Beta - apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] Single\-stack IPv6<br><br>* **DualStack**: [[Beta - apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] Dual stack IPv4 and IPv6 |


<span id="publicaccessconfigresponse"></span>
### PublicAccessConfigResponse


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|AccessSourceIpsv4 |Array of String |["0.0.0.0/0"] |The allowlist for public access via IPv4.<br><br>If this parameter is left empty, it indicates that all CIDR blocks are allowed (`0.0.0.0/0`). |
|PublicAccessNetworkConfig |Object of [EipConfigResponse](https://docs.byteplus.com/en/docs/90/21187#eipconfigresponse) |\- |The public access configurations.<br><br>This parameter is returned only if `ApiServerPublicAccessEnable is set to true`. |


<span id="eipconfigresponse"></span>
### EipConfigResponse


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Isp |String |BGP |The line type of the EIP. Valid values:<br><br>**BGP**: BGP (multipath) |
|Bandwidth |Integer |100 |The maximum bandwidth of the EIP. Unit: Mbit/s. |
|BillingType |Integer |3 |The billing type of the EIP. Valid values:<br><br><br>* **2**: Pay\-as\-you\-go \- by bandwidth limit<br><br>* **3**: Pay\-as\-you\-go \- by actual traffic |
|BandwidthPackageId |String |bwp\-2ze\*\*\*\*\*\*\*\* |The ID of the shared bandwidth package. This parameter indicates that the EIP has been added to this shared bandwidth package. |


<span id="clusterapiserverendpointsresponse"></span>
### ClusterApiServerEndpointsResponse


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|PublicIp |Object of [Endpoint](https://docs.byteplus.com/en/docs/90/21187#endpoint) |\- |The public endpoint address of the cluster API server. |
|PrivateIp |Object of [Endpoint](https://docs.byteplus.com/en/docs/90/21187#endpoint) |\- |The private endpoint address of the cluster API server. |


<span id="endpoint"></span>
### Endpoint


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Ipv4 |String |10.249.xx.xx |The IPv4 address of the endpoint. |


<span id="podsconfigresponse"></span>
### PodsConfigResponse


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|PodNetworkMode |String |Flannel |The Pod network model (CNI). Valid values:<br><br><br>* **Flannel**: Flannel, an independent Underlay container network model.<br><br>* **VpcCniShared**: VPC\-CNI, an Underlay container network model implemented based on the ENI of private networks. |
|VpcCniConfig |Object of [VpcCniConfigResponse](https://docs.byteplus.com/en/docs/90/21187#vpccniconfigresponse) |\- |The VPC\-CNI network configuration. |
|FlannelConfig |Object of [FlannelConfigResponse](https://docs.byteplus.com/en/docs/90/21187#flannelconfigresponse) |\- |The Flannel network configurations. |


<span id="vpccniconfigresponse"></span>
### VpcCniConfigResponse


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|SubnetIds |Array of String |["subnet\-5g39d\*\*\*\*","subnet\-5g39d\*\*\*\*"] |The list of pod subnet IDs in VPC\-CNI networking. |
|VciSubnetIds |Array of String |["subnet\-5g39\*\*\*\*","subnet\-5g39d\*\*\*\*"] |A list of IDs of VCI Pod subnets in the VPC\-CNI networking. |
|TrunkEniEnabled |Boolean |false |[[Beta - apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] Specify whether the Pod primary ENI supports Trunk ENI.<br><br><br>* **true**<br><br>* **false**<br><br>   This parameter is returned only if the `PodNetworkMode parameter is set to VpcCniShared`. |


<span id="flannelconfigresponse"></span>
### FlannelConfigResponse


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|PodCidrs |Array of String |["172.168.xx/19"] |The pod CIDR for Flannel pod networking. |
|SubnetIds |Array of String |["subnet\-5g39d\*\*\*\*","subnet\-5g39d\*\*\*\*"] |The list of pod subnet IDs that correspond to the Flannel network model. |
|MaxPodsPerNode |Integer |64 |The maximum number of pod instances per node for Flannel pod networking. |


<span id="servicesconfigresponse"></span>
### ServicesConfigResponse


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|ServiceCidrsv4 |Array of String |["172.25.xx/17"] |The private IPv4 address exposed by the Kubernetes Service. |


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


<span id="tagresponse"></span>
### TagResponse


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Key |String |key |The label key. |
|Type |String |Custom |Tag type. Valid values:<br><br><br>* **System:**  System tag<br><br>* **Custom**: User\-defined tag |
|Value |String |value |The label value. |


<span id="clusterloggingconfigresponse"></span>
### ClusterLoggingConfigResponse


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|LogSetups |Array of [LogSetupResponse](https://docs.byteplus.com/en/docs/90/21187#logsetupresponse) |\- |Cluster logging setups. |
|LogProjectId |String |d94b4eb4\-\*\*\*\*\*\*\*\* |The ID of the log project for the cluster. If this parameter is left empty, it indicates that the log project of the cluster has not been created. |


<span id="logsetupresponse"></span>
### LogSetupResponse


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|LogTtl |Integer |30 |The log retention period in TLS. Unit: days. A value of 3650 indicates permanent storage. |
|Enabled |Boolean |false |Specify whether to enable this log option. Valid values:<br><br><br>* **true**: It is enabled.<br><br>* **false**: It is disabled. |
|LogType |String |Audit |The type of enabled logs. Valid values:<br><br><br>* **Audit**: Cluster audit log<br><br>* **KubeApiServer**: kube\-apiserver add\-on log<br><br>* **KubeScheduler**: kube\-scheduler add\-on log<br><br>* **KubeControllerManager**: kube\-controller\-manager add\-on log |
|LogTopicId |String |a72b4eba\-\*\*\*\*\*\*\*\* |The ID of the TLS log topic for the collection target. If this parameter is left empty, it indicates that the corresponding log topic has not been created. |


<span id="irsaconfigresponse"></span>
### IrsaConfigResponse


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Issuer |String |https://oidc\-vke\-region.tos\-cn\-region.volces.com/\*\*\*\* |The URL of the OpenID Connect (OIDC) provider, which is its unique identifier. |
|Enabled |Boolean |false |Specify whether to enable the IRSA feature. Valid values:<br><br><br>* **true**: Enable it.<br><br>* **false**: Disable it. |
|JwksUrl |String |https://oidc\-vke\-region.tos\-cn\-region.volces.com/\*\*\*\* |The JSON Web Key Set (JWKS) URL. The public keys in the file are used to verify any JSON Web Tokens (JWTs) returned by the OIDC provider. |
|OidcTrn |String |trn:iam::210\*\*\*\*:oidc\-provider/\*\*\*\* |The provider TRN of OIDC. |
|Audience |String |sts.volcengine.com |The identifier of the token recipient. |
|OpenIdConfigUrl |String |https://oidc\-vke\-region.tos\-cn\-region.volces.com/cluster\-id/\*\*\*\* |The configuration file in the JSON format of the OIDC provider, which contains information about the OIDC provider. |


<span id="clusterconnectorconfigresponse"></span>
### ClusterConnectorConfigResponse


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Type |String |Direct |The connection type of the registered cluster. Valid values:<br><br><br>* **Direct**: Direct connection mode. The cluster is registered and managed through the direct connection mode of the KubeConfig for the target cluster.<br><br>* **Proxy**: Proxy mode. The cluster is registered and managed through an Agent. |
|Provider |String |Vke |The provider of the registered cluster. Valid values:<br><br><br>* **Ack**: Alibaba Cloud ACK<br><br>* **Tke**: Tencent Cloud TKE<br><br>* **Cce**: Huawei Cloud CCE<br><br>* **Gke**: Google Cloud GKE<br><br>* **Eks**: Amazon EKS<br><br>* **BaiduCce**: Baidu Cloud CCE<br><br>* **None**: custom cluster |
|ProxyConfig |Object of [ProxyConfigResponse](https://docs.byteplus.com/en/docs/90/21187#proxyconfigresponse) |\- |The connection configurations of the registered cluster. |


<span id="proxyconfigresponse"></span>
### ProxyConfigResponse


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|VpcId |String |vpc\-2d7\*\*\*\*\*\*\* |The ID of the VPC used by registered cluster. |
|SubnetIds |Array of String |["subnet\-2d73mha\*\*\*\*"] |The IDs of the subnets used by the registered cluster. |
|AclEnabled |Boolean |true |Specify whether to enable ACL allowlist control. Valid values:<br><br><br>* **false**<br><br>* **true** |
|AclIpWhitelist |Array of String |["192.168.1.0/24", "10.0.0.0/16"] |The IP address list in the listener ACL allowlist.<br><br>This parameter is returned only if `AclEnabled is set to true`. |
|ApiServerEndpoints |Object of [ClusterApiServerEndpointsResponse](https://docs.byteplus.com/en/docs/90/21187#clusterapiserverendpointsresponse) |\- |The endpoint used for accessing the API server of the registered cluster. |
|ApiServerPublicAccessConfig |Object of [PublicAccessConfigResponse](https://docs.byteplus.com/en/docs/90/21187#publicaccessconfigresponse) |\- |The public access configurations of the API server of the registered cluster.<br><br>This parameter is returned only if `ApiServerPublicAccessEnable is set to true`. |
|ApiServerPublicAccessEnabled |Boolean |false |Specify whether to enable public access to the API server of the registered cluster. Valid values:<br><br><br>* **false**: Disable it.<br><br>* **true**: Enable it. |


<span id="clusterkubernetesconfigresponse"></span>
### ClusterKubernetesConfigResponse


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|CustomSans |Array of String |["abc.com","192.168.0.10"] |The custom\-issued domain name or IP. |
|ClusterDomain |String |cluster.local |Cluster local domain name. |
|AdvancedConfig |Object of [AdvancedConfig](https://docs.byteplus.com/en/docs/90/21187#advancedconfig) |\- |The enhanced configuration for kube\-apiserver. |
|ControlPlaneConfig |Object of [KubernetesComponentConfigs](https://docs.byteplus.com/en/docs/90/21187#kubernetescomponentconfigs) |\- |The custom parameter configuration for Kubernetes core add\-ons. |


<span id="advancedconfig"></span>
### AdvancedConfig


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|InternalDnsEnabled |Boolean |true |Whether to enable private domain access to the API Server for the cluster. Valid values:<br><br><br>* **true**: Enable it. Node\-side components access the API Server via the private domain.<br><br>* **false**: Disable it. |


<span id="kubernetescomponentconfigs"></span>
### KubernetesComponentConfigs


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|KubeApiServerConfig |Object of [KubeApiServerConfig](https://docs.byteplus.com/en/docs/90/21187#kubeapiserverconfig) |\- |The custom parameter configuration for the kube\-apiserver add\-on. |
|KubeSchedulerConfig |Object of [KubeSchedulerConfig](https://docs.byteplus.com/en/docs/90/21187#kubeschedulerconfig) |\- |The custom parameter configuration for the kube\-scheduler add\-on. |
|KubeControllerManagerConfig |Object of [KubeControllerManagerConfig](https://docs.byteplus.com/en/docs/90/21187#kubecontrollermanagerconfig) |\- |The custom parameter configuration for the kube\-controller\-manager add\-on. |


<span id="kubeapiserverconfig"></span>
### KubeApiServerConfig


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|FeatureGates |Object of [KubeApiServerFeatureGates](https://docs.byteplus.com/en/docs/90/21187#kubeapiserverfeaturegates) |\- |The feature gates supported by kube\-apiserver. |
|RequestTimeout |String |60s |The request timeout, which is the maximum duration the handler waits for the request to complete before terminating it. Unit: seconds. |
|AdmissionPlugins |Object of [AdmissionPlugins](https://docs.byteplus.com/en/docs/90/21187#admissionplugins) |\- |The list of admission control add\-ons additionally enabled in kube\-apiserver beyond those enabled by default. |
|DefaultNotReadyTolerationSeconds |Integer |300 |The default toleration duration for Pods against the `NotReady:NoExecute` taint on nodes. Unit: seconds. |
|DefaultUnreachableTolerationSeconds |Integer |300 |The default toleration duration of the Pod for the `Unreachable:NoExecute` taint on the node. Unit: seconds. |


<span id="kubeapiserverfeaturegates"></span>
### KubeApiServerFeatureGates


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|SidecarContainers |Boolean |true |Whether to enable the SidecarContainers feature gate to support native Sidecar containers. Valid values:<br><br><br>* **true**: Enable it.<br><br>* **false**: Disable it.<br><br>* An empty value indicates that this feature gate is determined by the default policy of kube\-apiserver. |
|StatefulSetAutoDeletePVC |Boolean |true |Whether to enable the StatefulSetAutoDeletePVC feature gate to support automatic deletion of PVCs by StatefulSets. Valid values:<br><br><br>* **true**: Enable it.<br><br>* **false**: Disable it.<br><br>* An empty value indicates that this feature gate is determined by the default policy of kube\-apiserver. |
|InPlacePodVerticalScaling |Boolean |true |Whether to enable the InPlacePodVerticalScaling feature gate, which supports in\-place vertical scaling for Pods. Valid values:<br><br><br>* **true**: Enable it.<br><br>* **false**: Disable it.<br><br>* An empty value indicates that this feature gate is determined by the default policy of kube\-apiserver. |
|MaxUnavailableStatefulSet |Boolean |true |Whether to enable the MaxUnavailableStatefulSet feature gate to add the `maxUnavailable` configuration for StatefulSet rolling updates. This allows multiple Pods to be unavailable and updated in parallel during updates. Valid values:<br><br><br>* **true**: Enable it.<br><br>* **false**: Disable it.<br><br>* An empty value indicates that this feature gate is determined by the default policy of kube\-apiserver. |


<span id="admissionplugins"></span>
### AdmissionPlugins


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|PodNodeSelector |Boolean |true |Whether to enable the PodNodeSelector admission control add\-on. Valid values:<br><br><br>* **true**: Enable it. This indicates that a node selector is forcibly or by default attached to all Pods within the namespace. This schedules the Pods only onto nodes with specific labels.<br><br>* **false**: Disable it. |
|AlwaysPullImages |Boolean |true |Whether to enable the AlwaysPullImages admission control add\-on. Valid values:<br><br><br>* **true**: Enable it. It indicates that the image is forcibly re\-pulled when each Pod is modified.<br><br>* **false**: Disable it. |
|PodTolerationRestriction |Boolean |true |Whether to enable the PodTolerationRestriction admission control add\-on. Valid values:<br><br><br>* **true**: Enable it. This uniformly manages Pod tolerations within a namespace to prevent the abuse of high\-privilege taint tolerations.<br><br>* **false**: Disable it. |


<span id="kubeschedulerconfig"></span>
### KubeSchedulerConfig


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|KubeApiQps |Integer |50 |The QPS limit for communication between kube\-scheduler and the API server. |
|Parallelism |Integer |16 |The number of Goroutines that kube\-scheduler executes in parallel when running the scheduling algorithm. |
|FeatureGates |Object of [KubeSchedulerFeatureGates](https://docs.byteplus.com/en/docs/90/21187#kubeschedulerfeaturegates) |\- |The feature gate configuration for kube\-scheduler. |
|KubeApiBurst |Integer |100 |The maximum burst requests when kube\-scheduler communicates with the API Server. |
|PodMaxBackoffSeconds |Integer |10 |The maximum backoff delay for rescheduling pods in seconds. After a pod fails to be scheduled, the pod cannot be rescheduled until the delay ends. |
|PercentageOfNodesToScore |Integer |50 |The evaluated proportion of nodes that can run Pods when Pods are being scheduled. Filtering stops after the specified proportion is reached. Unit: %. |
|PodInitialBackoffSeconds |Integer |1 |The initial backoff time for unschedulable Pods. Unit: seconds. |


<span id="kubeschedulerfeaturegates"></span>
### KubeSchedulerFeatureGates


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|SidecarContainers |Boolean |true |Whether to enable the SidecarContainers feature gate to support native Sidecar containers. Valid values:<br><br><br>* **true**: Enable it.<br><br>* **false**: Disable it.<br><br>* An empty value indicates that this feature gate is determined by the default policy of kube\-scheduler. |
|InPlacePodVerticalScaling |Boolean |true |Whether to enable the InPlacePodVerticalScaling feature gate, which supports in\-place vertical scaling for Pods. Valid values:<br><br><br>* **true**: Enable it.<br><br>* **false**: Disable it.<br><br>* An empty value indicates that this feature gate is determined by the default policy of kube\-scheduler. |


<span id="kubecontrollermanagerconfig"></span>
### KubeControllerManagerConfig


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|KubeApiQps |Integer |50 |The QPS limit for communication between kube\-controller\-manager and the API server. |
|FeatureGates |Object of [KubeControllerManagerFeatureGates](https://docs.byteplus.com/en/docs/90/21187#kubecontrollermanagerfeaturegates) |\- |The feature gate configuration for kube\-controller\-manager. |
|KubeApiBurst |Integer |100 |The maximum burst requests when kube\-controller\-manager communicates with the API Server. |
|NodeEvictionRate |Double |0.1 |The Pod eviction rate in node failure scenarios, which controls the number of nodes from which Pods are evicted per second after a node failure when the region is in a healthy state. |
|NodeMonitorGracePeriod |Integer |50s |The duration after which a node is marked as `NotReady` or `Unknown` if it becomes unreachable. Unit: seconds. |
|UnhealthyZoneThreshold |Double |0.55 |The unhealthy threshold for availability zones. |
|TerminatedPodGCThreshold |Integer |12500 |The garbage collection threshold for terminated Pods, which is the maximum number of terminated Pods that can be retained. |
|LargeClusterSizeThreshold |Integer |50 |The large cluster size threshold. The node controller uses this threshold to determine whether the cluster is a large\-scale cluster, which determines the Pod eviction policy. |
|SecondaryNodeEvictionRate |Double |0.01 |The secondary node draining rate. When the Region is unhealthy and nodes fail, this parameter specifies the number of nodes from which Pods are evicted per second. |
|ConcurrentTTLAfterFinishedSyncs |Integer |10 |The number of concurrent synchronization goroutines of the TTLAfterFinished controller that is responsible for cleaning up expired Jobs. |
|HorizontalPodAutoscalerTolerance |Double |0.1 |When Horizontal Pod Autoscaler (HPA) is used, if the deviation between the actual metric and the desired metric is less than this tolerance rate, scaling will not be triggered. |
|HorizontalPodAutoscalerSyncPeriod |String |15s |The period for the HPA to synchronize the number of Pods. |
|ConcurrentHorizontalPodAutoscalerSyncs |Integer |5 |The number of HPA objects that can be concurrently synchronized. A larger value results in faster processing response for HPA objects, but consumes more CPU and network resources. |


<span id="kubecontrollermanagerfeaturegates"></span>
### KubeControllerManagerFeatureGates


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|StatefulSetAutoDeletePVC |Boolean |true |Whether to enable the StatefulSetAutoDeletePVC feature gate to support automatic deletion of PVCs by StatefulSets. Valid values:<br><br><br>* **true**: Enable it.<br><br>* **false**: Disable it.<br><br>* An empty value indicates that this feature gate is determined by the default policy of kube\-controller\-manager. |
|InPlacePodVerticalScaling |Boolean |true |Whether to enable the InPlacePodVerticalScaling feature gate, which supports in\-place vertical scaling for Pods. Valid values:<br><br><br>* **true**: Enable it.<br><br>* **false**: Disable it.<br><br>* An empty value indicates that this feature gate is determined by the default policy of kube\-controller\-manager. |
|MaxUnavailableStatefulSet |Boolean |true |Whether to enable the MaxUnavailableStatefulSet feature gate to add the `maxUnavailable` configuration for StatefulSet rolling updates. This allows multiple Pods to be unavailable and updated in parallel during updates. Valid values:<br><br><br>* **true**: Enable it.<br><br>* **false**: Disable it.<br><br>* An empty value indicates that this feature gate is determined by the default policy of kube\-controller\-manager. |


<span id="clustermonitoringconfigresponse"></span>
### ClusterMonitoringConfigResponse


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|WorkspaceId |String |6fxxx\-5cxx\-4\*\*\*\*\*\*\*\* |The ID of the VMP workspace used for cluster monitoring. |
|ComponentConfigs |Array of [ClusterMonitoringComponentConfigResponse](https://docs.byteplus.com/en/docs/90/21187#clustermonitoringcomponentconfigresponse) |\- |The configurations of the control plane monitoring for the managed cluster. |
|EnableMetricsExternalCollection |Boolean |false |Specify whether to enable external Prometheus to collect cluster control plane add\-on metrics. Valid values:<br><br><br>* **true**: Enable it.<br><br>* **false**: Disable it. |


<span id="clustermonitoringcomponentconfigresponse"></span>
### ClusterMonitoringComponentConfigResponse


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Name |String |KubeApiServer |The control plane add\-on of the cluster that needs to be monitored. Valid values: KubeApiServer, KubeScheduler, Etcd, and ClusterAutoscaler. |
|Enabled |Boolean |true |Specify whether to enable control plane add\-on monitoring. Valid values:<br><br><br>* **true**: Enable it.<br><br>* **false**: Disable it. |


<span id="clustermaintenancewindowconfigresponse"></span>
### ClusterMaintenanceWindowConfigResponse


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Duration |Integer |4 |The duration of automatic O&M. Unit: hours. |
|StartTime |String |20:00:00Z |The time when automatic O&M starts. |
|TaskConfigs |Array of [WindowTaskConfig](https://docs.byteplus.com/en/docs/90/21187#windowtaskconfig) |\- |The configurations of the automatic O&M task. |
|WeeklyCycle |Array of String |["Monday","Tuesday"] |The O&M window cycle. Valid values:<br><br><br>* **Monday**<br><br>* **Tuesday**<br><br>* **Wednesday**<br><br>* **Thursday**<br><br>* **Friday**<br><br>* **Saturday**<br><br>* **Sunday** |
|ExemptEndDate |String |20260704 |The end time of the automatic O&M exemption window, which is in the format of `YYYYMMDD`, and applied based on calendar days in Beijing Time (UTC+8). |
|ExemptStartDate |String |20260702 |The start time of the automatic O&M exemption window, which is in the format of `YYYYMMDD`, and applied based on calendar days in Beijing Time (UTC+8). |


<span id="windowtaskconfig"></span>
### WindowTaskConfig


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Group |String |Cluster |The group of automatic O&M tasks. Valid values:<br><br><br>* **Cluster**: Control plane O&M.<br><br>* **Addon**: Data plane O&M. |
|Action |String |AutoUpgradeAddonVersion |The automatic O&M task. Valid values:<br><br><br>* **AutoUpgradeClusterMinorVersion**: A task that automatically upgrades cluster patch versions.<br><br>* **AutoUpgradeAddonVersion**: A task that automatically upgrades add\-on versions. |
|Targets |Array of String |["metrics\-server","cluster\-autoscaler"] |The add\-on for which automatic version upgrade is performed. |


<span id="registerclustermonitoringconfigresponse"></span>
### RegisterClusterMonitoringConfigResponse


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|QueryUrl |String |http://query.prometheus\-xx.xx.com/workspaces/caxx\-8xxx\-\*\*\*\* |The query URL of the VMP workspace when you monitor a registered cluster by using VMP. |
|WorkspaceId |String |a72bxxxx\-83xx\-4axx\*\*\*\*\*\*\*\* |The ID of the VMP workspace when you monitor a registered cluster by using VMP. |
|RemoteWriteUrl |String |http://write.prometheus\-xxx.xx.com/workspaces/xxxx\-8xxx\-4exx\-8xxx\-1xxx/api/v1/write |The remote write URL of the VMP workspace when you monitor a registered cluster by using VMP. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1 200 OK

Content-Type:application/json
{
    "ResponseMetadata": {
        "RequestId": "2022051511********",
        "Action": "ListClusters",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {
        "TotalCount": 1,
        "PageNumber": 1,
        "PageSize": 10,
        "Items": [
            {
                "Id": "cc9q8****",
                "ClientToken": "",
                "CreateTime": "2022-05-06T02:49:19Z",
                "UpdateTime": "2022-05-15T03:13:20Z",
                "KubernetesVersion": "v1.36.1-vke.2",
                "Name": "test",
                "Description": "",
                "Status": {
                    "Phase": "Running",
                    "Conditions": [
                        {
                            "Type": "Ok"
                        }
                    ]
                },
                "DeleteProtectionEnabled": true,
                "ClusterConfig": {
                    "VpcId": "vpc-2d73ui********",
                    "SubnetIds": [
                        "subnet-2d73ao****"
                    ],
                    "SecurityGroupIds": [
                        "sg-3re8ffwj****"
                    ],
                    "ApiServerPublicAccessEnabled": true,
                    "ApiServerPublicAccessConfig": {
                        "PublicAccessNetworkConfig": {
                            "BillingType": 2,
                            "Bandwidth": 1,
                            "Isp": "BGP"
                        }
                    },
                    "ResourcePublicAccessDefaultEnabled": false,
                    "ApiServerEndpoints": {
                        "PrivateIp": {
                            "Ipv4": "192.168.**.**"
                        },
                        "PublicIp": {
                            "Ipv4": "10.249.**.**"
                        }
                    }
                },
                "PodsConfig": {
                    "PodNetworkMode": "Flannel",
                    "FlannelConfig": {
                        "PodCidrs": [
                            "172.18.**.**/20"
                        ],
                        "MaxPodsPerNode": 64
                    }
                },
                "ServicesConfig": {
                    "ServiceCidrsv4": [
                        "172.23.**.**/21"
                    ]
                },
                "NodeStatistics": {
                    "TotalCount": 3,
                    "CreatingCount": 0,
                    "RunningCount": 3,
                    "UpdatingCount": 0,
                    "DeletingCount": 0,
                    "FailedCount": 0
                },
                "ChargeType": "PostPaid",
                "Tags": [
                    {
                        "Key": "key",
                        "Value": "value",
                        "Type": "Custom"
                    }
                ],
                "LoggingConfig": {
                    "LogProjectId": "b68324a0-2680-48c7********",
                    "LogSetups": [
                        {
                            "LogType": "Audit",
                            "LogTopicId": "d94b4eb4-1108-4931********",
                            "LogTtl": 30,
                            "Enabled": true
                        }
                    ]
                }
            }
        ]
    }
}
```


```json
HTTP/1.1 200 OK

Content-Type:application/json
{
    "ResponseMetadata": {
        "RequestId": "2022051511********",
        "Action": "ListClusters",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {
        "TotalCount": 1,
        "PageNumber": 1,
        "PageSize": 10,
        "Items": [
            {
                "Id": "ccegi********",
                "KubernetesVersion": "v1.36.1-vke.2",
                "Name": "vpc-cni-test",
                "Description": "",
                "Status": {
                    "Phase": "Running",
                    "Conditions": [
                        {
                            "Type": "Ok"
                        }
                    ]
                },
                "DeleteProtectionEnabled": false,
                "ClusterConfig": {
                    "VpcId": "vpc-2bztfy****",
                    "SubnetIds": [
                        "subnet-2d74k****"
                    ],
                    "SecurityGroupIds": [
                        "sg-3re9w****"
                    ],
                    "ApiServerPublicAccessEnabled": true,
                    "ApiServerPublicAccessConfig": {
                        "PublicAccessNetworkConfig": {
                            "BillingType": 3,
                            "Bandwidth": 10,
                            "Isp": "BGP"
                        }
                    },
                    "ResourcePublicAccessDefaultEnabled": false,
                    "ApiServerEndpoints": {
                        "PrivateIp": {
                            "Ipv4": "192.168.**.**"
                        },
                        "PublicIp": {
                            "Ipv4": "10.249.**.**"
                        }
                    }
                },
                "PodsConfig": {
                    "PodNetworkMode": "VpcCniShared",
                    "VpcCniConfig": {
                        "SubnetIds": [
                            "subnet-2d74kxgqc******"
                        ],
                        "VciSubnetIds": [
                            "subnet-df4dgxgqc******"
                        ]
                    }
                },
                "ServicesConfig": {
                    "ServiceCidrsv4": [
                        "172.26.**.**/21"
                    ]
                },
                "NodeStatistics": {
                    "TotalCount": 2,
                    "CreatingCount": 0,
                    "RunningCount": 0,
                    "UpdatingCount": 0,
                    "DeletingCount": 0,
                    "FailedCount": 2
                },
                "ChargeType": "PostPaid",
                "CreateTime": "2022-12-20T03:29:24Z",
                "UpdateTime": "2022-12-20T03:37:43Z",
                "CreateClientToken": "1852d931f34-460249325618****",
                "UpdateClientToken": "",
                "Tags": [],
                "LoggingConfig": {
                    "LogProjectId": "b68324a0-2680-48c7********",
                    "LogSetups": [
                        {
                            "LogType": "Audit",
                            "LogTopicId": "d94b4eb4-1108-4931********",
                            "LogTtl": 30,
                            "Enabled": true
                        }
                    ]
                }
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no proprietary error codes for this API. See [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes) for details about public error codes.
