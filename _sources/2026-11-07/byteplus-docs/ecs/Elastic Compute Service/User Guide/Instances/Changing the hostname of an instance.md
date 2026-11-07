---
title: "Changing the hostname of an instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Changing-the-hostname-of-an-instance"
---

The hostname is the internal computer name within the operating system of an instance. Each hostname identifies a computer. We recommend that you specify a unique hostname for each ECS instance. This topic describes how to change the hostname of an instance in the ECS console.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can specify a unique hostname when you create an ECS instance. For more information, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances">Purchasing an instance by following the wizard</a>.</div>


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Only instances in the **Running ** or **Stopped ** state support hostname changes.

* After the change, you need to [restart the instance](https://docs.byteplus.com/en/docs/ecs/Restarting-instances) for the new hostname to take effect.

* Instances created using CentOS 6.9/6.10 or Ubuntu 14.04 do not support hostname changes.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


<Tabs>
<Tab zoneid="H9pCxKJRwB" title="Change one instance hostname">
<TabTitle>Change one instance hostname</TabTitle>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before changing the hostname, ensure that the reset\-authentication plug\-in has been upgraded to the specified version. <a href="https://docs.byteplus.com/en/docs/ecs/Updating-the-password-plug-in">Learn more</a></div>



1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, select "Instances & Images \> Instances".

3. In the top menu bar, select the region and project of the target instance.

4. On the "Instances" page, click the "··· \> Instances property \> Change instance hostname" button in the "Actions" column on the right of the target instance.

5. In the pop\-up dialog box, enter a new hostname.

6. Select the "Agree to restart Instances now" checkbox to apply the changes. You can also manually [restart the instance](https://docs.byteplus.com/en/docs/ecs/Restarting-instances) after the operation is complete.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Selecting the "Agree to restart Instances now" check\-box will interrupt your business. Proceed with caution.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After selecting immediate restart, the <strong>Running</strong> ECS instances will restart by default, and the <strong>Stopped</strong> ECS instances will start by default.   </div>
   

7. Click "Save" to complete the operation.


</Tab>
<Tab zoneid="pZ3TXrvvNK" title="Change multiple instance hostnames">
<TabTitle>Change multiple instance hostnames</TabTitle>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">This action is supported by the orchestration service, which by default uses the CustomerRoleForOOS role to submit operations. If you have not yet created this role, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Preparation">Orchestration permission management</a> to enable it.</div>


* <div data-tips="true" data-tips-type="warning">You can also refer to <a href="https://docs.byteplus.com/en/docs/ecs/Creating_a_batch_actions_instance_task">Create batch instance tasks</a> to directly modify instance attributes (including the instance name, hostname, and description) on the orchestration page.</div>


* <div data-tips="true" data-tips-type="warning">If the instance state is <strong>Running</strong>, changing the hostname will cause the instance to automatically restart.</div>


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, select "Instances & Images \> Instances".

3. In the top menu bar, select the region and project where the target instance resides.

4. On the Instances page, select one or more instances to modify and click the "··· \> Modify instance attribute" button at the bottom of the list.

5. In the pop\-up window, click the "Continue" button to navigate to the orchestration page and modify the relevant attributes. For specific configurations, please refer to [Creating batch instance tasks - Modifying attributes](https://docs.byteplus.com/en/docs/ecs/Creating_a_batch_actions_instance_task).


</Tab>
</Tabs>


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [How to view the instance hostname?](https://docs.byteplus.com/en/docs/ecs/Instance-FAQs#.5aaC5L2V5p-l55yL5a6e5L6L55qE5Li75py65ZCN77yf)

* [ModifyInstanceAttribute - Modifies instance information](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceAttribute)
