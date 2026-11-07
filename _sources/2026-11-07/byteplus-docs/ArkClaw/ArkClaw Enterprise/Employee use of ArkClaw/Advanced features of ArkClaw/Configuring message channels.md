---
title: "Configuring message channels"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Configuring_message_channels__"
---

This topic describes how to integrate bot message channels with ArkClaw. After the integration, you can chat with ArkClaw through the corresponding bot. ArkClaw can also use bot capabilities to help you perform operations such as creating documents and creating calendar entries.

<span id="ZUKitsVP"></span>
## Integrate Telegram

<span id="U9SronjN"></span>
### Step 1: Create a Telegram bot and obtain the information

If you already have a Telegram bot and possess its access token, skip this step.


1. Log in to your Telegram and search for `@Botfather`.

2. Send `/newbot` to `@Botfather` to create a new bot.

3. After creating the bot, you can obtain the bot access token from `@Botfather`'s reply. The format is: `123:abc`.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The bot access token will be used to configure OpenClaw. Store it securely.   </div>
   

<span id="BaTCGEro"></span>
### Step 2: Configure Telegram bot information in ArkClaw


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter to access the ArkClaw conversation page.

2. Switch to the target ArkClaw instance page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cb7e3a8f9a4aa1a5b53934536e0827f1.png) </span>

3. Click "... \> Configure message channel" in the upper\-right corner of the conversation page or click the "Configure message channel" button on the page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91f7cce2c48051fafe5a7e223005cd01.png) </span>

4. The first time you associate with a channel, select "Connect Telegram". If it is not the first time you associate with a message channel, click the "Add" button and select "Telegram".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4df9c873bf92e9aee7e6b53cf6f20eb2.png) </span>

5. Enter the bot Token you obtained, and click the "Confirm" button to submit the configuration request.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4cc614c369c664c62e56c980f0f89f77.png) </span>

6. Once ArkClaw completes the update, the Telegram bot information is configured successfully.


<span id="pZU50Hfq"></span>
## Integrate a Lark/Feishu bot

<span id="RJYroW5O"></span>
### Step 1: Integrate a bot

Simply scan the QR code via the Lark/Feishu app for authorization, and ArkClaw can quickly establish a connection with your Lark/Feishu bot.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If a Lark/Feishu bot has already been configured for your ArkClaw, the existing bot information will be overwritten by the new one.</div>



1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter to access the ArkClaw conversation page.

2. Switch to the target ArkClaw instance page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cb7e3a8f9a4aa1a5b53934536e0827f1.png) </span>

3. Click "... \> Configure message channel" in the upper\-right corner of the conversation page or click the "Configure message channel" button on the page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91f7cce2c48051fafe5a7e223005cd01.png) </span>

4. The first time you associate with a channel, select "Connect Lark or Feishu". If it is not the first time you associate with a message channel, click the "Add" button and select "Lark or Feishu".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_582661b3dd07830f0e33e22a73dca1cc.png) </span>

5. Click the "Generate QR code" button to generate a QR code for pairing.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After scanning the QR code, you need to enter the bot name and complete the creation within 10 minutes. If the operation times out, scan the QR code again to create the bot.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91a40994c3de870016954b66b3ed1d02.png) </span>

6. After the QR code is generated, use the Lark/Feishu app installed on your phone to scan the QR code.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Scan the QR code and create a bot using a Lark/Feishu account with ArkClaw Enterprise permissions. For example: Your enterprise Lark/Feishu account is eligible for ArkClaw Enterprise, yet you create a Lark/Feishu bot using your personal Lark/Feishu account. After successful creation, you will fail to access ArkClaw properly via this Lark/Feishu bot.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_714b541edfce1f0649443fada2e2dda4.png) </span>

7. Enter the bot name.

   * **Create a new bot**: Click the "Create now" button to start creating a new bot and configure the workflow.

   * **Use an existing bot**: Click the "Existing application" button and select the bot you want to use. If the selected bot lacks required permissions and authorization is needed, click the "View" button next to the permissions on the authorization page to view permissions required by the Lark/Feishu bot associated with ArkClaw. Click "Confirm" after verification.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After scanning the QR code, you need to enter the bot name and create the bot within 10 minutes. If the operation times out, scan the QR code again to create the bot.   </div>
   

8. When a message similar to the following example is displayed, it indicates that ArkClaw has completed the Lark/Feishu bot configuration. You can close the message channel configuration page.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">During the configuration process, ArkClaw needs to restart the gateway. Please wait for the process to complete. If there is no response for a long time, we recommend that you <a href="https://docs.byteplus.com/en/docs/ArkClaw/Restoring_ArkClaw_to_factory_settings__">restore ArkClaw to its factory settings</a> and configure the bot information again by following the instructions in this step.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6aaf567fc3e7036d86b00431e96616d9.png) </span>

9. Return to your Lark/Feishu app, click the "Open application" button. You can interact with ArkClaw via the bot.


<span id="HrLMDp4A"></span>
### Step 2: Enable persistent bot connection (optional)

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">After configuring bot information in ArkClaw, refer to this step to enable persistent bot connection if you want the bot to keep receiving messages and run stably in the backend without interruptions. You may skip this step if you only use the bot occasionally.</div>



1. Log in to the [Lark/Feishu Open Platform](https://open.larksuite.com/app).

2. Select the "Custom Apps" tab, and click the Lark open application you created.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0d9f3826de56a281eb681f773f04336a.png) </span>

3. In the directory tree on the left, select "Development Configuration \> Events and callbacks", and enable long connection in the event configuration and callback configuration.

   
   **Event configuration process**
   
   
   1. Select the "Event Configuration" tab, and click the edit button next to "Subscription mode".
   
      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d9c473be6f19a75186b6850ca4ac9874.png) </span>
   
   2. Select "Receive events through **persistent connection**" and click the "Save" button.
   
      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e200959181784485fe89df2f8f1875c4.png) </span>
   
   3. In the "Events added" section, click the "Add Events" button.
   
      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_65de29f2f76d85d889272ab2f919270f.png) </span>
   
   4. In the "Add Events" dialog box, select the "Tenant Token\-Based Subscription" tab. Search for "Message" and check "Message received", "reaction.created", and "reaction.deleted". Then, click "Add".
   
      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1d1614f89a9e102c44011ab675b4f8c9.png) </span>
   
   5.  **(Optional)**  If you want to add the bot to a chat group, refer to the following instructions to enable the permission to obtain group messages. Otherwise, skip this step.
   
      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
      
   
      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">As OpenClaw is designed as a personal AI assistant, using it in group chats may pose risks such as credential leakage. Use it with caution.   </div>
      
   
   
   **Procedure for enabling the "Obtain group message" permission**
   
   
   1. In the "Events added" module, click the "Expand" button in the "Required scopes (any one suffices)" column of the "Message received" event.
   
      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_30c0252acb78b37b459a3b0aa23ab97f.png) </span>
   
   2. Click "Read all messages in associated group chat (sensitive scope)".
   
      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_98623addfb548c8b36963bdeb3fea7ea.png) </span>
   
   3. In the pop\-up window, click the "Add" button to apply for authorization.
   
   
   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c031012d2468488537930c9ea6aec9db.png) </span>
   
   

   
   **Callback configuration process**
   
   
   1. Select the "Callback Configuration" tab and click the edit button next to "Subscription mode".
   
      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6d45b4338b34de6714399e2f60177f36.png) </span>
   
   2. Select "Receive callbacks through **persistent connection**" and click the "Save" button.
   
   3. In the "Callback subscriptions" section, click the "Add callback" button.
   
      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5914b1db2c3a7332d3aebcb83e9e09c7.png) </span>
   
   4. In the "Add callback" dialog box, select the "Card" tab, check "Card callback communication", and click the "Add" button.
   
      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a235975fe2cfc084a95706f309e72b56.png) </span>
   

4. After enabling persistent connection, create and publish a new bot version again to ensure the current configuration modifications take effect.

   1. Click the "Create version" button at the top.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b4dbe4e123501122db070f7bd33138f2.png) </span>

   2. Configure the application version number, default capabilities, update description, and other information as needed.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e6040d6f7a8de04a041b88159eafd3c9.png) </span>

   3. Click the "Save" button at the bottom of the page to complete the version creation.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d5d4aa7205d46fcf8fa95611413f1172.png) </span>

   4. In the pop\-up window, click the "Confirm publication" button to publish the application

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1c5a577c82a99c5a11601645f37640ab.png) </span>

5. At this point, you have completed all operations and can chat with ArkClaw via the bot.


<span id="vYkph6hG"></span>
## Integrate a Slack bot

<span id="XV59QiDA"></span>
### Step 1: Create a Slack bot and obtain the information

If you already have a Slack bot and its App\-Level Tokens and Bot User OAuth Token, skip this step.


**Step 1: Create a Slack workspace**

If you have a Slack workspace, skip this step.


1. Log in to the [Slack console](https://slack.com/get-started?entry_point=redirect_flow#/landing).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_65250e5449e36af5985c64b5c46f4704.png) </span>

2. Click the "Create a new workspace" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6a4492516c482183fce2d2c2fa7d06a2.png) </span>

3. Enter the name of the workspace, and click the "Next" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_27767e8641972d11c1cf43a85a13d2af.png) </span>

4. Customize your name and avatar as needed, and click the "Next" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8e7cefc9ea77f2c5b1d16792b9e0d202.png) </span>

5. To add colleagues to join the current workspace, click the "Next" button.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If no information needs to be added, click the "Skip this step" button.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_511dd969216e6169d5cc9ba23fb5b18f.png) </span>

6. Select the Slack version. In the example provided in this topic, "Start with Limit Free Version" is selected.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_057120c45046d3ced954007f255d65c2.png) </span>



**Step 2: Create a Slack application and obtain the Token information**


1. Log in to the [Slack API console](https://api.slack.com/apps), and click the "Create New App" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7e224db0315e53af3a598023afaa162a.png) </span>

2. In the pop\-up window, select "From a manifest".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1466f10a955357bcf4dc7b1e76055f34.png) </span>

3. Select the workspace to deploy the application, and click the "Next" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_adcca6914c492d7aef0067006c186004.png) </span>

4. Copy the following content to replace the default JSON format configuration file information in the pop\-up window, and click the "Next" button.

   ```JSON
   {
     "display_information": {
       "name": "TestArkclaw2",
       "description": "Slack connector for OpenClaw"
     },
     "features": {
       "bot_user": {
         "display_name": "TestArkclaw2",
         "always_online": false
       },
       "app_home": {
         "messages_tab_enabled": true,
         "messages_tab_read_only_enabled": false
       },
       "slash_commands": [
         {
           "command": "/openclaw",
           "description": "Send a message to OpenClaw",
           "should_escape": false
         }
       ]
     },
     "oauth_config": {
       "scopes": {
         "bot": [
           "chat:write",
           "channels:history",
           "channels:read",
           "groups:history",
           "groups:read",
           "groups:write",
           "im:history",
           "im:read",
           "im:write",
           "mpim:history",
           "mpim:read",
           "mpim:write",
           "users:read",
           "app_mentions:read",
           "reactions:read",
           "reactions:write",
           "pins:read",
           "pins:write",
           "emoji:read",
           "commands",
           "files:read",
           "files:write"
         ],
         "user": [
           "channels:history",
           "channels:read",
           "groups:history",
           "groups:read",
           "im:history",
           "im:read",
           "mpim:history",
           "mpim:read",
           "users:read",
           "reactions:read",
           "pins:read",
           "emoji:read",
           "search:read"
         ]
       }
     },
     "settings": {
       "socket_mode_enabled": true,
       "event_subscriptions": {
         "bot_events": [
           "app_mention",
           "message.channels",
           "message.groups",
           "message.im",
           "message.mpim",
           "reaction_added",
           "reaction_removed",
           "member_joined_channel",
           "member_left_channel",
           "channel_rename",
           "pin_added",
           "pin_removed"
         ]
       }
     }
   }
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a082d0b618b73dea388a42fa884d413d.png) </span>

5. After confirming the permission range and other information, click the "Create" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7a71c6b6e765a959ebe7d05a82e4881b.png) </span>

6. Obtain Slack bot information.

   1. In the directory on the left, select "Basic Information", and click the "Generate Token and Scopes" button in the App\-Level Tokens module.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_883d20a83d2470482c63f3ee44d110b7.png) </span>

   2. Configure the token name in the pop\-up window, click the "Add Scope" button, and add the `connections:write` permission. Click the "Generate" button to generate App\-Level Tokens.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a5aeb37cabc4119a1f358bc860259e2b.png) </span>

   3. Click the "Copy" button to obtain the App\-Level Tokens, and then click the "Done" button to close the pop\-up window.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d5bbcda3d6f5a0b0c3ff332c3ab65bc1.png) </span>

   4. In the left directory tree, click "OAuth & Permissions". In the "OAuth Tokens" module, click the "Install to <your_workspace_name\>" button.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_97fadac1df6350443178450997ddee22.png) </span>

   5. On the new page, click the "Allow" button to allow the application you created to access Slack.

   6. After authorization, you will be automatically redirected to the OAuth & Permissions page. Copy the Bot User OAuth Token from the OAuth Tokens module.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9f1ee8e9c248434e239d1a3e99252087.png) </span>


<span id="SyGUspnH"></span>
### Step 2: Configure Slack bot information in ArkClaw


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter to access the ArkClaw conversation page.

2. Switch to the target ArkClaw instance page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cb7e3a8f9a4aa1a5b53934536e0827f1.png) </span>

3. Click "... \> Configure message channel" in the upper\-right corner of the conversation page or click the "Configure message channel" button on the page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91f7cce2c48051fafe5a7e223005cd01.png) </span>

4. The first time you associate with a channel, select "Connect Slack". If it is not the first time you associate with a message channel, click the "Add" button and select "Slack".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e55d393138e20f63238c93e6cb16ffb0.png) </span>

5. Enter the obtained Slack bot App\-Level Tokens and Bot User OAuth Token, and click the "Confirm" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6f592376d279c6f5600f8c221db04845.png) </span>

6. After successful configuration, you can use ArkClaw via Slack.


<span id="NKBf7zK7"></span>
## Integrate a WeCom bot

<span id="ItnXsTor"></span>
### Method 1: Quickly create and integrate a bot

To create and use a new WeCom bot, refer to this section to create a WeCom bot and obtain its information. Simply use the WeCom app to scan the QR code and authorize access. ArkClaw will then assist you in creating a new WeCom bot and automatically integrate it with ArkClaw.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If a WeCom bot has already been configured for your ArkClaw, the existing bot information will be overwritten by the new one.</div>



1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter to access the ArkClaw conversation page.

2. Switch to the target ArkClaw instance page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cb7e3a8f9a4aa1a5b53934536e0827f1.png) </span>

3. Click "... \> Configure message channel" in the upper\-right corner of the conversation page or click the "Configure message channel" button on the page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91f7cce2c48051fafe5a7e223005cd01.png) </span>

4. The first time you associate with a channel, select "Connect WeCom".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_406d82db6b41bf64211f17a2c6a4b442.png) </span>

5. Click "Quick configuration" and click the "Generate QR code" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_939319237b604814dfbd3377ffa89390.png) </span>

7. After the QR code is generated, use the WeCom app installed on your phone to scan the QR code.

8. On your mobile device, follow the instructions to create a bot.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Start creating a bot <strong>within 1 minute</strong> after scanning the code. If the operation times out, scan the QR code again to create the bot.   </div>
   

   1. Click the "One\-click create intelligent bot" button to start the bot creation process.

   2. Click the "Confirm authorization" button to grant the bot permissions to access chat information, schedule, and more.

   3. Adjust the bot name as needed, and click the "Go to use" button to enter the conversation page.

9. Once the bot is created, ArkClaw will automatically configure the new bot information for you.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">During the configuration process, ArkClaw needs to restart the gateway. Please wait for the process to complete. If there is no response for a long time, we recommend that you <a href="https://docs.byteplus.com/en/docs/ArkClaw/Restoring_ArkClaw_to_factory_settings__">restore ArkClaw to its factory settings</a> and configure the bot information again by following the instructions in this step.   </div>
   

   When the "WeCom" option is displayed next to "Channels", it means the WeCom bot configuration has been completed for ArkClaw, and you can chat with ArkClaw via the WeCom bot.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7efe4641f95c5a054ea12b856078e9c3.png) </span>


<span id="i291hXkj"></span>
### Method 2: Integrate an existing bot

To use an existing WeCom bot, refer to this section for configuration. Set "Connection method" of the existing bot to "Use persistent connection" and obtain its Bot ID and Secret information.

<span id="AOfp8406"></span>
#### Step 1: Modify the bot configuration


1. Log in to the [WeCom official website](https://work.weixin.qq.com/) with an account that has enterprise administrator permissions. In the directory tree on the left, select "Security and management \> Management tools", and click the "Intelligent bot" card.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8cc64f3c07d137f32c65a3f10d2327b4.png) </span>

2. On the intelligent bot page, select "Management" in the left navigation tree, and click the target bot to enter the bot details page.

3. Click the "Edit" button to configure the bot.

4. Scroll directly to the bottom of the page and click the "Create in API mode" button to switch the creation mode.

5. Specify "Use persistent connection" as the connection method, click the "Click to obtain" button next to Secret to generate the Secret, copy and save the Bot ID and Secret, and then click the "Save" button.


<span id="f5a39hAG"></span>
#### Step 2: Configure WeCom bot information in ArkClaw


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter to access the ArkClaw conversation page.

2. Switch to the target ArkClaw instance page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cb7e3a8f9a4aa1a5b53934536e0827f1.png) </span>

3. Click "... \> Configure message channel" in the upper\-right corner of the conversation page or click the "Configure message channel" button on the page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5c81f343520b742a8236b0e2d42e7810.png) </span>

4. The first time you associate with a channel, select "Connect WeCom".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_406d82db6b41bf64211f17a2c6a4b442.png) </span>

5. Click "Manual configuration" and enter the information of the enterprise application bot to be associated.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_aadd7f62bd51a226ca69dcfe9ea4f3c2.png) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">During the configuration process, ArkClaw needs to restart the gateway. Please wait for the process to complete. If there is no response for a long time, we recommend that you <a href="https://docs.byteplus.com/en/docs/ArkClaw/Restoring_ArkClaw_to_factory_settings__">restore ArkClaw to its factory settings</a> and configure the bot information again by following the instructions in this step.   </div>
   

6. When the "WeCom" option is displayed next to "Channels", it means the WeCom bot configuration has been completed for ArkClaw, and you can chat with ArkClaw via the WeCom bot.

   ## <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7efe4641f95c5a054ea12b856078e9c3.png) </span>    <span id="bcKE3l8J"></span>


<span id="zMNNQbdP"></span>
## Integrate a WeChat bot

Use the WeChat app to scan the QR code, and ArkClaw can quickly help you integrate the WeChat bot.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If a WeChat bot has already been configured for your ArkClaw, the existing bot information will be overwritten by the new one.</div>



1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter to access the ArkClaw conversation page.

2. Switch to the target ArkClaw instance page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cb7e3a8f9a4aa1a5b53934536e0827f1.png) </span>

3. Click "... \> Configure message channel" in the upper\-right corner of the conversation page or click the "Configure message channel" button on the page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91f7cce2c48051fafe5a7e223005cd01.png) </span>

4. The first time you associate with a channel, select "Connect WeChat". If it is not the first time you associate with a message channel, click the "Add" button and select "WeChat".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a63d7248c9ef9b55eafc89279df3411d.png) </span>

5. Click the "Execute now" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_60479a50d869bad23cfbac8bd6059daf.png) </span>

6. ArkClaw will initialize in the terminal and generate an authorization QR code.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Before completing the WeChat bot integration process, <strong>do not close the page</strong>.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3900b7da1a11759642ed554700260738.png) </span>

7. Enable the WeChat ClawBot plugin.

   1. Use the WeChat app installed on your phone to scan the QR code.

   2. If a prompt indicates "The current WeChat version is outdated" after you scan the QR code, follow the on\-screen instructions to update WeChat and scan the QR code again.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If the same prompt appears after you update WeChat, wait 1 to 3 minutes, generate a new QR code, and scan it.      </div>
      

   3. Click the "Connect" button to confirm enabling the WeChat ClawBot plugin.

8. After authorization, ArkClaw will automatically configure the WeChat bot information for you.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">During the configuration process, ArkClaw needs to restart the gateway. Please wait for the process to complete. If there is no response for a long time, we recommend that you <a href="https://docs.byteplus.com/en/docs/ArkClaw/Restoring_ArkClaw_to_factory_settings__">restore ArkClaw to its factory settings</a> and configure the bot information again by following the instructions in this step.   </div>
   

9. Return to your WeChat app. You can now chat with ArkClaw via your WeChat bot.


<span id="f3RFpQ1n"></span>
## Integrate a Microsoft Teams bot

<span id="9gWRwcIH"></span>
### Method 1: Automatically create and integrate a bot

Simply log in to your Microsoft Teams account and complete the authorization. ArkClaw will then use Teams CLI to automatically create a Microsoft Teams bot and integrate it with ArkClaw. This method is suitable for scenarios where no custom Azure Bot configuration is needed.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If a Microsoft Teams bot has already been configured for your ArkClaw, the existing bot information will be overwritten by the new one.</div>



1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter to access the ArkClaw conversation page.

2. Switch to the target ArkClaw instance page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cb7e3a8f9a4aa1a5b53934536e0827f1.png) </span>

3. Click "... \> Configure message channel" in the upper\-right corner of the conversation page or click the "Configure message channel" button on the page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91f7cce2c48051fafe5a7e223005cd01.png) </span>

4. Select "Connect Microsoft Teams".

5. Select "Automatic configuration", specify a name for your Microsoft Teams bot, and click the "Execute now" button.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you do not specify a name for your Microsoft Teams bot, ArkClaw will name your bot based on the "ArkClaw\-xxxxx" rule.   </div>
   

6. After ArkClaw finishes preparing the environment, it will display a Microsoft Sign\-in URL and an authorization code (Code).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Do not close the terminal before all configuration steps are complete.   </div>
   

7. Open the `Sign-in URL` displayed in the terminal in a browser, enter the authorization code (Code) displayed in the terminal, and click "Next".

8. Follow the prompts to log in to your Microsoft account.

9. Add the newly created Microsoft Teams bot to your Teams.

   1. Click `Install URL` displayed in the ArkClaw terminal output.

   2. Click the "Open Microsoft Teams" button.

   3. Click the "Add" button to add the bot to your Teams chat.

10. You have now completed the personal chat integration. You can chat with ArkClaw by sending a direct message to the Teams bot.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you want to use the bot in a team, continue with the team chat integration. Otherwise, you can skip the remaining configuration steps and close the ArkClaw terminal.   </div>
   

11. Use the Teams bot in a team.

   1. Download the bot file.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">You can share the bot file compressed package with other members in your organization. Once they upload it, they can chat with your ArkClaw through the bot. This is suitable for scenarios where your ArkClaw serves as a general\-purpose intelligent assistant within an organization, such as expense reimbursement and process approval.      </div>
      

      1. Click `DEVELOPER_PORTAL_URL` displayed in the ArkClaw terminal output.

      2. In the directory tree on the left, select "Configure \> App package editor" and click the "Download" button to download the bot file compressed package.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8c9f7ea8b51aba697b01257db08e29f2.png) </span>

   2. Add the bot to a Microsoft Teams team channel.

      1.  **(Optional)**  Create a team channel. Under Chat, select "Teams and channels \> View all channels". On the all channels page, click "Create team" in the upper\-right corner to create a team.

         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">If you already have a team channel, you can skip this step.         </div>
         

      2. Under "Chat \> Teams and channels", click the name of the target channel under the target team (the channel where you want to use the Teams bot). In the channel, click "Publish in channel".

      3. In the chat box that appears, type "@", select "Get proxy and bot", and click "Get more apps" in the dialog box.

      4. Click "Manage your apps" at the bottom, select "Upload an app \> Upload a custom app". Then, upload the bot file compressed package you obtained in the previous step.

      5. After the package is uploaded, click the "Add" button and select the target channel name at the bottom of the window. Then click the "Go to" button to navigate to the "Posts" tab of the channel.

      6. In the chat box, click "Continue draft", type "@", and select "Get proxy and bot". In the pop\-up dialog box, select the bot you uploaded.

   3. You and your team members can now chat with ArkClaw through the Teams bot in the team channel.


<span id="1MxOlEHe"></span>
### Method 2: Manually create and integrate a bot

Use this method if you want to use an existing bot, or if you need to specify Bot permissions or configuration.

<span id="ZkHWRgmK"></span>
#### Step 1: Create and configure an Azure Bot


1. Go to the [Azure application registration page](https://portal.azure.com/#view/Microsoft_AAD_RegisteredApps/ApplicationsListBlade) and click "New registration".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ef386e2738392d3d1d3e14a185fe72f5.png) </span>

2. Configure the "Name" parameter for the application, select "Single tenant only" for "Supported account type", select "Web" for "Redirect URI" (do not fill in the actual URL), and then click the "Register" button.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">"Single tenant only" indicates that the application you create can be accessed by all accounts under the same tenant.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1fbfa113579e2dde36e8abc3716ba6e3.png) </span>

3. After the application is created, copy and record the **Application (client) ID** and **Directory (tenant) ID**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0f950e2e5ba918342720c9c102b2b2f3.png) </span>

4. Click the "Add a certificate or secret" button to navigate to "Manage \> Certificates & secrets".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b54eb119a9cc598462956cb1ac034235.png) </span>

5. In "Manage \> Certificates & secrets", click the "New client secret" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c68db36207fb91608e214b954a271fa7.png) </span>

6. Configure the "Description" and "Expires" parameters, and then click the "Add" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9f2b7cab48e55d0f1a5820407dbc6558.png) </span>

7. After creation, copy and record the "Value" as the **Client Secret**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Since the "Value" information cannot be viewed afterwards, make sure to record and save it.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2aa607f0012411fb18d569407375ccc4.png) </span>


<span id="YiDLDMJR"></span>
#### Step 2: Enable the Microsoft Teams channel in Azure Bot

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">An Azure subscription is required to create an Azure Bot. If you do not have an Azure subscription, create one first. For detailed instructions, see the official documentation: <a href="https://learn.microsoft.com/en-us/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&tabs=userassigned">Use the Azure portal to Create an Azure Bot resource</a>.</div>



1. Create resource groups.

   1. In the top search box, search for "Resource groups", and click "Resource groups" to go to the Resource Manager.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ecaad2fe152731f5f00c41d713a31b4f.png) </span>

   2. Click "Create" to create a resource group.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_811b4d773429eec0d96c2611a06fea9a.png) </span>

   3. Enter the relevant information. In this example, set "Resource group name" to "ArkClaw\-teams". After configuration, click "Review + create". Confirm that the information is correct, and then click "Create" to finish creating the resource group.

2. Create an Azure Bot.

   1. Enter "Azure Bot" in the top search box and click Azure Bot under MarketPlace.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_be832d4d181a269d3e5609e59fd42f83.png) </span>

   2. On the creation page, configure the parameters based on the following table. Keep the default settings for parameters not included in the table. After configuration, click the "Review + create" button. Confirm that the information is correct, and click the "Create" button to finish creating the Azure Bot.

      
      |Parameter​ |Description |
      |---|---|
      |Resource group |Select the associated resource group. Here, select the "ArkClaw\-teams" created in the previous step. |
      |Data residency |Select "Global". |
      |Creation type |Select "Use existing app registration". Enter the **Application (client) ID** and **Directory (tenant) ID** saved in "Step 1: Create and configure an Azure Bot". |
      

3. Enable Microsoft Teams Channel in the Azure Bot.

   1. After the Azure Bot is created, click "Go to resource" under "Next steps" on the completion page.

   2. Go to "Settings \> Channels", and click "Microsoft Teams" under "Available Channels".

   3. In the "Terms of Service" dialog box that pops up, select the checkbox to accept the terms, and click "Agree".

   4. On the "Messaging" tab, click the "Apply" button. On the "Publish" tab, click the "Apply" button. If the "Apply" button is grayed out and unavailable, switch to the "Calling" tab, check the "Enable calling" option, click the "Apply" button, and then proceed.

   5. After the operation is complete, verify that the status of the Microsoft Teams channel changes to **Healthy**.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_337bc5fb1e89b26b2735b363369c3aba.png) </span>


<span id="rBFT9eqf"></span>
#### Step 3: Create a Teams app and associate it with the Azure Bot


1. Log in to the [Teams Developer Portal](https://dev.teams.microsoft.com/) **.**  **Make sure that you use the same account used to log in to the Azure Portal, Microsoft Teams, and other platforms**.

2. Click the "Create a new app" button, specify the app name, and click the "Create" button to create a new app. For ease of understanding, in this example, the app name is "Claw\-demo".

3. In the directory tree on the left, select "Configure \> App features", and click "Bot" to enter the Bots page. Under "Identify your bot", select "Enter a bot ID", and enter the **Application (client) ID of the Azure Bot**. Then, select the `Personal`, `Team`, and `Group chat` scopes, and click "Save" to save the information.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bd3a28bc3a7300eb2a4f8e104f86a416.png) </span>

4. Go to "Configure \> Basic information", check and enter the following basic information. Keep the default values for filled fields. After completion, click "Save" to save the information.

   * Information parameters: `App name`, `Developer name`, `Website URL`, `Privacy URL`, `Terms of Use URL`, `Short description`, and `Full description`.

   * Note: **These fields come from the Microsoft 365 app manifest schema and are required parameters for releasing or distributing a Teams app.**  **`Application (client) ID`** ** refers to the previously recorded Application (client) ID of the Azure Bot. For URL\-related parameters, make sure that the placeholders are correctly formatted.** 

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f9362d425e8f01b55925d386d6bd3ac2.png) </span>

5. Modify the manifest.json file.

   1. In the directory tree on the left, select "Configure \> App package editor", and select "... \> Edit" next to manifest.json.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_59b1111d0bc66fd56bf6fc926d9ebe64.png) </span>

   2. When you edit the `manifest.json` file, change the version numbers in `schema` and `manifestVersion` to a version earlier than v1.25 (for example, v1.23). After completion, click "Save" to save the information.

   3. Click "Update" to update the configuration. After the update is completed, click the "Confirm" button in the dialog box to complete the operation.


<span id="OP8EMNmj"></span>
#### Step 4: Install the Teams app in Teams


1. After the app passes validation, on the "Publish \> Distribute" page, click the "Distribute" button in the upper\-right corner of the page. Then, click "Download the app package" to download the Teams app installation package.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_abe7effdcd31bd76e76cca99e71ef9a1.png) </span>

2. Open and log in to the Teams client. In the left navigation pane, select "Apps" and select "Manage your apps \> Upload an app \> Upload a custom app". Then, upload the downloaded Teams app installation package.

3. After the upload succeeds, the app name "Claw\-demo" is displayed. Click the "Add" button.


<span id="NlBUIQiq"></span>
#### Step 5: Configure Azure Bot information in ArkClaw


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter to access the ArkClaw conversation page.

2. Switch to the target ArkClaw instance page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cb7e3a8f9a4aa1a5b53934536e0827f1.png) </span>

3. Click "... \> Configure message channel" in the upper\-right corner of the conversation page or click the "Configure message channel" button on the page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91f7cce2c48051fafe5a7e223005cd01.png) </span>

4. The first time you associate with a channel, select "Connect Microsoft Teams". The following figure shows the operations if it is not the first time you associate with a message channel: Click the "Add" button and select "Microsoft Teams".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a89dadaab8cd7dfa0b0a8e2a6c6cbc39.png) </span>

5. Select "Manual configuration". Enter the recorded **Application (client) ID** and **Directory (tenant) ID** of the Azure Bot, and the "Value" used as the **Client Secret**. Then, click "Confirm".

6. The configuration takes about 1 to 4 minutes. Please wait. Once the configuration succeeds, the endpoint information is returned. Copy the endpoint and click the "Azure Portal" link.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Do not close this page or perform other operations on this page for now.   </div>
   

7. On the Azure Portal homepage, click the name of the target Azure Bot under "Resources". Go to "Settings \> Configuration" of the Azure Bot, paste the endpoint copied from ArkClaw into the "Manager endpoint" field, and click "Apply".

8. Return to the ArkClaw chat page, and click "Confirm" on the MS Teams message channel configuration page to submit the configuration.


<span id="31EBTu6g"></span>
#### Step 6: Pair Teams with the Azure Bot


1. Personal use of the app.

   1. Open and log in to the Teams client. In the left navigation pane, select "Apps" and select "Manage your apps".

   2. In the app list, click the uploaded custom app "Claw\-demo", and then click "Personal app".

   3. You can now send a message in the chat box, such as "hello". After you send the first message from Teams, the message delivery chain is Teams \> Azure Bot \> ArkClaw \> Teams. It takes about 1 to 2 minutes for a message to return.

2. Team use of the app.

   1.  **(Optional)**  Create a team channel. Under Chat, select "Teams and channels \> View all channels". On the all channels page, click "Create team" in the upper\-right corner to create a team.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If you already have a team channel, you can skip this step.      </div>
      

   2. Under "Chat \> Teams and channels", click the name of the target channel under the target team (the channel where you want to use the Teams bot). In the channel, click "Publish in channel".

   3. In the chat box that appears, type "@", select "Get proxy and bot", and click "Get more apps" in the dialog box.

   4. Click "Manage your apps" at the bottom, select "Upload an app \> Upload a custom app". Then, upload the bot file compressed package you obtained in the previous step.

   5. After the package is uploaded, click the "Add" button and select the target channel name at the bottom of the "Add" window. Then click the "Go to" button to navigate to the "Posts" tab of the channel.

   6. In the chat box, click "Continue draft", type "@", and select "Get proxy and bot". In the pop\-up dialog box, select the bot you uploaded.

3. You and your team members can now chat with ArkClaw through the Teams bot in the team channel.
