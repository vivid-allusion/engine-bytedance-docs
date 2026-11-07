---
title: "API overview"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/API-overview"
---

Auto Scaling provides the following API operations.

<span id=".5Ly457yp57uE"></span>
## Scaling group


|API name |Feature |
|---|---|
|[CreateScalingGroup](https://docs.byteplus.com/en/docs/as/CreateScalingGroup) |Create a scaling group |
|[ModifyScalingGroup](https://docs.byteplus.com/en/docs/as/ModifyScalingGroup) |Modify basic information and associated subnet of a scaling group |
|[DescribeScalingGroups](https://docs.byteplus.com/en/docs/as/DescribeScalingGroups) |Obtain scaling group information |
|[DeleteScalingGroup](https://docs.byteplus.com/en/docs/as/DeleteScalingGroup) |Delete a scaling group |
|[EnableScalingGroup](https://docs.byteplus.com/en/docs/as/EnableScalingGroup) |Enable a scaling group |
|[DisableScalingGroup](https://docs.byteplus.com/en/docs/as/DisableScalingGroup) |Disable a scaling group |
|[AttachServerGroups](https://docs.byteplus.com/en/docs/as/AttachServerGroups) |Associate one or multiple Load Balancer backend server groups with a scaling group |
|[DetachServerGroups](https://docs.byteplus.com/en/docs/as/DetachServerGroups) |Disassociate one or multiple Load Balancer backend server groups from a scaling group |
|[SuspendProcesses](https://docs.byteplus.com/en/docs/as/SuspendProcesses) |Pause specified processes in a scaling group |
|[ResumeProcesses](https://docs.byteplus.com/en/docs/as/ResumeProcesses) |Resume paused processes in a scaling group |


<span id=".5Ly457yp6YWN572u"></span>
## Scaling configurations


|API name |Feature |
|---|---|
|[CreateScalingConfiguration](https://docs.byteplus.com/en/docs/as/CreateScalingConfiguration) |Create a scaling configuration |
|[ModifyScalingConfiguration](https://docs.byteplus.com/en/docs/as/ModifyScalingConfiguration) |Modify a scaling configuration |
|[DeleteScalingConfiguration](https://docs.byteplus.com/en/docs/as/DeleteScalingConfiguration) |Delete a scaling configuration |
|[DescribeScalingConfigurations](https://docs.byteplus.com/en/docs/as/DescribeScalingConfigurations) |Query scaling configuration information |
|[EnableScalingConfiguration](https://docs.byteplus.com/en/docs/as/EnableScalingConfiguration) |Associate a specified scaling configuration with a scaling group |


<span id=".5a6e5L6L566h55CG"></span>
## Instance management


|API name |Feature |
|---|---|
|[DescribeScalingInstances](https://docs.byteplus.com/en/docs/as/DescribeScalingInstances) |Query instance information in a scaling group |
|[AttachInstances](https://docs.byteplus.com/en/docs/as/AttachInstances) |Manually add one or multiple instances to a scaling group |
|[DetachInstances](https://docs.byteplus.com/en/docs/as/DetachInstances) |Remove one or multiple instances from a scaling group |
|[RemoveInstances](https://docs.byteplus.com/en/docs/as/RemoveInstances) |Delete instances in a scaling group |
|[SetInstancesProtection](https://docs.byteplus.com/en/docs/as/SetInstancesProtection) |Enable protection for instances in a scaling group that you do not want to be automatically deleted/removed |
|[EnterStandby](https://docs.byteplus.com/en/docs/as/EnterStandby) |Set an ECS instance in a scaling group to standby status |
|[ExitStandby](https://docs.byteplus.com/en/docs/as/ExitStandby) |Remove an ECS instance in a scaling group from standby status |


<span id=".5Ly457yp6KeE5YiZ"></span>
## Scaling rule


|API name |Feature |
|---|---|
|[CreateScalingPolicy](https://docs.byteplus.com/en/docs/as/CreateScalingPolicy) |Create a scaling rule |
|[ModifyScalingPolicy](https://docs.byteplus.com/en/docs/as/ModifyScalingPolicy) |Modify a scaling rule |
|[DeleteScalingPolicy](https://docs.byteplus.com/en/docs/as/DeleteScalingPolicy) |Delete a scaling rule |
|[EnableScalingPolicy](https://docs.byteplus.com/en/docs/as/EnableScalingPolicy) |Enable a scaling rule |
|[DisableScalingPolicy](https://docs.byteplus.com/en/docs/as/DisableScalingPolicy) |Disable a scaling rule |
|[DescribeScalingPolicies](https://docs.byteplus.com/en/docs/as/DescribeScalingPolicies) |Query scaling rules |


<span id=".55Sf5ZG95ZGo5pyf5oyC6ZKp"></span>
## Lifecycle hook


|API name |Feature |
|---|---|
|[CreateLifecycleHook](https://docs.byteplus.com/en/docs/as/CreateLifecycleHook) |Create a lifecycle hook |
|[ModifyLifecycleHook](https://docs.byteplus.com/en/docs/as/ModifyLifecycleHook) |Modify a lifecycle hook |
|[DescribeLifecycleHooks](https://docs.byteplus.com/en/docs/as/DescribeLifecycleHooks) |Query lifecycle hooks |
|[DeleteLifecycleHook](https://docs.byteplus.com/en/docs/as/DeleteLifecycleHook) |Delete a lifecycle hook |
|[DescribeLifecycleActivities](https://docs.byteplus.com/en/docs/as/DescribeLifecycleActivities) |Query lifecycle hook activities |
|[CompleteLifecycleActivity](https://docs.byteplus.com/en/docs/as/CompleteLifecycleActivity) |Manually complete suspension triggered by a lifecycle hook |


<span id=".5Ly457yp5pel5b-X"></span>
## Scaling log


|API name |Feature |
|---|---|
|[DescribeScalingActivities](https://docs.byteplus.com/en/docs/as/DescribeScalingActivities) |Query scaling log |
