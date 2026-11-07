---
title: "Configuring message channels"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Configuring_message_channels_1"
---

This topic describes how to integrate message channels such as Telegram, Lark, and Discord bots with ArkClaw. After the integration, you can chat with ArkClaw through the corresponding bot. ArkClaw can also use bot capabilities to help you perform operations such as creating documents and scheduling calendar events.

<span id="gatZi2zr"></span>
## Integrate Telegram

<span id="Ou6f8jbA"></span>
### Step 1: Create a Telegram bot and obtain the information

If you already have a Telegram bot and possess its access token, skip this step.


1. Log in to your Telegram and search for `@Botfather`.

2. Send `/newbot` to `@Botfather` to create a new bot.

3. After creating the bot, you can obtain the bot access token from `@Botfather`'s reply. The format is: `123:abc`.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The bot access token will be used to configure ArkClaw. Store it securely.   </div>
   

<span id="q1EXAtgd"></span>
### Step 2: Configure Telegram bot information in ArkClaw


1. **Return to the ArkClaw chat page** and click the "Message channel" button.

2. In the pop\-up window, select "Telegram", enter the bot token you obtained, and click the "Confirm" button to submit the configuration request.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">During the configuration process, ArkClaw needs to restart the gateway. Wait patiently. If there is no response for a long time, we recommend that you<a href="https://docs.byteplus.com/en/docs/ArkClaw/Restoring_ArkClaw_to_factory_settings_and"> restore ArkClaw to its factory settings</a> and configure the Telegram bot information again by following the instructions in this step.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_28e6a88fe70c26f98c2bd301e4c04435.png) </span>

3. Once ArkClaw completes the update, the Telegram bot information is configured successfully.


<span id="dTUn446Y"></span>
### Step 3: **Pair with the Telegram bot**

Due to ArkClaw security restrictions, you need to pair the Telegram bot with ArkClaw using a pairing code for authentication.


1. Obtain the Telegram bot pairing code.

   1. In your Telegram, open the bot created earlier.

   2. Send `/start` to it, and obtain and record the pairing code value from the bot's reply.

2. **Return to the ArkClaw chat page** and click the "IM Pairing" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7e1d11598939fdbfbee1b61bdb583c03.png) </span>

3. Select Telegram and enter the pairing code you obtained in the previous step, and click the "Confirm" button to start pairing.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">During the pairing process, ArkClaw will open a terminal interface. Do not close this interface before the pairing is completed.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f94b82feb67cc78061ddbf1b003d5b70.png) </span>

4. When the message "Approve telegram sender xxxx" appears in the terminal interface, it indicates that the Telegram bot pairing is completed as expected. You can close the terminal to end the pairing process.

5. You can now chat with ArkClaw through the Telegram bot.


<span id="9K8GzHgi"></span>
## Integrate a Lark bot

<span id="vK1rd5LI"></span>
### Quickly create and integrate a bot

Simply use the Lark app to scan the QR code and authorize access, and ArkClaw will quickly help you create a new Lark bot and automatically integrate it for you.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If a Lark bot has already been configured for your ArkClaw, the existing bot information will be overwritten by the new one.</div>



1. On the ArkClaw chat interface, click the "Message channel" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1b1f2d3144f8d679bf8ef70b2bfbddfd.png) </span>

2. In the pop\-up window, select "Lark \> Quick pairing" and click the "Generate QR code" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9621205f7e8ae3b2103bf910c02b523c.png) </span>

3. After the QR code is generated, use the Lark app installed on your phone to scan the QR code.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_55a6a290a073d1fa7981fa4f3120c5b2.png) </span>

4. Enter the name of the Lark bot and click the "Create" button to start the creation process.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After scanning the QR code, you need to enter the bot name and complete the creation within 10 minutes. If the operation times out, scan the QR code again to create the bot.   </div>
   

5. Once the bot is created, ArkClaw will automatically configure the new bot information for you.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">During the configuration process, ArkClaw needs to restart the gateway. Wait patiently. If there is no response for a long time, we recommend that you <a href="https://docs.byteplus.com/en/docs/ArkClaw/Restoring_ArkClaw_to_factory_settings_and">restore ArkClaw to its factory settings</a> and configure the bot information again by following the instructions in this step.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_badd0801995d2aa0d64e4576164a8857.png) </span>

   When the message similar to the following example is displayed, it indicates that ArkClaw has completed the Lark bot configuration. You can close the message channel configuration page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fd113b3a151015e29c73d62afe73c99f.png) </span>

6. Return to your Lark app and click the "Open bot" button to communicate with ArkClaw via the Lark bot.


<span id="mfgPc05D"></span>
### Integrate an existing bot

<span id="rbq3FG0F"></span>
#### Step 1: Adjust the bot configuration


**Step 1: Configure permissions for the bot to perform operations such as chatting and managing Lark documents**


1. Log in to the[ Lark Open Platform](https://open.larksuite.com/app).

2. Select the "Custom Apps" tab, and click the Lark open application you created.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3bb47a77b26c7d960d821064de2c717a.png) </span>

3. In the directory tree on the left, select "Development Configuration \> Permissions & Scopes", and click the "Batch import/export scopes" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_170a769a91756f3fb89259675d234bad.png) </span>

4. On the "Import" tab, replace the original example with the following permissions, and click the "Next, Review New Scopes" button.

   ```JSON
   {
     "scopes": {
       "tenant": [
         "application:application:self_manage",
         "cardkit:card:read",
         "cardkit:card:write",
         "contact:contact.base:readonly",
         "contact:user.basic_profile:readonly",
         "docx:document:readonly",
         "im:chat:read",
         "im:chat:update",
         "im:message.group_at_msg:readonly",
         "im:message.p2p_msg:readonly",
         "im:message.pins:read",
         "im:message.pins:write_only",
         "im:message.reactions:read",
         "im:message.reactions:write_only",
         "im:message:readonly",
         "im:message:recall",
         "im:message:send_as_bot",
         "im:message:send_multi_users",
         "im:message:send_sys_msg",
         "im:message:update",
         "im:resource"
       ],
       "user": [
         "base:app:copy",
         "base:app:create",
         "base:app:read",
         "base:app:update",
         "base:field:create",
         "base:field:delete",
         "base:field:read",
         "base:field:update",
         "base:record:create",
         "base:record:delete",
         "base:record:retrieve",
         "base:record:update",
         "base:table:create",
         "base:table:read",
         "base:table:update",
         "base:view:read",
         "base:view:write_only",
         "board:whiteboard:node:create",
         "board:whiteboard:node:read",
         "calendar:calendar.event:create",
         "calendar:calendar.event:read",
         "calendar:calendar.event:reply",
         "calendar:calendar.event:update",
         "calendar:calendar.free_busy:read",
         "calendar:calendar:read",
         "contact:contact.base:readonly",
         "contact:user.base:readonly",
         "contact:user.basic_profile:readonly",
         "contact:user.employee_id:readonly",
         "contact:user:search",
         "docs:document.comment:create",
         "docs:document.comment:read",
         "docs:document.comment:update",
         "docs:document.media:download",
         "docs:document.media:upload",
         "docs:document:copy",
         "docs:document:export",
         "docx:document:create",
         "docx:document:readonly",
         "docx:document:write_only",
         "drive:drive.metadata:readonly",
         "drive:file:download",
         "drive:file:upload",
         "im:chat.members:read",
         "im:chat:read",
         "im:message",
         "im:message.group_msg:get_as_user",
         "im:message.p2p_msg:get_as_user",
         "im:message:readonly",
         "offline_access",
         "search:docs:read",
         "search:message",
         "sheets:spreadsheet.meta:read",
         "sheets:spreadsheet:create",
         "sheets:spreadsheet:read",
         "sheets:spreadsheet:write_only",
         "space:document:move",
         "space:document:retrieve",
         "task:comment:read",
         "task:comment:write",
         "task:task:read",
         "task:task:write",
         "task:task:writeonly",
         "task:tasklist:read",
         "task:tasklist:write",
         "wiki:node:copy",
         "wiki:node:create",
         "wiki:node:move",
         "wiki:node:read",
         "wiki:node:retrieve",
         "wiki:space:read",
         "wiki:space:retrieve",
         "wiki:space:write_only"
       ]
     }
   }
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_628e27247dc5e79ef5e5fb5014cea006.png) </span>

5. In the pop\-up window, confirm the permissions are correct and click the "Add" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_36d4c2fd955758cb75bd4ccb0179d10c.png) </span>

6. Click the "Config" button to set the accessible data scope for the permission (keep the default option "Identical to the availability of app" in this topic), and then click "Confirm" to complete the operation.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2eec7f09f5955d94eeef62adacd43002.png) </span>



**Step 2: Publish the bot application version to activate the bot**


1. Click the "Create version" button at the top.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1c361b8ad38d4af143e598e8ebd82d5e.png) </span>

2. Configure the application version number, default capabilities, update description, and other information as needed.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9ad67544c011d2ab03100727bd70fb04.png) </span>

3. Click the "Save" button at the bottom of the page to complete the version creation.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_36ad9c875194547757434f1e299b3096.png) </span>

4. In the pop\-up window, click the "Confirm publication" button to publish the application

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_423ee8a6f4ae31fec61a7fec548b11ab.png) </span>



**Step 3: Obtain the bot App ID and App Secret**


1. In the directory tree on the left, select "Basic Info \> Credentials & Basic Info".

2. In the "Credentials" module, obtain and record the App ID and App Secret information.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The obtained App ID and App Secret will be used to configure OpenClaw. Keep them secure.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_991b200da8f7bc1eaf4c46f4d08770e7.png) </span>


<span id="umfmTbyE"></span>
#### Step 2: Configure bot information in ArkClaw


1. **Return to the ArkClaw chat page** and click the "Message channel" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7d3889edd1d202ef9e741f31a0d56525.png) </span>

2. In the pop\-up window, select "Lark \> Associate existing bot", enter the bot App ID and App Secret you obtained, and click the "Confirm" button to submit the configuration request.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">During the configuration process, ArkClaw needs to restart the gateway. Wait patiently. If there is no response for a long time, we recommend that you <a href="https://docs.byteplus.com/en/docs/ArkClaw/Restoring_ArkClaw_to_factory_settings_and">restore ArkClaw to its factory settings </a>and configure the Lark bot information again by following the instructions in this step.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0d74257da768711f209477094d4a8702.png) </span>

3. When ArkClaw is restored to the **Running ** status, it indicates that you have configured the Lark bot information in ArkClaw.


<span id="pJ3fj14B"></span>
#### Step 3: Enable bot persistent connection

After configuring bot information in ArkClaw, you need to go to the Lark Developer Console to enable the persistent connection feature for the bot, ensuring normal message transmission between the bot and ArkClaw.


1. Log in to the [Lark Open Platform](https://open.larksuite.com/app).

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
   
      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f0966325594deddfed2fd43fc2cf4561.png) </span>
   
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


<span id="ImbAVNTQ"></span>
#### Step 4: **Pair with the bot**

Due to ArkClaw security restrictions, you need to pair the Lark bot with ArkClaw using a pairing code for authentication. This process is similar to receiving and entering a verification code to verify your identity when logging in to an application using your mobile phone number.


1. Send any message to the Lark bot (for example: Hello).

2. Obtain your pairing code from the reply of the bot.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f4a0f9fd2e2200ad5406c83beec44bb3.png) </span>

3. **Return to the ArkClaw chat page** and click the "IM Pairing" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7e1d11598939fdbfbee1b61bdb583c03.png) </span>

4. Select Lark and enter the pairing code you obtained in the previous step, and click the "Confirm" button to start pairing.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">During the pairing process, ArkClaw will open a terminal interface. Do not close this interface before the pairing is completed.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_11151988ac4b42b2a4ae7045eda05e51.png) </span>

5. When the message "Approve feishu sender xxxx" appears in the terminal interface, it indicates that the Lark bot pairing is completed as expected. You can close the terminal to end the pairing process.

6. You can now chat with ArkClaw through the Lark bot.


<span id="JAapvzSX"></span>
## Integrate a Discord bot

<span id="q04k3wx4"></span>
### Step 1: Create a Discord bot and obtain the information

If you already have a Discord bot and possess its access token, skip this step.


1. Log in to the [Discord Developer Portal](https://discord.com/developers/applications).

2. In the directory on the left, select "Applications", and click the "New Application" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ff0ceec5659a2c42073869d2efb021d4.png) </span>

3. Enter the bot name and click the "Create" button to create the bot.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_13feba9fda15ccae219c88754d6b8fb5.png) </span>

4. Obtain the bot access token.

   1. After the bot is created, select "Bot" in the directory on the left of the bot details page.

   2. Turn on the "Message Content Intent" and "Server Members Intent" switches.

   3. Click the "Reset Token" button in the token module, and record this token.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The bot access token will be used to configure ArkClaw. Store it securely.      </div>
      

5. Generate an invite URL.

   1. In the directory on the left, select "OAuth2".

   2. Select the `bot`, `applications.commands`, `View Channels`, `Send Messages`, `Read Message History`, `Embed Links`, and `Attach Files` permissions.

   3. Copy the URL.

6. Enable developer mode.

   1. Open the URL you obtained in your browser, and log in to the Discord app.

   2. Follow the instructions to complete all authorization operations.

   3. Click the settings icon, select "Advanced" in the directory on the left, and enable "Developer Mode".


<span id="pUM21lwD"></span>
### Step 2: Configure Discord bot information in ArkClaw


1. **Return to the ArkClaw chat page** and click the "Message channel" button.

2. In the pop\-up window, select "Discord", enter the bot token you obtained, and click the "Confirm" button to submit the configuration request.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">During the configuration process, ArkClaw needs to restart the gateway. Wait patiently. If there is no response for a long time, we recommend that you<a href="https://docs.byteplus.com/en/docs/ArkClaw/Restoring_ArkClaw_to_factory_settings_and"> restore ArkClaw to its factory settings </a>and configure the Discord bot information again by following the instructions in this step.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8971a1aedad727264ebd6196af287ab8.png) </span>

3. Once ArkClaw completes the update, the Discord bot information is configured successfully.


<span id="PIH3GBp9"></span>
### Step 3: **Pair with ** the Discord **bot**

Due to ArkClaw security restrictions, you need to pair the Discord bot with ArkClaw using a pairing code for authentication.


1. Obtain the Discord bot pairing command.

   1. In your Discord, open the bot created earlier.

   2. Send any message to the bot (for example: Hello), and obtain and record the pairing code from the reply of the bot.

2. **Return to the ArkClaw chat page** and click the "IM Pairing" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7e1d11598939fdbfbee1b61bdb583c03.png) </span>

3. Select Discord and enter the pairing code you obtained in the previous step, and click the "Confirm" button to start pairing.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">During the pairing process, ArkClaw will open a terminal interface. Do not close this interface before the pairing is completed.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a8bf3eb6a2f8d24936c214421b16e79d.png) </span>

4. When the message "Approve discord sender xxxx" appears in the terminal interface, it indicates that the Discord bot pairing is completed as expected. You can close the terminal to end the pairing process.

5. You can now chat with ArkClaw through the Discord bot.


<span id="I1r6Kwsp"></span>
## Integrate a Slack bot

<span id="7HqrlTDX"></span>
### Step 1: Create a Slack bot and obtain the information

If you already have a Slack bot and possess its App\-Level Tokens and Bot User OAuth Token, skip this step.


**Step 1: Create a Slack workspace**

If you have a Slack workspace, skip this step.


1. Log in to [Slack console](https://slack.com/get-started?entry_point=redirect_flow#/landing).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_65250e5449e36af5985c64b5c46f4704.png) </span>

2. Click the "Create a new workspace" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_896d47e4e474743594ef9650ff303870.png) </span>

3. Enter the name of the workspace, and click the "Next" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_59a81508d3247767b23a31ade3f8c43d.png) </span>

4. Customize your name and avatar as needed, and click the "Next" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9b5f61c767af3678a3cabb10bc19a3a1.png) </span>

5. To add colleagues to join the current workspace, click the "Next" button.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If no information needs to be added, click the "Skip this step" button.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_70074b1c3730b03733c0d0bcd64f88a0.png) </span>

6. Select the Slack version. In the example provided in this topic, "Start with Limit Free Version" is selected.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_057120c45046d3ced954007f255d65c2.png) </span>



**Step 2: Create a Slack application**


1. Log in to the [Slack API console](https://api.slack.com/apps) and click the "Create an App" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f00241f88f8671763a71e77df1eb7751.png) </span>

2. In the pop\-up window, select "From a manifest".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ce1511bb4eb45601ab527d7313364f95.png) </span>

3. Select the workspace to deploy the application, and click the "Next" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2b8e8f5f3a42a78dd70993a3ff188837.png) </span>

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

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ad147f0037a16d790ca51961896bc11d.png) </span>

   2. Configure the token name in the pop\-up window, click the "Add Scope" button, and add the `connections:write` permission. Click the "Generate" button to generate App\-Level Tokens.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4c8e291c8b98131f0621822226a9b26b.png) </span>

   3. Click the "Copy" button to obtain App\-Level Tokens.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cf910b4da74bdc079c7df674a98eb9a0.png) </span>

   4. In the directory on the left, select "OAuth & Permissions" and click the "Install to <your_workspace_name\>" button in the OAuth Tokens module.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_97fadac1df6350443178450997ddee22.png) </span>

   5. On the new page, click the "Allow" button to grant access to Slack to the application you created.

   6. After authorization, you will be automatically redirected to the OAuth & Permissions page. Copy the Bot User OAuth Token from the OAuth Tokens module.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0ac0af8bd99dc2c24edd7e3ab4eed7dd.png) </span>


<span id="G2YcDS9T"></span>
### Step 2: Configure Slack bot information in ArkClaw


1. **Return to the ArkClaw chat page** and click the "Message channel" button.

2. In the pop\-up window, select "Slack", enter the Bot User OAuth Token and App\-Level Tokens you obtained in sequence, and click the "Confirm" button to submit the configuration request.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">During the configuration process, ArkClaw needs to restart the gateway. Wait patiently. If there is no response for a long time, we recommend that you <a href="https://docs.byteplus.com/en/docs/ArkClaw/Restoring_ArkClaw_to_factory_settings_and">restore ArkClaw to its factory settings</a> and configure the Slack bot information again by following the instructions in this step.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3959e00ce2e6c9346ceedb44bfcd20c3.png) </span>

3. Once ArkClaw completes the update, the Slack bot information is configured successfully.


<span id="UFMz8Eku"></span>
### Step 3: **Pair with** the Slack **bot**

Due to ArkClaw security restrictions, you need to pair the Slack bot with ArkClaw using a pairing code for authentication.


1. Log in to the [Slack console](https://slack.com/get-started?entry_point=redirect_flow#/landing) and select the workspace where you deploy the Slack bot.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_83ccd6043138365d52e234c2d6f8901f.png) </span>

2. Obtain the pairing code.

   1. Among the workspace apps, open the Slack bot you created.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_63210a9b78806e9406f5cf7aec17e104.png) </span>

   2. Send any message to the bot (for example: Hello), and obtain and record the pairing code from the reply of the bot.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3649a5e6eb8b8b93f11e1be1fdd0892a.png) </span>

3. **Return to the ArkClaw chat page** and click the "IM Pairing" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7e1d11598939fdbfbee1b61bdb583c03.png) </span>

4. Select Slack and enter the pairing code you obtained in the previous step, and click the "Confirm" button to start pairing.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_905688cdbf50d2778d6951d5b6d1f182.png) </span>

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">During the pairing process, ArkClaw will open a terminal interface. Do not close this interface before the pairing is completed.   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_90cc9f8e631abce0531bd34cbca4ae32.png" width="438px" />   </div>
   

5. When the message "Approve slack sender xxxx" appears in the terminal interface, it indicates that the Slack bot pairing is completed as expected. You can close the terminal to end the pairing process.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ad34b6e2faa0b8251ade4a2c8d236a0a.png) </span>

6. You can now chat with ArkClaw through the Slack bot.

   ## <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ab0d8a093ffe27780843bae8799f6a9b.png) </span>    <span id="0nd7Xwxr"></span>
