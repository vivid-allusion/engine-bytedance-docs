---
title: "CreateCluster"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/CreateCluster"
---

Create a VKE cluster.

<span id=".5L2_55So6K-05piO"></span>
## Usage instructions

This is an asynchronous API. When it returns a success message, the cluster ID is returned. This does not necessarily indicate that the cluster is created. You need to call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to obtain the current status of the cluster, based on which you check whether it has been created. After the cluster is created (with the status of `{Running, [Ok]})`, VKE starts to bill the cluster on a pay\-as\-you\-go basis. For billing details, see [Product billing](https://docs.byteplus.com/en/docs/vke/Billing).

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point for your business region.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=CreateCluster&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateCluster&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table describes the API request parameters. You also need to provide public parameters when calling this API. For details about public request parameters, see [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters).


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |CreateCluster |The API name. The current API is `CreateCluster`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|ClientToken |String |No |BC028527\-33B9\-4990\-A633\-84E9F9\*\*\*\*\*\* |A string used to ensure the idempotency of the request. This string is passed in by the caller and must be unique across different requests. ClientToken is case\-sensitive and can consist of 64 ASCII characters at most. |
|Name |String |Yes |TestCluster |Cluster name.<br><br><br>* The name must be unique within the same region.<br><br>* It can contain uppercase and lowercase letters, Chinese characters, digits, and hyphens (\-). It can be 2 to 64 characters in length. |
|Description |String |No |A Kubernetes Cluster Managed by VKE |Cluster description. It cannot exceed 300 characters in length. |
|DeleteProtectionEnabled |Boolean |No |false |Specify whether to enable cluster deletion protection. Valid values:<br><br><br>* **false**: (Default) Disable deletion protection.<br><br>* **true**: Enable deletion protection. Direct deletion of the cluster is not allowed.<br><br>   To delete a cluster with deletion protection enabled, call the [UpdateClusterConfig](https://docs.byteplus.com/en/docs/vke/UpdateClusterConfig) API to modify the **DeleteProtectionEnabled** configuration before you delete the cluster or configure the **Force** parameter in a call to [DeleteCluster](https://docs.byteplus.com/en/docs/vke/DeleteCluster) to force deletion of the cluster. |
|ClusterConfig |Object of [ClusterConfigRequest](https://docs.byteplus.com/en/docs/90/21183#clusterconfigrequest) |No |\- |The network configurations of the control plane and nodes. |
|PodsConfig |Object of [PodsConfigRequest](https://docs.byteplus.com/en/docs/90/21183#podsconfigrequest) |No |\- |The cluster container (Pod) network configurations. |
|ServicesConfig |Object of [ServicesConfigRequest](https://docs.byteplus.com/en/docs/90/21183#servicesconfigrequest) |No |\- |Service network configuration of the cluster. |
|Tags |Array of [Tag](https://docs.byteplus.com/en/docs/90/21183#tag) |No |\- |Specify custom resource tags. They are used to classify, search, and aggregate clusters with the same characteristics from different dimensions, enabling flexible cluster management.<br><br><br>* Each **Key** in **Tags** must be unique.<br><br>* If the resource already has the same **Tags.Key**, an error will not occur if you bind the same **Tags.Key** again. Instead, the latest **Tags.Value** will be used.<br><br>* A resource can have up to 50 **tags**.<br><br>* The **Key** and **Value** in **Tags** cannot start or end with a space. |
|KubernetesVersion |String |No |1.36 |Kubernetes version of the cluster. The value is in the `x.xx` format. During cluster creation, the system automatically matches the latest VKE version corresponding to the specified Kubernetes version.<br><br>For the release notes for Kubernetes versions supported by VKE, see [Kubernetes version release notes](https://docs.byteplus.com/en/docs/vke/Kubernetes-version-release-notes). |
|LoggingConfig |Object of [ClusterLoggingConfigRequest](https://docs.byteplus.com/en/docs/90/21183#clusterloggingconfigrequest) |No |\- |The log configurations for the cluster. |
|ProjectName |String |No |default |Name of the project to which the cluster belongs. Each cluster can only belong to one project.<br><br><br>* It can only contain letters, digits, underscores (`_`), periods (`.`), and hyphens (`-`).<br><br>* It can be up to 64 characters in length.<br><br>* Default value: default. |
|KubernetesConfig |Object of [ClusterKubernetesConfigRequest](https://docs.byteplus.com/en/docs/90/21183#clusterkubernetesconfigrequest) |No |\- |The Kubernetes\-related parameter settings of the cluster. |
|MonitoringConfig |Object of [ClusterMonitoringConfigRequest](https://docs.byteplus.com/en/docs/90/21183#clustermonitoringconfigrequest) |No |\- |The monitoring configurations of the cluster. |
|MaintenanceWindowConfig |Object of [ClusterMaintenanceWindowConfigRequest](https://docs.byteplus.com/en/docs/90/21183#clustermaintenancewindowconfigrequest) |No |\- |The O&M configurations of the cluster. |


<span id="clusterconfigrequest"></span>
### ClusterConfigRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|SubnetIds |Array of String |No |["subnet\-5g39dwxvppo\*\*\*\*\*\*"] |The IDs of subnets used by the cluster control plane to communicate within the VPC.<br><br>You can call the [VPC API](https://docs.byteplus.com/en/docs/vpc/API-overview-1) to obtain subnet IDs.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">When creating a cluster, make sure that all specified SubnetIds (including but not limited to this parameter) belong to the same VPC.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">We recommend selecting subnets in different availability zones to improve the high availability of the control plane.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">You can select subnets from up to 3 availability zones, with up to 2 subnets allowed per availability zone.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The number of available IP addresses in a subnet must be at least 1.</div><br> |
|ApiServerPublicAccessEnabled |Boolean |No |false |Whether to enable public access to the API Server of the cluster. Values:<br><br><br>* **false**: (Default) Disable it.<br><br>* **true**: Enable it. |
|ApiServerPublicAccessConfig |Object of [PublicAccessConfigRequest](https://docs.byteplus.com/en/docs/90/21183#publicaccessconfigrequest) |No |\- |The public access configurations of the API server for the cluster.<br><br>This parameter takes effect only if `ApiServerPublicAccessEnabled is set to true`. |
|ResourcePublicAccessDefaultEnabled |Boolean |No |false |Public node access configuration. Values:<br><br><br>* **false**: (Default) Disable public access. Existing NAT Gateways and rules are not affected.<br><br>* **true**: Enable public access. If this option is enabled, a NAT Gateway will be automatically created for the VPC of the cluster, and corresponding rules will be configured. |
|IpFamily |String |No |Ipv4 |Cluster network protocol stack, available values:<br><br><br>* **Ipv4**: (Default) IPv4 single stack.<br><br>* **Ipv6**: [[Beta - apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] IPv6 single stack.<br><br>* **DualStack**: [Beta \- apply for trial][ ](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)Enable IPv4 and IPv6 dual stack.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">After cluster creation is complete, you cannot modify this parameter. Configure it appropriately.</div><br> |


<span id="publicaccessconfigrequest"></span>
### PublicAccessConfigRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|PublicAccessNetworkConfig |Object of [EipConfigRequest](https://docs.byteplus.com/en/docs/90/21183#eipconfigrequest) |No |\- |The public access configurations of the API server of the cluster. This setting is required only when `ApiServerPublicAccessEnabled is set to true`. Otherwise, it is ignored.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After cluster creation is complete, you cannot modify this parameter. Configure it appropriately.</div><br> |


<span id="eipconfigrequest"></span>
### EipConfigRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Isp |String |No |BGP |The line type of the EIP. Valid values:<br><br><br>* **BGP**: BGP (multi\-line). |
|Bandwidth |Integer |No |100 |The maximum bandwidth of the EIP. Unit: Mbit/s. Valid values:<br><br><br>* If `BillingType is set to 2`, the valid values of Bandwidth are 1 to 500, and the default value is 10.<br><br>* If `BillingType is set to 3`, the valid values of Bandwidth are 1 to 200, and the default value is 10. |
|BillingType |Integer |No |3 |The billing type of the EIP. Valid values:<br><br><br>* **3**: (Default) Pay\-as\-you\-go \- by actual traffic. This billing method requires a maximum bandwidth limit and incurs fees based on the actual outbound traffic over the Internet, regardless of the usage duration.<br><br>* **2**: Pay\-as\-you\-go \- by bandwidth limit. After you specify a maximum bandwidth, fees are calculated based on the usage duration, regardless of the actual traffic. |
|BandwidthPackageId |String |No |bwp\-2zeo\*\*\*\*\*\*\*\* |The ID of the shared bandwidth package. The EIP address will be added to the shared bandwidth package.<br><br>You can call the [DescribeBandwidthPackages](https://docs.byteplus.com/en/docs/bandwidthpackage/DescribeBandwidthPackages) API to query the ID of the shared bandwidth package.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">An EIP address can be added to a shared bandwidth package only when all of the following conditions are met:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The line types are identical.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The shared bandwidth package is of type IPv4.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">No security protection is configured for the shared bandwidth package.</div><br> |


<span id="podsconfigrequest"></span>
### PodsConfigRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|PodNetworkMode |String |Yes |Flannel |Pod network model (CNI). Values:<br><br><br>* **Flannel**: an independent underlay container network solution, based on which a high\-performance network for clusters can be built along with the global routing capabilities of VPCs.<br><br>* **VpcCniShared**: an underlay network solution implemented based on the ENIs of VPCs, providing high network performance.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">After cluster creation is complete, you cannot modify this parameter. Configure it appropriately.</div><br> |
|VpcCniConfig |Object of [VpcCniConfigRequest](https://docs.byteplus.com/en/docs/90/21183#vpccniconfigrequest) |No |\- |The VPC\-CNI network configuration.<br><br>It can be configured only when `PodNetworkMode` is set to VpcCniShared and is optional. |
|FlannelConfig |Object of [FlannelConfigRequest](https://docs.byteplus.com/en/docs/90/21183#flannelconfigrequest) |No |\- |The Flannel network configurations.<br><br>It is optional and can be specified only if `PodNetworkMode is set to Flannel`. |


<span id="vpccniconfigrequest"></span>
### VpcCniConfigRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|SubnetIds |Array of String |Yes |["subnet\-5g39dxxxx","subnet\-dwxvxxxx"] |The list of Pod subnet IDs in VPC\-CNI networking.<br><br>It is required only when `PodNetworkMode is VpcCniShared`. Otherwise, this parameter can be omitted.<br><br>You can call the [VPC API](https://docs.byteplus.com/en/docs/vpc/API-overview-1) to obtain subnet IDs.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When creating a cluster, make sure that all specified <strong>SubnetIds</strong> (including but not limited to this parameter) belong to the same VPC.</div><br> |


<span id="flannelconfigrequest"></span>
### FlannelConfigRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|PodCidrs |Array of String |Yes |["172.17. **.** /19"] |The Pod CIDR blocks in Flannel networking.<br><br>It is optional and can be specified only if `PodNetworkMode is set to Flannel`.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The number of Pods in the cluster is limited by the number of IP addresses in the CIDR blocks. After the cluster is created, you cannot modify the Pod CIDR blocks. Plan the Pod CIDR blocks appropriately.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">They cannot conflict with the following network segments:</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">The VPC network segments specified by <strong>ClusterConfig.SubnetIds</strong> of the same cluster.</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">The network segments specified by <strong>ServiceConfig.ServiceCidrsv4</strong> of the same cluster.</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">The network segments specified by <strong>ServiceConfig.ServiceCidrsv4</strong> of all clusters within the same VPC.</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">The network segments specified by <strong>FlannelConfig.PodCidrs</strong> (this parameter) of different clusters within the same VPC.</div><br> |
|SubnetIds |Array of String |No |["subnet\-5g39\*\*\*\*","subnet\-5g39\*\*\*\*"] |The VPC subnet that provides IP addresses for VCI Pods.<br><br>It is optional and can be specified only if `PodNetworkMode is set to Flannel`.<br><br>You can call the [VPC API](https://docs.byteplus.com/en/docs/vpc/API-overview-1) to obtain subnet IDs.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When creating a cluster, make sure that all specified <strong>SubnetIds</strong> (including but not limited to this parameter) belong to the same VPC.</div><br> |
|MaxPodsPerNode |Integer |No |64 |Maximum number of Pod instances per node for Flannel pod networking. Values:<br><br><br>* 64 (default value)<br><br>* 16<br><br>* 32<br><br>* 128<br><br>* 256 |


<span id="servicesconfigrequest"></span>
### ServicesConfigRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|ServiceCidrsv4 |Array of String |Yes |["172.25. **.** /17"] |The CIDR block used by services within the cluster.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">It must not conflict with the CIDR blocks of <strong>FlannelConfig.PodCidrs.SubnetIds</strong> or <strong>ClusterConfig.SubnetIds</strong> for any cluster in the same VPC.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Only one array element is supported. If you specify multiple elements, only the first one takes effect.</div><br> |


<span id="tag"></span>
### Tag


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Key |String |Yes |key |The tag key.<br><br><br>* It cannot start with `volc:` in ‌any case variation‌.<br><br>* It can only contain letters, digits, spaces, and special characters `_.:/=+-@`.<br><br>* The length is limited to 1 to 128 characters. |
|Value |String |No |value |The tag value, which can be left empty.<br><br><br>* It can only contain letters, digits, spaces, and the following special characters: `_.:/=+-@`.<br><br>* Its length does not exceed 256 characters. |


<span id="clusterloggingconfigrequest"></span>
### ClusterLoggingConfigRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|LogSetups |Array of [LogSetupRequest](https://docs.byteplus.com/en/docs/90/21183#logsetuprequest) |No |\- |The logging option information for the cluster.<br><br><br>* An empty array indicates that no logging options are enabled.<br><br>* When logging is enabled for the first time, a log topic is generated automatically.<br><br>* When multiple logging options are provided, `LogType` cannot be repeated. |
|LogProjectId |String |No |b68324a0\-2680\-48c7\*\*\*\*\*\*\*\* |ID of the log project for the cluster.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">It cannot be an empty string.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If <code>LogProjectId</code> is not specified during cluster creation, the system will automatically create a new log project.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">A log project automatically created by the system has a name in the format <code>k8s-log-{clusterId}-{6 random characters}</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If <code>LogSetups.Enabled</code> is set to <code>false</code>, no log project will be automatically created.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When updating the cluster configuration, if <code>LogProjectId</code> already points to a log project, it cannot be set to an empty value.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">In a cluster configuration update, if the cluster does not have any log configuration, and only <code>LogProjectId</code> is provided while <code>LogSetups</code> is empty, <code>LogProjectId</code> will be ignored.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Updating <code>LogProjectId</code> will create a topic for each log that is enabled.</div><br> |


<span id="logsetuprequest"></span>
### LogSetupRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|LogTtl |Integer |No |30 |Log retention duration in TLS. Logs that exceed the specified retention duration in this log topic will be automatically cleared.<br><br><br>* Valid values: 1 to 3650.<br><br>* Unit: days.<br><br>* Default value: 30 days.<br><br>   A value of 3650 indicates permanent storage. |
|Enabled |Boolean |No |false |Specify whether to enable this log option. Valid values:<br><br><br>* **false**: (Default) Disable it.<br><br>* **true**: Enable it.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">In a cluster configuration update, if <code>LogType</code> is <code>Audit</code>, modifying <code>Enabled</code> will restart the API server.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When you update the cluster configuration, if the value of <code>Enabled</code> changes from <code>false</code> to <code>true</code>, a new log topic will be created.</div><br> |
|LogType |String |Yes |Audit |The type of enabled logs. Valid values:<br><br><br>* **Audit**: cluster audit logging<br><br>* **KubeApiServer**: kube\-apiserver add\-on log<br><br>* **KubeScheduler**: kube\-scheduler add\-on log<br><br>* **KubeControllerManager**: kube\-controller\-manager add\-on log<br><br>* **Etcd**: etcd add\-on log<br><br>* **ClusterAutoscaler**: cluster\-autoscaler add\-on log |


<span id="clusterkubernetesconfigrequest"></span>
### ClusterKubernetesConfigRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|CustomSans |Array of String |No |["abc.com","192.168.0.10"] |Custom certificate SAN (Subject Alternative Name), i.e., the ability to customize domain names or IPs in certificates. Supports entering custom IPs, domain names, or URIs that comply with the specifications. Separate multiple configurations with half\-width commas (`,`), the Enter key, or spaces.<br><br>Supports up to 6 custom SAN entries in the certificate. |
|ClusterDomain |String |No |cluster.local |Cluster local domain name. A domain name consists of two or more parts separated by dots (`.`). Each part supports only lowercase letters, digits, and hyphens (\-), and must start and end with a lowercase letter or digit. The maximum length is 57 characters.<br><br>If you do not specify a local domain name for the cluster, it defaults to `cluster.local`. |
|AdvancedConfig |Object of [AdvancedConfig](https://docs.byteplus.com/en/docs/90/21183#advancedconfig) |No |\- |API Server advanced configuration. |
|ControlPlaneConfig |Object of [KubernetesComponentConfigs](https://docs.byteplus.com/en/docs/90/21183#kubernetescomponentconfigs) |No |\- |The custom parameter configuration for Kubernetes core add\-ons. |


<span id="advancedconfig"></span>
### AdvancedConfig


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|InternalDnsEnabled |Boolean |No |true |Whether to enable private domain access to the API Server for the cluster:<br><br><br>* **true**: (Default) Enabled. Node\-side components access the API Server via the private domain.<br><br>* **false**: Disable it.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When a new cluster is created, API Server private domain name access is enabled by default and is the only supported option. Disabling it is not supported, meaning that setting it to <code>false</code> will not take effect.</div><br> |


<span id="kubernetescomponentconfigs"></span>
### KubernetesComponentConfigs


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|KubeApiServerConfig |Object of [KubeApiServerConfig](https://docs.byteplus.com/en/docs/90/21183#kubeapiserverconfig) |No |\- |The custom parameter configuration for the kube\-apiserver add\-on. |


<span id="kubeapiserverconfig"></span>
### KubeApiServerConfig


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|AdmissionPlugins |Object of [AdmissionPlugins](https://docs.byteplus.com/en/docs/90/21183#admissionplugins) |No |\- |The list of admission control add\-ons additionally enabled in kube\-apiserver beyond those enabled by default. |


<span id="admissionplugins"></span>
### AdmissionPlugins


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|AlwaysPullImages |Boolean |No |true |Whether to enable the AlwaysPullImages admission control add\-on. Valid values:<br><br><br>* **true**: Enable it. This indicates that images are forcibly pulled again whenever a Pod is modified.<br><br>* **false**: (Default) Disable it. |


<span id="clustermonitoringconfigrequest"></span>
### ClusterMonitoringConfigRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|WorkspaceId |String |Yes |a72bxxxx\-83xx\-4axx\*\*\*\*\*\*\*\* |The ID of the VMP workspace used for cluster monitoring.<br><br>You can obtain the workspace ID by calling the [VMP API](https://docs.byteplus.com/en/docs/vmp/ListWorkspaces). |
|ComponentConfigs |Array of [ClusterMonitoringComponentConfigRequest](https://docs.byteplus.com/en/docs/90/21183#clustermonitoringcomponentconfigrequest) |No |\- |The control plane monitoring configuration. |


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
|StartTime |String |No |20:00:00Z |The start time of automatic O&M. It must follow the standard Golang time format and use a 24\-hour clock. Valid values are whole hours from 00 to 23. Examples: 01:00:00Z and 14:00:00Z.<br><br>If this parameter is not configured, the default value is 16:00:00Z (UTC). This corresponds to 00:00:00 the next day in Beijing Time (UTC+8).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter can only be set to UTC. If you need to use another time zone, you need to manually convert the time to UTC.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The <code>ExemptStartDate</code> and <code>ExemptEndDate</code> parameters use Beijing Time (UTC+8) as their default time zone. When the preceding parameters are specified together with this parameter, ensure time zone consistency.</div><br> |
|TaskConfigs |Array of [WindowTaskConfig](https://docs.byteplus.com/en/docs/90/21183#windowtaskconfig) |No |\- |The configurations of the automatic O&M task.<br><br>If this parameter is not specified, the system by default only executes **cluster control plane daily O&M** tasks and does not execute other O&M tasks. |
|WeeklyCycle |Array of String |No |["Monday","Tuesday"] |The automatic O&M cycle. Valid values:<br><br><br>* **Monday**<br><br>* **Tuesday**<br><br>* **Wednesday**<br><br>* **Thursday**<br><br>* **Friday**<br><br>* **Saturday**<br><br>* **Sunday**<br><br><br>If this parameter is not specified, the system performs O&M tasks every day by default. |
|ExemptEndDate |String |No |20260704 |The end time of the automatic O&M exemption window, which is in the format of `YYYYMMDD`, and calculated by calendar day in Beijing Time (UTC+8). For example, if the value is set to `20260704`, it indicates that automatic O&M tasks will no longer be executed by 23:59:59 on that date.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This date must be later than the date configured for <code>ExemptStartDate</code>, and the difference between the two dates must not exceed 60 days.</div><br> |
|ExemptStartDate |String |No |20260702 |The start time of the automatic O&M exemption window, which is in the format of `YYYYMMDD`, and calculated by calendar days in Beijing Time (UTC+8). For example, if the value is set to `20260702`, it indicates that automatic O&M tasks will no longer be executed from 00:00:00 on that date.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This date must be earlier than the date configured for <code>ExemptEndDate</code>, and the difference between the two dates must not exceed 60 days.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">In scenarios such as business\-critical periods or network lockdowns, you can configure an exemption window to prohibit the system from performing automatic O&M operations.</div><br> |


<span id="windowtaskconfig"></span>
### WindowTaskConfig


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Group |String |Yes |Cluster |The group of automatic O&M tasks. Valid values:<br><br><br>* **Cluster**: Control plane O&M.<br><br>* **Addon**: Data plane O&M. |
|Action |String |Yes |AutoUpgradeAddonVersion |The automatic O&M task. Valid values:<br><br><br>* **AutoUpgradeClusterMinorVersion**: A task that automatically upgrades cluster patch versions. This task can be configured only if `Group` is set to `Cluster`.<br><br>* **AutoUpgradeAddonVersion**: A task that automatically upgrades add\-on versions.<br><br>   * This task can be configured only if `Group` is set to `Addon`.<br><br>   * When you configure this task, you also need to use `Targets` to specify the add\-ons to be upgraded. |
|Targets |Array of String |No |["metrics\-server","cluster\-autoscaler"] |Specify the add\-on for which automatic version upgrade is performed. You can specify multiple add\-ons, which are separated by commas (`,`).<br><br>The following add\-ons are supported: cluster\-autoscaler, metrics\-server, log\-collector, event\-collector, node\-problem\-detector, metrics\-collector, and prometheus\-agent.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">For the introduction and description of the preceding add\-ons, see <a href="https://docs.byteplus.com/en/docs/vke/Add-on-overview">Add\-on overview</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Currently, only some add\-ons support automatic upgrades. To upgrade other add\-ons, manually upgrade them on the "Addons" page. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on">Upgrading add\-ons</a>.</div><br> |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vke.cn-beijing.byteplusapi.com.cn?Action=CreateCluster&Version=2022-05-12 HTTP/1.1
Content-Type:application/json
{
    "Name": "flannel-test",
    "Description": "",
    "DeleteProtectionEnabled": false,
    "ClusterConfig": {
        "SubnetIds": [
            "subnet-3rf6vwbif****"
        ]
    },
    "PodsConfig": {
        "PodNetworkMode": "Flannel",
        "FlannelConfig": {
            "MaxPodsPerNode": 32,
            "PodCidrs": [
                "172.17.**.**/19"
            ]
        }
    },
    "ServicesConfig": {
        "ServiceCidrsv4": [
            "172.25.**.**/17"
        ]
    },
    "Tags": [
        {
            "Key": "key",
            "Value": "value"
        }
    ],
    "KubernetesVersion": "1.36",
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


```json
POST https://vke.cn-beijing.byteplusapi.com.cn?Action=CreateCluster&Version=2022-05-12
Content-Type: application/json
{
    "Name": "vpc-cni-test",
    "Description": "xxxx",
    "DeleteProtectionEnabled": false,
    "ClusterConfig": {
        "SubnetIds": [
            "subnet-3rf6vwbif****"
        ],
        "ApiServerPublicAccessEnabled": true,
        "ResourcePublicAccessDefaultEnabled": true
    },
    "PodsConfig": {
        "PodNetworkMode": "VpcCniShared",
        "VpcCniConfig": {
            "SubnetIds": [
                "subnet-2d6tcundc****"
            ]
        }
    },
    "ServicesConfig": {
        "ServiceCidrsv4": [
            "172.17.**.**/21"
        ]
    },
    "Tags": [
        {
            "Key": "key",
            "Value": "value"
        }
    ],
    "KubernetesVersion": "1.36",
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

The following table contains the response parameters of this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Id |String |cc5si\*\*\*\*\*\* |Cluster ID. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1 200 OK
Content-Type:application/json

{
    "ResponseMetadata": {
        "RequestId": "021635330********",
        "Action": "CreateCluster",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {
        "Id": "cc5si******"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The error codes for this API are listed in the table below. For public error codes, see [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes).


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |Insufficient.Balance |Your account has run out of balance. |The balance of the current account is insufficient. Top up your account and try again. |
|400 |QuotaExceeded.Cluster |The number of clusters has reached the limit. |The number of clusters in the current region has reached the quota limit. For more information about product limits, see [Usage limits](https://docs.byteplus.com/en/docs/vke/Limits). You can create clusters in other regions, or [submit a ticket](https://console.byteplus.com/ticket/createTicketV2/?step=2&Service=vke) to apply for a quota increase. |
|400 |VpcMismatch.{{parameter}} |The specified {{resourceType}} {{resourceId}} is not in the same VPC. |The specified subnet IDs do not belong to the same VPC. Specify the parameter and try again. |
|400 |OutOfRange.{{cidrParameter}} |The range of specified CIDR is too small. |The range of the CIDR block is too small, which affects the number of Pods. Plan the CIDR block appropriately and try again. |
|400 |InvalidRange.{{parameter}} |The range of specified CIDR addresses is in conflict with that of CIDR/Subnet in the cluster or in conflict with that of CIDR/Subnet of another cluster or NOT in the valid CIDR ranges. |The CIDR address range is invalid. Check the parameter and try again. |
|400 |OperationDenied.VpcStatus |The status of the specified VPC {{vpcId}} is not valid. |The current status of the specified VPC does not support this action. Confirm the VPC status that this API depends on and try again. You can query VPC status by calling [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs). |
|409 |Conflict.Name |The specified name conflicts with existing {{resourceType}}. |A resource with the same name exists in the specified region. Update the resource name and try again. |
|400 |QuotaExceeded.{{ResourceType}} |The quota of {{ResourceType}} has reached the limit. |The quota for the specified resource (such as EIP, LogProject, and LogTopic) has reached the upper limit. Increase the relevant resource quota or delete unused resources. When the available quota is sufficient, try again later. |
|400 |NotSupported.{{parameter}} |The specified {{resourceType}} {{resourceContent}} is not supported. |The specified parameter (such as KubernetesVersion or SubnetId) is not supported. Check the parameter value and try again. |
|400 |Insufficient.SubnetIp |The IP of subnet {{subnetId}} is insufficient. |The available IP addresses in the specified subnet are insufficient. Please specify a compliant subnet and try again later. |
|400 |LimitExceeded.ClusterSubnetZones |You have reached the limit of the number of cluster subnet zones that you can add. |The number of availability zones of subnets in the cluster exceeds the limit. Make sure that the availability zones of subnets do not exceed three. |
|400 |LimitExceeded.ClusterSubnetsOfZone |You have reached the limit of the number of cluster subnets in zone {{zone}} that you can add. |The number of specified subnets in a single availability zone exceeds the limit. Make sure that the number of specified subnets in each availability zone does not exceed 2. |
