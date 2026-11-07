---
title: "API overview"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/List-of-API-actions"
---

VKE provides the following APIs.

<span id=".6ZuG576k"></span>
## Clusters


|API |Description |
|---|---|
|[CreateCluster](https://docs.byteplus.com/en/docs/vke/CreateCluster) |Create a cluster. |
|[ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) |Obtain the list and details of clusters. |
|[UpdateClusterConfig](https://docs.byteplus.com/en/docs/vke/UpdateClusterConfig) |Update cluster configurations. |
|[ListSupportedResourceTypes](https://docs.byteplus.com/en/docs/vke/ListSupportedResourceTypes) |Obtain the resource types supported by a cluster. |
|[DeleteCluster](https://docs.byteplus.com/en/docs/vke/DeleteCluster) |Delete a cluster. |
|[CreateKubeconfig](https://docs.byteplus.com/en/docs/vke/CreateKubeconfig) |Generate the Kubeconfig credentials for a cluster. |
|[ListKubeconfigs](https://docs.byteplus.com/en/docs/vke/ListKubeconfigs) |Query the list of Kubeconfig details for clusters that meet the specified criteria. |
|[DeleteKubeconfigs](https://docs.byteplus.com/en/docs/vke/DeleteKubeconfigs) |Revoke the Kubeconfig credentials of a cluster. |
|[UpdateClusterVersion](https://docs.byteplus.com/en/docs/vke/UpdateClusterVersion) |Upgrade the cluster control plane. |
|[UpgradeNodePools](https://docs.byteplus.com/en/docs/vke/UpgradeNodePools) |Upgrade the cluster data plane. |


<span id=".6IqC54K55rGg"></span>
## Node pools


|API |Description |
|---|---|
|[CreateNodePool](https://docs.byteplus.com/en/docs/vke/CreateNodePool) |Create a node pool. |
|[CreateDefaultNodePool](https://docs.byteplus.com/en/docs/vke/CreateDefaultNodePool) |Create a default node pool. |
|[UpdateNodePoolConfig](https://docs.byteplus.com/en/docs/vke/UpdateNodePoolConfig) |Update node pool configurations. |
|[UpdateNodePoolNodesConfig](https://docs.byteplus.com/en/docs/vke/UpdateNodePoolNodesConfig) |Update node configurations for node pools. |
|[ListNodePools](https://docs.byteplus.com/en/docs/vke/ListNodePools) |Query the list and details of node pools. |
|[DeleteNodePool](https://docs.byteplus.com/en/docs/vke/DeleteNodePool) |Delete a node pool. |
|[ScaleNodePool](https://docs.byteplus.com/en/docs/vke/ScaleNodePool) |Scale out the specified node pool. |
|[CreateScalingPolicy](https://docs.byteplus.com/en/docs/vke/CreateScalingPolicy) |Create an elastic scheduled scaling policy for a node pool. |
|[UpdateScalingPolicy](https://docs.byteplus.com/en/docs/vke/UpdateScalingPolicy) |Update an elastic scheduled scaling policy for a node pool. |
|[ListScalingPolicies](https://docs.byteplus.com/en/docs/vke/ListScalingPolicies) |Query the list of elastic scheduled scaling rules for node pools. |
|[DeleteScalingPolicies](https://docs.byteplus.com/en/docs/vke/DeleteScalingPolicies) |Delete elastic scheduled scaling rules for a node pool. |


<span id=".6IqC54K5"></span>
## Nodes


|API |Description |
|---|---|
|[CreateNodes](https://docs.byteplus.com/en/docs/vke/CreateNodes) |Add a node. |
|[ListNodes](https://docs.byteplus.com/en/docs/vke/ListNodes) |Obtain the list and details of nodes. |
|[DeleteNodes](https://docs.byteplus.com/en/docs/vke/DeleteNodes) |Remove a node. |


<span id="QucXSl32"></span>
## Virtual nodes

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default"><a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features">[Beta \- apply for trial</a>]: APIs related to virtual nodes are <strong>in beta</strong>. To use these APIs, submit an application.</div>



|API |Description |
|---|---|
|[CreateVirtualNode](https://docs.byteplus.com/en/docs/vke/CreateVirtualNode) |Create a virtual node. |
|[ListVirtualNodes](https://docs.byteplus.com/en/docs/vke/ListVirtualNodes) |Query the list and details of virtual nodes that meet the specified criteria. |
|[DeleteVirtualNode](https://docs.byteplus.com/en/docs/vke/DeleteVirtualNode) |Delete a specified virtual node. |


<span id=".57uE5Lu2"></span>
## Add\-ons


|API |Description |
|---|---|
|[ListSupportedAddons](https://docs.byteplus.com/en/docs/vke/ListSupportedAddons) |View details of add\-ons supported by VKE. |
|[CreateAddon](https://docs.byteplus.com/en/docs/vke/CreateAddon) |Install add\-ons for a specified cluster. |
|[UpdateAddonConfig](https://docs.byteplus.com/en/docs/vke/UpdateAddonConfig) |Update the configurations of a specified add\-on in a specified cluster. |
|[UpdateAddonVersion](https://docs.byteplus.com/en/docs/vke/UpdateAddonVersion) |Update the version of a specified add\-on in a specified cluster. |
|[DeleteAddon](https://docs.byteplus.com/en/docs/vke/DeleteAddon) |Remove a specified add\-on from a specified cluster. |
|[ListAddons](https://docs.byteplus.com/en/docs/vke/ListAddons) |Query the details of installed add\-ons that meet the criteria. |


<span id=".5qCH562-"></span>
## Tags


|API |Description |
|---|---|
|[TagResources](https://docs.byteplus.com/en/docs/vke/TagResources) |Add a tag to a specified resource. |
|[UntagResources](https://docs.byteplus.com/en/docs/vke/UntagResources) |Remove a tag from a resource. |
|[ListTagsForResources](https://docs.byteplus.com/en/docs/vke/ListTagsForResources) |List all tags for resources that meet the specified conditions. |


<span id="zEGKHfJD"></span>
## Access policy


|API |Description |
|---|---|
|[GrantPermission](https://docs.byteplus.com/en/docs/vke/GrantPermission) |Grant RBAC access permissions to an IAM user or role. |
|[ListPermissions](https://docs.byteplus.com/en/docs/vke/ListPermissions) |Query RBAC access policy resource information that meets the conditions. |
|[RevokePermission](https://docs.byteplus.com/en/docs/vke/RevokePermission) |Revoke the RBAC permission granted to an IAM user or role by specifying the resource ID of the permission policy. |


<span id="izcv7SiM"></span>
## Management of supported images for instance specifications


|API |Description |
|---|---|
|[ListSupportedImages](https://docs.byteplus.com/en/docs/vke/ListSupportedImages) |Obtain the list of images supported by ECS instance specifications that correspond to nodes. |
|[ListInstanceTypeLabels](https://docs.byteplus.com/en/docs/vke/ListInstanceTypeLabels) |Obtain the list of labels supported by ECS instance specifications that correspond to nodes. |
|[ListSupportedGpuDriverVersions](https://docs.byteplus.com/en/docs/vke/ListSupportedGpuDriverVersions) |Obtain a list of GPU driver versions supported by the image. |
|[ListSupportedAddInstanceTypes](https://docs.byteplus.com/en/docs/vke/ListSupportedAddInstanceTypes) |Obtain the list of specifications that can be added to VKE nodes within the current account. |


<span id="QCDtt78K"></span>
## Cloud native observability


|API |Description |
|---|---|
|[UpdateKubernetesObservabilityComponentConfigs](https://docs.byteplus.com/en/docs/vke/UpdateKubernetesObservabilityComponentConfigs?lang=en) |Enable basic observability capabilities of cloud\-native observability for the specified service. |


<span id="WUfMhhuS"></span>
## Job


|API |Description |
|---|---|
|[UpdateTask](https://docs.byteplus.com/en/docs/vke/UpdateTask) |Update a task. |
|[ListTasks](https://docs.byteplus.com/en/docs/vke/ListTasks) |Query tasks. |


<span id="zTJVKmR1"></span>
## VCI image cache


|API |Description |
|---|---|
|[CreateImageCache](https://docs.byteplus.com/en/docs/vke/CreateImageCache) |Create an image cache. |
|[UpdateImageCache](https://docs.byteplus.com/en/docs/vke/UpdateImageCache) |Update an image cache. |
|[ListImageCaches](https://docs.byteplus.com/en/docs/vke/ListImageCaches) |Query the list of image caches that meet the specified criteria. |
|[DeleteImageCache](https://docs.byteplus.com/en/docs/vke/DeleteImageCache) |Delete a specified image cache. |
|[UpdateImageCacheRetentionDays](https://docs.byteplus.com/en/docs/vke/UpdateImageCacheRetentionDays) |Update the expiration time of multiple image caches at the same time. |


<span id="KPKHE0pq"></span>
## Inspection and diagnosis


|API |Description |
|---|---|
|[CreateDiagnosticTask](https://docs.byteplus.com/en/docs/vke/CreateDiagnosticTask?lang=en) |Create an inspection and diagnostic task. |
|[ListDiagnosticTask](https://docs.byteplus.com/en/docs/vke/ListDiagnosticTask?lang=en) |Query diagnostic tasks. |
|[ListDiagnosticTaskResults](https://docs.byteplus.com/en/docs/vke/ListDiagnosticTaskResults?lang=en) |Query the results of a diagnostic task. |
|[CreateInspectionPolicy](https://docs.byteplus.com/en/docs/vke/CreateInspectionPolicy?lang=en) |Create an inspection policy. |
|[ListInspectionPolicies](https://docs.byteplus.com/en/docs/vke/ListInspectionPolicies?lang=en) |Query the inspection policy list. |
|[UpdateInspectionPolicy](https://docs.byteplus.com/en/docs/vke/UpdateInspectionPolicy?lang=en) |Update the configuration of an inspection policy. |
|[DeleteInspectionPolicy](https://docs.byteplus.com/en/docs/vke/DeleteInspectionPolicy?lang=en) |Delete an inspection policy. |
|[CreateRemedyRule](https://docs.byteplus.com/en/docs/vke/CreateRemedyRule?lang=en) |Creates a check and self\-healing rule. |
|[UpdateRemedyRule](https://docs.byteplus.com/en/docs/vke/UpdateRemedyRule?lang=en) |Update the configuration of the check and self\-healing rule. |
|[DeleteRemedyRule](https://docs.byteplus.com/en/docs/vke/DeleteRemedyRule?lang=en) |Delete a check and self\-healing rule. |


<span id="CuIMe3xX"></span>
## Cluster observability


|API |Description |
|---|---|
|[CreateKubernetesObservability](https://docs.byteplus.com/en/docs/vke/CreateKubernetesObservability?lang=en) |Enable basic observability for a cluster. |
|[ListKubernetesObservability](https://docs.byteplus.com/en/docs/vke/ListKubernetesObservability?lang=en) |Query whether basic observability is enabled for a cluster. |
