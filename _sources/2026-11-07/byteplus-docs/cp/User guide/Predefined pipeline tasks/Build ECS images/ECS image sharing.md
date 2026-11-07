---
title: "ECS image sharing"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/ECS_image_sharing"
---

Support adding a preset task for ECS image sharing in the pipeline to enable image sharing across accounts or among organization members under the same account.This article describes the configuration method for the built\-in ECS image sharing task.

<span id="F7ngDasq"></span>
## Prerequisites


* Created ECS image:

   * To share your own image, you must first create a custom ECS image. For details, refer to [Custom images](https://docs.byteplus.com/en/docs/ecs/Custom-images).

   * To share an ECS image via upstream pipeline artifact, you must first configure the built\-in **ECS image creation** task. For details, refer to [ECS image creation](https://docs.byteplus.com/en/docs/cp/ECS_image_creation).

* (Optional) If you need to share it within the organization under this account, please first turn on enterprise organization. For details, refer to [turn on enterprise organization](https://docs.byteplus.com/en/docs/organization/ActivatingOrganizationService).


<span id="vlmafabE"></span>
## Add task

When creating or editing a pipeline, go to the **Process Orchestration** tab, click **Add Job**, and the **Add Job** drawer will pop up. For task templates, select **Others \> ECS image sharing**.

<span id="cxkOEp5N"></span>
## Parameter description

The following section introduces the parameters for this built\-in task.


* **Job name**

   Customize the job name.

* **Upstream task**

   Show the name of the upstream serial task for the current task. If there is no upstream task, `-` is displayed.

* **Task configuration**

   
   |Parameter |Description |
   |---|---|
   |Region |Select the Region of the ECS image to be shared. |
   |ECS image |Select the ECS image to be shared.<br><br><br>* Release artifact: Select the ECS image created by the upstream built\-in **ECS image creation** task.<br><br>* Custom: Select the ECS custom image you created yourself. |
   |Share type |Support sharing images across accounts or across organizations within the same account.<br><br><br>* Account: Enter the account ID(s) to share with; multiple IDs are supported. Share the image to the entered account ID(s).<br><br>* Organization: Share with all members under the organization of this account.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">[<a href="https://docs.byteplus.com/en/docs/cp/Apply_for_the_invitation-based_trial_feature"><strong>Beta \- apply for trial</strong></a>] The <strong>Organization</strong> type image sharing feature is currently open for beta. To experience this feature, please contact your pre\-sales manager or solution manager.</div><br><br><br>* <div data-tips="true" data-tips-type="default">After sharing is complete, you can view the shared images on the <strong>Instance and Image</strong> \> <strong>Image</strong> \> <strong>Shared images</strong> tab in the ECS console. For more information on shared image usage limits and descriptions, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Sharing-or-canceling-sharing-image">Share or Cancel Shared Image</a>.</div><br> |
   

* **Task output**

   No

* **Advanced settings**

   * [Webhook notification](https://docs.byteplus.com/en/docs/cp/Webhook_notification): Support pushing task\-level messages via Webhook and Feishu bot to help you stay informed about task updates.
