---
title: "Adding a Slack robot"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-adding-slack-robot"
---

While using the dynamic rule and administrator alarm rule modules of the SealSuite Admin Console, you can add notification robots to receive Slack notifications. This article introduces how to add a Slack robot to the Admin Console, so that you can receive notifications from SealSuite through Slack.

<span id="31a3348e"></span>
# Instruction for use

Configure Slack applications or channels within SealSuite to receive SealSuite notifications.


* Receiving notifications through the Slack application.

   This method is applicable to the scenario where department and user information within SealSuite comes from Slack data sources. SealSuite will send notifications to designated users through the Slack application. For more information, please refer to [Receiving notifications through Slack application](https://docs.byteplus.com/docs/sealsuite/docs-adding-slack-robot#e6c9e95a)

* Receiving notifications through the Slack channel.

   This method does not require attention to the source of user information in the enterprise. As long as you add an application to the Slack channel and obtain the robot's WebHook, you can add corresponding notification robots in SealSuite. SealSuite will send notifications through group robots later on. For more information, please refer to [Receiving notifications through Slack channel](https://docs.byteplus.com/docs/sealsuite/docs-adding-slack-robot#f6d07ac3).


<span id="f284fcb5"></span>
# Creating an application within Slack

<span id="f42d5f94"></span>
## Obtain Bot Token


1. Log in to [Slack API platform](https://api.slack.com/apps).

2. In the middle of the page, click **Create an App**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you have already created a Slack app, you can use the existing app or click on <strong>Create New App</strong> in the upper right corner.   </div>
   

3. In the **Create an app** dialog box, click **From scratch**.

4. In the **Name app ＆ choose workspace** dialog box, enter **App Name**, select one workspace, and click **Create App**.

   The page will automatically redirect to the application's settings page.

5. In the left navigation bar, click **OAuth ＆ Permissions。** 

6. In the **Scopes** ＞ **Bot Token Scopes** area of the **OAuth ＆ Permissions** page, add **chat:write**, **user:read** and **user:read.email**.

7. In the **OAuth Tokens for Your Workspace** area of the **OAuth ＆ Permissions** page, click **Install/Reinstall to Workspace**.

8. After installation, copy **Bot User OAuth Token** for API calls.

9. Return to Slack Workspace, open the newly created application and add it to the channel you want it to send messages to.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the selected channel, a new message will prompt you that you have successfully added an application.   </div>
   

10. On the channel page, copy the channel ID from the link in the browser address bar:

* CXXXXXXXXXX: Indicates the channel.

* DXXXXXXXXXX: Indicates direct messages.

11. Using the Bot User OAuth Token and channel ID, you can call the API`chat:postMessage` to send messages to the channel `https://api.slack.com/methods/chat.postMessage/test`.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a726c3b464c04dfaa6d7d604cf67250e~tplv-goo7wpa0wc-image.image) </span>


<span id="cbcb6230"></span>
## Obtain Webhook


1. Log in to [Slack API platform](https://api.slack.com/apps).

2. In the middle of the page, click **Create an App**.

3. In the **Create an app** dialog box, click **From scratch**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you have already created a Slack app, you can use the existing app or click on <strong>Create New App</strong> in the upper right corner.   </div>
   

4. In the **Name app ＆ choose workspace** dialog box, enter **App Name**, select a workspace, and then click **Create App**.

   The page will automatically redirect to the application's settings page.

5. On the left navigation bar of the application settings page, click **Incoming Webhooks**.

6. On the **Incoming Webhooks** page, open **Activate Incoming Webhooks**, and on the bottom of the page, click **Add New Webhook to Workspace**, and select an app publishing channel.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the selected channel, a new message will prompt you that you have successfully added an application:added an integration to this channel:   </div>
   

7. Return to the **Incoming Webhooks** page. In the **Webhook URL** field, click **Copy** to copy the webhook URL.

8. Paste the webhook URL into the **Sample curl request to post to a channel** field.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8198016cf1f64d0981efce75ce453787~tplv-goo7wpa0wc-image.image) </span>


<span id="e6c9e95a"></span>
# Receiving notifications through Slack application


1. Log in to the Admin Console.

2. In the left navigation bar, click **Settings** \> **System** **Settings** \> **Notifications**.

3. On the **Notifications** page, click the **Third\-Party IM Applications** tab.

4. In the upper right corner of the page, click **New Integration**.

5. In the **New Integration** dialog box, complete the following configurations and click **OK**.

   
   |**Configuration Item** |**Description** |
   |---|---|
   |**Third\-Party IM Applications** |Select **Slack.**  |
   |**Approval Notification** |Select **Application**. |
   |**Name** |Create a custom name to identify the current notification robot. |
   |**Description** |Create an optional custom description. |
   |**Bot Token** |Enter the Bot Token for the Slack application. |
   

6. In the **Notification Template** area of the **Third\-party IM Applications** tab, click **Test** on the right of any template.

   The page will pop up the **Test Integration** dialog box.

7. In the **Test Integration** dialog box, select the newly created Slack robot in the **Select a configured integration** field and fill in the **Test Scope** field with the test scope.

8. After clicking **OK**, you can receive notifications in the specified Slack application.


<span id="f6d07ac3"></span>
# Receiving notifications through Slack channel


1. Log in to the Admin Console.

2. In the left navigation bar, click **Settings** \> **System** **Settings** \> **Notifications**.

3. On the **Notifications** page, click the **Third\-Party IM Applications** tab.

4. In the upper right corner of the page, click **New Integration**.

5. In the **New Integration** dialog box, complete the following configurations and click **OK**.

   
   |**Configuration Item** |**Description** |
   |---|---|
   |**Third\-Party IM Applications** |Select **Slack.**  |
   |**Approval Notification** |Select **WebHook.**  |
   |**Name** |Create a custom name to identify the current notification robot. |
   |**Description** |Create an optional custom description. |
   |**WebHook** |The WebHook address corresponds to the group robot. |
   

6. (Optional) In the **Notification Template** section at the bottom of the **Third\-Party IM Applications** tab, click **Edit** next to a template to customize notification content. You can configure multi\-language settings, reference variables (type `#` to trigger), and include hyperlinks. Click **Confirm** when finished.

7. Click **Test** next to any template, select the bot in the pop\-up window, and click **Confirm** to send a test notification. The test recipient will receive a message in the specified Slack channel.
