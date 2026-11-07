---
title: "Adding a WeCom robot"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-zya0oh878g"
---

While using the dynamic rule and administrator alarm rule modules of the SealSuite Admin Console, you can add notification robots to receive SealSuite notifications. This article introduces how to add a WeCom robot to the Admin Console, so that you can receive notifications from SealSuite through WeCom.

<span id="536ceb16"></span>
# Instructions for use

Configure WeCom application or group robots within SealSuite to receive SealSuite notifications.


* Receiving notifications through WeCom application

   This method is suitable for scenarios where department and user information within SealSuite comes from WeCom data sources. Later, SealSuite will send notifications to designated users through WeCom applications. For specific operations, please refer to [Receiving notifications through WeCom application](https://arcosite.bytedance.net/sites/1710852383103/65f98d6109f21f0304a5bdf9/editor/65f98da65d483e04e8c73143?docLang=en&bv=65f98d6309f21f0304a5be02).

* Receiving notifications through group robots

   This method does not require attention to the source of user information in the enterprise. As long as you add a group robot in the WeCom group chat and obtain the robot's WebHook, you can add the corresponding notification robot in SealSuite. Later, SealSuite will send notifications through the group robot. For specific operations, please refer to [Receiving notifications through group robots](https://arcosite.bytedance.net/sites/1710852383103/65f98d6109f21f0304a5bdf9/editor/65f98da65d483e04e8c73143?docLang=en&bv=65f98d6309f21f0304a5be02).


<span id="39bf8158"></span>
# Receiving notifications through WeCom application

<span id="01051ef1"></span>
## Prerequisite

The organizational structure of WeCom has been imported into SealSuite. For more information, please refer to [Integrating third-party data sources](https://docs.byteplus.com/docs/sealsuite/docs-importing-data-from-third-party-upstream-sources-).

<span id="a5fc82cc"></span>
## Step 1: Contact SealSuite technical support to develop enterprise WeChat applications on behalf of others

Due to the data security requirements of WeCom (please refer to the[ internal development configuration domain name guide](https://open.work.weixin.qq.com/wwopen/common/readDocument/40754) for details), you need to contact SealSuite technical support to help you develop applications on behalf of WeCom.

<span id="1b7e8744"></span>
## Step 2: Configuring notification robots in the Admin Console


1. Log in to the Admin Console.

2. In the left navigation bar, click **Settings** \> **System** **Settings** \> **Notifications**.

3. On the **Notifications** page, click the **Third\-Party IM Applications** tab.

4. In the upper right corner of the page, click **New Integration**.

5. In the **New Integration** dialog box, complete the following configurations and click **OK**.

   
   |**Configuration Item** |**Description** |
   |---|---|
   |**Third\-Party IM Applications** |Select **WeCom**. |
   |**Approval Notification** |Select **Application**. |
   |**Name** |Create a custom name to identify the current notification robot. |
   |**Description** |Create an optional custom description. |
   |**Corp ID** |Enterprise ID corresponding to WeCom. For obtaining method, please refer to [What is a company ID](https://open.work.weixin.qq.com/help2/pc/17377). |
   |**Secret** |The Secret for developing applications on behalf of others. When you contact SealSuite technical support to develop an application, they will provide you with the Secret of the application. |
   |**Agent ID** |The AgentId for developing applications on behalf of others. In the application management of the WeCom management backend, enter the details page of the development application to view AgentId information. |
   

6. (Optional) In the **Notification Template** section at the bottom of the **Third\-Party IM** **Applications** tab, click **Edit** next to a template to customize notification content. You can configure multi\-language settings, reference variables (type `#` to trigger), and include hyperlinks. Click **Confirm** when finished.

7. Click **Test** next to any template, select the bot in the pop\-up window, and click **Confirm** to send a test notification. The test recipient will receive a message in WeCom.


<span id="374f5d46"></span>
# Receiving notifications through group robots

<span id="78c30e93"></span>
## Step 1: Add group robots to the WeCom group

For details about how to add a group chat bot, please refer to [Group robot configuration instructions](https://developer.work.weixin.qq.com/document/path/99110). After creating a group robot, it is necessary to save the Webhook of it.

<span id="22a4415e"></span>
## Step 2: Configuring notification robots in the Admin Console


1. Log in to the Admin Console.

2. In the left navigation bar, click **Settings** \> **System** **Settings** \> **Notifications**.

3. On the **Notifications** page, click the **Third\-Party IM Applications** tab.

4. In the upper right corner of the page, click **New Integration**.

5. In the **New Integration** dialog box, complete the following configurations and click **OK**.

   
   |**Configuration Item** |**Description** |
   |---|---|
   |**Third\-Party IM Applications** |Select **WeCom**. |
   |**Approval Notification** |Select **WebHook**. |
   |**Name** |Create a custom name to identify the current notification robot. |
   |**Description** |Create an optional custom description. |
   |**WebHook** |The WebHook address corresponds to the group robot. |
   

6. (Optional) In the **Notification Template** section at the bottom of the **Third\-Party IM Applications** tab, click **Edit** next to a template to customize notification content. You can configure multi\-language settings, reference variables (type `#` to trigger), and include hyperlinks. Click **Confirm** when finished.

7. Click **Test** next to any template, select the bot in the pop\-up window, and click **Confirm** to send a test notification. The test recipient will receive a message in the WeCom group chat.
