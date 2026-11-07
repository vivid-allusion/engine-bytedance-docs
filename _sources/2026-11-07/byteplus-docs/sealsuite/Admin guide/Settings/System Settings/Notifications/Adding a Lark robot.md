---
title: "Adding a Lark robot"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-6zjnstxl2m"
---

While using the dynamic rule and administrator alarm rule modules of the SealSuite Admin Console, you can add notification robots to receive SealSuite notifications. This article introduces how to add a Lark robot to the SealSuite Admin Console, so that you can receive notifications from SealSuite through Lark.

<span id="91abdfba"></span>
# Instructions for use

Configuring Lark application or group robots to receive SealSuite notifications within SealSuite.


* Receiving notifications through the Lark application

   This method is suitable for scenarios where department and user information within SealSuite comes from Lark data sources. SealSuite will send notifications to designated users through Lark applications later. For specific operations, please refer to [Receiving notifications through the Lark application](https://arcosite.bytedance.net/sites/1673322421329/64b8d299f46a1b022f9c183b/editor/65b31e759ba46d02f092d491?docLang=en&bv=652fd8f3fb401502ea5effe0#62b474ad).

* Receiving notifications through group robots

   This method does not require attention to the source of enterprise user information. As long as you add a custom robot in the Lark group chat and obtain the robot's WebHook, you can add the corresponding notification robot in SealSuite. SealSuite will send notifications through the group robot later. For specific operations, please refer to [Receiving notifications through group robots](https://arcosite.bytedance.net/sites/1673322421329/64b8d299f46a1b022f9c183b/editor/65b31e759ba46d02f092d491?docLang=en&bv=652fd8f3fb401502ea5effe0#ddd146c7).


<span id="62b474ad"></span>
# Receiving notifications through the Lark application

<span id="0054bead"></span>
## Prerequisite

The organizational structure of Lark has been imported into SealSuite. For specific operations, please refer to [Integrating third-party data sources](https://docs.byteplus.com/docs/sealsuite/docs-importing-data-from-third-party-upstream-sources-).

<span id="57f90ee6"></span>
## Step 1: Create Custom App

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you already have an application for sending notifications within Lark, you can save the App ID and App Secret of the application and directly refer to Step 2 for configuration operations. For details on how to obtain information about Lark application, please refer to <a href="https://open.feishu.cn/document/faq/trouble-shooting/how-to-obtain-app-id">How to Obtain App ID</a>.</div>



1. Log in to [Lark Open Platform](https://open.feishu.cn/?lang=en-US).

2. Click **Developer Console** in the upper right corner of the page.

3. In the **Create your very first Lark app** area, click **Create Custom App**.

   For specific configuration instructions on creating a self\-built application for Lark Enterprise, please refer to [Custom app development process](https://open.feishu.cn/document/home/introduction-to-custom-app-development/self-built-application-development-process).

4. After creating a self\-built application for the enterprise, go to the application details page.

   On the **Credentials & Basic Info** page, view and save the **App ID** and **App Secret**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1086b2bbaa0e4ae7bf73908d1094e540~tplv-goo7wpa0wc-image.image) </span>


<span id="18af8caa"></span>
## Step 2: Configuring notification robots in the Admin Console


1. Log in to the Admin Console.

2. In the left navigation bar, click **Settings** \> **System** **Settings** \> **Notifications**.

3. On the **Notifications** page, click the **Third\-Party IM Applications** tab.

4. In the upper right corner of the page, click **New Integration**.

5. In the **New Integration** dialog box, complete the following configurations and click **OK**.

   
   |**Configuration Item** |**Description** |
   |---|---|
   |**Third\-Party IM Applications** |Select **Lark**. |
   |**Approval Notification** |Select **Application**. |
   |**Name** |Create a custom name to identify the current notification robot. |
   |**Description** |Create an optional custom description. |
   |**App ID** |The **App ID** information corresponds to Lark application. |
   |**App secret** |The **App Secret** information corresponds to Lark application. |
   

6. (Optional) In the **Notification Template** section at the bottom of the **Third\-Party IM Applications** tab, click **Edit** next to a template to customize its content:

   * **Language Support**: Configure separate templates for **Simplified Chinese** and **English**.

   * **Formatting**: Titles support up to 20 characters. Content has no length limit and supports hyperlinks.

   * **Variables**: Type `#` to call up the list of predefined system variables.

7. Click **Test** next to any template, select the bot in the pop\-up, and verify the notification. The test recipient will receive a message in Lark.


<span id="ddd146c7"></span>
# Receiving notifications through group robots

<span id="242912d0"></span>
## Step 1: Add a custom robot to the Lark group

For more information on how to add custom robots, please refer to [Custom bot usage guide](https://open.feishu.cn/document/client-docs/bot-v3/add-custom-bot). After adding the robot, you need to save the webhook address of the group robot.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4198b4777cbc45bcb60bde15c51d721f~tplv-goo7wpa0wc-image.image) </span>

<span id="e24aaa64"></span>
## Step 2: Configuring notification robots in the Admin Console


1. Log in to the Admin Console.

2. In the left navigation bar, click **Settings** \> **System** **Settings** \> **Notifications**.

3. On the **Notifications** page, click the **Third\-Party IM Applications** tab.

4. In the upper right corner of the page, click **New Integration**.

5. In the **New Integration** dialog box, complete the following configurations and click **OK**.

   
   |**Configuration Item** |**Description** |
   |---|---|
   |**Third\-Party IM Applications** |Select **Lark**. |
   |**Approval Notification** |Select **WebHook**. |
   |**Name** |Create a custom name to identify the current notification robot. |
   |**Description** |Create an optional custom description. |
   |**WebHook** |The WebHook address corresponds to the group robot. |
   

6. In the **Notification Template** section of the **Third\-Party IM Applications** tab, click **Edit** next to any template to customize the content (including multi\-language support and variables) and click **Confirm**.

7. Click **Test** next to the template, select the bot, and verify the notification. The test recipient will receive a message in the Lark group chat.
