---
title: "UpdateClusterConfig"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/UpdateClusterConfig"
---

Update the configurations of the specified VKE cluster.

<span id=".5L2_55So6K-05piO"></span>
## Usage instructions

This is an asynchronous API. When this API returns a success message, the cluster instance will be in the `{Updating, [Progressing]}` state. After all updates are complete, the cluster will enter the `{Running, [Ok]}` state. You can call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to obtain the current status and description of the cluster.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point for your business region.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=UpdateClusterConfig&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=UpdateClusterConfig&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table describes the API request parameters. You also need to provide public parameters when calling this API. See [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters) for details.


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |UpdateClusterConfig |The API name. The name of the current API is `UpdateClusterConfig`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|ClientToken |String |No |BC028527\-33B9\-4990\-\*\*\*\* |A string used to ensure the idempotency of the request. This string is passed in by the caller and must be unique across different requests. ClientToken is case\-sensitive and can consist of 64 ASCII characters at most. |
|Id |String |Yes |cc8o\*\*\*\*\* |The ID of the cluster to be updated.<br><br>You can call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to obtain cluster IDs.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The cluster to be updated must be in the <code>{Running,[*]}</code> state. You can call the <a href="https://docs.byteplus.com/en/docs/vke/ListClusters">ListClusters</a> API to obtain the current status of the cluster.</div><br> |
|Name |String |No |TestCluster |Cluster name.<br><br><br>* The name must be unique within the same region.<br><br>* It can contain uppercase and lowercase letters, Chinese characters, digits, and hyphens (\-). It can be 2 to 64 characters in length. |
|Description |String |No |A Kubernetes Cluster Managed by VKE |The cluster description. It cannot exceed 300 characters in length. |
|DeleteProtectionEnabled |Boolean |No |false |Specify whether to enable cluster deletion protection. Valid values:<br><br><br>* **false**: Disable deletion protection.<br><br>* **true**: Enable deletion protection. In this case, you cannot directly delete the cluster. After you update the cluster, you can specify the `Force` parameter when you call the [DeleteCluster](https://docs.byteplus.com/en/docs/vke/DeleteCluster) API to forcibly delete the cluster. |
|ClusterConfig |Object of [ClusterConfigUpdateRequest](https://docs.byteplus.com/en/docs/90/21190#clusterconfigupdaterequest) |No |\- |The network configurations of the control plane and nodes. |
|PodsConfig |Object of [PodsConfigUpdateRequest](https://docs.byteplus.com/en/docs/90/21190#podsconfigupdaterequest) |No |\- |The cluster container (pod) network configurations. |
|LoggingConfig |Object of [ClusterLoggingConfigRequest](https://docs.byteplus.com/en/docs/90/21190#clusterloggingconfigrequest) |No |\- |The log configurations for the cluster. |
|KubernetesConfig |Object of [ClusterKubernetesConfigRequestForUpdate](https://docs.byteplus.com/en/docs/90/21190#clusterkubernetesconfigrequestforupdate) |No |\- |Kubernetes\-related parameter configuration. |
|MonitoringConfig |Object of [ClusterMonitoringConfigUpdateRequest](https://docs.byteplus.com/en/docs/90/21190#clustermonitoringconfigupdaterequest) |No |\- |The monitoring configurations of the cluster. |
|MaintenanceWindowConfig |Object of [ClusterMaintenanceWindowConfigRequest](https://docs.byteplus.com/en/docs/90/21190#clustermaintenancewindowconfigrequest) |No |\- |The O&M configurations of the cluster. |
|IrsaEnabled |Boolean |No |false |Whether to enable the IRSA capability for the current cluster to isolate API permissions at the pod level within the cluster.<br><br><br>* **false**: (Default) Disable it.<br><br>* **true**: Enable it. |
|SourceRegion |String |No |cn\-beijing |The source region of the cluster. For specific values, see [Regions and availability zones](https://docs.byteplus.com/en/docs/vke/Regions-and-Availability-Zones). |
|RegisterMonitoringConfig |Object of [RegisterClusterMonitoringConfigUpdateRequest](https://docs.byteplus.com/en/docs/90/21190#registerclustermonitoringconfigupdaterequest) |No |\- |The monitoring configurations of the registered cluster. |


<span id="clusterconfigupdaterequest"></span>
### ClusterConfigUpdateRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|SubnetIds |Array of String |No |["subnet\-5g39\*\*\*","subnet\-5g39\*\*\*"] |The IDs of subnets within the VPC for the control plane of the cluster.<br><br>You can call the [VPC API](https://docs.byteplus.com/en/docs/vpc/API-overview-1) to obtain subnet IDs.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Make sure that all specified subnet IDs (not only those specified by this parameter) belong to the same VPC.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">You cannot delete configured subnets.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">You can select subnets from up to three availability zones, with up to two subnets allowed per availability zone.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The number of available IP addresses in a subnet must be at least 1.</div><br> |
|ApiServerPublicAccessEnabled |Boolean |No |false |Whether to enable public access to the API server of the cluster. Valid values:<br><br><br>* **false**: Disable it.<br><br>* **true**: Enable this option. |
|ApiServerPublicAccessConfig |Object of [PublicAccessConfigRequest](https://docs.byteplus.com/en/docs/90/21190#publicaccessconfigrequest) |No |\- |The public access configurations of the API server for the cluster.<br><br>This parameter takes effect only if `ApiServerPublicAccessEnabled is set to true`. |
|ClusterConnectorConfigRequest |Object of [ClusterConnectorConfigRequest](https://docs.byteplus.com/en/docs/90/21190#clusterconnectorconfigrequest) |No |\- |The connection configurations of the registered cluster. |
|ResourcePublicAccessDefaultEnabled |Boolean |No |false |The public access configurations of nodes and applications in the cluster. Valid values:<br><br><br>* **false**: Disable it.<br><br>* **true**: Enable this option. |


<span id="publicaccessconfigrequest"></span>
### PublicAccessConfigRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|PublicAccessNetworkConfig |Object of [EipConfigRequest](https://docs.byteplus.com/en/docs/90/21190#eipconfigrequest) |No |\- |The public access configurations of the API server of the cluster. This setting is required only when `ApiServerPublicAccessEnabled is set to true`. Otherwise, it is ignored.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After cluster creation is complete, you cannot modify this parameter. Configure it appropriately.</div><br> |


<span id="eipconfigrequest"></span>
### EipConfigRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Isp |String |No |BGP |The line type of the EIP. Valid values:<br><br><br>* **BGP**: BGP (multipath). |
|Bandwidth |Integer |No |100 |The maximum bandwidth of the EIP. Unit: Mbit/s. Valid values:<br><br><br>* If `BillingType` is set to 2, the valid values of Bandwidth are 1 to 500.<br><br>* If `BillingType` is set to 3, the valid values of Bandwidth are 1 to 200. |
|BillingType |Integer |No |3 |The billing type of the EIP. Valid values:<br><br><br>* **3**: Pay\-as\-you\-go \- usage\-based billing. It charges based on the actual outbound Internet traffic, regardless of the duration.<br><br>* **2**: Pay\-as\-you\-go. It charges based on a selected maximum bandwidth and the usage duration, regardless of the actual traffic volume. |
|BandwidthPackageId |String |No |bwp\-2zeo\*\*\*\*\*\*\*\* |The ID of the shared bandwidth package. The EIP address is added to the shared bandwidth package.<br><br>You can call the [DescribeBandwidthPackages](https://docs.byteplus.com/en/docs/bandwidthpackage/DescribeBandwidthPackages) API to query the ID of the shared bandwidth package.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">An EIP address can be added to a shared bandwidth package only when ‌all of the following conditions are met:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The line types are identical.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The shared bandwidth package is of type IPv4.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">No security protection is configured for the shared bandwidth package.</div><br> |


<span id="clusterconnectorconfigrequest"></span>
### ClusterConnectorConfigRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Type |String |Yes |Direct |The connection mode for cluster registration. Valid values:<br><br><br>* **Direct**: Direct connection mode. The cluster is registered and managed through the direct connection mode of the KubeConfig for the target cluster.<br><br>* **Agent**: Agent mode. The cluster is registered and managed based on an Agent within the target cluster. |
|Provider |String |Yes |Ack |The provider of the registered cluster. Valid values:<br><br><br>* **Ack**: Alibaba Cloud ACK<br><br>* **Tke**: Tencent Cloud TKE<br><br>* **Cce**: Huawei Cloud CCE<br><br>* **Gke**: Google Cloud GKE<br><br>* **Eks**: Amazon EKS<br><br>* **BaiduCce**: Baidu Cloud CCE<br><br>* **None**: custom cluster |
|ProxyConfig |Object of [ProxyConfigRequest](https://docs.byteplus.com/en/docs/90/21190#proxyconfigrequest) |No |\- |The proxy mode configurations of the registered cluster.<br><br>This parameter is required only if `Type` is set to `Agent`. |
|TargetKubeConfig |String |No |\- |The KubeConfig of the cluster to be registered. It must be Base64\-encoded. Valid values: 0 to 20480.<br><br>This parameter is required only if `Type` is set to Direct. Otherwise, it is ignored. |


<span id="proxyconfigrequest"></span>
### ProxyConfigRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|SubnetIds |Array of String |No |["subnet\-5g39\*\*\*","subnet\-5g39d\*\*\*"] |The list of subnet IDs used by the control plane of the registered cluster for network communications within the VPC. |
|AclEnabled |Boolean |No |true |The allowlist\-based admission control, which is used to restrict the IP addresses that can access the registered cluster. If you enable the allowlist and specify CIDR blocks in the allowlist, both the IP address of the agent used to access the cluster and the IP addresses allowed to access the API server after the cluster is accessed will be limited to the configured CIDR blocks in the allowlist. Otherwise, access is denied. Valid values:<br><br><br>* **true**<br><br>* **false** |
|AclIpWhitelist |Array of String |No |["192.168.1.0/24", "10.0.0.0/16"] |The IP address list in the ACL allowlist. The CIDR format is supported. This parameter is valid only if `AclEnabled` is set to `true`. |
|ApiServerPublicAccessConfig |Object of [PublicAccessConfigRequest](https://docs.byteplus.com/en/docs/90/21190#publicaccessconfigrequest) |No |\- |The public access configurations of the registered cluster. This parameter is required only if `ApiServerPublicAccessEnabled` is set to `true`. Otherwise, this parameter is ignored. |
|ApiServerPublicAccessEnabled |Boolean |No |false |Whether to enable public access to the API server of the registered cluster. Valid values:<br><br><br>* **false**: Disable it.<br><br>* **true**: Enable this option. |


<span id="podsconfigupdaterequest"></span>
### PodsConfigUpdateRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|VpcCniConfig |Object of [VpcCniConfigUpdateRequest](https://docs.byteplus.com/en/docs/90/21190#vpccniconfigupdaterequest) |No |\- |The VPC\-CNI network configuration. |
|FlannelConfig |Object of [FlannelConfigUpdateRequest](https://docs.byteplus.com/en/docs/90/21190#flannelconfigupdaterequest) |No |\- |The Flannel network configurations. |


<span id="vpccniconfigupdaterequest"></span>
### VpcCniConfigUpdateRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|SubnetIds |Array of String |No |["subnet\-5g39dw\*\*\*\*\*\*","subnet\-5g3vp\*\*\*\*\*\*"] |List of pod subnet IDs in VPC\-CNI networking.<br><br>It is required only when `PodNetworkMode is VpcCniShared`. Otherwise, this parameter can be omitted.<br><br>You can call the [VPC API](https://docs.byteplus.com/en/docs/vpc/API-overview-1) to obtain subnet IDs.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When you update a cluster, you can add more subnets to the pods based on the existing pod subnets in the current cluster.</div><br> |
|VciSubnetIds |Array of String |No |["subnet\-5g39d\*\*\*\*","subnet\-5g39d\*\*\*\*"] |A list of IDs of VCI Pod subnets in the VPC\-CNI networking.<br><br>It is required only when `PodNetworkMode is VpcCniShared`. Otherwise, this parameter can be omitted.<br><br>You can call the [VPC API](https://docs.byteplus.com/en/docs/vpc/API-overview-1) to obtain subnet IDs.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The VCI Pod subnets must be a subset of the Pod subnets.</div><br> |


<span id="flannelconfigupdaterequest"></span>
### FlannelConfigUpdateRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|SubnetIds |Array of String |No |["subnet\-5g39\*\*\*","subnet\-5g39\*\*\*"] |The list of pod subnet IDs that correspond to the Flannel network model.<br><br>It is required only when `PodNetworkMode is Flannel`. Otherwise, this parameter can be omitted.<br><br>You can call the [VPC API](https://docs.byteplus.com/en/docs/vpc/API-overview-1) to obtain subnet IDs. |


<span id="clusterloggingconfigrequest"></span>
### ClusterLoggingConfigRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|LogSetups |Array of [LogSetupRequest](https://docs.byteplus.com/en/docs/90/21190#logsetuprequest) |No |\- |Cluster logging setups.<br><br><br>* An empty array means that no logging setup is enabled.<br><br>* When logging is enabled for the first time, a log topic is generated automatically.<br><br>* When multiple logging setups are provided, `LogType` cannot be repeated. |
|LogProjectId |String |No |b68324a0\-2680\-48c7\*\*\*\*\*\*\*\* |ID of the log project for the cluster.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">It cannot be an empty string.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If <code>LogProjectId</code> is not specified during cluster creation, the system will automatically create a new log project.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">A log project automatically created by the system has a name in the format <code>k8s-log-{clusterId}-{6 random characters}</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If <code>LogSetups.Enabled</code> is set to <code>false</code>, no log project will be automatically created.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When updating the cluster configuration, if <code>LogProjectId</code> already points to a log project, it cannot be set to an empty value.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">In a cluster configuration update, if the cluster does not have any log configuration, and only <code>LogProjectId</code> is provided while <code>LogSetups</code> is empty, <code>LogProjectId</code> will be ignored.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Updating <code>LogProjectId</code> will create another topic for items for which logging is enabled.</div><br> |


<span id="logsetuprequest"></span>
### LogSetupRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|LogTtl |Integer |No |30 |Log retention duration in TLS. Logs that exceed the specified retention duration in this log topic will be automatically cleared.<br><br><br>* Value range: 1 to 3650.<br><br>* Unit: days.<br><br>   A value of 3650 indicates permanent storage. |
|Enabled |Boolean |No |false |Whether to enable this log option. Valid values:<br><br><br>* **false**: not enabled<br><br>* **true**: enabled<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">In a cluster configuration update, if <code>LogType</code> is <code>Audit</code>, changing the value to <code>Enabled</code> will restart the API server.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">In a cluster configuration update, if the value of <code>Enabled</code> changes from <code>false</code> to <code>true</code>, a new log topic will be created.</div><br> |
|LogType |String |Yes |Audit |The type of enabled logs. Valid values:<br><br><br>* **Audit**: cluster audit logging<br><br>* **KubeApiServer**: kube\-apiserver add\-on log<br><br>* **KubeScheduler**: kube\-scheduler add\-on log<br><br>* **KubeControllerManager**: kube\-controller\-manager log<br><br>* **Etcd**: etcd add\-on log<br><br>* **ClusterAutoscaler**: cluster\-autoscaler log |


<span id="clusterkubernetesconfigrequestforupdate"></span>
### ClusterKubernetesConfigRequestForUpdate


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|CustomSans |Array of String |No |["abc.com","192.168.0.10"] |Specify a list of Subject Alternative Names (SAN). You can enter custom IP addresses, domain names, or URIs that conform to the corresponding specifications. If you specify more than one, separate them with commas (,). You can specify up to six SANs. For more usage instructions, see [Connecting to clusters using custom domain names](https://docs.byteplus.com/en/docs/vke/Connecting_to_clusters_using_custom_domain_names). |
|ClusterDomain |String |No |cluster.local |Cluster local domain name. A domain name consists of two or more parts separated by dots (.). Each part may contain lowercase letters, digits, and hyphens (\-) and must start and end with a lowercase letter or digit. The entire name must not exceed 57 characters in length. |
|AdvancedConfig |Object of [AdvancedConfig](https://docs.byteplus.com/en/docs/90/21190#advancedconfig) |No |\- |The enhanced configuration for kube\-apiserver. |
|ControlPlaneConfig |Object of [KubernetesComponentConfigsForUpdate](https://docs.byteplus.com/en/docs/90/21190#kubernetescomponentconfigsforupdate) |No |\- |The custom parameter configuration for Kubernetes core add\-ons. |


<span id="advancedconfig"></span>
### AdvancedConfig


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|InternalDnsEnabled |Boolean |No |true |Whether to enable private domain access to the API Server for the cluster:<br><br><br>* **true**: Enabled. Node\-side components access the API Server via the private domain.<br><br>* **false**: (Default) Disable.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">For VKE\-managed clusters created before May 15, 2026, node\-side components access the API Server via CLB VIP. You can configure this parameter to switch the access route so that the node\-side components can access the API Server via a private domain. After configuration, you also need to perform a series of operations. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Enabling_API_Server_private_domain_access_for_existing_clusters">Enabling private domain name access to API Server for existing clusters</a>.</div><br> |


<span id="kubernetescomponentconfigsforupdate"></span>
### KubernetesComponentConfigsForUpdate


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|KubeApiServerConfig |Object of [KubeApiServerConfigForUpdate](https://docs.byteplus.com/en/docs/90/21190#kubeapiserverconfigforupdate) |No |\- |The custom parameter configuration for the kube\-apiserver add\-on. |
|KubeSchedulerConfig |Object of [KubeSchedulerConfigForUpdate](https://docs.byteplus.com/en/docs/90/21190#kubeschedulerconfigforupdate) |No |\- |The custom parameter configuration for the kube\-scheduler add\-on. |
|KubeControllerManagerConfig |Object of [KubeControllerManagerConfigForUpdate](https://docs.byteplus.com/en/docs/90/21190#kubecontrollermanagerconfigforupdate) |No |\- |The custom parameter configuration for the kube\-controller\-manager add\-on. |


<span id="kubeapiserverconfigforupdate"></span>
### KubeApiServerConfigForUpdate


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|FeatureGates |Object of [KubeApiServerFeatureGates](https://docs.byteplus.com/en/docs/90/21190#kubeapiserverfeaturegates) |No |\- |The feature gate configuration for kube\-apiserver. |
|RequestTimeout |String |No |60s |The request timeout, which is the maximum duration the handler waits for the request to complete before terminating it.<br><br><br>* The value is in the format of `number+s`. For example, `60s` means 60 seconds.<br><br>* Value range: [60s, 180s]<br><br>* Default value: 60s |
|AdmissionPlugins |Object of [AdmissionPlugins](https://docs.byteplus.com/en/docs/90/21190#admissionplugins) |No |\- |The list of admission control add\-ons additionally enabled in kube\-apiserver beyond those enabled by default. |
|DefaultNotReadyTolerationSeconds |Integer |No |300 |The toleration duration for Pods against the `NotReady:NoExecute` taint on nodes.<br><br><br>* Unit: seconds<br><br>* Value range: [1, 3000]<br><br>* Default value: 300 |
|DefaultUnreachableTolerationSeconds |Integer |No |300 |Toleration duration of the Pod for the `Unreachable:NoExecute` taint on the node.<br><br><br>* Unit: seconds<br><br>* Value range: [1, 3000]<br><br>* Default value: 300 |


<span id="kubeapiserverfeaturegates"></span>
### KubeApiServerFeatureGates


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|SidecarContainers |Boolean |No |true |Whether to enable the SidecarContainers feature gate to support native Sidecar containers. Valid values:<br><br><br>* **true**: Enable it.<br><br>* **false**: Disable it.<br><br>* The default is empty, which means this feature gate is not overridden and is determined by the default policy of kube\-apiserver itself.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This feature gate is supported only by the following VKE cluster versions:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">v1.30 ≤ cluster version ≤ v1.32</div><br> |
|StatefulSetAutoDeletePVC |Boolean |No |true |Whether to enable the StatefulSetAutoDeletePVC feature gate to support automatic deletion of PVCs by StatefulSets. Valid values:<br><br><br>* **true**: Enable it.<br><br>* **false**: Disable it.<br><br>* The default is empty, which means this feature gate is not overridden and is determined by the default policy of kube\-apiserver itself.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This feature gate is supported only in VKE clusters of the following versions:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">v1.28 ≤ Cluster version ≤ v1.30</div><br> |
|InPlacePodVerticalScaling |Boolean |No |true |Whether to enable the InPlacePodVerticalScaling feature gate, which supports in\-place vertical scaling for Pods. Valid values:<br><br><br>* **true**: Enable it.<br><br>* **false**: Disable it.<br><br>* This parameter is left empty by default. This means that this feature gate is not overridden and is determined by the default policy of kube\-apiserver.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This feature gate is supported only in VKE clusters running Kubernetes v1.34.</div><br> |
|MaxUnavailableStatefulSet |Boolean |No |true |Whether to enable the MaxUnavailableStatefulSet feature gate to add the `maxUnavailable` configuration for StatefulSet rolling updates. This allows multiple Pods to be unavailable and updated in parallel during updates. Valid values:<br><br><br>* **true**: Enable it.<br><br>* **false**: Disable it.<br><br>* The default is empty, which means this feature gate is not overridden and is determined by the default policy of kube\-apiserver itself.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This feature gate is supported only in VKE clusters of the following versions:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Cluster version ≥ v1.36</div><br> |


<span id="admissionplugins"></span>
### AdmissionPlugins


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|PodNodeSelector |Boolean |No |true |Whether to enable the PodNodeSelector admission control add\-on. Valid values:<br><br><br>* **true**: Enable. This indicates that a node selector is forcibly attached to all Pods within the namespace. This schedules the Pods only onto nodes with specific labels.<br><br>* **false**: (Default) Disable it. |
|AlwaysPullImages |Boolean |No |true |Whether to enable the AlwaysPullImages admission control add\-on. Valid values:<br><br><br>* **true**: Enable it. It indicates that the image is forcibly re\-pulled when each Pod is modified.<br><br>* **false**: (Default) Disable it. |
|PodTolerationRestriction |Boolean |No |true |Whether to enable the PodTolerationRestriction admission control add\-on. Valid values:<br><br><br>* **true**: Enable. This uniformly manages Pod tolerations within a namespace to prevent the abuse of high\-privilege taint tolerations.<br><br>* **false**: (Default) Disable it. |


<span id="kubeschedulerconfigforupdate"></span>
### KubeSchedulerConfigForUpdate


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|KubeApiQps |Integer |No |50 |The QPS limit for communication between kube\-scheduler and the API server.<br><br><br>* Default value: 50<br><br>* Value range: [1, 10000] |
|Parallelism |Integer |No |16 |The number of Goroutines that kube\-scheduler executes in parallel when running the scheduling algorithm.<br><br><br>* Default value: 16<br><br>* Value range: Positive integers |
|FeatureGates |Object of [KubeSchedulerFeatureGates](https://docs.byteplus.com/en/docs/90/21190#kubeschedulerfeaturegates) |No |\- |The feature gate configuration for kube\-scheduler. |
|KubeApiBurst |Integer |No |100 |The maximum burst requests when kube\-scheduler communicates with the API Server.<br><br><br>* Default value: 100<br><br>* Value range: [1, 10000]<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The value of <strong>KubeApiBurst</strong> must be greater than or equal to the value of <strong>KubeApiQps</strong>.</div><br> |
|PodMaxBackoffSeconds |Integer |No |10 |The maximum backoff delay for rescheduling pods in seconds. After a pod fails to be scheduled, the pod cannot be rescheduled until the delay ends.<br><br><br>* Default value: 10.<br><br>* Unit: seconds<br><br>* Value range: [0, 3600] |
|PercentageOfNodesToScore |Integer |No |50 |The evaluated proportion of nodes that can run Pods when Pods are being scheduled. Filtering stops after the specified proportion is reached.<br><br><br>* Default value: 50<br><br>* Unit: %<br><br>* Value range: [0, 100] |
|PodInitialBackoffSeconds |Integer |No |1 |The initial backoff time for unschedulable Pods.<br><br><br>* Default value: 1<br><br>* Unit: seconds<br><br>* Value range: Positive integers |


<span id="kubeschedulerfeaturegates"></span>
### KubeSchedulerFeatureGates


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|SidecarContainers |Boolean |No |true |Whether to enable the SidecarContainers feature gate to support native Sidecar containers. Valid values:<br><br><br>* **true**: Enable it.<br><br>* **false**: Disable it.<br><br>* This parameter is left empty by default. This means that this feature gate is not overridden and is determined by the default policy of kube\-scheduler.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This feature gate is supported only by the following VKE cluster versions:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">v1.30 ≤ cluster version ≤ v1.32</div><br> |
|InPlacePodVerticalScaling |Boolean |No |true |Whether to enable the InPlacePodVerticalScaling feature gate, which supports in\-place vertical scaling for Pods. Valid values:<br><br><br>* **true**: Enable it.<br><br>* **false**: Disable it.<br><br>* This parameter is left empty by default. This means that this feature gate is not overridden and is determined by the default policy of kube\-scheduler.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This feature gate is supported only in VKE clusters running Kubernetes v1.34.</div><br> |


<span id="kubecontrollermanagerconfigforupdate"></span>
### KubeControllerManagerConfigForUpdate


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|KubeApiQps |Integer |No |50 |The QPS limit for communication between kube\-controller\-manager and the API server.<br><br><br>* Default value: 50<br><br>* Value range: [1, 10000] |
|FeatureGates |Object of [KubeControllerManagerFeatureGates](https://docs.byteplus.com/en/docs/90/21190#kubecontrollermanagerfeaturegates) |No |\- |The feature gate configuration for kube\-controller\-manager. |
|KubeApiBurst |Integer |No |100 |The maximum burst requests when kube\-controller\-manager communicates with the API Server.<br><br><br>* Default value: 100<br><br>* Value range: [1, 10000]<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The value of <strong>KubeApiBurst</strong> must be greater than or equal to the value of <strong>KubeApiQps</strong>.</div><br> |
|NodeEvictionRate |Double |No |0.1 |The Pod eviction rate in node failure scenarios. When the availability zone is healthy, this parameter controls the number of nodes from which Pods are evicted per second.<br><br><br>* Default value: 0.1, which means 0.1 nodes are evicted per second, that is, 1 node is evicted every 10 seconds.<br><br>* Value range: [0, 1.0] |
|NodeMonitorGracePeriod |Integer |No |50s |The duration after which a node is marked as `NotReady` or `Unknown` if it becomes unreachable.<br><br><br>* The value is in the format of `number+s`. For example, `50s` means 50 seconds.<br><br>* Default value: 50s<br><br>* Value range: [1, 10000] |
|UnhealthyZoneThreshold |Double |No |0.55 |The unhealthy threshold for availability zones. When the proportion of nodes in the NotReady state within the same availability zone exceeds this threshold, the control plane determines that the availability zone has experienced an infrastructure\-wide failure and triggers a zone\-level rate\-limited eviction policy.<br><br><br>* Default value: 0.55<br><br>* Value range: [0, 1.0] |
|TerminatedPodGCThreshold |Integer |No |12500 |The garbage collection threshold for terminated Pods, which is the maximum number of terminated Pods that can be retained.<br><br><br>* Default value: 12500<br><br>* Value range: [10000, 50000] |
|LargeClusterSizeThreshold |Integer |No |50 |The large cluster size threshold. The node controller uses this threshold to determine whether the cluster is a large\-scale cluster, which determines the Pod eviction policy.<br><br><br>* Default value: 50<br><br>* Value range: [1,10000] |
|SecondaryNodeEvictionRate |Double |No |0.01 |The secondary node draining rate during large\-scale failures. This parameter specifies the number of nodes from which Pods are evicted per second when the availability zone is deemed “unhealthy” (for example, when the failure ratio exceeds the configured UnhealthyZoneThreshold) and nodes fail.<br><br><br>* Default value: 0.01<br><br>* Value range: [0, 1.0] |
|ConcurrentTTLAfterFinishedSyncs |Integer |No |10 |The number of concurrent synchronization goroutines of the TTLAfterFinished controller that is responsible for cleaning up expired Jobs.<br><br><br>* Default value: 10.<br><br>* Value range: [1, 50] |
|HorizontalPodAutoscalerTolerance |Double |No |0.1 |When Horizontal Pod Autoscaler (HPA) is used, if the deviation between the actual metric and the desired metric is less than this tolerance rate, scaling will not be triggered.<br><br><br>* Default value: 0.1<br><br>* Value range: [0, 1.0] |
|HorizontalPodAutoscalerSyncPeriod |String |No |15s |The period for the HPA to synchronize the number of Pods.<br><br><br>* The value is in the format of `number+s` or `number+m`. For example, `15s` means 15 seconds and `1m` means 1 minute.<br><br>* Default value: 15s<br><br>* Value range: [5s, 1m] |
|ConcurrentHorizontalPodAutoscalerSyncs |Integer |No |5 |The number of HPA objects that can be concurrently synchronized. A larger value results in faster processing response for HPA objects, but consumes more CPU and network resources.<br><br><br>* Default value: 5<br><br>* Value range: Positive integers<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This parameter is supported only in clusters running on Kubernetes v1.26 or later.</div><br> |


<span id="kubecontrollermanagerfeaturegates"></span>
### KubeControllerManagerFeatureGates


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|StatefulSetAutoDeletePVC |Boolean |No |true |Whether to enable the StatefulSetAutoDeletePVC feature gate to support automatic deletion of PVCs by StatefulSets. Valid values:<br><br><br>* **true**: Enable it.<br><br>* **false**: Disable it.<br><br>* This parameter is left empty by default. This means that this feature gate is not overridden and is determined by the default policy of kube\-controller\-manager.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This feature gate is supported only by the following VKE cluster versions:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">v1.28 ≤ Cluster version ≤ v1.30</div><br> |
|InPlacePodVerticalScaling |Boolean |No |true |Whether to enable the InPlacePodVerticalScaling feature gate, which supports in\-place vertical scaling for Pods. Valid values:<br><br><br>* **true**: Enable it.<br><br>* **false**: Disable it.<br><br>* This parameter is left empty by default. This means that this feature gate is not overridden and is determined by the default policy of kube\-controller\-manager.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This feature gate is supported only in VKE clusters running Kubernetes v1.34.</div><br> |
|MaxUnavailableStatefulSet |Boolean |No |true |Whether to enable the MaxUnavailableStatefulSet feature gate to add the `maxUnavailable` configuration for StatefulSet rolling updates. This allows multiple Pods to be unavailable and updated in parallel during updates. Valid values:<br><br><br>* **true**: Enable it.<br><br>* **false**: Disable it.<br><br>* This parameter is left empty by default. This means that this feature gate is not overridden and is determined by the default policy of kube\-controller\-manager.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This feature gate is supported only by the following VKE cluster versions:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Cluster version ≥ v1.36</div><br> |


<span id="clustermonitoringconfigupdaterequest"></span>
### ClusterMonitoringConfigUpdateRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|WorkspaceId |String |No |2521550\*\*\*\*\*\*\*\* |The ID of the VMP workspace used for cluster monitoring.<br><br>You can obtain the workspace ID by calling the [API of VMP](https://docs.byteplus.com/en/docs/vmp/ListWorkspaces). |
|ComponentConfigs |Array of [ClusterMonitoringComponentConfigRequest](https://docs.byteplus.com/en/docs/90/21190#clustermonitoringcomponentconfigrequest) |No |\- |The configurations of the control plane monitoring for the cluster. |
|EnableMetricsExternalCollection |Boolean |No |false |Specify whether to enable external Prometheus to collect cluster control plane add\-on metrics. Valid values:<br><br><br>* **true**: Enable it.<br><br>* **false**: (Default) Disable.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After you enable this feature, you can use self\-managed Prometheus to collect metrics of managed control plane add\-ons in the cluster. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Using_self-managed_Prometheus_to_collect_control_plane_metrics">Using self\-built Prometheus to collect control plane add\-on metrics</a>.</div><br> |


<span id="clustermonitoringcomponentconfigrequest"></span>
### ClusterMonitoringComponentConfigRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Name |String |Yes |KubeApiServer |The control plane add\-on of the cluster that needs to be monitored. Valid values: KubeApiServer, KubeScheduler, Etcd, and ClusterAutoscaler. |
|Enabled |Boolean |No |true |Specify whether to enable control plane add\-on monitoring. Valid values:<br><br><br>* **true**: Enable it.<br><br>* **false**: (Default) Disable it. |


<span id="clustermaintenancewindowconfigrequest"></span>
### ClusterMaintenanceWindowConfigRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Duration |Integer |No |4 |The duration of automatic O&M. The value is an integer. Value range: 4 to 24. Unit: hours.<br><br>The default value is 4 if this parameter is not specified. |
|StartTime |String |No |20:00:00Z |The start time of automatic O&M. It must follow the standard time format of Golang and a 24\-hour clock. Value range: A whole hour within 00 to 23. Example: 01:00:00Z and 14:00:00Z.<br><br>If this parameter is not configured, the default value is 16:00:00Z (UTC). This corresponds to 00:00:00 the next day in Beijing Time (UTC+8).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter can only be set to UTC. If you need to use another time zone, you need to manually convert the time to UTC.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The <code>ExemptStartDate</code> and <code>ExemptEndDate</code> parameters use Beijing Time (UTC+8) as their default time zone. When the preceding parameters are specified together with this parameter, ensure time zone consistency.</div><br> |
|TaskConfigs |Array of [WindowTaskConfig](https://docs.byteplus.com/en/docs/90/21190#windowtaskconfig) |No |\- |The configurations of the automatic O&M task.<br><br>If this parameter is not specified, the system only executes **cluster control plane daily O&M** tasks by default and does not execute other O&M tasks. |
|WeeklyCycle |Array of String |No |["Monday","Tuesday"] |The automatic O&M cycle. Valid values:<br><br><br>* **Monday**<br><br>* **Tuesday**<br><br>* **Wednesday**<br><br>* **Thursday**<br><br>* **Friday**<br><br>* **Saturday**<br><br>* **Sunday**<br><br><br>If this parameter is not specified, the system performs O&M tasks every day by default. |
|ExemptEndDate |String |No |20260704 |The end time of the automatic O&M exemption window, which is in the format of `YYYYMMDD`, and applied based on calendar days in Beijing Time (UTC+8). For example, if the value is set to `20260704`, it indicates that automatic O&M tasks will no longer be executed from 23:59:59 on that date.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This date must be later than the date configured for <code>ExemptStartDate</code>, and the difference between the two dates must not exceed 60 days.</div><br> |
|ExemptStartDate |String |No |20260702 |The start time of the automatic O&M exemption window, which is in the format of `YYYYMMDD`, and applied based on calendar days in Beijing Time (UTC+8). For example, if the value is set to `20260702`, it indicates that automatic O&M tasks will no longer be executed from 00:00:00 on that date.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This date must be earlier than the date configured for <code>ExemptEndDate</code>, and the difference between the two dates must not exceed 60 days.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">In scenarios such as business\-critical periods or network lockdowns, you can configure an exemption window to prohibit the system from performing automatic O&M operations.</div><br> |


<span id="windowtaskconfig"></span>
### WindowTaskConfig


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Group |String |Yes |Cluster |The group of automatic O&M tasks. Valid values:<br><br><br>* **Cluster**: Control plane O&M.<br><br>* **Addon**: Data plane O&M. |
|Action |String |Yes |AutoUpgradeAddonVersion |The automatic O&M task. Valid values:<br><br><br>* **AutoUpgradeClusterMinorVersion**: A task that automatically upgrades cluster patch versions. This task can be configured only if `Group` is set to `Cluster`.<br><br>* **AutoUpgradeAddonVersion**: A task that automatically upgrades add\-on versions.<br><br>   * This task can be configured only if `Group` is set to `Addon`.<br><br>   * When you configure this task, you also need to use `Targets` to specify the add\-ons to be upgraded. |
|Targets |Array of String |No |["metrics\-server","cluster\-autoscaler"] |Specify the add\-on for which automatic version upgrade is performed. You can specify multiple add\-ons, which are separated by commas (`,`).<br><br>The following add\-ons are supported: cluster\-autoscaler, metrics\-server, log\-collector, event\-collector, node\-problem\-detector, metrics\-collector, and prometheus\-agent.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">For the introduction and description of the preceding add\-ons, see <a href="https://docs.byteplus.com/en/docs/vke/Add-on-overview">Add\-on overview</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Currently, only some add\-ons support automatic upgrades. To upgrade other add\-ons, manually upgrade them on the "Addons" page. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on">Upgrading add\-ons</a>.</div><br> |


<span id="registerclustermonitoringconfigupdaterequest"></span>
### RegisterClusterMonitoringConfigUpdateRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|QueryUrl |String |No |http://query.prometheus\-cn\-beijing.ivolces.com/workspaces/1d0\*\*\* |The query URL of the VMP workspace when you monitor a registered cluster by using VMP. The registered cluster uses this URL to query monitoring data saved in the workspace.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For more information about workspaces and addresses, see <a href="https://docs.byteplus.com/en/docs/vmp/Obtaining-the-Remote-Write-URL-and-Query-URL">Obtaining workspace addresses</a>.</div><br> |
|WorkspaceId |String |No |e28ae750\-bbb8\*\*\*\*\*\*\*\* |The ID of the VMP workspace when you monitor a registered cluster by using VMP.<br><br>You can obtain the workspace ID by calling the [API of VMP](https://docs.byteplus.com/en/docs/vmp/ListWorkspaces). |
|RemoteWriteUrl |String |No |http://write.prometheus\-cn\-beijing.ivolces.com/workspaces/1d0\*\*\* |The remote write URL of the VMP workspace when you monitor a registered cluster by using VMP. The registered cluster uses this URL to save cluster monitoring data in the specified workspace.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For more information about workspaces and addresses, see <a href="https://docs.byteplus.com/en/docs/vmp/Obtaining-the-Remote-Write-URL-and-Query-URL">Obtaining workspace addresses</a>.</div><br> |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vke.cn-beijing.byteplusapi.com.cn?Action=UpdateClusterConfig&Version=2022-05-12
Content-Type: application/json
{
    "Id": "cc8oo0ivqt********",
    "DeleteProtectionEnabled": true,
    "PodsConfig": {
        "VpcCniConfig": {
            "SubnetIds": [
                "subnet-****1",
                "subnet-****2"
            ]
        }
    },
    "LoggingConfig": {
        "LogSetups": [
            {
                "LogType": "Audit",
                "LogTtl": 30,
                "Enabled": true
            }
        ]
    }
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

There are no proprietary response parameters for this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.

<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104********",
        "Action": "UpdateClusterConfig",
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
|400 |QuotaExceeded.{{ResourceType}} |The quota of {{ResourceType}} has reached the limit. |The quota for the specified resource (such as EIP, LogProject, and LogTopic) has reached the upper limit. Increase the relevant resource quota or delete unused resources. When the available quota is sufficient, try again later. |
|400 |Insufficient.SubnetIp |The IP of subnet {{subnetId}} is insufficient. |The available IP addresses in the specified subnet are insufficient. Specify a compliant subnet and try again. |
|400 |LimitExceeded.ClusterSubnetZones |You have reached the limit of the number of cluster subnet zones that you can add. |The number of availability zones of subnets in the cluster exceeds the limit. Make sure that the availability zones of subnets do not exceed three. |
|400 |LimitExceeded.ClusterSubnetsOfZone |You have reached the limit of the number of cluster subnets in zone {{zone}} that you can add. |The number of specified subnets in a single availability zone exceeds the limit. Make sure that the number of specified subnets in each availability zone does not exceed 2. |
|409 |Conflict.Name |The specified name conflicts with existing {{resourceType}}. |A resource with the same name exists in the specified region. Update the resource name and try again later. |
|400 |IpFamilyMismatch.{{parameter}} |The specified {{resourceType}} {{resourceContent}} and IpFamily {{ipFamily}} are mismatched. |The specified resources do not match the network protocol stack. Confirm the network protocol stack supported by the resources and try again. |
|403 |OperationDenied.{{cause}} |Operation is denied because {{causeDescription}}. |Indicates that the operation is denied. Updating the cluster is not allowed in the current environment. Resolve the issue based on the error message and retry. |
