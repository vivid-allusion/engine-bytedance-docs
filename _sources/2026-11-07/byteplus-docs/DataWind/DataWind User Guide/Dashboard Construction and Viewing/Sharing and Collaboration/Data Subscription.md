---
title: "Data Subscription"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Data_Subscription"
---

Users can subscribe to dashboards to receive scheduled data push notifications, making it easy to track business updates. This document provides a detailed introduction to the steps for creating and managing subscriptions, as well as configuring various push methods.

<span id="42f96794"></span>
# Feature overview

Users can subscribe to dashboards to regularly receive dashboard information pushed by the system, allowing close monitoring of recent data changes. At the same time, the product offers subscription management features to help users manage their own subscription records and supports editing subscriptions for dashboards where they have management permissions.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning"><strong>Email subscription prerequisites</strong>: Administrators must first complete<a href="https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f628f7">Office platform integration</a>, and newly added users must provide email information</div>


* <div data-tips="true" data-tips-type="warning"><strong>IM</strong> <strong>subscription prerequisites</strong>: Complete integration with office software (<a href="https://docs.byteplus.com/docs/DataWind/Basic_Configuration_for_Lark_Integration">Basic Configuration for Lark Integration</a>)</div>



<span id="0f899d52"></span>
# Quick start

<span id="a9ed0771"></span>
## Create a subscription


1. On the dashboard viewing page, click the option in the upper right corner of the page, then click "Create subscription" to create a new push notification.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b3175350fb1b401486b0bc08c2e35630~tplv-goo7wpa0wc-image.image) </span>

2. Select the subscription scope, subscription title, subscription description, subscription content, push time, push method, and other settings.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cfc907f055434d52948568a0de48a734~tplv-goo7wpa0wc-image.image) </span>

3. After completing the settings, you can click "Send test". After clicking "Send test", the push bot you configured will send a test subscription (for example, if you set the "Data Platform Push Service" bot here).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7aec3edb590749f99bb7acddaa50eaae~tplv-goo7wpa0wc-image.image) </span>

4. After confirming that the test content is correct, you can click "Confirm" to save the subscription settings. At the same time, the push bot you configured (the "Data Platform Push Service" bot) will send a notification about the subscription creation.

5. Saved subscriptions can be edited and managed in batches in [(Dashboard对应功能文档不发布)Subscription Management](https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f628c3).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6d846713da774c05b120e8450ced8bf9~tplv-goo7wpa0wc-image.image) </span>


<span id="1fa38060"></span>
## Subscription management

Go to [(Dashboard对应功能文档不发布)Subscription Management](https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f628c3), or on the dashboard viewing page, click "Subscription management" to go to the [(Dashboard对应功能文档不发布)Subscription Management](https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f628c3) page, where you can view and manage your subscription records.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/014a0e4269b340b081c722349d0ea0b8~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7ba418f1a70d457db026ffc2af953a74~tplv-goo7wpa0wc-image.image) </span>

<span id="0c9c71f6"></span>
# Feature introduction

<span id="de5ec8f3"></span>
## Subscription scope

<span id="a8fb8eef"></span>
### Dashboard page

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/549f61011c90444db1f1ae6ebd905b29~tplv-goo7wpa0wc-image.image) </span>


* When there are multiple sheets in the dashboard, you can choose to push only certain sheets.

* If multiple sheets or all pages are pushed, the system will take screenshots of each sheet separately and combine them into a single push message.

* The push message will contain as many screenshots as the number of sheets selected.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Currently, subscriptions do not support pushing multiple tabs; only the first tab saved by default will be pushed. To push multiple pages, you can try adding new sheets instead of using tabs.</div>


<span id="a7dad981"></span>
### Based on bookmarks


* The product supports a bookmark feature, which allows you to save the current dashboard view as a bookmark, including selected filter criteria, dynamic dimensions, global parameters, and custom fields of charts. Later, when using the dashboard, you can open the corresponding dashboard view by selecting the bookmark.

* Subscriptions also support sending the content of a bookmark as the subscription content.


**Operation steps**:


1. After configuring the filter criteria and other settings on the current dashboard, click the option in the upper right corner of the dashboard, select Bookmark, and create a bookmark.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb6ec3811ca84459b04d820724fde72b~tplv-goo7wpa0wc-image.image) </span>

2. Select Create subscription, check Based on bookmark within the subscription scope, select the previously created bookmark, and then create the subscription as usual to send the dashboard according to the bookmark content.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/21287683aa184fac9335e8ed880b44e5~tplv-goo7wpa0wc-image.image) </span>


<span id="bf1a7c6d"></span>
### Quick bookmark (subscribe based on the current page state)

In addition to subscribing based on existing bookmark content, when users configure filter criteria on the dashboard, they can also select the "Quick bookmark" option in the subscription. Once selected, the dashboard will send the subscription based on the current page state, without the need to create a bookmark.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2be1dfe46794402abc6187db77a979a2~tplv-goo7wpa0wc-image.image) </span>

<span id="55a28174"></span>
## Push notification

<span id="ee515ec4"></span>
### Subscription title


* Modifying the subscription title is supported. You can choose to include the date; if selected, the subscription title will display the date (for example: "2020\-10\-03 My subscription title").


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You can add a note to the subscription.</div>


   * <div data-tips="true" data-tips-type="tip">You can modify the text font.</div>


   * <div data-tips="true" data-tips-type="tip">You can insert hyperlinks.</div>


   * <div data-tips="true" data-tips-type="tip">You can insert images.</div>


   * <div data-tips="true" data-tips-type="tip">Highlight recipients</div>



<span id="df5d4c88"></span>
### Subscription summary/interpretation

Interpretation of subscription content using AI models is supported. By default, this option is not selected.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">This feature requires purchasing and enabling the Analytics Assistant value\-added module. For details, see <a href="https://docs.byteplus.com/docs/undefined/6a065841837de4052888ff58">Dashboard Intelligent Interpretation</a>.</div>


* <div data-tips="true" data-tips-type="warning">This feature currently only supports subscriptions with the "Lark" push method; other push methods are not supported at this time.</div>



<span id="46981739"></span>
### Content


* Dashboard access link: Selected by default. If deselected, the subscription notification will not include the dashboard access link.

* Dashboard screenshot "full\-size image" / dashboard screenshot "thumbnail image" / dashboard PDF download link.

   * Selected by default. If you clear the selection, the subscription push notifications will not include dashboard screenshots or dashboard PDF download links.

   * You can choose to push dashboard screenshots or dashboard PDF download links.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To receive pushed screenshots, the recipient must be a user of this product. For the DingTalk channel, preview is supported, but non\-product users cannot open and view the content. For the WeCom channel, preview is not supported and non\-product users cannot open and view the content. (This feature is controlled by a switch. If your company needs it, please contact your CSM for further discussion.)</div>


<span id="67eae82f"></span>
### Remarks

Supports adding remarks to the dashboard. The configured remarks will be displayed at the end of the subscription push notification. Both text and hyperlinks are supported, as well as font formatting modifications.


* Screenshot time: Selected by default. If you clear the selection, the subscription will not display the screenshot time (if neither dashboard screenshot nor dashboard PDF download link is selected in the content options, this option will not be available).

* Subscription management link: Selected by default. If you clear the selection, the subscription management link will not be displayed.


<span id="253de410"></span>
## Subscription notification

<span id="647541dd"></span>
### Subscription time

Supports scheduled push, or triggering when data synchronization is complete.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/039a75cf4f0e4768b1737473165dd6e6~tplv-goo7wpa0wc-image.image) </span>

<span id="a0f9f712"></span>
#### Scheduling


* Supports scheduled push. When scheduled push is set, the system will take a dashboard screenshot and push it at the specified time.

* Supports daily, weekly, and monthly push.

* Supports custom scheduling by trading day, working day, or every day.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Because chart data on the dashboard must be queried at the time of subscription, the query time for the charts in the pushed screenshots is before the subscription push.</div>


<span id="e6a1338d"></span>
#### Trigger when data synchronization is complete

Extracted datasets support this feature. (In the privatized version, direct connection datasets can trigger synchronization upon data completion by configuring a dataset that stores "upstream data source readiness configuration information". For details, see [Dataset Management Overview](https://docs.byteplus.com/docs/DataWind/Dataset_Management_Overview).)


* Extracted datasets can be directly set to trigger push when data synchronization is complete. If a dashboard contains multiple charts, each corresponding to different datasets, the synchronization status of the relevant dataset for the specified date will be checked before pushing when this setting is enabled. This ensures that the system does not push data that has not been updated.

* If the data synchronization completion time is later than the scheduled push time, the system will wait until data synchronization is complete before pushing.

* If the dataset's business date is for the previous day (yesterday's business data) and synchronization is completed at 9:00, the subscription will be pushed at 10:30; if synchronization is completed at 12:00, the subscription will be pushed at 12:00.


<span id="97aa83bd"></span>
### Push language


* You can configure the language for subscription push messages.

* If Auto is selected, the system will detect the current language setting and push messages according to the language type configured at the time of subscription.

* Users can also directly select Chinese or English to explicitly specify the push language.


<span id="b91c1e16"></span>
### Push method & recipients

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/323d7c64e842476090ef639acf9a38a1~tplv-goo7wpa0wc-image.image) </span>

Dashboard subscriptions support pushing to: Lark, Lark groups, WeCom, WeCom groups, Webex, Webex groups, email, email groups, DingTalk, DingTalk groups, DingTalk standard groups, general IM, Webhook, and more.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Currently, in privatized environments, the message sending channels for enterprise email and WeCom can be configured separately by project. The steps are as follows:</div>


   * <div data-tips="true" data-tips-type="warning"><strong>Prerequisite configuration (required)</strong>: First, in "System Configuration" \- "Office Platform", connect the enterprise email or WeCom application, and configure multiple sending channels for messages on this page. For detailed steps, see <a href="https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f628f7">Office platform integration</a>.</div>


   * <div data-tips="true" data-tips-type="warning"><strong>Associate by project (optional)</strong>: After completing the prerequisite configuration, go to "System Management" \- "System Settings" \- "Message Push Channels" to associate the sending channels configured in the office platform with specific projects. This step is optional. If project\-level association is not performed, the default sending channel will be used. For detailed steps, see <a href="https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f62a56#ba9f5451">Message push channels</a>.</div>


* <div data-tips="true" data-tips-type="warning">The logic for selecting a push channel when creating a dashboard subscription is as follows:</div>


   * <div data-tips="true" data-tips-type="warning">When the push method <strong>email (group)</strong> is selected, the system will prioritize using the sender email specified for the current project in "Message Push Channel". If the project does not have a specifically associated email, the default email set in "Office Platform" \- "Enterprise Email" will be used.</div>


   * <div data-tips="true" data-tips-type="warning">When the push method <strong>WeCom (group)</strong> is selected, the system will prioritize using the WeCom application specified for the current project in "Message Push Channel". If the project does not have a specifically associated WeCom application, the default application set in "Office Platform" \- "WeCom" will be used.</div>



Users with dashboard view permissions can create subscriptions, but available push methods differ; only administrators (with current dashboard management permissions) can push to groups:


|Push method |Dashboard administrator |Non\-administrator |
|---|---|---|
|Lark, WeCom, DingTalk |Supported |Supported |
|Lark group, DingTalk group |Supported; an application bot must be added to the group |Not supported |
|Email |Supported |Supported |
|Email group |Supported |Not supported |
|Webhook |Supported |Supported |


**IM individual**

When the push method is set to "Lark" (or another IM), the subscription will be pushed via Lark (or the selected IM) to each user in the recipient list.


* After the subscription time is reached, users will receive subscription messages pushed by the "Data Platform Push Service" bot. If the subscription has been confirmed as pushed but the message is not received, please first check whether messages from this bot have been muted.

* Batch user upload is supported. Download the template, enter user information in the template, and select batch upload.


**IM group**

The product supports pushing subscription messages to groups, using Lark groups as an example:

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Caution: There are security risks in pushing "subscription" messages via groups. Please use with caution:</div>



* <div data-tips="true" data-tips-type="warning">When sending "subscription" messages, dashboard authentication will not be performed for members of the group.</div>


* <div data-tips="true" data-tips-type="warning">The members of the group may change, so the recipients of "subscription" messages may also change accordingly, and new members can view "subscription" information in historical messages.</div>


1. The application bot, in this case "Data Platform Push Service", must be added to the Lark group; otherwise, the Lark group will not be able to receive subscription pushes.

2. Click to find the group ID, locate and copy the group ID of the group chat you want to push to (only groups you are a member of can be searched).

3. Enter the group ID and the user whose permissions will determine the data scope for the subscription push.

4. You can click "Add" to set up pushes to multiple group chats at the same time.


**Email**

The product supports pushing subscription emails to individual mailboxes via email.


* Similar to pushing to individuals, batch user upload is supported. You can download the template, enter user information in the template, and select batch upload.


**Email group**

The product supports pushing subscription emails via email groups.


* A permission reference user must be set. The permission reference user determines the scope of data pushed by the subscription. For details, refer to the "Permission reference user" section below.


**Webhook**

To push dashboard subscription messages to enterprise WeChat groups, DingTalk regular groups, Lark external groups, or system APIs, you can select the Webhook push method to receive messages in the enterprise IM group. For specific operations, see [（暂不发布）Webhook Subscription Push Method Configuration](https://docs.byteplus.com/docs/DataWind/Webhook_Subscription_Push_Method_Configuration).

<span id="edc02d4a"></span>
### Permission reference user

When selecting **group or email group** push, you must specify a permission reference user.


* Permission reference user: the user whose permissions determine the content of the push. For example, when a chart's corresponding dataset in the dashboard has row\-level permissions set, selecting different permission reference users may result in different data being pushed. After setting the permission reference user, the referenced user will receive a notification.


<span id="22201827"></span>
### Exception handling


* If there is a chart exception in the dashboard, no push will occur: if any chart in the dashboard has no data, query failure, or query timeout, the dashboard screenshot message will not be sent to the recipient.

* Automatic retry on failure: if the push fails, the system will automatically attempt to resend after 1 hour.

* If any chart data in the dashboard is empty, no push will occur.


<span id="b82888f2"></span>
### Subscription modification notification

If the subscription is modified, a notification can be pushed to the recipient or the creator. The subscription modification notification includes information such as subscription creation, modification, and deletion.

<span id="501bf82b"></span>
## Subscription management

For more operation instructions, see [(Dashboard对应功能文档不发布)Subscription Management](https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f628c3).
