---
title: "Lark-Side Intelligent Agent Configuration and Testing"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Lark-Side_Intelligent_Agent_Configuration_and_Testing"
---

This article introduces the relevant operations for configuring the Feishu\-side of the intelligent analysis Agent.

<span id="6cc702fd"></span>
# Prerequisites


* The operations for purchasing, enabling, creating a project, and preparing data have been completed. For details, see [Guide to Building an Intelligent Agent from 0 to 1](https://docs.byteplus.com/docs/dataagent/Guide_to_Building_an_Intelligent_Agent_from_0_to_1).

* To integrate the intelligent analysis Agent with Feishu applications, before referring to the configuration steps below for Feishu\-side integration, contact the operations administrator to configure the Feishu office platform in the office platform integration. Once completed, you can then configure the Feishu\-side integration in the intelligent analysis Agent. For detailed steps, see [Office Platform Integration](https://docs.byteplus.com/docs/dataagent/Office_Platform_Integration).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2fb115b1fa24f6b8cdacbde2ac5d00b~tplv-goo7wpa0wc-image.image) </span>


<span id="6cd78b72"></span>
# Create an intelligent agent


1. Create a new intelligent agent. Go to the configuration page of the intelligent analysis Agent configuration, click "Create intelligent agent" in the upper right corner to enter the initial configuration page for the agent.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1354e5797ebf4148be125888a3588aa5~tplv-goo7wpa0wc-image.image) </span>

2. General configuration for the intelligent agent. Configure the avatar, name, description, administrator, and other basic information for the intelligent agent. After configuration, click "Save".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4fd287b56ee94839945783c4ebe50f79~tplv-goo7wpa0wc-image.image) </span>

3. Obtain the callback address. Click and copy the "Feishu callback address" below the agent name.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ba3b0df300ee45569f5bd085186775f9~tplv-goo7wpa0wc-image.image) </span>


<span id="b329dfba"></span>
# Feishu\-side preparation

<span id="d2b6f33f"></span>
### Step 1: Apply for a Feishu bot


1. Apply for a Feishu bot. To create a Feishu bot, go to [Lark open platform](https://open.larkoffice.com/app) and select "Create enterprise self\-built application".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f37dec5c084440be968f1a2f4f89fda8~tplv-goo7wpa0wc-image.image) </span>

2. Create an enterprise self\-built application.

   * In the pop\-up window for creating an enterprise self\-built application, enter the application name, description, and icon. The application name will correspond to the agent name that users search for in Feishu.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/86a2e2eab6ea432dbff7af76941a6c2c~tplv-goo7wpa0wc-image.image) </span>

   * After entering the information, click "Create" to create an application.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b799e345f55b488a8175efd8cd36ff7c~tplv-goo7wpa0wc-image.image) </span>

3. Add bot capabilities to the created application. First, go to the application's configuration page, select "Add application capabilities" on the left, and choose to add "Bot".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2b4023e596fd4fce99d8f7646d98ddde~tplv-goo7wpa0wc-image.image) </span>

4. Add the required permissions for the bot\*\*.\*\* To enable normal interaction for the bot, you need to add certain permissions to the bot. You can find "Permission management" in "Development configuration" on the left. In permission management, select "Batch import/export permissions", check the options, and enable permissions in bulk.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/38325f06087c45a49464e3df009f12db~tplv-goo7wpa0wc-image.image) </span>

   The permissions that need to be enabled are as follows:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/893976fc2ce047f780290ac55113eed3~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b71534427c614c7897dab1fc60c7d415~tplv-goo7wpa0wc-image.image) </span>

   Users can directly copy the code below and then **paste it in the permission import section**:

   ```JSON
   {
     "scopes": {
       "tenant": [
         "admin:app.info:readonly",
         "application:application:self_manage",
         "contact:contact.base:readonly",
         "contact:user.employee_id:readonly",
         "contact:user.id:readonly",
         "im:chat:read",
         "im:chat:update",
         "im:message.group_at_msg:readonly",
         "im:message.group_msg",
         "im:message.p2p_msg:readonly",
         "im:message.pins:read",
         "im:message.pins:write_only",
         "im:message.reactions:read",
         "im:message.reactions:write_only",
         "im:message:readonly",
         "im:message:recall",
         "im:message:send_as_bot",
         "im:message:send_multi_depts",
         "im:message:send_multi_users",
         "im:message:update",
         "im:resource",
         "im:user_agent:read"
       ],
       "user": [
         "contact:user.employee_id:readonly",
         "contact:user.id:readonly",
         "drive:drive.metadata:readonly",
         "drive:drive:version",
         "drive:drive:version:readonly",
         "im:chat:read",
         "im:message:readonly",
         "im:message:update"
       ]
     }
   }
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the agent is a <strong>group chat agent:</strong>   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Add <code>"im:chat:read"</code> and <code>"im:message.group_at_msg:readonly"</code> in "tenant". Caution: Do not add <code>im:message.group_msg</code>, otherwise the agent will respond to all messages in the group.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To use the <strong>download data to Feishu</strong> feature:   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Add <code>"drive:drive.metadata:readonly"</code> and <code>"drive:drive"</code> in "user".   </div>
   

5. After configuring the permissions, publish the Feishu bot\*\*.\*\* Once you have filled in the required permissions for the bot, you can create a version and publish it on the "Version management and publishing" page. The version number, description, and other information, as well as the application reason, can be filled in as needed.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e80db5f805044a5fa12090be5e18c8e7~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Before proceeding to the next step, you must publish the enterprise application, otherwise you cannot continue.   </div>
   

<span id="a418f47b"></span>
### Step 2: Create a new agent and associate it with the bot


1. Configure the request address for the bot\*\*.\*\* Return to the Feishu bot page created in the previous step, and paste the copied callback address into the request address fields in the "Event and callback" page under "Event configuration" and "Callback configuration".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/20ba5a0f801c476e869e871b16d38d08~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Both event configuration and callback configuration need to be added.   </div>
   

2. Configure events for the bot. After entering the address, you also need to "Add event" separately for both event and callback configurations.

   * The event configuration needs to add: im.message.receive_v1, p2p_chat_create

   * The callback configuration needs to add: card.action.trigger_v1

3. Publish the bot. After completing the previous steps, you can publish the bot once by creating a version and publishing it on the "Version management and publishing" page. The version number and description, as well as other information, can be filled in as needed.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e80db5f805044a5fa12090be5e18c8e7~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Before proceeding to the next step, you must publish the enterprise application, otherwise you cannot continue.   </div>
   

4. Obtain the App ID and App Secret of the Feishu bot. After publishing the Feishu bot, return to the bot's configuration page and copy the App ID and App Secret separately from the "Credentials and basic information" page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6e55458cef594aa9ada6974efcdfd9e6~tplv-goo7wpa0wc-image.image) </span>

5. (Optional) Configure an encryption policy.

   * When the agent is used for external scenarios or special cases that require encrypted request content, you can choose to configure an encryption policy for the agent; **if the agent is only for internal company colleagues, configuration is generally not required.** 

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a3d8e4ad94a7482b8a776da0c5bb1215~tplv-goo7wpa0wc-image.image) </span>


<span id="6adaaffd"></span>
### Step 3: Add available members for the agent


1. Add members entry point.

   * The available members of the agent are the available members of the bound robot, so you need to add on the [Lark Open Platform](https://open.larkoffice.com/app/).

2. Add members. Edit the available members of the robot. Search for users and select them as needed. Do not select "All members".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/662e8cd8a6b94b5fafbd99eb852002f5~tplv-goo7wpa0wc-image.image) </span>

3. Save and publish. After adding, simply save and publish. Note that publishing is required for the changes to take effect.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e80db5f805044a5fa12090be5e18c8e7~tplv-goo7wpa0wc-image.image) </span>


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">In addition to being added as available members, users of the agent must also have at least view permissions for the dataset currently bound to the agent in order to use the agent normally. For detailed permission configuration steps, refer to <a href="https://docs.byteplus.com/docs/dataagent/Intelligent_Analysis_Agent_Administrator_Quick_Start_Guide">Intelligent Analysis Agent Administrator Quick Start Guide</a>.</div>


<span id="90b110f5"></span>
# Agent Feishu endpoint configuration


1. Enable the Feishu endpoint. Go to the configuration page of the previously created agent, find "Feishu endpoint configuration" under "Basic Information", and select "Enable Feishu endpoint".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/65956bf650db42d3adf0b43b7fe3cbba~tplv-goo7wpa0wc-image.image) </span>

2. Add the agent. Enter the App ID and App Secret of the Feishu robot in the Feishu basic settings. Click "Save" in the upper right corner. The agent will then be associated with the Feishu robot. See [Step 2: Create a new agent and associate it with the bot](https://docs.byteplus.com/docs/dataagent/Lark-Side_Intelligent_Agent_Configuration_and_Testing#a418f47b) for how to obtain it.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f172b99282e94fc2a1a619ed50a73032~tplv-goo7wpa0wc-image.image) </span>

3. (Optional) Configure the encryption policy. Fill in the "Encryption type" and "Verification code" on the agent configuration page, then save. See [Step 2: Create a new agent and associate it with the bot](https://docs.byteplus.com/docs/dataagent/Lark-Side_Intelligent_Agent_Configuration_and_Testing#a418f47b) for how to obtain it.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fcdd1a58ced3416aab754c840fdcfc6c~tplv-goo7wpa0wc-image.image) </span>

4. Add a dataset to the agent. After configuration, click "Publish". The agent will appear in the list of published agents.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/317cb20f0e464af8950ff7c03ac93c44~tplv-goo7wpa0wc-image.image) </span>

5. Click "Publish" to publish the agent.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6e4c0780965348baa67d25c2bd804c19~tplv-goo7wpa0wc-image.image) </span>

<span id="0321d73c"></span>
# Using the agent on the Feishu endpoint

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After configuration is completed, the Feishu intelligent agent can also be used directly on the web platform.</div>


For agents on the Feishu endpoint, after publishing, you can search for the agent name in Feishu and click to use it.
