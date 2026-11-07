---
title: "Lifecycle hook overview"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Overview-of-lifecycle-hooks"
---

After the scaling group triggers the scaling rule, health check, or instance quantity check, the lifecycle hook can suspend the "Adding", "Removing", and "Disabling" instance status, and target instances enter the **Adding/removal suspended** state. At this time, instances are in a pending state. You can perform custom actions during this period until the lifecycle hook times out, or manually end the suspension.

<span id=".6YCC55So5Zy65pmv"></span>
## Applicable scenarios


* After an instance is added to a scaling group, it is initialized (such as installing or configuring software) or associated with one or multiple secondary network interfaces. Then, it needs to be associated with Load Balancer to provide external services.

* Before you remove or delete an instance from a scaling group, back up the relevant data or download logs first to prevent data loss.

* Before you remove or delete an instance from a scaling group, disassociate it from Load Balancer first. Besides, make sure that all requests received by the instance are processed, and your business will not be impacted.


<span id=".55u45YWz5Yqf6IO9"></span>
## Related features

In scenarios where a large number of instances are added to or removed from a batch, lifecycle hooks support association with Cloud assistant, allowing you to conveniently execute operation and maintenance commands on a single execution object or multiple execution objects. This feature enables you to select one O&M command and execute it across multiple instances, significantly improving maintenance efficiency.

Before associating the lifecycle hook with the Cloud assistant, you need to first complete the following preparations.


* Create required O&M command: BytePlus offers preset public commands of different types for common O&M operations. You can select an appropriate command based on your needs or create a custom command. Refer to [Cloud assistant command management](https://docs.byteplus.com/en/docs/ecs/Managing-commands) to view public commands or to create custom commands, then return to this page to make your selection.

* Install the Cloud assistant Agent on the instance: Instances that are automatically scaled up through Auto Scaling (AS) come with the client preinstalled by default. For instances you manually add to, you need to install the client in advance. Please refer to [Install the Cloud assistant Agent](https://docs.byteplus.com/en/docs/ecs/Install-the-Cloud-Assistant-client) to complete the installation.


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* The maximum number of lifecycle hooks that can be created for one scaling group is 6.

* Lifecycle hooks take effect for [adjustments](https://docs.byteplus.com/en/docs/as/Adjustment-types) triggered by scaling rules, health checks, and instance quantity checks. Adjustments triggered by manual scaling do not support this feature.

* When an instance is in a suspended state after scaling, the scaling group enters the **Locked** status and does not perform any adjustments.

* [Deleting a scaling group](https://docs.byteplus.com/en/docs/as/Deleting-a-scaling-group) is an action to clear resources within the group, and therefore does not trigger lifecycle hooks.


<span id=".5omn6KGM5rWB56iL5ZKM562W55Wl"></span>
## Execution process and policy

After a lifecycle hook is triggered, execution processes and policies for adding and removing instances differ slightly due to the suspension state. Details are listed below:


|Lifecycle hook adjustment |Start time of suspended state |End time of suspended state |Scale\-out after suspension ends |
|---|---|---|---|
|Triggered lifecycle hook for scale\-out |An instance enters the suspended state after being created and before being associated with Load Balancer. |* When the lifecycle hook reaches the timeout period or [Cloud assistant commands](https://docs.byteplus.com/en/docs/ecs/Managing-commands) fail to execute, the pending state ends, and Auto Scaling (AS) proceeds with the scale\-out/scale\-in adjustment based on the hook's execution policy.<br><br>* When [Cloud assistant commands](https://docs.byteplus.com/en/docs/ecs/Managing-commands) execute successfully, the pending state ends, and Auto Scaling (AS) proceeds with the scale\-out/scale\-in adjustment based on the "Continue" policy.<br><br>* After a scale\-out instance enters the suspended state, if it is deleted in the ECS console, the suspended state ends. The scale\-out adjustment continues based on the "Reject" policy. |* If the execution policy is "Continue", the instance is then associated with Load Balancer and provides services externally.<br><br>* If the execution policy is "Reject" or "Roll back", the instance and associated resources will be reverted and deleted, and a new instance will be created in the scaling group. |
|Triggered lifecycle hook for scale\-in |An instance enters the suspended state after being disassociated with Load Balancer. ||* When the execution policy is "Continue" or "Reject", instances are then removed.<br><br>* When the execution policy is "Roll back", the instance is reverted to the state before it was removed. Then, it needs to be removed again.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Whether the instance and the associated resources are deleted during removal depends on whether the instance is entrusted and under scale\-in protection. For details, refer to <a href="https://docs.byteplus.com/en/docs/as/Instance-lifecycle#.5a6e5L6L55Sf5ZG95ZGo5pyf566h55CG">Instance lifecycle management</a>.</div><br> |
|Simultaneously triggered lifecycle hooks |All lifecycle hooks whose trigger conditions (which refer to scale\-in and scale\-out adjustments mentioned above) are met can be triggered. If they are not manually completed, after the longest timeout period is reached among the hooks, the execution policy of that hook will be performed. When the timeout periods of all hooks are the same, the "Reject" policy takes precedence over the "Continue" policy. In other words, if you specified "Reject" as the execution policy for one triggered hook, adjustment activity is executed based on the "Reject" policy. |||
