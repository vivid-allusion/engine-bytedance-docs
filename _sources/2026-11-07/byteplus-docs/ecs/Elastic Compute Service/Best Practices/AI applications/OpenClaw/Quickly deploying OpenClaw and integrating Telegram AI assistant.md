---
title: "Quickly deploying OpenClaw and integrating Telegram AI assistant"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Deploying_OpenClaw_rapidly_and_integrating_Telegram_AI_assistant"
---

OpenClaw is an open\-source, local\-first AI agent and automation platform. With OpenClaw, you can deeply integrate multi\-channel communication capabilities with large language models to build a customized AI assistant with persistent memory and proactive execution capabilities.

This topic describes how to quickly deploy OpenClaw on an ECS instance in two scenarios and configure your customized private AI assistant in Telegram.

<span id="qeQePttX"></span>
## Change history

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To <strong>upgrade</strong> or <strong>reset</strong> OpenClaw deployed on the ECS instance, you can <a href="https://docs.byteplus.com/en/docs/ecs/Creating_application_update_tasks">create an OpenClaw application update task</a> to complete the operation.</div>



|Update time |Description |
|---|---|
|March 5, 2026 |Added support for the latest features of the **Community Edition released on March 2, 2026**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can upgrade ECS instances created via the old version of the application template by following the <a href="https://docs.byteplus.com/en/docs/ecs/OpenClaw_deployment_FAQ#xCkp2KYB">solution</a> guide.</div><br> |
|February 27, 2026 |Added support for the latest features of the **Community Edition released on February 23, 2026**. |
|February 10, 2026 |Added support for the latest features of the Community Edition **up to February 6, 2026**. |


<span id="pEjb6Nnp"></span>
## Prerequisites


* You have completed [account registration](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account) on BytePlus.

* You have a Telegram account.


<span id="vkFrT6gz"></span>
## Configure the model and integrate Telegram during ECS instance purchase

<span id="tSdPTy3H"></span>
### Step 1: Create an ECS instance


1. [Click here](https://console.byteplus.com/ecs/region:ecs+ap-southeast-1/buy?projectName=default&type=app) to log in to the ECS console.

2. Quickly purchase an ECS instance pre\-installed with OpenClaw by using an application template, and configure the following parameters.

   
   |Parameter​ |Description |
   |---|---|
   |**Instance configuration** ||
   |Application template |Select "OpenClaw". |
   |Billing method |Select the billing method of the instance. In this topic, "Subscription" is selected as an example. [Learn more](https://docs.byteplus.com/en/docs/ecs/Billing-methods). |
   |Region |Select the region where the instance is located. In the example provided in this topic, Asia Pacific (Johor) is used.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Currently, only China (Beijing), China (Shanghai), Asia Pacific (Johor), and Asia Pacific (Jakarta) are supported. <a href="https://docs.byteplus.com/en/docs/ecs/Regions-and-Availability-Zones">Learn more</a>.</div><br> |
   |Package specification |Select the instance type. Select 2 vCPU, 2 GiB memory or higher. This topic uses the "e\-c1m1, 2 vCPU, 2 GiB" type as an example. |
   |Login password |Configure the instance login password. |
   |Confirm password |Re\-enter the instance login password for confirmation. |
   |Role authorized |Select whether to complete the required role authorization for the cloud assistant.<br><br><br>*  **(Recommended)**  Authorize: Check the "Confirm authorized Cloud assistant roles" option. You can perform version upgrades, data synchronization, and other related operations only after the authorization is complete.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After authorization, you can use the application management feature to view your Coding Plan quota usage, upgrade OpenClaw versions, and manage its associated models and message channels. <a href="https://docs.byteplus.com/en/docs/ecs/Managing_applications">Learn more</a>.   </div><br>   <br><br>* Do not authorize: You cannot use the related services. |
   |**Advanced configuration**: ||
   |Model configuration |Select and configure a model on the ModelArk platform. OpenClaw will use this model for inference after your ECS instance starts.<br><br><br>* **Model selection**: Supports LLMs from "Foundation models" of ModelArk. Multiple model services, including ByteDance\-Seed\-Code, GLM\-4.7, DeepSeek\-V3.2, and Kimi\-K2\-Thinking, are now fully compatible with the OpenClaw technical ecosystem.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you have not activated the ModelArk service, after you select a model and create an instance, the platform will automatically activate the selected model service for you. After that, the model will be <a href="https://docs.byteplus.com/en/docs/ModelArk/1544106">billed by token</a>.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">OpenClaw deployed via the "OpenClaw" application template is integrated with common Skills from AgentKit. It natively supports multimodal capabilities like image and video generation. To use these capabilities, please <a href="https://console.byteplus.com/ark/region:ark+ap-southeast-1/openManagement?LLM=%7B%7D&advancedActiveKey=model">go to enable</a> and then select the bytedance\-seedance\-1\-5\-pro (251215) model.   </div><br>   <br><br>* **API Key**: Go to "ModelArk \> [API keys](https://console.byteplus.com/ark/region:ark+ap-southeast-1/apiKey?apikey=%7B%7D)" to create and retrieve your API Key.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Keep your ModelArk API Key secure. If leaked, it could allow third parties to impersonate you for unauthorized use, causing unexpected token fees.   </div><br>    |
   |Telegram integration |After "Telegram integration" is configured, OpenClaw will automatically connect to the Telegram message channel when the ECS instance starts.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can refer to the following steps to create a Telegram bot and obtain the relevant information.</div><br><br><br><br>1. <div data-tips="true" data-tips-type="default">Log in to your Telegram and search for <code>@Botfather</code>.</div><br><br><br>2. <div data-tips="true" data-tips-type="default">Send <code>/newbot</code> to <code>@Botfather</code> to create a new bot.</div><br><br><br>3. <div data-tips="true" data-tips-type="default">After creating the bot, you can obtain the bot access token from <code>@Botfather</code>'s reply. The format is: <code>123:abc</code>.</div><br> |
   

3. In the "Configuration details" section on the right, confirm the instance configuration and fee, and check "I have read and agree with Elastic Compute Service Terms of Service".

4. Click the "Buy now" button to complete the purchase.

5. You can also click the "Go to console" button to view the specifications of the newly created instance on the instance list page. You can also [log in to the instance through the console](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_39da8163b004eda94a54076075c36cdb.png) </span>


<span id="IKgAqVhP"></span>
### Step 2: Configure the OpenClaw Telegram AI assistant


1. Obtain the Telegram bot pairing code.

   1. In your Telegram, open the bot created earlier.

   2. Send `/start` to it, and obtain and record the pairing code from the bot's reply.

2. Configure OpenClaw.

   1. [Log in to the ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

   2. Execute the following command to associate the Telegram bot information with OpenClaw.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code><Pairing Code></code> with the Telegram bot Pairing Code obtained earlier.      </div>
      

      ```Bash
      openclaw pairing approve telegram <Pairing Code>
      ```
      

      If the output contains "Approved telegram sender xxx", the configuration succeeds.

3. Subsequently, your Telegram bot will serve as a customized personal AI assistant, completing various tasks you assign.


<span id="8x012CjQ"></span>
## Configure the model and integrate Telegram after ECS instance purchase

<span id="HzckDWU6"></span>
### Step 1: Create an ECS instance


1. [Click here](https://console.byteplus.com/ecs/region:ecs+ap-southeast-1/buy?projectName=default&type=app) to log in to the ECS console.

2. Quickly purchase an ECS instance pre\-installed with OpenClaw by using an application template, and configure the following parameters.

   
   |Parameter​ |Description |
   |---|---|
   |**Instance configuration** ||
   |Application template |Select "OpenClaw". |
   |Billing method |Select the billing method of the instance. In this topic, "Subscription" is selected as an example. [Learn more](https://docs.byteplus.com/en/docs/ecs/Billing-methods). |
   |Region |Select the region where the instance is located. In the example provided in this topic, Asia Pacific (Johor) is used.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Currently, only China (Beijing), China (Shanghai), Asia Pacific (Johor), and Asia Pacific (Jakarta) are supported. <a href="https://docs.byteplus.com/en/docs/ecs/Regions-and-Availability-Zones">Learn more</a>.</div><br> |
   |Package specification |Select the instance type. Select 2 vCPU, 2 GiB memory or higher. This topic uses the "e\-c1m1, 2 vCPU, 2 GiB" type as an example. |
   |Login password |Configure the instance login password. |
   |Confirm password |Re\-enter the instance login password for confirmation. |
   |Role authorized |Select whether to complete the required role authorization for the cloud assistant.<br><br><br>*  **(Recommended)**  Authorize: Check the "Confirm authorized Cloud assistant roles" option. You can perform version upgrades, data synchronization, and other related operations only after the authorization is complete.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After authorization, you can use the application management feature to view your Coding Plan quota usage, upgrade OpenClaw versions, and manage its associated models and message channels. <a href="https://docs.byteplus.com/en/docs/ecs/Managing_applications">Learn more</a>.   </div><br>   <br><br>* Do not authorize: You cannot use the related services. |
   |**Advanced configuration**: Configure the parameters in this section after you purchase the ECS instance. Retain the default settings when you purchase the ECS instance. ||
   

3. In the "Configuration details" section on the right, confirm the instance configuration and fee, and check "I have read and agree with Elastic Compute Service Terms of Service".

4. Click the "Buy now" button to complete the purchase.

5. You can also click the "Go to console" button to view the specifications of the newly created instance on the instance list page. You can also [log in to the instance through the console](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_39da8163b004eda94a54076075c36cdb.png) </span>


<span id="xZ5rTIGf"></span>
### Step 2: Create a Telegram bot and obtain the configuration


1. Create a Telegram bot.

   1. Log in to your Telegram and search for `@Botfather`.

   2. Send `/newbot` to `@Botfather` to create a new bot.

   3. After creating the bot, you can obtain the bot access token from `@Botfather`'s reply. The format is: `123:abc`.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The bot access token will be used to configure OpenClaw. Store it securely.      </div>
      

2. Obtain the Telegram bot pairing code.

   1. In your Telegram, open the bot created earlier.

   2. Send `/start` to it, and obtain and record the pairing code from the bot's reply.


<span id="oSVpL5d2"></span>
### Step 3: Configure the OpenClaw Telegram AI assistant


1. [Log in to the ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Configure the model and Telegram bot access token.

   1. Execute the following command to download and run the configuration script.

      ```Bash
      bash <(curl -fsSL https://openclaw.tos-cn-beijing.volces.com/config-tool.sh) 
      ```
      

   2. Configure model\-related parameters.

      1. Enter `1` and press Enter to start the model configuration process.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b550b2663b41ad558b3d978f9673957e.png) </span>

      2. Confirm whether to use the Coding Plan and its supported models.

         * If you have subscribed and want to use the Coding Plan, enter `yes` and press Enter to confirm.

         * If you have not subscribed to the ModelArk Coding Plan or do not want to use the Coding Plan, enter `no` and press Enter to confirm.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_54eb0e5de9deb818532617e654ef8472.png) </span>

      3. Follow the instructions to configure the ModelArk API Key and the ModelArk model you want OpenClaw to use, in sequence.

         <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="3">warning         </div>
         

         * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="3">If you do not use the Coding Plan, enter the ID of the ModelArk model you want to use.         </div>
         

         * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="3">If you use the Coding Plan, enter the name of the supported model. Follow the guide on the <a href="https://docs.byteplus.com/en/docs/ModelArk/1928261">Configure model name (via config file)</a> tab to obtain the model name.         </div>
         

      4. After successful configuration, press Enter to return to the main process interface.

   3. Configure the Telegram bot access token.

      1. Enter `4` and press Enter to start the Telegram application information configuration process.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7439ed223e1b8075479da6982e9e718e.png) </span>

      2. Follow the instructions to configure the Telegram bot access token. When the "Telegram configured!" message is displayed, press Enter to complete the configuration.

   1. Enter `6` and press Enter to restart the service. When the "Gateway restarted!" message is displayed, the service has been restarted. Press Enter to return to the home page.

   2. Enter `0` and press Enter to exit the configuration process.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1f17080aa7339f048dc3c24f79aed05c.png) </span>

3. Execute the following command to associate the Telegram bot information with OpenClaw.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code><Pairing Code></code> with the Telegram bot Pairing Code obtained earlier.   </div>
   

   ```Bash
   openclaw pairing approve telegram <Pairing Code>
   ```
   

   If the output contains "Approved telegram sender xxx", the configuration succeeds.

4. Subsequently, your Telegram bot will serve as a customized personal AI assistant, completing various tasks you assign.


<span id="6xmIhkrn"></span>
## Configure the ModelArk Coding Plan

To switch to a subscribed [Coding Plan](https://www.byteplus.com/en/activity/codingplan) and its supported models, follow the instructions in this section to adjust the OpenClaw configuration.


1. [Log in to the ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to modify the OpenClaw configuration.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code><your_key></code> with the <a href="https://console.byteplus.com/ark/region:ark+cn-beijing/apiKey?apikey=%7B%7D">API Key</a> you created in ModelArk.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code><model_name></code> with the model name included in the Coding Plan. The <code>bytedance-seed-code</code>, <code>glm-4.7</code>, <code>deepseek-v3.2</code>, <code>kimi-k2.5</code>, and <code>gpt-oss-120b</code> models are supported.   </div>
   

   ```Bash
   openclaw config set models.providers.ark.baseUrl https://ark.cn-beijing.volces.com/api/coding/v3
   openclaw config set models.providers.ark.apiKey <your_key>
   openclaw config set models.providers.ark.models[0].id <model_name>
   openclaw config set models.providers.ark.models[0].name <model_name>
   openclaw models set ark/<model_name>
   openclaw gateway restart
   ```
