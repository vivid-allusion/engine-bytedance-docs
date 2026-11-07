---
title: "Receiving alert notifications through the Feishu application bot"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Receiving_alerting_notifications_through_Lark_application_robot"
---

VMP supports multiple alert notification methods. You can use the Feishu application bot to receive alerts generated in VMP. This topic describes the procedure and considerations for receiving alerts by Lark application robot.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A VMP workspace has been created. For more details, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

* Cloud services or custom businesses have been integrated with VMP. For details, see [Integration guide](https://docs.byteplus.com/en/docs/vmp/Monitoring-overview).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

VMP allows you to receive alerts and achieve alert claims and silence with a few clicks by using the Lark application robot.

<span id=".5q2l6aqk5LiA77ya6I635Y-W6aOe5Lmm5bqU55So5py65Zmo5Lq6"></span>
### Step 1: Obtain the Lark application robot

Before you use the Lark application robot, you need to first apply for it in the [Lark Application Center](https://app.feishu.cn/all) and add the application robot to the current organization. Procedure:


1. Log in to Lark as an Identity and Access Management (IAM) user.

2. Enter **Application center** in the search box and press Enter to go to the Lark Application Center.

3. Search for **Vital Managed Service for Prometheus Alerting** in the Feishu Application Center to find the application bot. Click **Apply for Use** and wait for approval by the administrator.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you cannot search for the application robot or cannot apply to obtain it after searching, contact your Lark administrator.   </div>
   

4. Log in to the [Lark management platform](https://ecnczee95qqe.feishu.cn/admin/appCenter/manage/cli_a68c28beb273900b?lang=zh-CN) by using the administrator account and grant application permissions for the **Vital Managed Service for Prometheus Alerting** application bot. Click **Configure next to Contact Data Scope Covered by the Preceding Permissions** to add IAM users. After alert notifications are received, IAM users with permissions can view the operator information.


<span id=".5q2l6aqk5LqM77ya5re75Yqg6aOe5Lmm5bqU55So5py65Zmo5Lq6"></span>
### Step 2: Add the Lark application robot

After the Lark application robot is added to the current organization, you need to add a bot to the alert group. Procedure:


1. Create or find the group that needs to receive alerts. Click the `...` icon in the upper right corner of the group, and click **Settings** on the drop\-down menu.



&nbsp;

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6a5178e59219015e76e17c1f46cb3556.png) </span>



&nbsp;

2. In the pop\-up window, click **Bots** \> **Add Bot**.



&nbsp;

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0ad3813aadc3172004fee2a04d3457dc.png) </span>



&nbsp;

3. In the bot list, find **Vital Managed Service for Prometheus Alerting** and click **Add** next to it to add the bot to the group.


<span id=".5q2l6aqk5LiJ77ya6YWN572u5ZGK6K2m6IGU57O75Lq6"></span>
### Step 3: Configure an alert contact

When you configure alert contacts in the VMP console, you can choose to receive alert notifications by Feishu group. Procedure:


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the left navigation pane, click **Alert Center \> Alert Notification Policy**. Click the **Notification contact** tab.

3. Click **Create notification contact** to configure the alert notification contact. Enter the Lark group name and search for and select the alert receiving group where the Lark application robot is located in the **Lark group** field.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_51ba20a79cc3966433ff645acfe3efc3.png) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you cannot search and obtain the Lark group, you need to click <strong>To authorize</strong> to go to the Lark authorization page for authorization.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">VMP will not recognize which groups contain a Feishu bot. You need to select the group with a Feishu bot. Otherwise, alert notifications may not be received as expected.   </div>
   

4. Click **Add** to complete the configuration.


<span id=".5q2l6aqk5Zub77ya6YWN572u5ZGK6K2m6IGU57O75Lq657uE"></span>
### Step 4: Configure an alert contact group


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the left navigation pane, click **Alert Center \> Alert Notification Policy**. Click the **Notification contact** tab.

3. Click **Create notification contact**. Select **Contact group** for the Object type parameter, configure the alert notification contact group, and add users to this group.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_753de1f458fb55a13636a4d94a1a20d1.png) </span>

4. Click **Add** to complete the configuration.


<span id=".5q2l6aqk5LqU77ya6YWN572u5ZGK6K2m6YCa55-l562W55Wl"></span>
### Step 5: Configure an alert notification policy


1. In the left navigation pane, click **Alert Center \> Alert Notification Policy**. Click the **Policy list** tab.

2. Click **Create notification policy** and configure the alert notification policy. Notification method: Select **Lark application robot**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e6d2a84ca541da9db2d2beff5b7116ad.png) </span>

3. Click **Add** to complete the configuration.


<span id=".5q2l6aqk5YWt77ya6YWN572u5ZGK6K2m6KeE5YiZ"></span>
### Step 6: Configure an alert rule


1. In the left navigation pane, click **Alert Center \> Alert Rule**.

2. Click **Create \> Create manually** to configure an alert rule. Here:

   1. Select the **workspace** to which the alert rule applies.

   2. Configure the query statement. `count(up) by (job)` is used in this example.

   3. Configure a trigger policy. You can specify different thresholds for different levels of alerts.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d8544439bce7a45200d1ed4c5583c6a8.png) </span>

   4. Configure an alert notification. Specify the **Notify policy** and **Aggregation policy** parameters.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5c64e0cac10fee4d5a88d0d12224796c.png) </span>

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If you have not configured an aggregation policy, you can directly use the system default policy, named "default". For the configuration method of an aggregation policy, see <a href="https://docs.byteplus.com/en/docs/vmp/Creating-alerting-aggregation-rules">Creating alert aggregation policies</a>.      </div>
      

3. Click **Add** to complete the configuration.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

<span id=".5o6l5pS25ZGK6K2m"></span>
### Receive alerts

After alert\-related configurations are complete, alert notifications will be sent to Feishu through the Feishu application bot when an alert that meets the alert rule is generated. In this case, you can receive the details of alert notifications in the Lark group.

<span id=".5LiA6ZSu6Z2Z6buY5ZGK6K2m"></span>
### Silence alerts with a few clicks

After you receive a Feishu alert notification, you can **claim** or **silence** the alert by clicking the button at the bottom of the notification.


* Click **Claim** at the bottom of the notification to claim the alert.

* Click the default silence duration buttons at the bottom of the notification (**3h, 12h, 1d, and 3d**), the system will automatically create a silence policy to silence the alert. You can view the silence policy that is automatically generated in the VMP console.

* Click **Cancel** to cancel alert silence.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The alert silence policy that is automatically generated takes effect when the button is clicked. The alert silence policy does not take effect at the time when the alert is generated or received.</div>


* <div data-tips="true" data-tips-type="tip">If you click the default silence duration button at the bottom of the alert notification multiple times, the duration of the silence policy will be automatically refreshed but will not be accumulated.</div>


* <div data-tips="true" data-tips-type="tip">If the default alert silence duration does not meet your business requirements, click <strong>Specify custom silence policy</strong> to manually configure an alert silence policy. For more details, see <a href="https://docs.byteplus.com/en/docs/vmp/create-alerting-silence-rule">Creating alert silence policies</a>.</div>



<span id=".5p-l55yL5ZGK6K2m6Z2Z6buY562W55Wl"></span>
### View alert silence policies


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the top navigation bar, select the target region.

3. Click **Alert center \> Alert suppression policy** in the left navigation bar, and click the **Auto\-generate policy** tab to view the alert silence policies automatically generated by the Feishu application bot.
