---
title: "API release notes"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Change-history"
---

This topic describes changes to VKE APIs after their official release.

<span id="57w60ZnF"></span>
## October 2026


|API |Release date |Change record |Associated features |
|---|---|---|---|
|[CreateKubernetesObservability](https://docs.byteplus.com/en/docs/vke/CreateKubernetesObservability?lang=en) |2026\-10\-08 |Adds the cluster observability API. |Cluster observability |
|[ListKubernetesObservability](https://docs.byteplus.com/en/docs/vke/ListKubernetesObservability?lang=en) ||||


<span id="GOLD4m3c"></span>
## September 2026


|API |Release date |Change record |Associated features |
|---|---|---|---|
|[UpdateNodePoolNodesConfig](https://docs.byteplus.com/en/docs/vke/UpdateNodePoolNodesConfig?lang=en) |2026\-09\-25 |Adds the node configuration update API. |Node pool management. |
|[CreateNodePool](https://docs.byteplus.com/en/docs/vke/CreateNodePool?lang=en) ||* Adds the **PodPidsLimit**, **ImageMaximumGcAge**, and **ImageMinimumGcAge** Parameters in the **NodePoolKubeletConfig** structure.<br><br>* Adds the **UseLocalImagePull**, **MaxConcurrentUnpacks**, **MaxConcurrentDownloads**, and **ConcurrentLayerFetchBuffer** Parameters in the **NodePoolContainerdConfig** structure. |Node pool management. |
|[UpdateNodePoolConfig](https://docs.byteplus.com/en/docs/vke/UpdateNodePoolConfig?lang=en) ||||
|[ListNodePools](https://docs.byteplus.com/en/docs/vke/ListNodePools?lang=en) ||||
|[CreateAddon](https://docs.byteplus.com/en/docs/vke/CreateAddon?lang=en) ||Updates the parameter descriptions and examples for the p2p\-accelerator add\-on. |Add\-on management |
|[CreateNodes](https://docs.byteplus.com/en/docs/vke/CreateNodes?lang=en) |September 10, 2026 |Adds the **ContainerStorageMountPoint** parameter. |Node management |
|[DeleteNodes](https://docs.byteplus.com/en/docs/vke/DeleteNodes?lang=en) |September 10, 2026 |Adds the **Drain** parameter. |Node management |
|[CreateDiagnosticTask](https://docs.byteplus.com/en/docs/vke/CreateDiagnosticTask?lang=en) |September 9, 2026 |Adds inspection and diagnosis APIs. |Inspection and diagnosis |
|[ListDiagnosticTask](https://docs.byteplus.com/en/docs/vke/ListDiagnosticTask?lang=en) ||||
|[ListDiagnosticTaskResults](https://docs.byteplus.com/en/docs/vke/ListDiagnosticTaskResults?lang=en) ||||
|[CreateInspectionPolicy](https://docs.byteplus.com/en/docs/vke/CreateInspectionPolicy?lang=en) ||||
|[ListInspectionPolicies](https://docs.byteplus.com/en/docs/vke/ListInspectionPolicies?lang=en) ||||
|[UpdateInspectionPolicy](https://docs.byteplus.com/en/docs/vke/UpdateInspectionPolicy?lang=en) ||||
|[DeleteInspectionPolicy](https://docs.byteplus.com/en/docs/vke/DeleteInspectionPolicy?lang=en) ||||
|[CreateRemedyRule](https://docs.byteplus.com/en/docs/vke/CreateRemedyRule?lang=en) ||||
|[UpdateRemedyRule](https://docs.byteplus.com/en/docs/vke/UpdateRemedyRule?lang=en) ||||
|[DeleteRemedyRule](https://docs.byteplus.com/en/docs/vke/DeleteRemedyRule?lang=en) ||||
|[UpdateClusterVersion](https://docs.byteplus.com/en/docs/vke/UpdateClusterVersion) |September 1, 2026 |Adds the cluster upgrade API. |Cluster upgrade management. |
|[UpgradeNodePools](https://docs.byteplus.com/en/docs/vke/UpgradeNodePools) ||||
|[UpdateTask](https://docs.byteplus.com/en/docs/vke/UpdateTask) |September 1, 2026 |New task management APIs are available. |Task management. |
|[ListTasks](https://docs.byteplus.com/en/docs/vke/ListTasks) ||||


<span id="As8Zztgy"></span>
## August 2026


|API |Release date |Change record |Associated features |
|---|---|---|---|
|[CreateNodePool](https://docs.byteplus.com/en/docs/vke/CreateNodePool) |August 31, 2026 |* The **NodePoolKubeletConfig** structure contains the following new parameters: **FailSwapOn**, **ImageGcLowThresholdPercent**, and **ImageGcHighThresholdPercent**.<br><br>* Adds **SpotWithPriceLimit** to the values of the SpotStrategy parameter in the **NodePoolNodeConfigRequest** structure.<br><br>* The **NodePoolNodeConfigRequest** structure contains a new parameter: **SpotPriceLimits**.<br><br>* The **DataVolume** structure contains the following new parameters: **KmsKeyId** and **Encrypted**.<br><br>* The **InstanceTypeSpotPriceLimit** parameter and its sub\-parameters are added. |Node pool management. |
|[UpdateNodePoolConfig](https://docs.byteplus.com/en/docs/vke/UpdateNodePoolConfig) ||||
|[ListNodePools](https://docs.byteplus.com/en/docs/vke/ListNodePools) ||||
|[UpdateKubernetesObservabilityComponentConfigs](https://docs.byteplus.com/en/docs/vke/UpdateKubernetesObservabilityComponentConfigs?lang=en) |August 25, 2026 |Adds a cloud\-native observability management API. |Add\-on management |


<span id="DcAvXPob"></span>
## July 2026


|API |Release date |Change record |Associated features |
|---|---|---|---|
|[CreateCluster](https://docs.byteplus.com/en/docs/vke/CreateCluster) |July 30, 2026 |The **MaintenanceWindowConfig** parameter and its sub\-parameters are added. |Cluster O&M management |
|[UpdateNodePoolConfig](https://docs.byteplus.com/en/docs/vke/UpdateNodePoolConfig) ||||
|[ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) ||||
|[CreateNodePool](https://docs.byteplus.com/en/docs/vke/CreateNodePool) |July 21, 2026 |* Adds the **BurstEnabled** parameter under the **SystemVolume** structure.<br><br>* Adds the **BurstEnabled** parameter under the **DataVolume** structure. |Node pool management. |
|[UpdateNodePoolConfig](https://docs.byteplus.com/en/docs/vke/UpdateNodePoolConfig) ||||
|[ListNodePools](https://docs.byteplus.com/en/docs/vke/ListNodePools) ||||
|[CreateCluster](https://docs.byteplus.com/en/docs/vke/CreateCluster) |July 17, 2026 |Adds the **KubernetesConfig** parameter and its sub\-parameters. |Cluster control plane management |
|[UpdateNodePoolConfig](https://docs.byteplus.com/en/docs/vke/UpdateNodePoolConfig) ||||
|[ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) |July 17, 2026 |* Adds the **KubernetesConfig** parameter and its sub\-parameters.<br><br>* Adds the **Values** parameter under the **Tags** structure. |Cluster control plane management |
|[CreateAddon](https://docs.byteplus.com/en/docs/vke/CreateAddon) |July 2, 2026 |Adds the description of the configuration file for the **cr\-signature\-verifier** add\-on. |Add\-on management |
|[ScaleNodePool](https://docs.byteplus.com/en/docs/vke/ScaleNodePool) |July 2, 2026 |Adds this API. |Node pool management. |
|[CreateNodePool](https://docs.byteplus.com/en/docs/vke/CreateNodePool) |July 2, 2026 |* Adds the **GpuDriverConfig** parameter.<br><br>* Deprecates the **GpuDriverVersion** parameter. |Node pool management. |
|[UpdateNodePoolConfig](https://docs.byteplus.com/en/docs/vke/UpdateNodePoolConfig) ||||
|[CreateNodes](https://docs.byteplus.com/en/docs/vke/CreateNodes) ||||


<span id="VIXYBD5A"></span>
## May 2026


|API |Release date |Change record |Associated features |
|---|---|---|---|
|[CreateNodePool](https://docs.byteplus.com/en/docs/vke/CreateNodePool) |May 28, 2026 |Adds the **BandwidthPackageId** parameter. |Node pool management. |
|[UpdateNodePoolConfig](https://docs.byteplus.com/en/docs/vke/UpdateNodePoolConfig) ||||
|[ListNodePools](https://docs.byteplus.com/en/docs/vke/ListNodePools) ||||
|[CreateScalingPolicy](https://docs.byteplus.com/en/docs/vke/CreateScalingPolicy) |May 26, 2026 |Adds the **Name** parameter. |Node pool management. |
|[UpdateScalingPolicy](https://docs.byteplus.com/en/docs/vke/UpdateScalingPolicy) |May 26, 2026 |||
|[ListScalingPolicies](https://docs.byteplus.com/en/docs/vke/ListScalingPolicies) |May 26, 2026 |||
|[CreateNodePool](https://docs.byteplus.com/en/docs/vke/CreateNodePool) |May 6, 2026 |* Adds the **Runtime** parameter and its sub\-parameters.<br><br>* Adds the **AffinityGroupConfig** parameter and its sub\-parameters.<br><br>* Adds the **ExtraPerformanceIops**, **ExtraPerformanceTypeId**, and **ExtraPerformanceThroughputMb** parameters under the **DataVolume** structure. |* Node runtime management<br><br>* Node pool and node affinity group management |
|[UpdateNodePoolConfig](https://docs.byteplus.com/en/docs/vke/UpdateNodePoolConfig) ||||
|[ListNodePools](https://docs.byteplus.com/en/docs/vke/ListNodePools) ||||
|[CreateDefaultNodePool](https://docs.byteplus.com/en/docs/vke/CreateDefaultNodePool) |May 6, 2026 |Adds the **Runtime** parameter and its sub\-parameters. |Node runtime management |
|[CreateNodes](https://docs.byteplus.com/en/docs/vke/CreateNodes) |May 6, 2026 |Adds the **AffinityGroupConfig** parameter and its sub\-parameters. |Node pool and node affinity group management |
|[ListNodes](https://docs.byteplus.com/en/docs/vke/ListNodes) ||||
|[DeleteNodes](https://docs.byteplus.com/en/docs/vke/DeleteNodes) ||||
|[ListSupportedImages](https://docs.byteplus.com/en/docs/vke/ListSupportedImages) |May 6, 2026 |Adds the **Intersection** and **KubernetesVersion** parameters. |Image management by instance type |


<span id="446mjisu"></span>
## April 2026


|API |Release date |Change record |Associated features |
|---|---|---|---|
|[CreateNodePool](https://docs.byteplus.com/en/docs/vke/CreateNodePool) |April 3, 2026 |Updates the description of the **HpcClusterIds** parameter. |Node pool management. |
|[UpdateNodePoolConfig](https://docs.byteplus.com/en/docs/vke/UpdateNodePoolConfig) ||||


<span id="1EqvrFWS"></span>
## February 2026


|API |Release date |Change record |Associated features |
|---|---|---|---|
|[ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) |February 27, 2026 |Adds the **VciSubnetIds** parameter. |Cluster management |
|[UpdateClusterConfig](https://docs.byteplus.com/en/docs/vke/UpdateClusterConfig) ||||


<span id="DBYEbZPO"></span>
## January 2026


|API |Release date |Change record |Associated features |
|---|---|---|---|
|[CreateNodePool](https://docs.byteplus.com/en/docs/vke/CreateNodePool) |January 18, 2025 |Adds the **GpuDriverVersion** parameter. |Node pool management. |
|[UpdateNodePoolConfig](https://docs.byteplus.com/en/docs/vke/UpdateNodePoolConfig) ||||
|[ListNodePools](https://docs.byteplus.com/en/docs/vke/ListNodePools) ||||
|[CreateNodes](https://docs.byteplus.com/en/docs/vke/CreateNodes) ||||
|[ListSupportedGpuDriverVersions](https://docs.byteplus.com/en/docs/vke/ListSupportedGpuDriverVersions) |January 18, 2025 |Adds an API to obtain the list of GPU driver versions supported for image installation. |Node pool management. |
|[CreateNodePool](https://docs.byteplus.com/en/docs/vke/CreateNodePool) |January 8, 2025 |Adds the `LOCAL_SSD`, `LOCAL_HDD`, `LOCAL_LVM_SSD`, and `LOCAL_SSD_SRIOV`**** values under the **DataVolume.Type** structure. |Node pool management. |
|[UpdateNodePoolConfig](https://docs.byteplus.com/en/docs/vke/UpdateNodePoolConfig) ||||
|[ListNodePools](https://docs.byteplus.com/en/docs/vke/ListNodePools) |January 8, 2025 |* Adds the `LOCAL_SSD`, `LOCAL_HDD`, `LOCAL_LVM_SSD`, and `LOCAL_SSD_SRIOV`**** values under the **DataVolume.Type** structure.<br><br>* Adds the `ScalingFailed` value to the **Conditions.Type** parameter. |Node pool management. |
|[CreateNodes](https://docs.byteplus.com/en/docs/vke/CreateNodes) |January 8, 2025 |Adds the **SkipReplaceSystem** parameter. |Node management |
|[CreateAddon](https://docs.byteplus.com/en/docs/vke/CreateAddon) |January 8, 2025 |The configurations of the **cluster\-autoscaler** add\-on are updated. The **MaxNodeProvisionTime**, **ScaleDown.IgnoreDaemonSetsUtilizationEnabled**, and **ScaleDown.ScaleDownDelayTypeLocalEnabled** parameters are added. |Add\-on management |


<span id="CpuOQr2e"></span>
## December 2025


|API |Release date |Change record |Associated features |
|---|---|---|---|
|[CreateNodePool](https://docs.byteplus.com/en/docs/vke/CreateNodePool) |December 2, 2025 |* Adds the **ContainerdConfig** parameter and its sub\-parameters.<br><br>* Adds the `Ultra_Disk` and `TSSD_TL0` values under the **SystemVolume.Type** structure.<br><br>* Adds the `Ultra_Disk` and `TSSD_TL0` values under the **DataVolume.Type** structure.<br><br>* The following error codes are deleted:<br><br>   * `InstanceChargeTypeMismatch.PublicAccessEnabled`<br><br>   * `SpotStrategyMismatch.PublicAccessEnabled` |Node pool management. |
|[UpdateNodePoolConfig](https://docs.byteplus.com/en/docs/vke/UpdateNodePoolConfig) |December 2, 2025 |* Adds the **ContainerdConfig** parameter and its sub\-parameters.<br><br>* Adds the `Ultra_Disk` and `TSSD_TL0` values under the **SystemVolume.Type** structure.<br><br>* Adds the `Ultra_Disk` and `TSSD_TL0` values under the **DataVolume.Type** structure.<br><br>* The description of the **NodeConfigForUpdate.InstanceChargeType** parameter is updated. Subscription node pools now support automatic EIP binding to nodes. Related limit descriptions are deleted.<br><br>* The following error codes are deleted:<br><br>   * `InstanceChargeTypeMismatch.PublicAccessEnabled`<br><br>   * `SpotStrategyMismatch.PublicAccessEnabled` ||
|[ListNodePools](https://docs.byteplus.com/en/docs/vke/ListNodePools) |December 2, 2025 |Adds the **ContainerdConfig** parameter and its sub\-parameters. ||
|[ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) |December 2, 2025 |The following valid values are added to the **Conditions.Type** parameter under **ClusterStatusFilter** and **ClusterStatusCondition**:<br><br><br>* `UpdatingCluster`<br><br>* `SyncingAddon`<br><br>* `SyncingNode`<br><br>* `SyncingNodePool` |Cluster management |


<span id="EK7zkhBO"></span>
## November 2025


|API |Release date |Change record |Associated features |
|---|---|---|---|
|[CreateNodePool](https://docs.byteplus.com/en/docs/vke/CreateNodePool) |November 30, 2025 |Adds the `RSSD_PL0` value for the **DataVolume.Type** parameter, which allows you to configure remote elastic disks with performance level PL0 for data volumes during the creation or update of node pools. |Node pool management. |
|[UpdateNodePoolConfig](https://docs.byteplus.com/en/docs/vke/UpdateNodePoolConfig) ||||
|[UpdateClusterConfig](https://docs.byteplus.com/en/docs/vke/UpdateClusterConfig) |November 26, 2025 |Adds the **EnableMetricsExternalCollection** parameter, which allows you to enable the custom collection feature for cluster control plane add\-ons. |Cluster management |
|[UpdateClusterConfig](https://docs.byteplus.com/en/docs/vke/UpdateClusterConfig) |November 18, 2025 |* Adds the **ResourcePublicAccessDefaultEnabled** parameter, which allows you to disable cluster public access.<br><br>* Adds the **MonitoringConfig** parameter, which allows you to configure cluster monitoring. |Cluster management |
|[CreateNodePool](https://docs.byteplus.com/en/docs/vke/CreateNodePool) |November 4, 2025 |Adds the `InstanceChargeTypeMismatch.AutoScalingEnabled` error code. |Node pool management |
|[UpdateNodePoolConfig](https://docs.byteplus.com/en/docs/vke/UpdateNodePoolConfig) ||* Adds the **InstanceChargeType** parameter.<br><br>* The following two error codes are added:<br><br>   * `InstanceChargeTypeMismatch.AutoScalingEnabled`<br><br>   * `InstanceChargeTypeMismatch.SpotStrategy` ||
|[ListSupportedImages](https://docs.byteplus.com/en/docs/vke/ListSupportedImages) |November 4, 2025 |Adds the API for managing images supported by ECS instance types. |Management of node pool specifications and images |
|[ListInstanceTypeLabels](https://docs.byteplus.com/en/docs/vke/ListInstanceTypeLabels) ||||
|[ListSupportedAddInstanceTypes](https://docs.byteplus.com/en/docs/vke/ListSupportedAddInstanceTypes) ||||


<span id="QLty0Idy"></span>
## October 2025


|API |Release date |Change record |Associated features |
|---|---|---|---|
|[CreateNodePool](https://docs.byteplus.com/en/docs/vke/CreateNodePool) |October 22, 2025 |The **Management** parameter and its sub\-parameters are added, which allow you to configure the managed node pool. |Managed node pool |
|[UpdateNodePoolConfig](https://docs.byteplus.com/en/docs/vke/UpdateNodePoolConfig) ||||
|[ListNodePools](https://docs.byteplus.com/en/docs/vke/ListNodePools) ||||
|[CreateScalingPolicy](https://docs.byteplus.com/en/docs/vke/CreateScalingPolicy) |October 21, 2025 |APIs related to node pool elastic scheduled scaling rules are added. |Elastic scheduled scaling of node pools |
|[UpdateScalingPolicy](https://docs.byteplus.com/en/docs/vke/UpdateScalingPolicy) ||||
|[ListScalingPolicies](https://docs.byteplus.com/en/docs/vke/ListScalingPolicies) ||||
|[DeleteScalingPolicies](https://docs.byteplus.com/en/docs/vke/DeleteScalingPolicies) ||||
|[CreateCluster](https://docs.byteplus.com/en/docs/vke/CreateCluster) |October 17, 2025 |* The **LogType** parameter supports the following values:<br><br>   * Etcd<br><br>   * ClusterAutoscaler |Cluster log configuration |
|[UpdateClusterConfig](https://docs.byteplus.com/en/docs/vke/UpdateClusterConfig) ||* The **LogType** parameter supports the following values:<br><br>   * Etcd<br><br>   * ClusterAutoscaler<br><br>* The request parameters now include the **IrsaEnabled** parameter. |* Cluster log configuration<br><br>* IRSA can be enabled for clusters. |


<span id="EKkuprfT"></span>
## July 2025


|API |Release date |Change record |Associated features |
|---|---|---|---|
|[CreateNodePool](https://docs.byteplus.com/en/docs/vke/CreateNodePool) |July 30, 2025 |The following fields are added under the **NodePoolKubeletConfig** structure:<br><br><br>* Adds the `MaxPods` field, which is used to specify the maximum number of pods supported by a node.<br><br>* Adds the `KubeApiQps` and `KubeApiBurst` fields to configure the number of requests sent to the API server per second and the burst request threshold.<br><br>* Adds the `EvictionHard` field, which is used to configure a set of hard eviction thresholds that trigger pod eviction.<br><br>* Adds the `KubeReserved` and `SystemReserved` fields, which are used to configure resources reserved for the Kubernetes system and add\-ons on nodes.<br><br>* The `RegistryPullQps` and `RegistryBurst` fields are added to configure the QPS and burst thresholds for pulling images from image registries.<br><br>* Adds the `SerializeImagePulls` field, which is used to specify whether to serially pull images.<br><br>* Adds the `CpuManagerPolicy` field, which is used to configure a CPU manager policy. |Configuration of node kubelet parameters |
|[UpdateNodePoolConfig](https://docs.byteplus.com/en/docs/vke/UpdateNodePoolConfig) ||||
|[ListNodePools](https://docs.byteplus.com/en/docs/vke/ListNodePools) ||||


<span id=".XzIwMjTlubQxMuaciA=="></span>
## December 2024


|API |Release date |Change record |Associated features |
|---|---|---|---|
|[GrantPermission](https://docs.byteplus.com/en/docs/vke/GrantPermission) |December 3, 2024 |APIs related to RBAC access policy management are added. |VKE supports configuring RBAC permissions for IAM users and IAM roles. |
|[ListPermissions](https://docs.byteplus.com/en/docs/vke/ListPermissions) ||||
|[RevokePermission](https://docs.byteplus.com/en/docs/vke/RevokePermission) ||||


<span id=".XzIwMjTlubQxMeaciA=="></span>
## November 2024


|API |Release date |Change record |Associated features |
|---|---|---|---|
|[CreateImageCache](https://docs.byteplus.com/en/docs/vke/CreateImageCache) |November 25, 2024 |Adds the **RegistryHostnameResolvNameservers** parameter. |Image caches support custom DNS. |
|[UpdateImageCache](https://docs.byteplus.com/en/docs/vke/UpdateImageCache) ||||


<span id=".XzIwMjTlubQwN-aciA=="></span>
## July 2024


|API |Release date |Change record |Associated features |
|---|---|---|---|
|[CreateNodes](https://docs.byteplus.com/en/docs/vke/CreateNodes) |July 30, 2024 |Updates the description of the **NodePoolId** parameter. You can retain the original ECS instance names when you add existing nodes. |The original ECS instance names can be retained when you add existing nodes. |


<span id=".XzIwMjTlubQwMeaciA=="></span>
## January 2024


|API |Release date |Change record |Associated features |
|---|---|---|---|
|[CreateCluster](https://docs.byteplus.com/en/docs/vke/CreateCluster) |January 19, 2024 |Adds the error codes **Insufficient.SubnetIp**, **LimitExceeded.ClusterSubnetZones**, and **LimitExceeded.ClusterSubnetsOfZone**. |Clusters support modifying the API server subnet. |
|[UpdateClusterConfig](https://docs.byteplus.com/en/docs/vke/UpdateClusterConfig) ||* Adds the **SubnetIds** field under the **ClusterConfig** structure.<br><br>* Adds the error codes **Insufficient.SubnetIp**, **LimitExceeded.ClusterSubnetZones**, and **LimitExceeded.ClusterSubnetsOfZone**. ||
|[CreateNodePool](https://docs.byteplus.com/en/docs/vke/CreateNodePool) |January 19, 2024 |Adds the **NamePrefix** field under the **KubernetesConfig** structure. |Custom metadata name prefix |
|[ListNodePools](https://docs.byteplus.com/en/docs/vke/ListNodePools) ||||
|[ListKubeconfigs](https://docs.byteplus.com/en/docs/vke/ListKubeconfigs) |January 19, 2024 |Adds the **RoleIds** field under the **Filter** parameter. |Cluster RBAC permissions can be granted to IAM roles. |
|[CreateAddon](https://docs.byteplus.com/en/docs/vke/CreateAddon) |January 19, 2024 |Updates the configurations of the **cluster\-autoscaler** add\-on and adds the **ScaleDownGpuUtilizationThreshold** parameter. |CA supports configuring the GPU scale\-in threshold. |


<span id=".XzIwMjPlubQxMuaciA=="></span>
## December 2023


|API |Release date |Change record |Associated features |
|---|---|---|---|
|[DeleteCluster](https://docs.byteplus.com/en/docs/vke/DeleteCluster) |December 18, 2023 |Adds the **RetainResources** parameter, and deprecates the **CascadingDeleteResources** parameter. |API operations related to cluster resources are optimized or removed. |
|[DeleteNodePool](https://docs.byteplus.com/en/docs/vke/DeleteNodePool) ||||
|[DeleteNodes](https://docs.byteplus.com/en/docs/vke/DeleteNodes) ||||
|[DeleteAddon](https://docs.byteplus.com/en/docs/vke/DeleteAddon) ||||
|[CreateAddon](https://docs.byteplus.com/en/docs/vke/CreateAddon) |December 1, 2023 |The configurations of the **prometheus\-agent** add\-on and the **nvidia\-device\-plugin** add\-on are updated. |Optimization of add\-on parameter names |


<span id=".XzIwMjPlubQxMeaciA=="></span>
## November 2023


|API |Release date |Change record |Associated features |
|---|---|---|---|
|[CreateAddon](https://docs.byteplus.com/en/docs/vke/CreateAddon) |November 9, 2023 |Updated the configurations of the **mgpu**, **p2p\-accelerator**, and **prometheus\-adapter** add\-ons. |Optimization of add\-on parameter names |


<span id=".XzIwMjPlubQxMOaciA=="></span>
## October 2023


|API |Release date |Change record |Associated features |
|---|---|---|---|
|[CreateNodes](https://docs.byteplus.com/en/docs/vke/CreateNodes) |October 30, 2023 |Adds the error code **OperationDenied.NodePoolReplicas**. |Optimization of service API capabilities |
|[DeleteNodes](https://docs.byteplus.com/en/docs/vke/DeleteNodes) ||||


<span id=".XzIwMjPlubQwNeaciA=="></span>
## May 2023


|API |Release date |Change record |Associated features |
|---|---|---|---|
|[CreateNodePool](https://docs.byteplus.com/en/docs/vke/CreateNodePool) |May 6, 2023 |Adds the error code **ClusterVersionMismatch.ImageId**. |Node images for some instance types support the veLinux CentOS\-compatible operating system. |
|[UpdateNodePoolConfig](https://docs.byteplus.com/en/docs/vke/UpdateNodePoolConfig) ||||
|[CreateNodes](https://docs.byteplus.com/en/docs/vke/CreateNodes) ||||
|[CreateAddon](https://docs.byteplus.com/en/docs/vke/CreateAddon) ||The configurations of the **prometheus\-agent** add\-on are updated. |Optimization of code related to add\-ons |


<span id=".XzIwMjPlubQwNOaciA=="></span>
## April 2023


|API |Release date |Change record |Associated features |
|---|---|---|---|
|[API overview](https://docs.byteplus.com/en/docs/vke/List-of-API-actions) |April 30, 2023 |The API documentation for VKE is officially released. |Official release of the documentation |
