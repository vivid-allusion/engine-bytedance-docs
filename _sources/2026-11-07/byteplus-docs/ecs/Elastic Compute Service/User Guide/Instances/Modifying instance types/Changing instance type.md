---
title: "Changing instance type"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Modify-instance-type"
---

When using Pay\-as\-you\-go or Subscription instances, if you find that the current instance type (original type) cannot meet or exceeds application requirements, you can refer to this topic to change the instance to the target type (including vCPU and memory) for an upgrade or downgrade.

<span id=".5pON5L2c6K-05piO"></span>
## Operation instructions


|Time Period |Usage notes |Description |
|---|---|---|
|Before change |View scenarios where type change is supported |Please refer to [Instance types that support changing](https://docs.byteplus.com/en/docs/ecs/Overview-2) to confirm whether the current type (original type) support modification. |
||Instance state must be **Stopped** |You can refer to the [procedure](https://docs.byteplus.com/en/docs/ecs/Modify-instance-type#.5pON5L2c5q2l6aqk) to stop a **Running** instance, or manually [stop the instance](https://docs.byteplus.com/en/docs/ecs/Stopping-instances) before performing actions. |
||Install the Virtio1.1 driver (conditionally required) |3rd\-generation ECS instances (g3i/c3i/r3i/g3a/c3a/r3a) require the Virtio 1.1 driver to be installed before they can be used. Before you change instance type, check and confirm that the image you are using has the Virtio1.1 driver installed. For specific operations, please refer to [Installing Virtio1.1 driver](https://docs.byteplus.com/en/docs/ecs/Creating-Linux-images#.5a6J6KOFdmlydGlvMS0x6amx5Yqo). |
|During change |Do not perform any other operations on the instance before the operation is completed. Otherwise the change may fail. ||
|After change |The instance will be started immediately, and the new configuration will take effect in real time upon startup. Please confirm the impact on your business and proceed with caution. ||


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* For subscription ECS instances created using Windows images, you can change their instance types only to those in the same instance family.

* If the actual number of volumes mounted on the original type exceeds the volume quantity limit of the target type, you cannot change from the original type to the target type.

   > The number of volumes that can be mounted on different instance types varies. Please refer to the ["Volume Quantity"](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types#.5a6e5L6L6KeE5qC85peP5YiX6KGo) column of each type list.   
   

* When you change instances in batch, the instances to be changed must have the same **availability zone, billing method, and type**, and their state must be **Running** or **Stopped**. A maximum of 20 instances can be changed in a batch.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).  

2. In the left\-side navigation pane, select "Instances & Images \> Instances".

3. In the top menu bar, select the project and region of the target instance.

4. On the Instances page, enter the modification page by referring to the following methods.

   * Individual change: Click the "... \> Resource reallocation \> Modify instance type" button under the "Actions" column of the original type.

   * Batch change: Select the instances to be changed, and click the "Modify instance type" button at the bottom of the page.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Notes for batch change:      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">The multiple instances to be changed must have the same <strong>availability zone, billing method, and type</strong>, and their state must be <strong>Running</strong> or <strong>Stopped</strong>.      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">You can select up to 20 ECS instances each time.      </div>
      

5. Confirm the current configuration, and select "Agree to stop instance immediately" to stop the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the ECS instance is in the <strong>Stopped</strong> state, skip this step.   </div>
   

   6. Check the agreement: Please follow the console instructions to review and confirm the legal agreements.

7. Click the "Confirm" button to go to the application submission success page, and wait for the instance reconfiguration to complete.

8. Click the "Go to console" button to navigate to the Instances page. Here, you can view the reconfigured instance.

9. View configuration change results: After an instance is reconfigured, a corresponding system event is generated. You can view the status and details of events of the "Instance configuration changed" type on the "System Events" tab of the instance details page.

   You can also [subscribe to event notifications](https://docs.byteplus.com/en/docs/ecs/Receiving-event-notifications#.6K6i6ZiF5LqL5Lu26YCa55-l) to receive updates on instance configuration change results via internal messages, SMS, email, and other channels.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3643035ea072836390b2674819e32863.png) </span>


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[ModifyInstanceSpec - Modifies instance type](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceSpec)

<span id=".5bi46KeB6Zeu6aKY"></span>
## FAQ

[Adjusting instance configuration FAQ](https://docs.byteplus.com/en/docs/ecs/Instance-FAQs#.6LCD5pW05a6e5L6L6YWN572u6Zeu6aKY).
