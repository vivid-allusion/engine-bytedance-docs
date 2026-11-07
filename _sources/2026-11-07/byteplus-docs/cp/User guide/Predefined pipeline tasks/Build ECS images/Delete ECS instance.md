---
title: "Delete ECS instance"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Delete_ECS_instance"
---

Supports adding a built\-in task to delete ECS instances in the pipeline, releasing ECS instances that are no longer needed. This article describes the configuration method for the built\-in ECS instance deletion task.

<span id="xh6Ot70w"></span>
## Prerequisites


* (Optional) To delete ECS instances created using the custom method, you must first create the ECS instance. For details, refer to [Create cloud server instance](https://docs.byteplus.com/en/docs/ecs/Buying-and-using-ECS-instances).

* (Optional) To delete ECS instances created using upstream pipeline artifacts, you must first configure the built\-in **ECS instance creation** task. For details, refer to [ECS instance creation](https://docs.byteplus.com/en/docs/cp/Create_ECS_instance).


<span id="bZLHZNDt"></span>
## Add task

When creating or editing a pipeline, go to the **Process Orchestration** tab, click **Add Job**, and the **Add Job** drawer will pop up. Select **Others \> Delete ECS instance** from the task templates.

<span id="SMP3sBeR"></span>
## Parameter description

The following section introduces the parameters for this built\-in task.


* **Job name**

   Custom job name.

* **Upstream task**

   Shows the name of the upstream serial task for the current task. If there is no upstream task, `-` will be displayed.

* **Task configuration**

   
   |Parameter |Description |
   |---|---|
   |Region |Select the region of the ECS instance to be deleted. |
   |ECS instance |Select the ECS instance to be deleted.<br><br><br>* Online artifact: Select the ECS instance created by the upstream built\-in **ECS instance creation** task.<br><br>* Custom: Select the ECS instance created independently in the cloud service. |
   

* **Task output**

   No

* **Advanced settings**

   * [Webhook notification](https://docs.byteplus.com/en/docs/cp/Webhook_notification): Supports pushing task\-level messages via Webhook and Larkbot, so you can stay informed about task status.
