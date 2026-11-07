---
title: "ECS image cross-region copy"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/ECS_image_cross-region_copy"
---

Supports adding the built\-in ECS image cross\-region copy task in the pipeline. This article describes how to configure the built\-in ECS image cross\-region copy task.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The <a href="https://docs.byteplus.com/en/docs/ecs/CopyImage">CopyImage</a> function, which this feature depends on, is currently in the invitation\-only beta phase on ECS. For a trial, please contact your account manager to apply.</div>


<span id="7ak29l9N"></span>
## Prerequisites

An ECS image has been created.


* When copying your own image across regions, you must first create a custom ECS image. For details, refer to [Custom images](https://docs.byteplus.com/en/docs/ecs/Custom-images).

* When copying an ECS image using the pipeline upstream artifact method, you must first configure the **ECS image creation** built\-in task. For details, refer to [ECS image creation](https://docs.byteplus.com/en/docs/cp/ECS_image_creation).


<span id="um0eUHUN"></span>
## Add task

When creating or editing a pipeline, go to the **Process Orchestration** tab, click **Add Job**, and the **Add Job** drawer will pop up. For task templates, select **Others \> ECS image cross\-region copy**.

<span id="NH09s2zr"></span>
## Parameter description

The following describes the parameters for this built\-in task.


* **Job name**

   Customize the job name.

* **Upstream task**

   Displays the name of the upstream serial task for the current task. If there is no upstream task, `-` will be displayed.

* **Task configuration**

   
   |Parameter |Description |
   |---|---|
   |Source region |Select the region where the ECS image to be copied is located. |
   |ECS image |Select the ECS image to be copied.<br><br><br>* Online artifact: Select the ECS image created by the upstream built\-in task, **ECS image creation**.<br><br>* Custom: Select the custom ECS image you created. |
   |Target region |Select the target region for copying the ECS image.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The target region and source region must not be the same.</div><br> |
   

* **Task output**

   ID of the new ECS image after copying.

* **Advanced settings**

   * [Webhook notification](https://docs.byteplus.com/en/docs/cp/Webhook_notification): Supports pushing task\-level messages via Webhook and Feishu bot, helping you stay informed about task updates in a timely manner.
