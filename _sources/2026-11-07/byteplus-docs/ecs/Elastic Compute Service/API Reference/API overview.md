---
title: "API overview"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Elastic-Compute-Service-API-overview"
---

This topic provides a detailed list of ECS APIs.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The Action (operation name) of an API defines the scope of operations allowed in an IAM policy. The <strong>Whether project\-specific authorization is supported</strong> column in the tables is used to determine whether an API operation can take effect in an IAM policy restricted to a specific project. For example, if a user is associated with the ECSFullAccess policy (full management permissions for ECS) with a project scope restriction, the permissions will be affected as follows:</div>



* <div data-tips="true" data-tips-type="default">Actions that support project\-specific authorization: These operations will be strictly limited to the specified project. Users can only perform relevant operations on ECS resources within that project.</div>


* <div data-tips="true" data-tips-type="default">Actions that do not support project\-specific authorization: Even if the overall permissions are restricted to the specified project, the operation itself is not bound by the project scope and will prompt "Insufficient permissions". You need to grant global permissions in the IAM policy for normal access. <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-3">Learn more</a>.</div>



<span id=".5Zyw5Z-f"></span>
## Region


|API |Description |Whether project\-specific authorization is supported |
|---|---|---|
|[DescribeRegions](https://docs.byteplus.com/en/docs/ecs/DescribeRegions) |Obtains region information |Not supported |
|[DescribeZones](https://docs.byteplus.com/en/docs/ecs/DescribeZones) |Obtains information about availability zones in a region |Not supported |


<span id=".5a6e5L6L"></span>
## Instance


|API |Description |Whether project\-specific authorization is supported |
|---|---|---|
|[RunInstances](https://docs.byteplus.com/en/docs/ecs/RunInstances) |Creates one or more instances |Supported |
|[AllocateInstances](https://docs.byteplus.com/en/docs/ecs/AllocateInstances) |Creates one or more instances with availability zone flexibility |Supported |
|[StartInstance](https://docs.byteplus.com/en/docs/ecs/StartInstance) |Starts an instance |Supported |
|[StopInstance](https://docs.byteplus.com/en/docs/ecs/StopInstance) |Stops an instance |Supported |
|[RebootInstance](https://docs.byteplus.com/en/docs/ecs/RebootInstance) |Restarts an instance |Supported |
|[DeleteInstance](https://docs.byteplus.com/en/docs/ecs/DeleteInstance) |Deletes an instance |Supported |
|[StartInstances](https://docs.byteplus.com/en/docs/ecs/StartInstances) |Starts one or more instances |Supported |
|[StopInstances](https://docs.byteplus.com/en/docs/ecs/StopInstances) |Stops one or more instances |Supported |
|[RebootInstances](https://docs.byteplus.com/en/docs/ecs/RebootInstances) |Restarts one or more instances |Supported |
|[DeleteInstances](https://docs.byteplus.com/en/docs/ecs/DeleteInstances) |Deletes one or more instances |Supported |
|[DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) |Obtains instance information |Supported |
|[DescribeInstanceTypes](https://docs.byteplus.com/en/docs/ecs/DescribeInstanceTypes) |Obtains information about all instance types provided by ECS |Not supported |
|[DescribeInstanceTypeFamilies](https://docs.byteplus.com/en/docs/ecs/DescribeInstanceTypeFamilies) |Obtains information about instance type families provided by ECS |Not supported |
|[DescribeAvailableResource](https://docs.byteplus.com/en/docs/ecs/DescribeAvailableResource) |Queries stock information of compute resources in an availability zone |Not supported |
|[DescribeUserData](https://docs.byteplus.com/en/docs/ecs/DescribeUserData) |Queries the custom data of an instance |Supported |
|[ModifyInstanceMetadataOptions](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceMetadataOptions) |Modifies the access mode of instance metadata |Supported |
|[DescribeInstanceVncUrl](https://docs.byteplus.com/en/docs/ecs/DescribeInstanceVncUrl) |Queries the VNC management terminal address of an instance |Supported |
|[DescribeInstanceECSTerminalUrl](https://docs.byteplus.com/en/docs/ecs/DescribeInstanceECSTerminalUrl) |Queries the ECS terminal address of an ECS instance​ |Supported |
|[RenewInstance](https://docs.byteplus.com/en/docs/ecs/RenewInstance) |Renews a subscription instance |Supported |
|[ModifyInstanceAttribute](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceAttribute) |Modifies information of an instance |Supported |
|[ModifyInstanceSpec](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceSpec) |Modifies the type of an instance |Supported |
|[ModifyInstancesSpec](https://docs.byteplus.com/en/docs/ecs/ModifyInstancesSpec) |Modifies the types of multiple instances at one time |Supported |
|[ModifyInstanceChargeType](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceChargeType) |Modifies the billing method of the specified instance |Supported |
|[AssociateInstancesIamRole](https://docs.byteplus.com/en/docs/ecs/AssociateInstancesIamRole) |Associates an IAM role with one or more instances |Supported |
|[DisassociateInstancesIamRole](https://docs.byteplus.com/en/docs/ecs/DisassociateInstancesIamRole) |Dissociates an IAM role from one or more instances |Supported |
|[DescribeInstancesIamRoles](https://docs.byteplus.com/en/docs/ecs/DescribeInstancesIamRoles) |Obtains IAM roles associated with one or more instances |Supported |
|[DescribeSpotAdvice](https://docs.byteplus.com/en/docs/ecs/DescribeSpotAdvice) |Queries information such as the average release rate and average discount rate of spot instances over the past 30 days |Not supported |
|[DescribeSpotPriceHistory](https://docs.byteplus.com/en/docs/ecs/DescribeSpotPriceHistory) |Queries the historical prices of spot instances within the past 30 days |Not supported |
|[ModifyInstanceVpcAttribute](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceVpcAttribute) |Modifies the VPC, subnet, or security group of an instance |Supported |
|[PurchaseReservedInstances](https://docs.byteplus.com/en/docs/ecs/PurchaseReservedInstances) |Purchases Reserved Instances |Supported |
|[DescribeReservedInstances](https://docs.byteplus.com/en/docs/ecs/DescribeReservedInstances) |Queries information about purchased Reserved Instances |Supported |
|[ModifyReservedInstances](https://docs.byteplus.com/en/docs/ecs/ModifyReservedInstances) |Modifies RIs |Supported |
|[CreateScheduledInstances](https://docs.byteplus.com/en/docs/ecs/CreateScheduledInstances) |Creating ESIs |Not supported |
|[DescribeScheduledInstances](https://docs.byteplus.com/en/docs/ecs/DescribeScheduledInstances) |Queries ESI orders |Not supported |
|[DeleteScheduledInstance](https://docs.byteplus.com/en/docs/ecs/DeleteScheduledInstance) |Cancels the reservation of Elastic Scheduled Instances |Not supported |
|[DescribeScheduledInstanceStock](https://docs.byteplus.com/en/docs/ecs/DescribeScheduledInstanceStock) |Queries the reservation status of Elastic Scheduled Instances |Not supported |


<span id=".6ZWc5YOP"></span>
## Image


|API |Description |Whether project\-specific authorization is supported |
|---|---|---|
|[DescribeImages](https://docs.byteplus.com/en/docs/ecs/DescribeImages) |Obtains image information |Supported |
|[ReplaceSystemVolume](https://docs.byteplus.com/en/docs/ecs/ReplaceSystemVolume) |Reinstalls the system or changes the system volume for an instance |Supported |
|[ImportImage](https://docs.byteplus.com/en/docs/ecs/ImportImage) |Importing custom images |Supported |
|[ExportImage](https://docs.byteplus.com/en/docs/ecs/ExportImage) |Exporting custom images |Supported |
|[ModifyImageAttribute](https://docs.byteplus.com/en/docs/ecs/ModifyImageAttribute) |Modifies information such as the name, description, and status of a custom image |Supported |
|[DeleteImages](https://docs.byteplus.com/en/docs/ecs/DeleteImages) |Delete custom images |Supported |
|[DescribeImageSharePermission](https://docs.byteplus.com/en/docs/ecs/DescribeImageSharePermission) |Queries all users with whom a custom image is shared |Supported |
|[ModifyImageSharePermission](https://docs.byteplus.com/en/docs/ecs/ModifyImageSharePermission) |Manages image sharing permissions |Supported |
|[DescribeTasks](https://docs.byteplus.com/en/docs/ecs/DescribeTasks) |Queries the progress of one or more asynchronous requests |Not supported |
|[CreateImage](https://docs.byteplus.com/en/docs/ecs/CreateImage) |Creating custom images based on instances |Supported |
|[CopyImage](https://docs.byteplus.com/en/docs/ecs/CopyImage) |Copies a custom image or shared image |Supported |
|[DetectImage](https://docs.byteplus.com/en/docs/ecs/DetectImage) |Initiates an image detection process |Supported |
|[DescribeAutoInstallPackages](https://docs.byteplus.com/en/docs/ecs/DescribeAutoInstallPackages) |Queries automatic installation packages supported by images and instance type families |Supported |


<span id=".6L-Q57u0"></span>
## HPC cluster


|API |Description |Whether project\-specific authorization is supported |
|---|---|---|
|[CreateHpcCluster](https://docs.byteplus.com/en/docs/ecs/CreateHpcCluster) |Creates an HPC cluster |Not supported |
|[DeleteHpcCluster](https://docs.byteplus.com/en/docs/ecs/DeleteHpcCluster) |Deletes an HPC cluster |Not supported |
|[DescribeHpcClusters](https://docs.byteplus.com/en/docs/ecs/DescribeHpcClusters) |Queries the list of HPC clusters that meet the specified conditions with detailed information |Not supported |
|[DescribeHpcInstancePosition](https://docs.byteplus.com/en/docs/ecs/DescribeHpcInstancePosition) |Queries the location of HPC\-optimized instances in the RDMA network |Not supported |


<span id=".5a-G6ZKl5a-5"></span>
## Key pair


|API |Description |Whether project\-specific authorization is supported |
|---|---|---|
|[ImportKeyPair](https://docs.byteplus.com/en/docs/ecs/ImportKeyPair) |Imports the public key of a key pair |Supported |
|[CreateKeyPair](https://docs.byteplus.com/en/docs/ecs/CreateKeyPair) |Creates a key pair |Supported |
|[DescribeKeyPairs](https://docs.byteplus.com/en/docs/ecs/DescribeKeyPairs) |Queries the list of key pairs |Supported |
|[ModifyKeyPairAttribute](https://docs.byteplus.com/en/docs/ecs/ModifyKeyPairAttribute) |Modifies the description of a key pair |Supported |
|[AttachKeyPair](https://docs.byteplus.com/en/docs/ecs/AttachKeyPair) |Associates one or more key pairs with one or more Linux instances |Supported |
|[DetachKeyPair](https://docs.byteplus.com/en/docs/ecs/DetachKeyPair) |Disassociates a key pair from one or more Linux instances |Supported |
|[DeleteKeyPairs](https://docs.byteplus.com/en/docs/ecs/DeleteKeyPairs) |Deleting key pairs |Supported |


<span id=".5qCH562-"></span>
## Tag


|API |Description |Whether project\-specific authorization is supported |
|---|---|---|
|[TagResources (new version)](https://docs.byteplus.com/en/docs/ecs/TagResources) |Adds tags to one or more resources such as instances, images, key pairs, orchestration tasks or plans, and launch templates |Supported |
|[UntagResources (new version)](https://docs.byteplus.com/en/docs/ecs/UntagResources) |Removes tags from one or more resources such as instances, images, key pairs, orchestration plans or tasks, and launch templates |Supported |
|[ListTagsForResources (new version)](https://docs.byteplus.com/en/docs/ecs/ListTagsForResources) |Queries resources with tags |Supported |
|[CreateTags (old version)](https://docs.byteplus.com/en/docs/ecs/CreateTags) |Adds tags to one or more resources such as instances, images, and key pairs |Not supported |
|[DeleteTags (old version)](https://docs.byteplus.com/en/docs/ecs/DeleteTags) |Removes tags from one or more resources such as instances, images, and key pairs |Not supported |
|[DescribeTags (old version)](https://docs.byteplus.com/en/docs/ecs/DescribeTags) |Queries resources with tags |Not supported |
|[CreateTags](https://docs.byteplus.com/en/docs/ecs/CreateTags-01) |Adds tags to one or more volumes |\- |
|[DeleteTags](https://docs.byteplus.com/en/docs/ecs/DeleteTags-02) |Removes tags from one or more volumes |\- |
|[Describetags](https://docs.byteplus.com/en/docs/ecs/DescribeTags-01) |Queries tags added to one or more volumes |\- |


<span id=".5LqR55uY"></span>
## Volume


|API |Description |
|---|---|
|[CreateVolume](https://docs.byteplus.com/en/docs/ecs/Createvolume) |Creates a volume |
|[DeleteVolume](https://docs.byteplus.com/en/docs/ecs/Deletevolume) |Deletes a volume |
|[AttachVolume](https://docs.byteplus.com/en/docs/ecs/Attachvolume) |Mounts a volume to an instance |
|[DetachVolume](https://docs.byteplus.com/en/docs/ecs/Detachvolume) |Unmounts a volume from an instance |
|[ExtendVolume](https://docs.byteplus.com/en/docs/ecs/Extendvolume) |Expands a volume |
|[RollbackVolume](https://docs.byteplus.com/en/docs/ecs/Rollbackvolume) |Rolls back a volume |
|[DescribeVolumes](https://docs.byteplus.com/en/docs/ecs/Describevolumes) |Queries the list of volumes |
|[DescribeVolumeType](https://docs.byteplus.com/en/docs/ecs/Describevolumetype) |Queries the types of volumes that can be created in the availability zones of each region |
|[ModifyVolumeSpec](https://docs.byteplus.com/en/docs/ecs/Modifyvolumespec) |Modifies the specifications of a volume |
|[ModifyVolumeAttribute](https://docs.byteplus.com/en/docs/ecs/Modifyvolumeattribute) |Modifies the attributes of a volume |
|[ModifyVolumeChargeType](https://docs.byteplus.com/en/docs/ecs/ModifyVolumeChargeType) |Modifies the billing method of a volume |
|[ModifyVolumeExtraPerformance](https://docs.byteplus.com/en/docs/ecs/ModifyVolumeExtraPerformance) |Configures extra performance for a volume or modifies its extra performance attributes |
|[CalculatePriceV2](https://docs.byteplus.com/en/docs/ecs/CalculatePriceV2) |Queries the volume price |
|[ReInitializeVolume](https://docs.byteplus.com/en/docs/ecs/ReInitializevolume) |Reinitializes a volume |
|[PurchaseReservedStorageCapacity](https://docs.byteplus.com/en/docs/ecs/Purchasereservedstoragecapacity) |Creates Reserved Storage Capacity |
|[DescribeReservedStorageCapacity](https://docs.byteplus.com/en/docs/ecs/Describereservedstoragecapacity) |Queries Reserved Storage Capacity |
|[ModifyReservedStorageCapacityEffectiveAt](https://docs.byteplus.com/en/docs/ecs/ModifyReservedStorageCapacityEffectiveAt) |Modifies the effective time of Reserved Storage Capacity |
|[CreatePlacementGroup](https://docs.byteplus.com/en/docs/ecs/Createplacementgroup) |Creates a storage placement group |
|[DescribePlacementGroups](https://docs.byteplus.com/en/docs/ecs/Describeplacementgroups) |Queries information of a storage placement group |
|[DescribePlacementGroupDetails](https://docs.byteplus.com/en/docs/ecs/Describeplacementgroupdetails) |Queries information about volumes associated with a storage placement group |
|[ModifyPlacementGroup](https://docs.byteplus.com/en/docs/ecs/Modifyplacementgroup) |Modifies a storage placement group |
|[DeletePlacementGroup](https://docs.byteplus.com/en/docs/ecs/Deleteplacementgroup) |Deletes a storage placement group |


<span id=".5b-r54Wn"></span>
## Snapshot


|API |Description |
|---|---|
|[CreateSnapshot](https://docs.byteplus.com/en/docs/ecs/Createsnapshot) |Creates a snapshot |
|[DeleteSnapshot](https://docs.byteplus.com/en/docs/ecs/Deletesnapshot) |Deletes a snapshot |
|[DescribeSnapshots](https://docs.byteplus.com/en/docs/ecs/Describesnapshots) |Queries the list of snapshots |
|[ModifySnapshotAttribute](https://docs.byteplus.com/en/docs/ecs/Modifysnapshotattribute) |Modifies snapshot attributes |
|[DescribeSnapshotChains](https://docs.byteplus.com/en/docs/ecs/Describesnapshotchains) |Queries snapshot chains |
|[DescribeSnapshotsUsage](https://docs.byteplus.com/en/docs/ecs/DescribeSnapshotsUsage) |Queries snapshot usage |
|[CreateAutoSnapshotPolicy](https://docs.byteplus.com/en/docs/ecs/Createautosnapshotpolicy) |Creates an auto snapshot policy |
|[DeleteAutoSnapshotPolicy](https://docs.byteplus.com/en/docs/ecs/Deleteautosnapshotpolicy) |Deletes an auto snapshot policy |
|[ModifyAutoSnapshotPolicy](https://docs.byteplus.com/en/docs/ecs/Modifyautosnapshotpolicy) |Modifies an auto snapshot policy |
|[DescribeAutoSnapshotPolicy](https://docs.byteplus.com/en/docs/ecs/Describeautosnapshotpolicy) |Queries an auto snapshot policy |
|[ApplyAutoSnapshotPolicy](https://docs.byteplus.com/en/docs/ecs/Applyautosnapshotpolicy) |Applies an auto snapshot policy to a volume |
|[CancelAutoSnapshotPolicy](https://docs.byteplus.com/en/docs/ecs/Cancelautosnapshotpolicy) |Cancels an auto snapshot policy |
|[CreateSnapshotGroup](https://docs.byteplus.com/en/docs/ecs/Createsnapshotgroup) |Creates a snapshot consistency group |
|[DescribeSnapshotGroups](https://docs.byteplus.com/en/docs/ecs/DescribeSnapshotGroups) |Queries snapshot consistency groups |
|[ModifySnapshotGroup](https://docs.byteplus.com/en/docs/ecs/ModifySnapshotGroup) |Modifies a snapshot consistency group |
|[DeleteSnapshotGroup](https://docs.byteplus.com/en/docs/ecs/DeleteSnapshotGroup) |Deletes a snapshot consistency group |
|[RollbackSnapshotGroup](https://docs.byteplus.com/en/docs/ecs/RollbackSnapshotGroup) |Rolls back a snapshot consistency group |


<span id=".6YOo572y6ZuG"></span>
## Deployment set


|API |Description |Whether project\-specific authorization is supported |
|---|---|---|
|[CreateDeploymentSet](https://docs.byteplus.com/en/docs/ecs/CreateDeploymentSet) |Creates a deployment set |Not supported |
|[DescribeDeploymentSets](https://docs.byteplus.com/en/docs/ecs/DescribeDeploymentSets) |Queries attributes of a deployment set |Not supported |
|[DescribeDeploymentSetSupportedInstanceTypeFamily](https://docs.byteplus.com/en/docs/ecs/DescribeDeploymentSetSupportedInstanceTypeFamily) |Queries instance type families that support deployment sets |Not supported |
|[ModifyDeploymentSetAttribute](https://docs.byteplus.com/en/docs/ecs/ModifyDeploymentSetAttribute) |Modifies the name and description of a deployment set |Not supported |
|[ModifyInstanceDeployment](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceDeployment) |Modify the deployment set of instances |Supported |
|[DeleteDeploymentSet](https://docs.byteplus.com/en/docs/ecs/DeleteDeploymentSet) |Deletes a deployment set |Not supported |


<span id=".5a6e5L6L5ZCv5Yqo5qih54mI"></span>
## Instance launch template


|API |Description |
|---|---|
|[CreateLaunchTemplate](https://docs.byteplus.com/en/docs/ecs/CreateLaunchTemplate) |Creates an instance launch template |
|[CreateLaunchTemplateVersion](https://docs.byteplus.com/en/docs/ecs/CreateLaunchTemplateVersion) |Creates a version of an instance launch template |
|[DescribeLaunchTemplates](https://docs.byteplus.com/en/docs/ecs/DescribeLaunchTemplates) |Queries instance launch templates |
|[DescribeLaunchTemplateVersions](https://docs.byteplus.com/en/docs/ecs/DescribeLaunchTemplateVersions) |Queries the version of an instance launch template |
|[ModifyTemplateDefaultVersion](https://docs.byteplus.com/en/docs/ecs/ModifyTemplateDefaultVersion) |Modifies the default version of an instance launch template |
|[DeleteLaunchTemplate](https://docs.byteplus.com/en/docs/ecs/DeleteLaunchTemplate) |Deletes an instance launch template |
|[DeleteLaunchTemplateVersion](https://docs.byteplus.com/en/docs/ecs/DeleteLaunchTemplateVersion) |Deletes a version of an instance launch template |


<span id=".55uR5o6n"></span>
## Monitoring


|API |Description |Whether project\-specific authorization is supported |
|---|---|---|
|[DescribeSystemEvents](https://docs.byteplus.com/en/docs/ecs/DescribeSystemEvents) |Queries the system event information of an instance |Supported |
|[UpdateSystemEvents](https://docs.byteplus.com/en/docs/ecs/UpdateSystemEvents) |Modifies the system event status |Not supported |
|[CreateSubscription](https://docs.byteplus.com/en/docs/ecs/CreateSubscription) |Subscribes to ECS event notifications |Not supported |
|[ModifySubscriptionEventTypes](https://docs.byteplus.com/en/docs/ecs/ModifySubscriptionEventTypes) |Modifies the type of a subscribed event |Not supported |
|[DescribeSubscriptions](https://docs.byteplus.com/en/docs/ecs/DescribeSubscriptions) |Queries event notification subscriptions |Not supported |
|[DescribeEventTypes](https://docs.byteplus.com/en/docs/ecs/DescribeEventTypes) |Queries the list of event types |Not supported |
|[ModifySystemEventDefaultAction](https://docs.byteplus.com/en/docs/ecs/ModifySystemEventDefaultAction_-_Modify_the_default_operations_and_maintenance_actions_for_events) |Modifies the default O&M operations for events |Not supported |
|[DescribeSystemEventDefaultAction](https://docs.byteplus.com/en/docs/ecs/DescribeSystemEventDefaultAction_-_Query_the_default_maintenance_actions_for_events) |Queries the default O&M operations for events |Not supported |


<span id="5iV24dIY"></span>
## O&M


|API |Description |Whether project\-specific authorization is supported |
|---|---|---|
|[GetConsoleOutput](https://docs.byteplus.com/en/docs/ecs/GetConsoleOutput) |Retrieves the system command line output at the most recent start, restart, or shutdown of an instance |Supported |
|[GetConsoleScreenshot](https://docs.byteplus.com/en/docs/ecs/GetConsoleScreenshot) |Obtains a JPG screenshot of a running instance to assist with troubleshooting |Supported |


<span id=".5om56YeP5L2c5Lia"></span>
## Cloud assistant


|API |Description |
|---|---|
|[CreateCommand](https://docs.byteplus.com/en/docs/ecs/CreateCommand-Creating_a_custom_command) |Creates a custom command for the cloud assistant |
|[ModifyCommand](https://docs.byteplus.com/en/docs/ecs/ModifyCommand_-_Modify_custom_command) |Modifies the content of a cloud assistant custom command |
|[DeleteCommand](https://docs.byteplus.com/en/docs/ecs/DeleteCommand_-_Deleting_a_custom_command) |Deletes the specified custom command |
|[DescribeCommands](https://docs.byteplus.com/en/docs/ecs/DescribeCommands_-_Query_the_command_list) |Queries the list of cloud assistant commands |
|[RunCommand](https://docs.byteplus.com/en/docs/ecs/RunCommand_-_Execute_command) |Creates a cloud assistant task by manually entering commands |
|[InvokeCommand](https://docs.byteplus.com/en/docs/ecs/InvokeCommand_-_Execute_command) |Creates a cloud assistant task using existing custom or public commands |
|[StopInvocation](https://docs.byteplus.com/en/docs/ecs/StopInvocation_-_Stop_executing_tasks) |Stops a running cloud assistant command |
|[DescribeInvocations](https://docs.byteplus.com/en/docs/ecs/DescribeInvocations_-_Query_task_list) |Queries the execution list and status of the cloud assistant |
|[DescribeInvocationInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInvocationInstances_-_Query_the_task_execution_object_list) |Queries the list of cloud assistant execution objects |
|[DescribeInvocationResults](https://docs.byteplus.com/en/docs/ecs/DescribeInvocationResults_-_View_command_execution_results) |Views one or more execution results of the cloud assistant |
|[InstallCloudAssistant](https://docs.byteplus.com/en/docs/ecs/InstallCloudAssistant_-_Install_Cloud_assistant_Agent) |Installs the cloud assistant Agent on an ECS instance |
|[UpgradeCloudAssistants](https://docs.byteplus.com/en/docs/ecs/UpgradeCloudAssistants_-_Upgrade_Cloud_assistant_Agent) |Upgrades the installed cloud assistant Agent to the latest version |
|[UninstallCloudAssistants](https://docs.byteplus.com/en/docs/ecs/UninstallCloudAssistants_-_Uninstall_Cloud_assistant_Agent) |Uninstalls the cloud assistant Agent |
|[DescribeCloudAssistantStatus](https://docs.byteplus.com/en/docs/ecs/DescribeCloudAssistantStatus) |Queries the installation status of the cloud assistant Agent on an instance |
