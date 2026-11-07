---
title: "Managing applications"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Managing_applications"
---

The platform provides the application management feature for you to easily manage the version, model, and other configurations of agents (such as OpenClaw) deployed in instances through application templates.

<span id="m8oPglXX"></span>
## Prerequisites


* Your instance is created using an application template. [Learn more](https://docs.byteplus.com/en/docs/6396/2189942).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you have changed the operating system with an image not associated with an application template (such as a custom image), you will not be able to use this feature. In this case, you can <a href="https://docs.byteplus.com/en/docs/ecs/Creating_application_update_tasks">create an OpenClaw (Linux) system reinstallation task</a> to reinstall the instance operating system, and this feature will become available again.   </div>
   

* You have authorized the cloud assistant to assume the required role. Otherwise, follow the instructions on the page and click the "Authorize" button to complete authorization.


<span id="drbzhKdg"></span>
## Upgrade the agent version

You can quickly upgrade the agent deployed in the current instance to the latest version maintained by BytePlus while retaining the agent (such as OpenClaw) data.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The upgraded version is the latest version adapted by BytePlus based on the community version, not the latest version published by the community.</div>


* <div data-tips="true" data-tips-type="warning">To prevent irreversible data loss, the platform will automatically create a snapshot to back up instance data before the upgrade.</div>


   * <div data-tips="true" data-tips-type="warning"><a href="https://console.byteplus.com/ebs/region:ebs+cn-beijing/snap">Enable the snapshot service</a> before upgrading the version.</div>


   * <div data-tips="true" data-tips-type="warning">Creating snapshots may incur certain fees. <a href="https://docs.byteplus.com/en/docs/ecs/Snapshot_billing">Learn more</a>.</div>


   * <div data-tips="true" data-tips-type="warning">The snapshot will be automatically deleted one day after the upgrade. You may also <a href="https://docs.byteplus.com/en/docs/ecs/Delete-a-snapshot">delete it manually</a> in advance.</div>


   * <div data-tips="true" data-tips-type="warning">If the upgrade fails, you can <a href="https://docs.byteplus.com/en/docs/ecs/Rollback-volume-through-snapshot">use the snapshot to roll back</a> and restore instance data.</div>


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, select "Instances & Images \> Instances".

3. In the top menu bar, select the project and region of the target instance.

4. Click the name of the target instance to enter its details page.

5. Select the "Application Management" tab and click the "Version upgrade" button.

6. In the pop\-up window, click the "Confirm" button to confirm the agent version upgrade.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">During the upgrade, the agent will enter the <strong>Upgrading</strong> state. It will return to the <strong>Running</strong> state after the configuration succeeds.   </div>
   

<span id="VUnu2XKi"></span>
## Synchronize agent data

If no agent data is displayed on the "Application template" tab or the displayed data is abnormal, you can initiate a data synchronization to synchronize the configuration information of the agent (such as OpenClaw) deployed in the instance to the console for unified viewing and management.


1. Click the "Data synchronization" button to synchronize data.

2. In the pop\-up window, click the "Confirm" button to confirm data synchronization.

3. After data synchronization starts, the agent changes to the **Synchronizing** status.

4. After data synchronization is completed, the agent will return to the **Running** state, and the data displayed on the current tab will be refreshed.


<span id="E4ut3Qak"></span>
## Manage agent model

You can configure the inference model for the agent, or modify the configured model information and switch to another model to provide inference services for the agent.


1. Enter the model configuration process.

   * If your agent has not been configured with a model, click the "Configure now" button.

   * If your agent has been configured with a model and you want to change it, click the "Change configuration" button.

2. Configure the parameters described in the following table.

   
   |Parameter​ |Description |
   |---|---|
   |Configuration method |* **Foundation models**: Supports LLMs from "Foundation models" of ModelArk. Multiple model services, including Doubao\-Seed\-Code, GLM\-4.7, DeepSeek\-V3.2, and Kimi\-K2\-Thinking, are now fully compatible with the OpenClaw technical ecosystem.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you have not activated the ModelArk service, after you select a model and create an instance, the platform will automatically activate the selected model service for you. After that, the model will be <a href="https://docs.byteplus.com/en/docs/82379/1544681">billed by token</a>.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">OpenClaw deployed via the "OpenClaw" application template is integrated with common Skills from AgentKit. It natively supports multimodal capabilities like image and video generation. To use related capabilities, first <a href="https://console.byteplus.com/ark/region:ark+cn-beijing/openManagement?LLM=%7B%7D&advancedActiveKey=model">enable the corresponding models</a>, and select the target models such as doubao\-seedream\-4\-5 (251128) or doubao\-seedance\-1\-5\-pro (251215).   </div><br>   <br><br>* **Coding Plan**: ModelArk Coding Plan is a subscription service tailored for developers for AI coding scenarios. It supports the use and free switching of mainstream code models (including the latest versions of Doubao\-Seed\-Code, GLM, Kimi, DeepSeek, and more).<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can go to the ModelArk <a href="https://www.byteplus.com/en/activity/codingplan">Coding Plan</a> promotion page, and click the "Subscribe now" button to subscribe to a package as needed.   </div><br>    |
   |API Key |Select the API Key you want to use from the drop\-down list.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Keep your ModelArk API Key secure. If leaked, it could allow third parties to impersonate you for unauthorized use, causing unexpected token fees.</div><br> |
   

3. Click the "Confirm" button to submit the configuration request.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">During the configuration, the agent will enter the <strong>Updating</strong> state. It will return to the <strong>Running</strong> state after the configuration succeeds.   </div>
   

4. After the configuration, you can view the details of the model currently used by the agent.

   If you have selected the Coding Plan and its included models, you can view the Coding Plan quota usage, and click the "Renew" button to go to the ModelArk console for renewal.


<span id="NSVKuc66"></span>
## Manage message channels

If your agent supports message channel configuration, you can quickly complete message channel integration through simple configuration (for example, integrate the Feishu application as the message channel for OpenClaw).


1. Enter the message channel configuration process.

   * If your agent has not been configured with a message channel, click the "Configure now" button.

   * If your agent has been configured with a message channel and you want to configure a new one, click the "Message channel configuration" button.

2. Select the required message channel type and configure the following parameters.

   * **Telegram**

      After the update, the agent will automatically use the Telegram bot as the message notification channel.

      * **BotToken**: The access token for the target bot.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">You can refer to the following steps to create a Telegram bot and obtain the relevant information.      </div>
      

      1. <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Log in to your Telegram and search for <code>@Botfather</code>.      </div>
      

      2. <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Send <code>/newbot</code> to <code>@Botfather</code> to create a new bot.      </div>
      

      3. <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">After creating the bot, you can obtain the bot access token from <code>@Botfather</code>'s reply. The format is: <code>123:abc</code>.      </div>
      

4. Click the "Confirm" button to submit the configuration request.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">During the configuration, the agent will enter the <strong>Updating</strong> state. It will return to the <strong>Running</strong> state after the configuration succeeds.   </div>
   

5. After the configuration, you can view the message channel currently used by the agent.
