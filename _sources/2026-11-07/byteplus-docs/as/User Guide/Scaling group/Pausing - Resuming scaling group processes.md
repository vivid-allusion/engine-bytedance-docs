---
title: "Pausing/Resuming scaling group processes"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/suspensionresumption-of-scaling-group-processes"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenario

By default, a scaling group automatically executes [adjustments](https://docs.byteplus.com/en/docs/as/Adjustment-types), such as instance scaling triggered by health checks or scaling tasks. You may need precise control over adjustments, such as pausing adjustments to perform other operations on instances or enabling automatic scaling again after resuming the adjustments. You can refer to this topic to pause or resume the scaling process of a scaling group.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This operation only provides process\-level control for scaling group scale\-out or scale\-in. To achieve instance\-level control, we recommend that you use the following two features:</div>



* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/as/Setting-instance-scale-in-protection">Configure instance protection</a>: Instances in the protected state will not be automatically removed or deleted.</div>


* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/as/Setting-instance-standby">Configure standby instances</a>: Instances in the standby state will no longer receive business traffic, their load balancing weight will be set to zero, and they will not be automatically removed or deleted.</div>



<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

When the scaling group is in **Locked** or **Deleting** status, this operation is not supported.

<span id=".5Ly457yp57uE5rWB56iL57G75Z6L"></span>
## Scaling group process types


|Scaling group process type |Impact of pause on the scaling group |Impact of resuming on the scaling group |
|---|---|---|
|Scale\-in process |* The scaling group will no longer execute scale\-in operations, including [automatic instance scale-in](https://docs.byteplus.com/en/docs/as/Removing-instances-manually) and manual instance [removal](https://docs.byteplus.com/en/docs/as/Removing-instances-automatically) or [deletion](https://docs.byteplus.com/en/docs/as/Deleting-instances-manually).<br><br>* If the expected instance count feature is enabled, you can modify the [expected instance count](https://docs.byteplus.com/en/docs/as/Desire-instance-number-capacity#.5L-u5pS55pyf5pyb5a6e5L6L5pWwL-WuuemHjw==), but this will not change the number of instances in the scaling group. |* The scaling group will resume the execution of all scale\-in operations, including [automatic instance scale-in](https://docs.byteplus.com/en/docs/as/Removing-instances-manually) and manual instance [removal](https://docs.byteplus.com/en/docs/as/Removing-instances-automatically) or [deletion](https://docs.byteplus.com/en/docs/as/Deleting-instances-manually).<br><br>* If the expected instance count feature is enabled and the [expected instance count](https://docs.byteplus.com/en/docs/as/Desire-instance-number-capacity#.5L-u5pS55pyf5pyb5a6e5L6L5pWwL-WuuemHjw==) is modified during the pause, the scaling group will automatically remove or delete instances based on the updated expected instance count once scaling group processes are resumed. |
|Scale\-out process |* The scaling group will no longer execute scale\-out operations, including [automatic instance scale-out](https://docs.byteplus.com/en/docs/as/Adding-instances-automatically) and manual instance [addition](https://docs.byteplus.com/en/docs/as/Adding-instances-manually).<br><br>* If the expected instance count feature is enabled, you can [modify the expected instance count](https://docs.byteplus.com/en/docs/as/Desire-instance-number-capacity#.5L-u5pS55pyf5pyb5a6e5L6L5pWwL-WuuemHjw==), but this will not change the number of instances in the scaling group. |* The scaling group will resume all scale\-out operations, including [automatic instance scale-out](https://docs.byteplus.com/en/docs/as/Adding-instances-automatically) and manual instance [addition](https://docs.byteplus.com/en/docs/as/Adding-instances-manually).<br><br>* If the expected instance count feature is enabled and [the expected instance count is modified](https://docs.byteplus.com/en/docs/as/Desire-instance-number-capacity#.5L-u5pS55pyf5pyb5a6e5L6L5pWwL-WuuemHjw==) during the pause, the scaling group will automatically add instances based on the updated expected instance count once scaling group processes are resumed. |
|Health Check |The [health check](https://docs.byteplus.com/en/docs/as/Health-checks) capability is paused and unhealthy instances are not removed or deleted even if they exist in the scaling group. |The [health check](https://docs.byteplus.com/en/docs/as/Health-checks) capability is recovered and unhealthy instances are automatically removed. |
|Alert task |When [alert tasks](https://docs.byteplus.com/en/docs/as/Overview-of-scaling-policys#.5Ly457yp6KeE5YiZ57G75Z6L) are created for the scaling group, adjustments will not be executed even if the trigger conditions of the tasks are met. |When [alert tasks](https://docs.byteplus.com/en/docs/as/Overview-of-scaling-policys#.5Ly457yp6KeE5YiZ57G75Z6L) are created for the scaling group and the trigger conditions of the tasks are met, adjustments will be resumed. |
|Scheduled tasks |When [scheduled/periodic tasks](https://docs.byteplus.com/en/docs/as/Overview-of-scaling-policys#.5Ly457yp6KeE5YiZ57G75Z6L) are created for the scaling group, adjustments will not be executed even if the trigger time has arrived. |When [scheduled/periodic tasks](https://docs.byteplus.com/en/docs/as/Overview-of-scaling-policys#.5Ly457yp6KeE5YiZ57G75Z6L) are created for the scaling group and the trigger time of the tasks has not yet arrived, adjustments will be resumed. |


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Scaling Group console](https://console.byteplus.com/as/group). 

2. In the top menu bar, select the project and region of your target resource.

3. Click the name of the scaling group and select the "Overview" tab.

4. Click the edit button to the right of "Suspended process", and then select or clear the scaling group process types.

5. Click the "OK" button to complete the operation.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [SuspendProcesses](https://docs.byteplus.com/en/docs/as/SuspendProcesses): Pauses scaling group processes

* [ResumeProcesse](https://docs.byteplus.com/en/docs/as/ResumeProcesses): Resumes scaling group processes
