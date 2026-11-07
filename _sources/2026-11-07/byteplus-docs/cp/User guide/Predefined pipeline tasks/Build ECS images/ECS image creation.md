---
title: "ECS image creation"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/ECS_image_creation"
---

Supports adding a built\-in task for creating an ECS image in the pipeline. This article describes the configuration method for the ECS image creation built\-in task.

<span id="MVvhQU31"></span>
## Prerequisites


* (Optional) To create an ECS instance image using the custom method, you must first create an ECS instance. For details, refer to [Create cloud server instance](https://docs.byteplus.com/en/docs/ecs/Buying-and-using-ECS-instances).

* (Optional) To create an ECS instance image using the upstream artifact method in the pipeline, you must first configure the **ECS instance creation** built\-in task. For details, refer to [ECS instance creation](https://docs.byteplus.com/en/docs/cp/Create_ECS_instance).


<span id="mGhXN7U0"></span>
## Add task

When creating or editing a pipeline, go to the **Process Orchestration** tab, click **Add Job**, and the **Add Job** drawer will pop up. In the task templates, select Others ** \> ECS image creation**.

<span id="oS0T1n1j"></span>
## Parameter description

The following sections describe the parameters for this built\-in task.


* **Task name**

   Specify the task name.

* **Upstream task**

   Displays the name of the upstream serial task for the current task. If there is no upstream task, it is displayed as `-`.

* **Task configuration**

   
   |Parameter |Description |
   |---|---|
   |Region |Select the region for ECS image creation. |
   |ECS instance |Select the ECS instance for which the image will be created.<br><br><br>* Upstream artifact: Select the ECS instance created by the upstream built\-in task **ECS instance creation ** .<br><br>* Custom: Select the ECS instance you created in the cloud service. |
   |Image name |Specify the name of the ECS instance image to be created. |
   

* **Task output**

   Displays the ID of the ECS image to be created.

* **Advanced settings**

   * [Webhook notification](https://docs.byteplus.com/en/docs/cp/Webhook_notification): Supports sending task\-level messages via Webhook and Larkbot to help you stay informed about task updates.
