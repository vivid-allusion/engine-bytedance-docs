---
title: "API release history"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/API-release-notes"
---

This topic describes the updates of server\-side APIs for the AS service.

<span id="ueO00rUx"></span>
## January 2026


|API |Release time |Change record |Associated feature |
|---|---|---|---|
|[CreateScalingConfiguration](https://docs.byteplus.com/en/docs/as/CreateScalingConfiguration)<br><br>[ModifyScalingConfiguration](https://docs.byteplus.com/en/docs/as/ModifyScalingConfiguration) |<div style="text-align: center"><br>2026\-01</div><br> |* New request parameters: Volumes.N.ExtraPerformanceTypeId, Volumes.N.ExtraPerformanceIOPS, Volumes.N.ExtraPerformanceThroughputMB, all optional. |Scaling configuration |
|[DescribeScalingConfigurations](https://docs.byteplus.com/en/docs/as/DescribeScalingConfigurations) ||* New response parameters: ExtraPerformanceTypeId, ExtraPerformanceIOPS, ExtraPerformanceThroughputMB. ||


<span id="4wnw9ExP"></span>
## May 2025


|API |Release time |Change record |Associated feature |
|---|---|---|---|
|[CreateScalingPolicy](https://docs.byteplus.com/en/docs/as/CreateScalingPolicy)<br><br>[ModifyScalingPolicy](https://docs.byteplus.com/en/docs/as/ModifyScalingPolicy) |<div style="text-align: center"><br>2025\-05</div><br> |* Added Request parameters: AlarmPolicy.Effective and ScheduledInstancePolicy.BestEffort.<br><br>* Modified Request parameters: ScheduledPolicy.RecurrenceEndTime, allowing empty values. |Scaling rule |
|[DescribeScalingPolicies](https://docs.byteplus.com/en/docs/as/DescribeScalingPolicies) ||* The response structure of AlarmPolicy added a new response parameter: Effective.<br><br>* ScheduledInstancePolicy response structure adds a new response parameter: BestEffort. ||


<span id=".MjAyNCDlubQgMDgg5pyI"></span>
## March 2025


|API |Release time |Change record |Associated feature |
|---|---|---|---|
|All APIs |<div style="text-align: center"><br>2025\-03</div><br> |Published all error codes. |All |
|[DescribeLifecycleActivities](https://docs.byteplus.com/en/docs/as/DescribeLifecycleActivities) ||Added Request parameters: ScalingGroupId, LifecycleHookIds.N. |Lifecycle hook |
|[CompleteLifecycleActivity](https://docs.byteplus.com/en/docs/as/CompleteLifecycleActivity) ||New request parameters: LifecycleHookId. ||
|[CreateScalingGroup](https://docs.byteplus.com/en/docs/as/CreateScalingGroup) ||Modified request parameter: ProjectName. The default value was changed from empty to default. |Scaling group |


<span id=".MjAyNCDlubQgMDgg5pyI"></span>
## January 2025


|API |Release time |Change record |Associated feature |
|---|---|---|---|
|[CreateScalingPolicy](https://docs.byteplus.com/en/docs/as/CreateScalingPolicy)<br><br>[ModifyScalingPolicy](https://docs.byteplus.com/en/docs/as/ModifyScalingPolicy) |2025\-01 |Modify request parameters<br><br><br>* AlarmPolicy.Condition.MetricName adds the following values: Instance_NetTxBits_Avg, Instance_NetRxBits_Avg, Instance_NetTxPackets_Avg, Instance_NetRxPackets_Avg<br><br>* AlarmPolicy.Condition.MetricUnit adds the following values: Bits/Second (IEC), Packet/Second |Scaling rule |
|[DescribeScalingPolicies](https://docs.byteplus.com/en/docs/as/DescribeScalingPolicies) ||Condition structure Modify Response parameters:<br><br><br>* New values added to MetricName: Instance_NetTxBits_Avg, Instance_NetRxBits_Avg, Instance_NetTxPackets_Avg, Instance_NetRxPackets_Avg.<br><br>* New values added to MetricUnit: Bits/Second(IEC), Packet/Second. ||
|[CreateScalingConfiguration](https://docs.byteplus.com/en/docs/as/CreateScalingConfiguration)<br><br>[ModifyScalingConfiguration](https://docs.byteplus.com/en/docs/as/ModifyScalingConfiguration) ||Added request parameter: Eip.ReleaseWithInstance. Optional. |Scaling configuration |
|[DescribeScalingConfigurations](https://docs.byteplus.com/en/docs/as/DescribeScalingConfigurations) ||New response parameter: Eip.ReleaseWithInstance. ||


<span id=".MjAyNCDlubQgMDgg5pyI"></span>
## August 2024


|API |Release time |Change record |Associated feature |
|---|---|---|---|
|[ModifyScalingGroup](https://docs.byteplus.com/en/docs/as/ModifyScalingGroup) |2024\-08 |Modify Request parameters: DesireInstanceNumber, support switching the desired number of instances. |Scaling group |
|[CreateScalingPolicy](https://docs.byteplus.com/en/docs/as/CreateScalingPolicy) ||New request parameters: AlarmPolicy.Conditions.N.MetricName, AlarmPolicy.Conditions.N.MetricUnit, AlarmPolicy.Conditions.N.Threshold, AlarmPolicy.Conditions.N.ComparisonOperator, AlarmPolicy.ConditionOperator, all optional. |Scaling policy |
|[ModifyScalingPolicy](https://docs.byteplus.com/en/docs/as/ModifyScalingPolicy) ||||
|[DescribeScalingPolicies](https://docs.byteplus.com/en/docs/as/DescribeScalingPolicies) ||New response structure: Conditions. ||


<span id=".MjAyNCDlubQgMDcg5pyI"></span>
## July 2024


|API |Release time |Change record |Associated feature |
|---|---|---|---|
|[CreateScalingPolicy](https://docs.byteplus.com/en/docs/as/CreateScalingPolicy) |2024\-06 |Modified request parameter: AlarmPolicy.Condition.MetricName, added with new values. |Scaling policy |
|[ModifyScalingPolicy](https://docs.byteplus.com/en/docs/as/ModifyScalingPolicy) ||||
|[DescribeScalingPolicies](https://docs.byteplus.com/en/docs/as/DescribeScalingPolicies) |2024\-06 |Modified Response parameter: AlarmPolicy.Condition.MetricName, with new values added. ||


<span id=".MjAyNCDlubQgMDUg5pyI"></span>
## May 2024


|API |Release time |Change record |Associated feature |
|---|---|---|---|
|[DescribeScalingGroups](https://docs.byteplus.com/en/docs/as/DescribeScalingGroups) | |New response parameter: SuspendedProcesses. |Scaling group |
|[SuspendProcesses](https://docs.byteplus.com/en/docs/as/SuspendProcesses) ||Added new APIs. ||
|[ResumeProcesses](https://docs.byteplus.com/en/docs/as/ResumeProcesses) ||||
|[DescribeScalingInstances](https://docs.byteplus.com/en/docs/as/DescribeScalingInstances) ||The request parameter Status is added with a new value: Standby. |Instance management |
|[EnterStandby](https://docs.byteplus.com/en/docs/as/EnterStandby) ||Added new APIs. ||
|[ExitStandby](https://docs.byteplus.com/en/docs/as/ExitStandby) ||||


<span id=".MjAyNCDlubQgMDIg5pyI"></span>
## February 2024


|API |Release time |Change record |Associated feature |
|---|---|---|---|
|[CreateScalingGroup](https://docs.byteplus.com/en/docs/as/CreateScalingGroup) |2024\-02 |Added optional Request parameters `LaunchTemplateOverrides.N.PriceLimit`. |Scaling group |
|[ModifyScalingGroup](https://docs.byteplus.com/en/docs/as/ModifyScalingGroup) ||||
|[DescribeScalingGroups](https://docs.byteplus.com/en/docs/as/DescribeScalingGroups) ||A new Response parameter `PriceLimit` was added to the LaunchTemplateOverride structure. ||
|[CreateScalingConfiguration](https://docs.byteplus.com/en/docs/as/CreateScalingConfiguration) ||* New request parameters: `InstanceTypeOverrides.N.InstanceType` and `InstanceTypeOverrides.N.PriceLimit`, optional.<br><br>* Updated request parameter: `SpotStrategy`, added with a value SpotWithPriceLimit. |Scaling configuration |
|[ModifyScalingConfiguration](https://docs.byteplus.com/en/docs/as/ModifyScalingConfiguration) ||||
|[DescribeScalingConfigurations](https://docs.byteplus.com/en/docs/as/DescribeScalingConfigurations) ||The scaling configuration response structure adds an `InstanceTypeOverride` structure. ||


<span id=".XzIwMjQt5bm0LTAxLeaciA=="></span>
## January 2024


|API |Release time |Change record |Associated feature |
|---|---|---|---|
|[CreateScalingGroup](https://docs.byteplus.com/en/docs/as/CreateScalingGroup) |2024\-01\-08 |Added request parameter `ServerGroupAttributes.N.Type`, which is optional. |Scaling group |
|[AttachServerGroups](https://docs.byteplus.com/en/docs/as/AttachServerGroups) ||||
|[DetachServerGroups](https://docs.byteplus.com/en/docs/as/DetachServerGroups) ||||
|[DescribeScalingGroups](https://docs.byteplus.com/en/docs/as/DescribeScalingGroups) ||New response parameters added to the ServerGroupAttribute response structure: `Type`. ||
|[CreateScalingConfiguration](https://docs.byteplus.com/en/docs/as/CreateScalingConfiguration) ||Added Request parameters `Eip.SecurityProtectionInstanceId`, which is optional |Scaling configuration |
|[ModifyScalingConfiguration](https://docs.byteplus.com/en/docs/as/ModifyScalingConfiguration) ||||
|[DescribeScalingConfigurations](https://docs.byteplus.com/en/docs/as/DescribeScalingConfigurations) ||A new response parameter `Eip.SecurityProtectionInstanceId` is added to the EIP response structure. ||
|[CreateLifecycleHook](https://docs.byteplus.com/en/docs/as/CreateLifecycleHook) ||Added request parameter `ClientToken`. |Lifecycle hook |


<span id=".XzIwMjPlubQxMeaciA=="></span>
## November 2023


|Module |API name |Change record |Release regions |
|---|---|---|---|
|Scaling group |[CreateScalingGroup](https://docs.byteplus.com/en/docs/as/CreateScalingGroup) |New optional request parameters `InstancesDistribution.OnDemandBaseCapacity`, `InstancesDistribution.OnDemandPercentageAboveBaseCapacity`, `InstancesDistribution.CompensateWithOnDemand`, `InstancesDistribution.SpotInstanceRemedy` were added. |All |
||[ModifyScalingGroup](https://docs.byteplus.com/en/docs/as/ModifyScalingGroup) |||
||[DescribeScalingGroups](https://docs.byteplus.com/en/docs/as/DescribeScalingGroups) |Added new response parameter structure:` InstancesDistribution`. ||
|Scaling configuration |[CreateScalingConfiguration](https://docs.byteplus.com/en/docs/as/CreateScalingConfiguration) |Added `Request parameters Eip.BandwidthPackageId`, `Eip.SecurityProtectionTypes.N`, both optional. ||
||[ModifyScalingConfiguration](https://docs.byteplus.com/en/docs/as/ModifyScalingConfiguration) |||
||[DescribeScalingConfigurations](https://docs.byteplus.com/en/docs/as/DescribeScalingConfigurations) |Added Response parameters `BandwidthPackageId` and `SecurityProtectionTypes` in the EIP response structure. ||


<span id=".XzIwMjPlubQ55pyI"></span>
## September 2023


|Module |API name |Release record |Release regions |
|---|---|---|---|
|Lifecycle hook |[CreateLifecycleHook](https://docs.byteplus.com/en/docs/as/CreateLifecycleHook)<br><br>[ModifyLifecycleHook](https://docs.byteplus.com/en/docs/as/ModifyLifecycleHook) |New Request parameters: `LifecycleCommand.CommandId`, `LifecycleCommand.Parameters`. |All |
||[DescribeLifecycleHooks](https://docs.byteplus.com/en/docs/as/DescribeLifecycleHooks) |New response data: `LifecycleCommand`. |All |


<span id=".XzIwMjPlubQ45pyI"></span>
## August 2023


|Module |API name |Change record |Release regions |
|---|---|---|---|
|Scaling group |[CreateScalingGroup](https://docs.byteplus.com/en/docs/as/CreateScalingGroup) |New Request parameters `LaunchTemplateOverrides.N.InstanceType`, `DBInstanceIds.N`, `ScalingMode`, `HealthCheckType`, `ProjectName`, `Tags.N.Key`, `Tags.N.Value`, are optional. |All |
||[ModifyScalingGroup](https://docs.byteplus.com/en/docs/as/ModifyScalingGroup) |New request parameters `LaunchTemplateOverrides.N.InstanceType` and `HealthCheckType` (optional) are added. ||
||[DescribeScalingGroups](https://docs.byteplus.com/en/docs/as/DescribeScalingGroups) |* The optional `request parameter ProjectName`, `TagFilters.N.Key`, and `TagFilters.N.Value`, were added.<br><br>* New `response parameters`: `LaunchTemplateOverrides`, `DBInstanceIds`, `ScalingMode`, `StoppedInstanceCount`, `HealthCheckType`, `ProjectName`, `Tags`, and LoadBalancerHealthCheckGracePeriod. ||
|Instance management |[AttachInstances](https://docs.byteplus.com/en/docs/as/AttachInstances)<br><br>[DetachInstances](https://docs.byteplus.com/en/docs/as/DetachInstances) |The new request parameter `LifecycleHook` (optional) is added. ||
||[RemoveInstances](https://docs.byteplus.com/en/docs/as/RemoveInstances) |Added request parameters: `RemoveMode` and `LifecycleHook` (optional). ||
|Lifecycle hook |[CreateLifecycleHook](https://docs.byteplus.com/en/docs/as/CreateLifecycleHook)<br><br>[ModifyLifecycleHook](https://docs.byteplus.com/en/docs/as/ModifyLifecycleHook)<br><br>[CompleteLifecycleActivity](https://docs.byteplus.com/en/docs/as/CompleteLifecycleActivity) |Modifid request parameter: `LifecycleHookPolicy`, with new values added. ||
||[DescribeLifecycleHooks](https://docs.byteplus.com/en/docs/as/DescribeLifecycleHooks) |Modify response parameters: `LifecycleHookPolicy` adds values. ||
|Tag |[TagResources](https://docs.byteplus.com/en/docs/as/TagResources)<br><br>[UntagResources](https://docs.byteplus.com/en/docs/as/UntagResources)<br><br>[ListTagResources](https://docs.byteplus.com/en/docs/as/ListTagResources) |Added new APIs. ||


<span id=".XzIwMjPlubQwNuaciDI25pel"></span>
## June 26, 2023


|Module |API name |Change record |Release regions |
|---|---|---|---|
|Scaling group |[CreateScalingGroup](https://docs.byteplus.com/en/docs/as/CreateScalingGroup)<br><br>[AttachServerGroups](https://docs.byteplus.com/en/docs/as/AttachServerGroups)<br><br>[DetachServerGroups](https://docs.byteplus.com/en/docs/as/DetachServerGroups) |The optional request parameter `ClientToken` was added. |All |
|Lifecycle hook |[CompleteLifecycleActivity](https://docs.byteplus.com/en/docs/as/CompleteLifecycleActivity) |||
|Scaling configuration |[CreateScalingConfiguration](https://docs.byteplus.com/en/docs/as/CreateScalingConfiguration) |Added `HpcClusterId`, `Ipv6AddressCount`, and `ClientToken` as optional Request parameters. |All |
||[ModifyScalingConfiguration](https://docs.byteplus.com/en/docs/as/ModifyScalingConfiguration) |Added Request parameters `HpcClusterId` and `Ipv6AddressCount`, optional. |All |
||[DescribeScalingConfigurations](https://docs.byteplus.com/en/docs/as/DescribeScalingConfigurations) |Added Response parameters `HpcClusterId`, `Ipv6AddressCount`. |All |


<span id=".XzIwMjPlubQwMeaciDEx5pel"></span>
## January 11, 2023


|Module |API name |Change record |Release regions |
|---|---|---|---|
|Scaling group |[CreateScalingGroup](https://docs.byteplus.com/en/docs/as/CreateScalingGroup)<br><br>[ModifyScalingGroup](https://docs.byteplus.com/en/docs/as/ModifyScalingGroup) |Added request arguments `LaunchTemplateId`, `LaunchTemplateVersion`, both optional. |All |
||[DescribeScalingGroups](https://docs.byteplus.com/en/docs/as/DescribeScalingGroups) |The “**ScalingGroup structure**” adds response data `LaunchTemplateId` and `LaunchTemplateVersion` ||
|Scaling configuration |[CreateScalingConfiguration](https://docs.byteplus.com/en/docs/as/CreateScalingConfiguration)<br><br>[ModifyScalingConfiguration](https://docs.byteplus.com/en/docs/as/ModifyScalingConfiguration) |Added `SpotStrategy`, `ProjectName`, and `Tags` as optional request parameters. ||
||[DescribeScalingConfigurations](https://docs.byteplus.com/en/docs/as/DescribeScalingConfigurations) |New response data added to "**ScalingConfiguration structure**": `SpotStrategy`, `InstanceChargeType`, `ProjectName`, `Tags`. ||
|Instance management |[DescribeScalingInstances](https://docs.byteplus.com/en/docs/as/DescribeScalingInstances) |Added response data LaunchTemplateId and LaunchTemplateVersion to "ScalingInstance struct****`LaunchTemplateId and LaunchTemplateVersion to "ScLaunchTemplateVersion to "ScalingInstance structure`". ||


<span id=".XzIwMjLlubQwOeaciDAy5pel"></span>
## September 2, 2022


|Module |API name |Change record |Release regions |
|---|---|---|---|
|Scaling group |[CreateScalingGroup](https://docs.byteplus.com/en/docs/as/CreateScalingGroup) |Added optional request parameter `MultiAZPolicy`, modified the value range of request parameter `SubnetIds.N`. |All |
||[ModifyScalingGroup](https://docs.byteplus.com/en/docs/as/ModifyScalingGroup) |Modify request parameter `SubnetIds.N` value range. ||
||[DescribeScalingGroups](https://docs.byteplus.com/en/docs/as/DescribeScalingGroups) |**ScalingGroup structure** adds `MultiAZPolicy` response parameters. ||
|Lifecycle hook |[CreateLifecycleHook](https://docs.byteplus.com/en/docs/as/CreateLifecycleHook) |A new API for creating lifecycle hook. ||
||[ModifyLifecycleHook](https://docs.byteplus.com/en/docs/as/ModifyLifecycleHook) |Added an interface for modifying the lifecycle hook. ||
||[DescribeLifecycleHooks](https://docs.byteplus.com/en/docs/as/DescribeLifecycleHooks) |A new API for querying lifecycle hooks. ||
||[DeleteLifecycleHook](https://docs.byteplus.com/en/docs/as/DeleteLifecycleHook) |A new API for deleting lifecycle hooks. ||
||[DescribeLifecycleActivities](https://docs.byteplus.com/en/docs/as/DescribeLifecycleActivities) |A new API for querying lifecycle hook activities. ||
||[CompleteLifecycleActivity](https://docs.byteplus.com/en/docs/as/CompleteLifecycleActivity) |New interface for querying lifecycle hook activities. ||


<span id=".XzIwMjLlubQwN-aciDI25pel"></span>
## July 26, 2022


|Module |API name |Change record |Release regions |
|---|---|---|---|
|Scaling group |[CreateScalingGroup](https://docs.byteplus.com/en/docs/as/CreateScalingGroup) |Supplementary note: The scaling group created successfully through this interface defaults to selecting notification for successful and failed scaling activities. |All |


<span id=".XzIwMjLlubQwNuaciDA35pel"></span>
## June 7, 2022


|Module |API name |Change record |Release regions |
|---|---|---|---|
|Scaling group |[CreateScalingGroup](https://docs.byteplus.com/en/docs/as/CreateScalingGroup) |Modify the value range of `DefaultCooldown`. |All |
||[ModifyScalingGroup](https://docs.byteplus.com/en/docs/as/ModifyScalingGroup) |Add `DefaultCooldown` request parameters. ||
||[DescribeScalingGroups](https://docs.byteplus.com/en/docs/as/DescribeScalingGroups) |**Scaling group structure** adds `InstanceTerminatePolicy` Response parameters. ||
|Scaling configuration |[CreateScalingConfiguration](https://docs.byteplus.com/en/docs/as/CreateScalingConfiguration) |Added `Eip.BillingType` request parameter, modified the value range of `Eip.Bandwidth` and `Eip.ISP` request parameters. ||
||[ModifyScalingConfiguration](https://docs.byteplus.com/en/docs/as/ModifyScalingConfiguration) |Add `Eip.BillingType` request parameters, modify the values of `Eip.Bandwidth` and `Eip.ISP` request parameters. ||
||[DescribeScalingConfigurations](https://docs.byteplus.com/en/docs/as/DescribeScalingConfigurations) |**EIP structure** adds `BillingType` Response parameters. ||


<span id=".XzIwMjLlubQwNeaciDIz5pel"></span>
## May 23, 2022


|Module |API name |Update information |Release regions |
|---|---|---|---|
|Scaling group |[CreateScalingGroup](https://docs.byteplus.com/en/docs/as/CreateScalingGroup) |Modified the value range for the `MinInstanceNumber`, `MaxInstanceNumber`, and `DesireInstanceNumber` arguments. |All |
||[ModifyScalingGroup](https://docs.byteplus.com/en/docs/as/ModifyScalingGroup) |Modified the value range for the `MinInstanceNumber` and `MaxInstanceNumber` parameters. ||
|Instance management |[DescribeScalingInstances](https://docs.byteplus.com/en/docs/as/DescribeScalingInstances) |Modify the `Status` argument value range. ||
|Scaling rule |[CreateScalingPolicy](https://docs.byteplus.com/en/docs/as/CreateScalingPolicy) |Modify the value range of the `AdjustmentValue` argument ||
||[ModifyScalingPolicy](https://docs.byteplus.com/en/docs/as/ModifyScalingPolicy) |||


<span id=".XzIwMjLlubQwNeaciDEz5pel"></span>
## May 13, 2022


|Module |API name |Change record |Release regions |
|---|---|---|---|
|Auto scaling |All |For the first time, OpenAPI is opened, supporting creating, modifying, and deleting AS resources by calling OpenAPI. |All |
