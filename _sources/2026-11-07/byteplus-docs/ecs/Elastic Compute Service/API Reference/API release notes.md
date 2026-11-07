---
title: "API release notes"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/API-release-notes"
---

This topic describes OpenAPI updates for ECS.

<span id="6QShpYbA"></span>
## September 2026


|API |Change record |Associated feature |Release regions |
|---|---|---|---|
|[DescribeInstanceTypes](https://docs.byteplus.com/en/docs/ecs/DescribeInstanceTypes) |Added response parameter:<br><br><br>* Added the VrdmaCrossS2BandwidthMbps parameter to the Network structure |Instance |All |
|[DescribeImages](https://docs.byteplus.com/en/docs/ecs/DescribeImages) |Added request parameter: LifecycleStatus.N |Image ||


<span id="AP2HA245"></span>
## August 2026


|API |Change record |Associated feature |Release regions |
|---|---|---|---|
|[RunInstances](https://docs.byteplus.com/en/docs/ecs/RunInstances)<br><br>[ModifyInstanceAttribute](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceAttribute?lang=en) |Added new error code: OperationDenied.EnableJumboFrameForceDisabled. |Instance |All |
|[DescribeImages](https://docs.byteplus.com/en/docs/ecs/DescribeImages) |Added response parameter: The LifecycleStatus parameter is added to the Image structure. |Image ||


<span id="B7HvzvZE"></span>
## July 2026


|API |Change record |Associated feature |Release regions |
|---|---|---|---|
|[RunInstances](https://docs.byteplus.com/en/docs/ecs/RunInstances) |Added request parameter:<br><br><br>* EnablePrimaryInterfaceHighBandwidthType |Instance |All |
|[DescribeImages](https://docs.byteplus.com/en/docs/ecs/DescribeImages) |Added response parameter: The MarketplacelmageBillType parameter is added to the Image structure. |Image ||


<span id="PfyV5LcD"></span>
## May 2026


|API |Change record |Associated feature |Release regions |
|---|---|---|---|
|[RunInstances](https://docs.byteplus.com/en/docs/ecs/RunInstances) |Modified error messages for the error codes:<br><br><br>* InvalidEipAddressChargeType.Malformed<br><br>* InvalidHttpTokens.Malformed<br><br>* InvalidImageForConfidentialComputing.UnSupported<br><br>* InvalidInstanceTypeForConfidentialComputing.NotSupported<br><br>* LimitExceeded.MaximumEipBandwidth<br><br>* LimitExceeded.MinimumEipBandwidth<br><br>* QuotaExceeded.MaximumEipAddresses<br><br>* InvalidNetworkInterfacesVpc.Conflict<br><br>* InvalidAffinityGroupSize.CountMismatch<br><br>* InvalidAffinityGroupSize.DeploymentSetIdMismatch<br><br>* InvalidAffinityGroupSize.MinCountMismatch<br><br>* InvalidSecurityProtectionInstance.SpecMismatch |Instance |All |
|[CreateScheduledInstances](https://docs.byteplus.com/en/docs/ecs/CreateScheduledInstances) |Modified descriptions for the error codes:<br><br><br>* InvalidEipAddressChargeType.Malformed<br><br>* LimitExceeded.MaximumEipBandwidth<br><br>* LimitExceeded.MinimumEipBandwidth<br><br>* InvalidNetworkInterfacesVpc.Conflict<br><br>* InvalidSecurityProtectionInstance.SpecMismatch |||
|[StopInstance](https://docs.byteplus.com/en/docs/ecs/StopInstance?lang=en) |Modified descriptions for the error codes:<br><br><br>* InvalidStoppedMode.ChargeTypeMismatch<br><br>* InvalidStoppedMode.InstanceTypeMismatch |||
|[StopInstances](https://docs.byteplus.com/en/docs/ecs/StopInstances?lang=en) |Modified descriptions for the error codes:<br><br><br>* InvalidStoppedMode.ChargeTypeMismatch<br><br>* InvalidStoppedMode.InstanceTypeMismatch |||
|[ModifyInstanceVpcAttribute](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceVpcAttribute?lang=en) |The description of the error code "InvalidInstance.DependenceAnycastEipExit" is modified. |||
|[ModifyInstanceMetadataOptions](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceMetadataOptions?lang=en) |The description of the error code "InvalidHttpTokens.Malformed" is modified. |||
|[CreatImage](https://docs.byteplus.com/en/docs/ecs/CreateImage) |Modified descriptions for the error codes:<br><br><br>* InvalidSnapshotIdOrSnapshotGroupIdForCreateImage.UnSupported<br><br>* LimitExceeded.MaximumSystemVolumeSize |Image ||
|[CopyImage](https://docs.byteplus.com/en/docs/ecs/CopyImage) |The description of the error code "LimitExceeded.MaximumImageSize" is modified. |||
|[ImportImage](https://docs.byteplus.com/en/docs/ecs/ImportImage) |The description of the error code "LimitExceeded.MaximumImageSize" is modified. |||


&nbsp;

<span id="kRNGI1nK"></span>
## April 2026


|API |Change record |Associated feature |Release regions |
|---|---|---|---|
|[RunInstances](https://docs.byteplus.com/en/docs/ecs/RunInstances) |Added error codes: OperationDenied.NotSupportPaypal, OperationDenied.MainAccountNotSupportPaypal. |Instance |All |
|[DescribeUserData](https://docs.byteplus.com/en/docs/ecs/DescribeUserData) |Added request and response parameters: ScheduledInstanceId. |||


<span id="oo4Ekdqa"></span>
## March 2026


|API |Change record |Associated feature |Release regions |
|---|---|---|---|
|[RunInstances](https://docs.byteplus.com/en/docs/ecs/RunInstances) |Added request parameter: NetworkOptions.EnableJumboFrame |Instance |All |
|[DescribeUserData](https://docs.byteplus.com/en/docs/ecs/DescribeUserData) |Added request and response parameters: ScheduledInstanceId. |||
|[DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) |Added response parameter: IsSupportJumboFrame. |||
|[DescribeInstanceTypes](https://docs.byteplus.com/en/docs/ecs/DescribeInstanceTypes) ||||
|[ModifyInstanceAttribute](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceAttribute) |Added request parameter: EnableJumboFrame. |||


<span id="YmQyGz2g"></span>
## January 2026


|API |Change record |Associated feature |Release regions |
|---|---|---|---|
|* [CreateScheduledInstances](https://docs.byteplus.com/en/docs/ecs/CreateScheduledInstances)<br><br>* [DescribeScheduledInstances](https://docs.byteplus.com/en/docs/ecs/DescribeScheduledInstances)<br><br>* [DeleteScheduledInstance](https://docs.byteplus.com/en/docs/ecs/DeleteScheduledInstance)<br><br>* [DescribeScheduledInstanceStock](https://docs.byteplus.com/en/docs/ecs/DescribeScheduledInstanceStock) |First released online. |Instance |All |
|[ModifyInstanceChargeType](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceChargeType) |Added new error code: QuotaExceeded.MaximumVolumes. |||
|[StartInstance](https://docs.byteplus.com/en/docs/ecs/StartInstance) |Added new error code: InvalidActionOrVersion. |||
|[ModifyInstanceAttribute](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceAttribute) |The description of the request parameter EnableJumboFrame is changed. |||


<span id="lWC5zsDJ"></span>
## December 2025


|API |Change record |Associated feature |Release regions |
|---|---|---|---|
|[ModifyImageSharePermission](https://docs.byteplus.com/en/docs/ecs/ModifyImageSharePermission) |Added new error code: InvalidImageSharePermissionForRemove.UnSupported. |Image |All |
|[ReplaceSystemVolume](https://docs.byteplus.com/en/docs/ecs/ReplaceSystemVolume) |The description of the error code "InvalidInstance.RequestForbidden" is modified. |||
|[CopyImage](https://docs.byteplus.com/en/docs/ecs/CopyImage) |Added new error code: InvalidImageStatus. |||
|[RunInstances](http://volcengine.com/docs/6396/1431709) |The description of the error code "RequestForbidden" is modified. |Instance ||
|[ModifyInstanceChargeType](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceChargeType) |The description of the error code "InvalidInstance.RequestForbidden" is modified. |||
|[ModifyInstanceAttribute](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceAttribute) ||||
|[RebootInstances](https://docs.byteplus.com/en/docs/ecs/RebootInstances) ||||
|[RebootInstance](https://docs.byteplus.com/en/docs/ecs/RebootInstance) ||||
|[ModifyInstanceSpec](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceSpec) ||||
|[RenewInstance](https://docs.byteplus.com/en/docs/ecs/RenewInstance) ||||
|[StartInstance](https://docs.byteplus.com/en/docs/ecs/StartInstance) ||||
|[StartInstances](https://docs.byteplus.com/en/docs/ecs/StartInstances) ||||


<span id="xdS2oywk"></span>
## November 2025


|API |Change record |Associated feature |Release regions |
|---|---|---|---|
|[RunInstances](https://docs.byteplus.com/en/docs/ecs/RunInstances) |Added new error codes: OperationDenied.AccountCountryAreaInvalid, OperationDenied.AccountDeleted, OperationDenied.AccountTaxNoInvalid, OperationDenied.NotOpeningQualified, OperationDenied.RiskInterception, InvalidChargeTypeForDeletionProtection.Unsupported, InvalidEnableVrdma.JumboFrameMismatch. |Instance |All |
|[DeleteInstance](https://docs.byteplus.com/en/docs/ecs/DeleteInstance) |Added new error code: InvalidOperation.DeletionProtection. |||
|[DeleteInstances](https://docs.byteplus.com/en/docs/ecs/DeleteInstances) |Added batch operation error code: InvalidOperation.DeletionProtection |||
|[ModifyInstanceAttribute](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceAttribute) |Added a new error code:<br><br>InvalidChargeTypeForDeletionProtection.Unsupported<br><br>InvalidDisableJumboFrame.VrdmaMismatch. |||


<span id="nOyP3xZR"></span>
## September 2025


|API |Change record |Associated feature |Release regions |
|---|---|---|---|
|[CreateHpcCluster](https://docs.byteplus.com/en/docs/ecs/CreateHpcCluster) |Added request parameters: ProjectName, Tags.N.Key, and Tags.N.Value. |HPC cluster |All |
|[DescribeHpcClusters](https://docs.byteplus.com/en/docs/ecs/DescribeHpcClusters) |* Added request parameters: ProjectName, TagFilters.N.Key, and TagFilters.N.Values.N.<br><br>* Added response parameters: ProjectName and Tags. |||
|[ExportImage](https://docs.byteplus.com/en/docs/ecs/ExportImage) |Added new error code: LimitExceeded.TaskConcurrent. |Image ||
|[DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) |Added response parameter: RdmaNetworkInterfaceDetails. |Instance |China (Beijing) |
|[ModifySystemEventDefaultAction](https://docs.byteplus.com/en/docs/ecs/ModifySystemEventDefaultAction_-_Modify_the_default_operations_and_maintenance_actions_for_events) |Added new APIs. |Monitoring |All |
|[DescribeSystemEventDefaultAction](https://docs.byteplus.com/en/docs/ecs/DescribeSystemEventDefaultAction_-_Query_the_default_maintenance_actions_for_events) |Added new APIs. |||


<span id="nOyP3xZR"></span>
## August 2025


|API |Change record |Associated feature |Release regions |
|---|---|---|---|
|[ModifyInstancesSpec](https://docs.byteplus.com/en/docs/ecs/ModifyInstancesSpec) |Added new APIs. |Instance |All |
|[RunInstances](https://docs.byteplus.com/en/docs/ecs/RunInstances) |The request parameter "NetworkOptions.EnableJumboFrame" is added. |||
|[DescribeInstanceTypes](https://docs.byteplus.com/en/docs/ecs/DescribeInstanceTypes) |The response parameter "IsSupportJumboFrame" is added. |||
|[DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) |The response parameter "EnableJumboFrame" is added. |||
|[ModifyInstanceAttribute](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceAttribute) |* The request parameter "EnableJumboFrame" is added.<br><br>* The error code "InvaliDescribeInstancesdEnableJumboFrameForModifyInstanceAttribute.Unsupported" is added. |||
|[CreateLaunchTemplate](https://docs.byteplus.com/en/docs/ecs/CreateLaunchTemplate)<br><br> |Added response parameters: Volumes.N.ExtraPerformanceTypeId, Volumes.N.ExtraPerformanceIOPS, Volumes.N.ExtraPerformanceThroughputMB, and Volumes.N.SnapshotId. All parameters are optional. |Instance launch template |All |
|[CreateLaunchTemplateVersion](https://docs.byteplus.com/en/docs/ecs/CreateLaunchTemplateVersion) |Added response parameters: Volumes.N.ExtraPerformanceTypeId, Volumes.N.ExtraPerformanceIOPS, and Volumes.N.ExtraPerformanceThroughputMB. All parameters are optional. |||
|[DescribeLaunchTemplateVersions](https://docs.byteplus.com/en/docs/ecs/DescribeLaunchTemplateVersions) ||||


<span id="U2mZl0pl"></span>
## July 2025


|API |Change record |Associated feature |Release regions |
|---|---|---|---|
|[RunInstances](https://docs.byteplus.com/en/docs/ecs/RunInstances) |* Added request parameter: HttpTokens.<br><br>* The description of the request parameter "CpuMaxFrequency" is modified.<br><br>* Added new error codes: InvalidHttpTokens.Malformed, InvalidHttpTokensForImage.Unsupported, QuotaExceeded.MaximumEipInterfaceLimit, InvalidExtraPerformanceValue.Malformed, InvalidVolumeKindForExtraPerformance.Unsupported, LimitExceeded.ExtraPerformance, and InvalidVolumeStatus. |Instance |All |
|[AllocateInstances](https://docs.byteplus.com/en/docs/ecs/AllocateInstances) |A new interface (Beta). |||
|[DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) |Added response parameter: MetadataOptions.HttpTokens. |||
|[ModifyInstanceMetadataOptions](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceMetadataOptions) |Added new APIs. |||
|[PurchaseReservedInstances](https://docs.byteplus.com/en/docs/ecs/PurchaseReservedInstances) |Added new error code: InvalidConfiguration.Unsupported. |||
|[DescribeAvailableResource](https://docs.byteplus.com/en/docs/ecs/DescribeAvailableResource) |The description of the response parameter "Status" is modified. |||
|[DescribeAutoInstallPackages](https://docs.byteplus.com/en/docs/ecs/DescribeAutoInstallPackages) |Added new APIs. |Image ||
|[DescribeImages](https://docs.byteplus.com/en/docs/ecs/DescribeImages) |Added response parameter: The `ProductCode` parameter is added to the `Images` structure, which indicates the product code of the marketplace image. |||
|[CopyImage](https://docs.byteplus.com/en/docs/ecs/CopyImage) |Added request parameters: `Tags.N.Key` and `Tags.N.Value`, which indicate the tag key and value of the target image. |||
|[DescribeHpcInstancePosition](https://docs.byteplus.com/en/docs/ecs/DescribeHpcInstancePosition) |Added new APIs. |HPC cluster ||


<span id=".MjAyNOW5tDEy5pyI"></span>
## June 2025


|API |Change record |Associated feature |Release regions |
|---|---|---|---|
|[RunInstances](https://docs.byteplus.com/en/docs/ecs/RunInstances) |Added request parameter: DeletionProtection. |Instance |All |
|[ModifyInstanceAttribute](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceAttribute) |Added request parameter: DeletionProtection. |||
|[DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) |Added response parameters: DeletionProtection and VolumeId. |||
|[ExportImage](https://docs.byteplus.com/en/docs/ecs/ExportImage) |Added new error code: LimitExceeded.ExportImageOneday. |Image ||


<span id=".MjAyNOW5tDEy5pyI"></span>
## April 2025


|API |Change record |Associated feature |Release regions |
|---|---|---|---|
|[RunInstances](https://docs.byteplus.com/en/docs/ecs/RunInstances) |* The request parameter "AffinityGroupSize" (optional, Beta) is added.<br><br>* The value range of the request parameter "DeploymentSetGroupNumber" is updated.<br><br>* Added new error codes: InvalidInstanceTypeForAffinityGroupSize.Unsupported, InvalidInstanceTypeForNonAffinityGroup.Unsupported, InvalidSecurityGroupStatus, QuotaExceeded.MaximumEipAddresses, InvalidAffinityGroupSize.CountMismatch, InvalidAffinityGroupSize.DeploymentSetIdMismatch, InvalidAffinityGroupSize.MinCountMismatch, and InvalidInstanceChargeType.AffinityGroupSizeMismatch.<br><br>* The description of the error code "OperationDenied.TrafficModeNotAuthorized" is updated. |Instance |All |
|[DeleteInstance](https://docs.byteplus.com/en/docs/ecs/DeleteInstance)<br><br>[RenewInstance](https://docs.byteplus.com/en/docs/ecs/RenewInstance)<br><br>[DeleteInstances](https://docs.byteplus.com/en/docs/ecs/DeleteInstances) |Added new error code: OperationDenied.AffinityGroupInstance.<br><br> |||
|[StopInstance](https://docs.byteplus.com/en/docs/ecs/StopInstance) |Added new error code: InvalidStoppedModeForAffinityGroupInstance.Unsupported. |||
|[StopInstances](https://docs.byteplus.com/en/docs/ecs/StopInstances) |Updated response parameter: "InvalidStoppedModeForAffinityGroupInstance.Unsupported" is added to the Error structure. |||
|[DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) |* Added request parameter (optional): AffinityGroupIds.N. Updated request parameter: DeploymentSetGroupNumbers.<br><br>* The response parameter "AffinityGroupId" is added.<br><br>* The error code "LimitExceeded.MaximumAffinityGroupIds" is added. |||
|[DescribeInstanceTypes](https://docs.byteplus.com/en/docs/ecs/DescribeInstanceTypes) |Added response parameters: AffinityGroupSizes and IsSupportAffinityGroup. RdmaProductName is added to the RDMA structure. |||
|[ModifyInstanceChargeType](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceChargeType) |Added new error codes: InvalidAffinityGroupInstanceForModifyInstanceChargeType.Unsupported, and OperationDenied.AffinityGroupInstance. |||
|[ModifyInstanceSpec](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceSpec) |Added new error code: InvalidAffinityGroupInstanceForModifyInstanceSpec.Unsupported. |||
|[ImportImage](https://docs.byteplus.com/en/docs/ecs/ImportImage) |Added request parameter:<br><br>ImportDataVolumes.N.DataVolumeUrl, optional.<br><br>Added a new error code:<br><br>400, LimitExceeded.MaximumImportDataVolumes |Image ||
|[CreateDeploymentSet](https://docs.byteplus.com/en/docs/ecs/CreateDeploymentSet) |The values of GroupCount and Granularity are updated. |Deployment set ||
|[DescribeDeploymentSets](https://docs.byteplus.com/en/docs/ecs/DescribeDeploymentSets) |The Granularity description is updated. |||
|[ModifyInstanceDeployment](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceDeployment) |The value range of DeploymentSetGroupNumber is updated. |||
|[DescribeHpcClusters](https://docs.byteplus.com/en/docs/ecs/DescribeHpcClusters) |The request parameter "AccountId" is deleted. |HPC cluster ||
|[CreateLaunchTemplate](https://docs.byteplus.com/en/docs/ecs/CreateLaunchTemplate) |Added request parameters (both optional): LaunchTemplateTags.N.Key and LaunchTemplateTags.N.Value. |Launch template ||
|[DescribeLaunchTemplates](https://docs.byteplus.com/en/docs/ecs/DescribeLaunchTemplates) |Added response parameter: LaunchTemplateTags. |||


<span id=".MjAyNOW5tDEy5pyI"></span>
## February 2025


|API |Change record |Associated feature |Release regions |
|---|---|---|---|
|[RunInstances](https://docs.byteplus.com/en/docs/ecs/RunInstances) |* Added request parameter (optional, Beta): CpuMaxFrequency.<br><br>* Added new error codes: InvalidNetworkInterfaceType, InvalidSubnetStatus, LimitExceeded.MaximumHighPerformanceNetworkInterfaces, and OperationDenied.TrafficModeNotAuthorized. |Instance |All |
|[DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) |Added response parameter: SecurityGroupIds. |||
|[ModifyInstanceSpec](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceSpec) |Added new error code: LimitExceeded.MaximumHighPerformanceNetworkInterfaces. |||
|[PurchaseReservedInstances](https://docs.byteplus.com/en/docs/ecs/PurchaseReservedInstances) |* Added request parameters: EffectiveAt, RscAutoRenew, RscAutoRenewPeriod, ReservedStorageCapacityName, ReservedCapacity, and VolumeType.<br><br>* Added response parameter: ReservedStorageCapacityId.<br><br>* Added new error codes: InvalidReservedStorageCapacityName.Malformed, InvalidVolumeType.Malformed, LimitExceeded.ReservedCapacitySize, and OperationDenied.ReservedStorageCapacityNotAvailable. |||
|[CreateTags](https://docs.byteplus.com/en/docs/ecs/CreateTags)<br><br>[ListTagsForResources](https://docs.byteplus.com/en/docs/ecs/ListTagsForResources) |* Modified request parameter: ResourceIds.N is optional.<br><br>* Added new error code: MissingParameter.ResourceType. |Tag ||
|[CreateLaunchTemplate](https://docs.byteplus.com/en/docs/ecs/CreateLaunchTemplate)<br><br>[CreateLaunchTemplateVersion](https://docs.byteplus.com/en/docs/ecs/CreateLaunchTemplateVersion) |Added request parameter: Eip.ReleaseWithInstance. Optional. |Instance launch template ||
|[DescribeLaunchTemplateVersions](https://docs.byteplus.com/en/docs/ecs/DescribeLaunchTemplateVersions) |New response parameter: Eip.ReleaseWithInstance. |||
|[CreateSubscription](https://docs.byteplus.com/en/docs/ecs/CreateSubscription)<br><br>[ModifySubscriptionEventTypes](https://docs.byteplus.com/en/docs/ecs/ModifySubscriptionEventTypes) |* Added enumeration values of the request parameter "EventTypes.N": InstanceFileSystemFailure.StopAndRepair:Succeeded, InstanceFileSystemFailure.StopAndRepair:Failed, ElasticScheduledInstance.Create, MemoryRiskDetected:Succeeded, DiskError.ReplaceDisk:Succeeded, SystemFailure.Redeploy:Failed, SystemMaintenance.Redeploy:Failed<br><br>* Naming optimizations of the following enumeration values for the request parameter "EventTypes.N": DiskError.Redeploy, SystemFailure.Redeploy, SystemMaintenance.Redeploy, InstanceFailure |Event monitoring ||
|[DescribeSystemEvents](https://docs.byteplus.com/en/docs/ecs/DescribeSystemEvents)<br><br>[DescribeEventTypes](https://docs.byteplus.com/en/docs/ecs/DescribeEventTypes) |* Added enumeration values for request parameter Types.N: InstanceFileSystemFailure_StopAndRepair, ElasticScheduledInstance, MemoryRiskDetected, SystemFailure_Repair, SystemMaintenance_StopAndRepair.<br><br>* Naming optimizations of the following enumeration values for the request parameter "Types.N": SystemFailure, DiskError_Redeploy, SystemMaintenance, InstanceFailure |||
|[CreateHpcCluster](https://docs.byteplus.com/en/docs/ecs/CreateHpcCluster)<br><br>[DeleteHpcCluster](https://docs.byteplus.com/en/docs/ecs/DeleteHpcCluster)<br><br>[DescribeHpcClusters](https://docs.byteplus.com/en/docs/ecs/DescribeHpcClusters) |Added new APIs. |HPC cluster ||


<span id=".MjAyNOW5tDEy5pyI"></span>
## December 2024


|API |Change record |Associated feature |
|---|---|---|
|[CreateLaunchTemplate](https://docs.byteplus.com/en/docs/ecs/CreateLaunchTemplate) |Added request parameter (optional): LaunchTemplateProjectName. |Launch template |
|[DescribeLaunchTemplates](https://docs.byteplus.com/en/docs/ecs/DescribeLaunchTemplates) |* Added request parameter (optional): LaunchTemplateProjectName.<br><br>* Added response parameter: LaunchTemplateProjectName. ||
|[TagResources](https://docs.byteplus.com/en/docs/ecs/TagResources)<br><br>[UntagResources](https://docs.byteplus.com/en/docs/ecs/UntagResources)<br><br>[ListTagsForResources](https://docs.byteplus.com/en/docs/ecs/ListTagsForResources) |Added new APIs. |Tag |


<span id=".MjAyNOW5tDEx5pyI"></span>
## November 2024


|API |Change record |Associated feature |
|---|---|---|
|[RunInstances](https://docs.byteplus.com/en/docs/ecs/RunInstances) |Added request parameter:<br><br>`ImageReleaseVersion` (optional), which indicates the specific version of the public image to be used. |Instance |
|[DescribeInstanceTypes](https://docs.byteplus.com/en/docs/ecs/DescribeInstanceTypes) |The request parameter `InstanceTypeIds.N` is modified, with the length limit of N increased from 10 to 100. ||
|[CreateTags](https://docs.byteplus.com/en/docs/ecs/CreateTags)<br><br>[DeleteTags](https://docs.byteplus.com/en/docs/ecs/DeleteTags)<br><br>[DescribeTags](https://docs.byteplus.com/en/docs/ecs/DescribeTags) |Modified request parameter: `ResourceType` supports the new value `keypair`. |Tag |
|[ImportKeyPair](https://docs.byteplus.com/en/docs/ecs/ImportKeyPair)<br><br>[CreateKeyPair](https://docs.byteplus.com/en/docs/ecs/CreateKeyPair) |* Added request parameters (optional): `Tags.N.Key` and `Tags.N.Value`, which indicate the tag key and tag value associated with the key pair.<br><br>* Added new error codes: InvalidTagKey.Malformed, InvalidTagValue.Malformed, LimitExceeded.MaximumTags, and InvalidTagKey.Conflict. |Key pair |
|[DescribeKeyPairs](https://docs.byteplus.com/en/docs/ecs/DescribeKeyPairs) |* Added request parameters (optional): `TagFilters.N.Key` and `TagFilters.N.Value`, which are used to search for resources based on tag keys and tag values.<br><br>* Added response parameters: `Key` and `Value` are added to the Tag structure.<br><br>* Added new error codes: InvalidTagFilterKey.Malformed, InvalidTagFilterValue.Malformed, LimitExceeded.MaximumTagFilterKeys, LimitExceeded.MaximumTagFilterResults, LimitExceeded.MaximumTagFilterValues, and InvalidTagFilterKey.Conflict. ||
|[ReplaceSystemVolume](https://docs.byteplus.com/en/docs/ecs/ReplaceSystemVolume) |* Added request parameter:<br><br>   `ImageReleaseVersion` (optional), which indicates the specific version of the public image to be used.<br><br>* Added new error code: LimitExceeded.MaximumVolumes. |Image |
|[DescribeInvocations](https://docs.byteplus.com/en/docs/ecs/DescribeInvocations_-_Query_task_list) |Added request parameter (optional): TagFilters.N.Values.N. |Cloud assistant |
|[DescribeCommands](https://docs.byteplus.com/en/docs/ecs/DescribeCommands_-_Query_the_command_list) |||
|[All interfaces except "UpgradeCloudAssistants" and "UninstallCloudAssistants"](https://docs.byteplus.com/en/docs/ecs/CreateCommand-Creating_a_custom_command) |All currently existing error codes are added. ||


<span id=".MjAyNOW5tDEw5pyI"></span>
## October 2024


|API |Change record |Associated feature |
|---|---|---|
|[RunInstances](https://docs.byteplus.com/en/docs/ecs/RunInstances) |* Added request parameter (Beta, optional): `NetworkInterfaces.N.Ipv6AddressCount`, which indicates the number of IPv6 addresses assigned to the primary network interface.<br><br>* Added new error codes: InvalidIpv6AddressCount.Malformed and InvalidSubnet.DisableIPv6. |Instance |
|[DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) |Added response parameter: `Ipv6Addresses` is added to the `NetworkInterfaces` structure. The response parameter "Ipv6Addresses" indicates the IPv6 address assigned to the network interface. ||


<span id=".MjAyNOW5tDA55pyI"></span>
## September 2024


|API |Change record |Associated feature |
|---|---|---|
|[StopInstance](https://docs.byteplus.com/en/docs/ecs/StopInstance)<br><br>[StopInstances](https://docs.byteplus.com/en/docs/ecs/StopInstances) |The description of the `StoppedMode` parameter is modified. |Instance |
|[ModifyInstanceAttribute](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceAttribute) |The description of the `Password` parameter is modified. ||
|[DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) |* The request parameter `Ipv6Addresses.N` (optional) is added, which indicates the instance IPv6 address.<br><br>* Added new error codes: LimitExceeded.MaximumIpv6Addresses and InvalidActionOrVersion. ||
|[RunInstances](https://docs.byteplus.com/en/docs/ecs/RunInstances) |* Added request parameters (optional): `Volumes.N.ExtraPerformanceIOPS`, `Volumes.N.ExtraPerformanceThroughputMB`, and `Volumes.N.ExtraPerformanceTypeId`. They indicate the extra performance of the volume.<br><br>* Added new error codes:<br><br>   * IPv6\-related: InvalidIPv6OnlySubnet.Unsupported, InvalidSubnetImage.Mismatch, InvalidIpv6OnlyNetworkInterfaceAndIpv4NetworkInterface.Mismatch.<br><br>   * Quota and authentication\-related: QuotaExceeded.MaximumGeneralCpus, QuotaExceeded.MaximumGpuBasicNums, QuotaExceeded.MaximumHighPerformanceGpus, QuotaExceeded.MaximumLocalVolumeCpus, QuotaExceeded.MaximumReservedInstanceGeneralCpus, QuotaExceeded.MaximumReservedInstanceGpuBasicNums, QuotaExceeded.MaximumReservedInstanceHighPerformanceGpus, QuotaExceeded.MaximumReservedInstanceLocalVolumeCpus, NotPaymentQualified.<br><br>   * Extra performance\-related: InvalidExtraPerformanceTypeId.Malformed, InvalidSystemVolumeForExtraPerformance.Unsupported, InvalidVolumeSizeForExtraPerformance.Unsupported, InvalidVolumeTypeForExtraPerformance.Unsupported, LimitExceeded.ExtraPerformanceThroughput, LimitExceeded.MaximumExtraPerformanceIOPS, LimitExceeded.MaximumExtraPerformanceThroughputMB, LimitExceeded.MinimumExtraPerformanceIOPS, LimitExceeded.MinimumExtraPerformanceThroughputMB. ||
|[StartInstance](https://docs.byteplus.com/en/docs/ecs/StartInstance) |Added new error codes: OperationDenied.InstanceIsSnapshotRollback and InvalidActionOrVersion. ||
|[DescribeInstanceTypes](https://docs.byteplus.com/en/docs/ecs/DescribeInstanceTypes) |Added new error code: InvalidActionOrVersion. ||
|[ModifyInstanceChargeType](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceChargeType) |Added new error codes: QuotaExceeded.MaximumGeneralCpus, QuotaExceeded.MaximumGpuBasicNums, QuotaExceeded.MaximumHighPerformanceGpus, QuotaExceeded.MaximumLocalVolumeCpus, QuotaExceeded.MaximumReservedInstanceGeneralCpus, QuotaExceeded.MaximumReservedInstanceGpuBasicNums, QuotaExceeded.MaximumReservedInstanceHighPerformanceGpus, QuotaExceeded.MaximumReservedInstanceLocalVolumeCpus, and DryRunOperation. ||
|[ModifyInstanceSpec](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceSpec) |Added new error codes: QuotaExceeded.MaximumGeneralCpus, QuotaExceeded.MaximumGpuBasicNums, QuotaExceeded.MaximumHighPerformanceGpus, QuotaExceeded.MaximumLocalVolumeCpus, QuotaExceeded.MaximumReservedInstanceGeneralCpus, QuotaExceeded.MaximumReservedInstanceGpuBasicNums, QuotaExceeded.MaximumReservedInstanceHighPerformanceGpus, and QuotaExceeded.MaximumReservedInstanceLocalVolumeCpus. ||
|[ModifyReservedInstances](https://docs.byteplus.com/en/docs/ecs/ModifyReservedInstances)<br><br>[PurchaseReservedInstances](https://docs.byteplus.com/en/docs/ecs/PurchaseReservedInstances) |* Added request parameter (optional): `Description`, which indicates RI descriptions.<br><br>* Added new error codes: QuotaExceeded.MaximumGeneralCpus, QuotaExceeded.MaximumGpuBasicNums, QuotaExceeded.MaximumHighPerformanceGpus, QuotaExceeded.MaximumLocalVolumeCpus, QuotaExceeded.MaximumReservedInstanceGeneralCpus, QuotaExceeded.MaximumReservedInstanceGpuBasicNums, QuotaExceeded.MaximumReservedInstanceHighPerformanceGpus, QuotaExceeded.MaximumReservedInstanceLocalVolumeCpus, and InvalidInstanceDescription.Malformed. ||
|[DescribeReservedInstances](https://docs.byteplus.com/en/docs/ecs/DescribeReservedInstances) |Added response parameter: `Description`, which indicates the RI description. ||
|[CopyImage](https://docs.byteplus.com/en/docs/ecs/CopyImage) |Added new error code: 412 (OperationDenied.SnapshotServiceUnavailable) |Image |
|[CreateImage](https://docs.byteplus.com/en/docs/ecs/CreateImage) |Added new error code: 400 (LimitExceeded.MaximumSnapshotCount) ||
|[ImportImage](https://docs.byteplus.com/en/docs/ecs/ImportImage) |Added new error code: 412 (OperationDenied.SnapshotServiceUnavailable) ||
|[DescribeImages](https://docs.byteplus.com/en/docs/ecs/DescribeImages) |The following response parameters are added to the "DescribeImageNextTokenResponse.Images" structure:<br><br><br>* `IsInstallRunCommandAgent`, which indicates whether the cloud assistant Agent is installed in the public image.<br><br>* `Kernel`, which indicates the image kernel version. ||


<span id=".MjAyNOW5tDA45pyI"></span>
## August 2024


|API |Release time |Change record |Associated feature |
|---|---|---|---|
|[CreateLaunchTemplate](https://docs.byteplus.com/en/docs/ecs/CreateLaunchTemplate) |August 2024 |Added new APIs. |Instance launch template |
|[CreateLaunchTemplateVersion](https://docs.byteplus.com/en/docs/ecs/CreateLaunchTemplateVersion) ||||
|[DescribeLaunchTemplates](https://docs.byteplus.com/en/docs/ecs/DescribeLaunchTemplates) ||||
|[DescribeLaunchTemplateVersions](https://docs.byteplus.com/en/docs/ecs/DescribeLaunchTemplateVersions) ||||
|[ModifyTemplateDefaultVersion](https://docs.byteplus.com/en/docs/ecs/ModifyTemplateDefaultVersion) ||||
|[DeleteLaunchTemplate](https://docs.byteplus.com/en/docs/ecs/DeleteLaunchTemplate) ||||
|[DeleteLaunchTemplateVersion](https://docs.byteplus.com/en/docs/ecs/DeleteLaunchTemplateVersion) ||||


<span id=".MjAyNOW5tDA35pyI"></span>
## July 2024


|API |Release time |Release record |Associated feature |
|---|---|---|---|
|[RunInstances](https://docs.byteplus.com/en/docs/ecs/RunInstances) |2024\-07\-30 |Added new error codes: LimitExceeded.MaximumSecurityProtectionTypes, OperationDenied.PurchaseLimited, and InvalidTenancy.InstanceTypeIdMismatch. |Instance |
|[ModifyInstanceSpec](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceSpec) ||Added new error codes: LimitExceeded.MaximumVolumes, OperationDenied.InstanceHasUnfinishedOrder, and OperationDenied.InstanceIsSnapshotRollback. ||
|[DeleteInstance](https://docs.byteplus.com/en/docs/ecs/DeleteInstance) ||Added new error code: OperationDenied.InstanceIsSnapshotRollback. ||
|[ModifyInstanceVpcAttribute](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceVpcAttribute) ||Added new error codes: Insufficient.Balance, and OperationDenied.SpecifiedSecurityGroupNotAuthorized. ||
|[ModifyReservedInstances](https://docs.byteplus.com/en/docs/ecs/ModifyReservedInstances) ||Added new error code: InvalidReservedInstance.ProjectMismatch. ||
|[DescribeInstanceTypes](https://docs.byteplus.com/en/docs/ecs/DescribeInstanceTypes) ||* Added request parameter:<br><br>   * `ImageId` parameter, which can be used to query the instance types that can be created based on the image.<br><br>* Added a new error code:<br><br>   * InvalidImage.NotFound. ||
|[DescribeImages](https://docs.byteplus.com/en/docs/ecs/DescribeImages) ||Added response parameter:<br><br>The `LicenseType` parameter is added to the `Images` structure. The "LicenseType" parameter indicates the image license type. |Image |
|[CreateImage](https://docs.byteplus.com/en/docs/ecs/CreateImage) ||* Added request parameter:<br><br>   The `CreateWholeImage` parameter is added, which indicates whether to create the whole image.<br><br>* Added a new error code:<br><br>   400, InvalidVolumeTypeForCreateImage.Unsupported ||
|[ImportImage](https://docs.byteplus.com/en/docs/ecs/ImportImage) ||* Added request parameter:<br><br>   The `LicenseType` parameter is added, which indicates the image license type.<br><br>* Added a new error code:<br><br>   400, InvalidImageFormat.Malformed ||
|[CreateSubscription](https://docs.byteplus.com/en/docs/ecs/CreateSubscription) ||Added value of request parameter:<br><br>Added value of the request parameter `EventTypes.N`: SystemFailure.Stop.Succeeded. This indicates that the instance is stopped successfully due to a system failure. |Event monitoring |
|[ModifySubscriptionEventTypes](https://docs.byteplus.com/en/docs/ecs/ModifySubscriptionEventTypes) ||Added value of request parameter:<br><br>Added value of the request parameter `EventTypes.N`: SystemFailure.Stop.Succeeded. This indicates that the instance is stopped successfully due to a system failure. ||


<span id=".MjAyNOW5tDA15pyI"></span>
## May 2024


|API |Release time |Change record |Associated feature |
|---|---|---|---|
|[RunInstances](https://docs.byteplus.com/en/docs/ecs/RunInstances) |2024\-05\-21 |* Added a new error code:<br><br>   * InvalidBandwidthPackageStatus<br><br>   * QuotaExceeded.BandwidthPackage<br><br>   * RequestForbidden<br><br>   * InvalidISP.BandwidthPackageMismatch<br><br>   * InvalidInstanceTenancy.DeploymentSetIdMismatch<br><br>* Modified error code: The description of InvalidSnapshotStatus is modified to "The status of the specified snapshot does not support this operation". |Instance |
|[StartInstance](https://docs.byteplus.com/en/docs/ecs/StartInstance)<br><br>[StartInstances](https://docs.byteplus.com/en/docs/ecs/StartInstances)<br><br>[RebootInstance](https://docs.byteplus.com/en/docs/ecs/RebootInstance)<br><br>[RebootInstances](https://docs.byteplus.com/en/docs/ecs/RebootInstances)<br><br>[ModifyInstanceChargeType](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceChargeType)<br><br>[ModifyInstanceAttribute](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceAttribute)<br><br>[ModifyInstanceSpec](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceSpec)<br><br>[RenewInstance](https://docs.byteplus.com/en/docs/ecs/RenewInstance) ||The error code "InvalidInstance.RequestForbidden" is added. ||
|[CreateImage](https://docs.byteplus.com/en/docs/ecs/CreateImage) ||* Added a new error code:<br><br>   * InvalidSnapshotStatus |Image |
|[ImportImage](https://docs.byteplus.com/en/docs/ecs/ImportImage) ||* Added new error code:<br><br>   * InvalidPlatformVersion.Malformed ||
|[DescribeImages](https://docs.byteplus.com/en/docs/ecs/DescribeImages) ||* Added request parameter:<br><br>   * `Platform`: Indicates the version of the image operating system. ||
|[ReplaceSystemVolume](https://docs.byteplus.com/en/docs/ecs/ReplaceSystemVolume) ||* Added a new error code:<br><br>   * InvalidInstance.RequestForbidden<br><br>   * InvalidDedicatedHostStatus.Unsupported<br><br>   * InvalidInstanceForReplaceSystemVolume.Unsupported<br><br>   * InvalidSnapshotStatus<br><br>   * InvalidDedicatedHost.Expired<br><br>* Updated error code:<br><br>   * After being modified, the description of InvalidSnapshotStatus is "The status of the specified snapshot does not support this request". ||
|[ModifyInstanceDeployment](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceDeployment) ||The error code "InvalidDedicatedHostInstanceForModifyInstanceDeploymentSet.Unsupported" is added. |Deployment set |
|[CreateCommand](https://docs.byteplus.com/en/docs/ecs/CreateCommand-Creating_a_custom_command) |May 23, 2024 |* Added request parameter:<br><br>   * `ContentEncoding`, which indicates whether the command content is Base64 encoded. |Cloud assistant |
|[ModifyCommand](https://docs.byteplus.com/en/docs/ecs/ModifyCommand_-_Modify_custom_command) ||* Added request parameter:<br><br>   * `ContentEncoding`, which indicates whether the command content is Base64 encoded. ||
|[DescribeCommands](https://docs.byteplus.com/en/docs/ecs/DescribeCommands_-_Query_the_command_list) ||* Added request parameter:<br><br>   * `ContentEncoding`, which indicates whether the returned command content is Base64 encoded. ||
|[RunCommand](https://docs.byteplus.com/en/docs/ecs/RunCommand_-_Execute_command) ||* Added request parameter:<br><br>   * `ContentEncoding`, which indicates whether the returned command content is Base64 encoded. ||
|[DescribeInvocations](https://docs.byteplus.com/en/docs/ecs/DescribeInvocations_-_Query_task_list) ||* Added request parameter:<br><br>   * `ContentEncoding`, which indicates whether the returned command content is Base64 encoded. ||


<span id=".MjAyNOW5tDAz5pyI"></span>
## March 2024


|API |Release time |Change record |Associated feature |
|---|---|---|---|
|[RunInstances](https://docs.byteplus.com/en/docs/ecs/RunInstances) |2024\-03\-22 |* Added request parameters (optional):<br><br>   * `EipAddress.ReleaseWithInstance`, which specifies whether the EIP is released together with the instance when the instance is created.<br><br>   * `Volumes.N.SnapshotId`, which indicates using the snapshot to create the volume. Only data volumes are supported.<br><br>   * `EipAddress.SecurityProtectionInstanceId` and `EipAddress.SecurityProtectionTypes.N`. They indicate the security properties of the EIP.<br><br>* Added a new error code:<br><br>   * InvalidSnapshotStatus<br><br>   * InvalidVolumeTypeForSnapshot.UnSupported<br><br>   * InvalidSnapshot.NotFound<br><br>   * InvalidSnapshotZoneId.Mismatch<br><br>   * InvalidReleaseWithInstance.ChargeTypeMismatch<br><br>   * LimitExceeded.MaximumEipBandwidth<br><br>   * InvalidSecurityProtectionTypes.Malformed<br><br>   * InvalidSecurityProtectionTypes.BandwidthPackageIdMismatch<br><br>   * OperationDenied.SpecifiedSecurityGroupNotAuthorized |Instance |
|[DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) ||* Added request parameter (optional): `EipAddresses.N`, which indicates that querying the instance by the EIP address is supported.<br><br>* Added response parameter: `IpAddress`, which indicates the EIP address associated with the instance.<br><br>* Added new error codes: LimitExceeded.PrimaryIpAddresses, and LimitExceeded.MaximumEipAddresses. ||
|[DetectImage](https://docs.byteplus.com/en/docs/ecs/DetectImage) ||A new interface for initiating the image inspection process. |Image |
|[CreateImage](https://docs.byteplus.com/en/docs/ecs/CreateImage) ||* Added request parameter:<br><br>   * `NeedDetection`, which indicates whether to detect the image.<br><br>   * `SnapshotGroupId`, which indicates creating the custom image by using the snapshot or snapshot consistency group.<br><br>   * `SnapshotId`, which indicates using the system volume snapshot to create a custom image.<br><br>* Updated request parameters:<br><br>   * The `InstanceId` parameter is changed to an optional parameter.<br><br>   * The usage limits of `Tags.N.Key `are increased: the key cannot start with` sys: `in any combination of uppercase or lowercase letters.<br><br>* Added a new error code:<br><br>   * 400: InvalidPlatformForDetect.UnSupported. This indicates that the specified image platform does not support detection.<br><br>   * 400: InvalidSnapshotIdOrSnapshotGroupIdForCreateImage.UnSupported. This indicates you can not create a custom image with the specified snapshot or consistency group.<br><br>   * 400: LimitExceeded.MaximumSnapshotGroupTotalSize. This indicates the capacity of the specified snapshot consistency group exceeds the limit.<br><br>   * 404: InvalidSnapshotGroupId.NotFound. This indicates the specified snapshot consistency group ID does not exist.<br><br>   * 404: InvalidSnapshotId.NotFound. This indicates the specified snapshot ID does not exist.<br><br>   * 412: OperationDenied.SnapshotServiceUnavailable. This indicates the specified operation was denied because the snapshot service is not activated. ||
|[ImportImage](https://docs.byteplus.com/en/docs/ecs/ImportImage) ||* Added request parameter:<br><br>   * `NeedDetection`, which indicates whether to detect the image.<br><br>* Updated request parameter:<br><br>   * `Tags.N.Key` argument increases limit, does not support any case of starting with `sys:`<br><br>* Added a new error code:<br><br>   * 400: InvalidPlatformForDetect.UnSupported. This indicates that the specified image platform does not support detection. ||
|[DescribeImages](https://docs.byteplus.com/en/docs/ecs/DescribeImages) ||* Added response parameter:<br><br>   * The following structures are added to the `Images` structure:<br><br>      * The `DetectionResults` structure, which indicates the image detection result.<br><br>      * The `Snapshots` structure, which indicates snapshot information associated with the image. ||
|[DeleteImages](https://docs.byteplus.com/en/docs/ecs/DeleteImages) ||* Added request parameter:<br><br>   * `DeleteBindedSnapshots`, which indicates whether to delete the corresponding snapshot or the snapshot consistency group when the image is deleted. ||


<span id=".MjAyNOW5tDAx5pyI"></span>
## January 2024


|API |Release time |Change record |Associated feature |
|---|---|---|---|
|[RunInstances](https://docs.byteplus.com/en/docs/ecs/RunInstances) |2024\-01\-12 |Added request parameters (optional): `EipAddress.ChargeType`, `EipAddress.ISP`, `EipAddress.BandwidthMbps`, and `EipAddress.BandwidthPackageId`. The parameters indicate that when you create an instance, an EIP can be associated with it. |Instance |
|[StopInstance](https://docs.byteplus.com/en/docs/ecs/StopInstance) ||Added new error code: InvalidStoppedModeForScheduledInstance.Unsupported. ||
|[StopInstances](https://docs.byteplus.com/en/docs/ecs/StopInstances) ||||
|[ModifyInstanceSpec](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceSpec) ||Added new error code: InvalidScheduledInstanceForModifyInstanceSpec.Unsupported. ||
|[ModifyInstanceChargeType](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceChargeType) ||Added new error code: InvalidScheduledInstanceForModifyInstanceChargeType.Unsupported. ||
|[DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) ||* Added request parameter (optional): `ScheduledInstanceId`, which indicates the ID of the ESI order.<br><br>* Modified response parameter: "Segmented" is added to `ElasticScheduledInstanceType`. "Segmented" indicates Elastic Scheduled Instances\-Segmented.<br><br>* Added response parameter: `ScheduledInstanceId`, which indicates the ID of the ESI order. ||
|[DescribeAvailableResource](https://docs.byteplus.com/en/docs/ecs/DescribeAvailableResource) ||* Added request parameter (optional): `ElasticScheduledInstanceType`, which indicates the ESI type.<br><br>* Added new error code: InvalidElasticScheduledInstanceType.Malformed. ||
|[CreateTags](https://docs.byteplus.com/en/docs/ecs/CreateTags) ||Modified request parameter: The `ResourceType` parameter supports the value "scheduledinstance" which indicates ESIs can be managed by tags. |Tag |
|[DeleteTags](https://docs.byteplus.com/en/docs/ecs/DeleteTags) ||||
|[DescribeTags](https://docs.byteplus.com/en/docs/ecs/DescribeTags) ||||
|[ModifyInstanceDeployment](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceDeployment) ||Added new error code: InvalidScheduledInstanceForModifyInstanceDeploymentSet.Unsupported. |Deployment set |
|[PurchaseReservedInstances](https://docs.byteplus.com/en/docs/ecs/PurchaseReservedInstances) ||Added new error code: Insufficient.VolumePoolCapacity. |RI |
|[UpgradeCloudAssistants](https://docs.byteplus.com/en/docs/ecs/UpgradeCloudAssistants_-_Upgrade_Cloud_assistant_Agent) |2024\-01\-11 |A new interface for upgrading the cloud assistant Agent of ECS instances to the latest version. |Cloud assistant |
|[UninstallCloudAssistants](https://docs.byteplus.com/en/docs/ecs/UninstallCloudAssistants_-_Uninstall_Cloud_assistant_Agent) ||A new interface for uninstalling the cloud assistant Agent of ECS instances. ||
|[DescribeCloudAssistantStatus](https://docs.byteplus.com/en/docs/ecs/DescribeCloudAssistantStatus) ||Modified request parameter:<br><br>Added enumeration values of the `Status` parameter:<br><br><br>* `Lost`: Heartbeat timeout.<br><br>* `ReadyReboot`: Pending restart.<br><br>* `InstallFailed`: Installation failed.<br><br>* `Uninstalling`: Uninstalling.<br><br>* `Initializing`: Initializing. ||
