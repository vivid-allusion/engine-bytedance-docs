---
title: "Configure IT Assistant"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-configuring-expert-services-"
---

SealSuite IT Assistant helps employees contact the enterprise IT team from the client for IT support. This topic describes how to configure the service entry point and how it appears in the client.

## Overview

Enterprise IT teams usually have fixed employee support channels, such as IT on\-call groups, ticketing systems, or internal support pages. However, these entry points are scattered across group chats, onboarding materials, and various documents, making them difficult to find when employees need help. IT Assistant provides an IT support entry point in the lower\-left corner of the **Help** page in the SealSuite client. The entry point has a fixed position and cannot be changed. After an administrator configures the icon, name, and redirect link in the Admin Console, employees can click the entry point to open the specified channel.

The redirect link supports both web pages, such as ticketing systems, knowledge bases, and online customer service pages, and custom protocol links for IM applications, such as `lark://`, `dingtalk://`, and `wxwork://`. These links can launch Lark, DingTalk, and WeCom, or directly open a specified group chat, service desk, or contact conversation.

Supported redirect scenarios are as follows:

|Redirect target |Supported scenarios |
|---|---|
|Lark |Launch the Lark client, a specified group chat, or Service Desk (on\-call account). |
|DingTalk |Launch the DingTalk client, a one\-to\-one user conversation, or an Employee Service Desk bot. |
|WeCom |Launch the WeCom client. |
|Web\-based online chat |Open a web chat window, such as a Slack channel page. |
|Web\-based help center |Open the web URL of a specified help center. |

## Configure the entry point

The IT Assistant configuration determines how the IT support entry point is displayed in the client and where it redirects employees. Follow these steps to configure the entry point and verify the result:

1. Log in to the Admin Console. In the left navigation pane, choose **Settings** \> **IT Tools**.

2. In the **Services & help** area, click **IT Assistant**.

3. In **Configure IT Assistant**, enter the following information.

   |Configuration item |Description |
   |---|---|
   |**Display icon** |Helps employees identify the enterprise IT service entry point. Set an icon that matches the service purpose. |
   |**Assistant name** |Describes the service provided by the client entry point. Enter a name that employees can easily understand, such as "Contact the IT team". |
   |**Redirect link** |Specifies the application, conversation, service desk, or web page that opens after employees click the entry point. Based on the service channel used by your enterprise, enter the link by following the corresponding method in [Obtain and enter a redirect link](https://docs.byteplus.com/docs/sealsuite/docs-configuring-expert-services-#doxcnv2LtyBZzeb3ggT9bMNiZYf). |

4. Use **Preview** to check the name and icon. Click **Test** as needed to verify the redirect target.

5. Click **Confirm** to save the configuration.

   After the configuration is complete, IT Assistant is automatically enabled. You can later disable this feature by using the switch on the **IT Assistant** card.

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/it-tools-en-20261023/expert-admin-live.png)

## Obtain and enter a redirect link

The redirect link determines which application, conversation, or web page opens after an employee clicks the IT Assistant entry point. Based on the service channel used by your enterprise, select the corresponding method below to obtain the link, and enter it in **Redirect link** in the SealSuite Admin Console. These methods are optional configuration options and do not need to be performed in sequence.

### Lark

Lark can open the client, a specified group chat, or Service Desk (on\-call account). Select the appropriate configuration based on where employees should go.

|Redirect scenario |Configuration method |
|---|---|
|Open the Lark client |To open the Lark client after employees click the entry point, enter `lark://` in **Redirect link**. |
|Open a specified group chat |To direct employees to a specified group chat, such as an IT support group, obtain and enter the group link as follows:<br><br><br>1. In Lark, open the target group chat. Click the group name at the top of the conversation, and then click **Share group card** in the drawer on the right.<br><br>2. Select **Group link**, set the validity period to **Permanent**, and then click **Copy**.<br><br>3. Enter the copied link in **Redirect link** in the SealSuite Admin Console. Replace the leading `https://` with `lark://` and keep the rest of the link unchanged. |
|Open Service Desk (on\-call account) |To direct employees to a service desk such as an IT on\-call account, first select how the service desk receives requests, and then obtain the corresponding share link:<br><br><br>1. Open **Workplace** in Lark, search for **Service Desk**, and enter its Admin Console.<br><br>   If no service desk has been created, create the required service desk first.<br><br>2. Go to **Settings Center \> Share Service Desk**, and select a sharing scenario based on reception requirements. The differences between the two scenarios are as follows:<br><br>   * **Enter the service desk welcome page**: Employees enter the welcome page and receive a greeting, recommended questions, or category cards. Configure the related content in **Settings Center \> Service Desk Welcome Page**.<br><br>   * **Invite human agents based on routing skills**: Employees enter a customer service group, and the system invites agents who match the user's question based on routing skills. This scenario does not display greetings, recommended questions, or category cards. Configure routing skills in **Settings Center \> Ticket Assignment \> Routing Skills**.<br><br>3. Click the **Link** button on the right of the target scenario, and copy the share link.<br><br>4. Enter the link in **Redirect link** in the SealSuite Admin Console. Replace the leading `https://` with `lark://` and keep the rest of the link unchanged. |

### DingTalk

DingTalk can open the client, a specified one\-to\-one conversation, or an Employee Service Desk bot. Select the appropriate configuration based on your enterprise support method.

|Redirect scenario |Configuration method |
|---|---|
|Open the DingTalk client |Enter `dingtalk://` in **Redirect link**. The DingTalk client opens after employees click the entry point. |
|Open a specified one\-to\-one conversation |To let employees directly contact a specific owner, use the following link format:<br><br>`dingtalk://dingtalkclient/action/sendmsg?dingtalk_id={id}`<br><br>Replace `{id}` with the owner's DingTalk ID. The DingTalk ID is available in **Me \> Personal information** on the DingTalk mobile app. After replacement, enter the complete link in **Redirect link** in the SealSuite Admin Console. |
|Open an Employee Service Desk bot |This method requires a DingTalk enterprise administrator to obtain the service desk link. Configure it as follows:<br><br><br>1. In DingTalk, go to **Workplace \> Process Efficiency \> Employee Service Desk**.<br><br>2. Find **Bot conversation QR code** and copy the link.<br><br>3. Paste the copied link into **Redirect link** in the SealSuite Admin Console. After employees click the IT Assistant entry point, the corresponding DingTalk Service Desk bot opens. |

### WeCom

To open the WeCom client, enter `wxwork://` in **Redirect link**.

### Web\-based online chat

If your enterprise provides support through a web\-based chat channel, you can directly configure the URL of the chat page. The following example uses a Slack channel:

1. Open the channel used to provide support in Slack for Web, such as the enterprise IT support channel.

2. Copy the URL of the channel page.

3. Enter the complete URL in **Redirect link** in the SealSuite Admin Console. After employees click the entry point, the web chat page opens.

### Web\-based help center

If your enterprise provides self\-service support through a web\-based help center, configure it as follows:

1. Open the help center web page to provide to employees, and copy its complete URL.

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/it-tools-en-20261023/lark-help-final.png)

2. Enter the URL in **Redirect link** in the SealSuite Admin Console. After employees click the entry point, the corresponding web\-based help center opens.

After entering the link, return to the configuration steps to check the preview and redirect target, and then save the configuration.

> **说明**

> To use a redirect target other than the preceding options, contact SealSuite staff for confirmation.

## Client experience and usage

The service entry point is in the lower\-left corner of the **Help** page in the desktop client. An administrator can customize the icon, name, and redirect link. The configuration page does not provide settings for the entry point position. After employees click the entry point, the corresponding client, conversation, service desk, or web page opens based on the configured link.

For steps to obtain links for different types of targets, required formats, and notes, see [Obtain and enter a redirect link](https://docs.byteplus.com/docs/sealsuite/docs-configuring-expert-services-#doxcnv2LtyBZzeb3ggT9bMNiZYf).

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a338b0608eda49a6ba27fee6ae44fdb7~tplv-goo7wpa0wc-topic.webp)
