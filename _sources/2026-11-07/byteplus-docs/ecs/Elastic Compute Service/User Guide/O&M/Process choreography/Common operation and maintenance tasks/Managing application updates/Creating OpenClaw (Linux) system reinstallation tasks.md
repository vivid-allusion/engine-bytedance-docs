---
title: "Creating OpenClaw (Linux) system reinstallation tasks"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Creating_application_update_tasks"
---

You can use the application update feature of Orchestration to reinstall the operating system of your ECS instance with the latest image that includes the newest application version. No additional purchase or reconfiguration is required, significantly reducing deployment time and costs.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Currently, only the following regions are supported: China (Beijing), China (Shanghai), China (Guangzhou), Asia Pacific (Johor), and Asia Pacific (Jakarta). <a href="https://docs.byteplus.com/en/docs/ecs/Regions-and-Availability-Zones">Learn more</a>.</div>


<span id="zHN8zQ7Y"></span>
## Applicable scenarios


|ECS instance |Scenarios |Description |
|---|---|---|
|ECS instance with OpenClaw already deployed |Update to latest version |Follow BytePlus version updates without repurchasing or reconfiguring the instance. Simply reinstall the operating system of your existing instance to the latest version to use the latest OpenClaw capabilities supported by BytePlus on your original ECS instance. |
||Restore to the initial state |For any ECS instance that needs to be restored to its initial OpenClaw state, you can reset the operating system to its initial state using this method. |
|ECS instance without OpenClaw deployed |Deploy OpenClaw on an existing ECS instance |Reinstall the operating system to convert an existing ECS instance without a preinstalled OpenClaw application into an ECS instance with a preinstalled OpenClaw application. No additional purchase or configuration is required, significantly reducing deployment time and costs. |


<span id="KeqWViOU"></span>
## Usage notes

Operating system reinstallation is a high\-risk operation. Read and fully understand the following usage notes before proceeding:

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The application update feature reinstalls the operating system using a brand\-new application image, and the operation is irreversible. Proceed with caution.</div>


* <div data-tips="true" data-tips-type="warning">Reinstalling the operating system restores the system volume to its initial state (all data on the system volume, including saved configurations and logs, is cleared and cannot be recovered). We recommend that you <a href="https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration">back up your system volume data</a> in advance. To back up OpenClaw context data, follow the <a href="https://docs.byteplus.com/en/docs/ecs/Back_up_data">OpenClaw data backup and recovery</a> guide.</div>



<span id="r2FdKoPw"></span>
## Prerequisites


* [Cloud assistant Agent](https://docs.byteplus.com/en/docs/ecs/Install-the-Cloud-Assistant-client) has been installed on the instance for which you want to reinstall the operating system.

* To configure the model and complete notification channel integration in the application update task, obtain the following information based on the notification channel to be integrated:

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can also configure the following information after creating and executing the application update task. For details, see the advanced configuration section in the procedure.   </div>
   

   
   |Required information |Notification channels |Description |
   |---|---|---|
   |Model API Key |Telegram integration |* If you do not use the Coding Plan, obtain the ID of the ModelArk model you want to use.<br><br>* If you use the Coding Plan, obtain the name of the supported model. Currently supported: bytedance\-seed\-code.  |
   |BotToken |Telegram integration |BotToken: The token for accessing the bot.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can refer to the following steps to create a Telegram bot and obtain the relevant information.</div><br><br><br><br>1. <div data-tips="true" data-tips-type="default">Log in to your Telegram and search for <code>@Botfather</code>.</div><br><br><br>2. <div data-tips="true" data-tips-type="default">Send <code>/newbot</code> to <code>@Botfather</code> to create a new bot.</div><br><br><br>3. <div data-tips="true" data-tips-type="default">After creating the bot, you can obtain the bot access token from <code>@Botfather</code>'s reply. The format is: <code>123:abc</code>. <a href="https://docs.byteplus.com/en/docs/ecs/Deploying_OpenClaw_rapidly_and_integrating_Telegram_AI_assistant">Learn more</a>.</div><br> |
   


<span id="ZcfUlG7m"></span>
## Procedure


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, click "Maintenance & Monitoring \> Orchestration".

3. In the top menu bar, select the region and project of your business.

4. On the "CloudOps Orchestration" page, click the "Common O&M tasks" tab and select "App update".

5. Click the "Create task" button and configure the parameters described in the following table.

   
   |Parameter​ ||Description |
   |---|---|---|
   |**Application configuration** |||
   |Application template ||The OpenClaw application deployed by the user. The default value is "OpenClaw" and cannot be modified. |
   |Task template ||The preset standardized O&M process template. Select "Reinstall operating system". |
   |**Login credentials** |||
   |Reset password ||Configure the instance login password.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Instances after batch operating system reinstallation will share the same new login credentials you configured. Keep your password secure. You can also <a href="https://docs.byteplus.com/en/docs/ecs/Resetting-passwords">reset the login password</a> separately for the target instance.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">We recommend that you increase password complexity to improve security.</div><br> |
   |Confirm password ||Re\-enter the instance login password for confirmation. |
   |**Select instances** |||
   |Select instances ||Select the instance for which you want to reinstall the operating system.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If the target ECS instance is preconfigured with OpenClaw, use the filter "Application template: OpenClaw" for faster searching. Otherwise, clear the filter to select your instance.</div><br><br><br> |
   |**Advanced configuration (optional)** <br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The model and notification channel integration parameters in this section can also be configured after the task is executed. For details, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Deploying_OpenClaw_rapidly_and_integrating_Telegram_AI_assistant#8x012CjQ">Configure the model and integrate Telegram after ECS instance purchase</a>.</div><br> |||
   |Model configuration ||After you configure the model on the ModelArk platform, OpenClaw will use this model for inference after your ECS instance starts. For details, see [Configure the model and integrate Telegram during ECS instance](https://docs.byteplus.com/en/docs/ecs/Deploying_OpenClaw_rapidly_and_integrating_Telegram_AI_assistant?lang=en#vkFrT6gz).  |
   |Message channel integration |Feishu integration |Enter the App Id and App Secret of the Feishu bot. For details, see Prerequisites. |
   ||WeCom integration |Enter the Token and EncodingAESKey of the WeCom bot. For details, see Prerequisites. |
   ||DingTalk integration |Enter the Client ID and Client Secret of the DingTalk application. For details, see Prerequisites. |
   ||Telegram |Enter the Telegram BotToken. For details, see Prerequisites. |
   |**Relevant information** |||
   |Associated project | |You can add the application update task to the project and manage it in a centralized manner by project dimension, which helps maintain resource independence and ensure data security. [Learn more](https://docs.byteplus.com/en/docs/ecs/Managing-projects).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">After you select a project, new instances that meet the conditions automatically match the application update task.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The project displayed here is the one you selected in Step 3. You can change the project in the top menu bar.</div><br> |
   |Tag | |Optional. Used to select the scope of instances the application update task applies to based on tags. Click the "Add tag" button, and then select or enter the tag key and its corresponding tag value.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Up to 20 tags can be added.</div><br><br><br>* <div data-tips="true" data-tips-type="default">A tag is a key\-value pair used to identify cloud resources. Tags help you categorize resources based on different dimensions, such as purpose, owner, or environment. This allows you to search and aggregate your resources. <a href="https://docs.byteplus.com/en/docs/ecs/Tag-overview">Learn more</a>.</div><br> |
   

6. Click "Create".

7. After you confirm that the information to be updated is correct, click the "Confirm" button to start reinstalling the system.


<span id="uClll7sz"></span>
## Expected results


* **Reinstallation succeeded**

   The reinstallation completes, and the instance starts automatically in approximately 3 to 5 minutes. Its status is updated to **Running** synchronously. 

* **Reinstallation failed**

   The instance will enter an abnormal state and fail to start. All original data on the system volume will be cleared and cannot be recovered. [Submit a ticket](https://console.byteplus.com/workorder/create) to obtain technical support.
