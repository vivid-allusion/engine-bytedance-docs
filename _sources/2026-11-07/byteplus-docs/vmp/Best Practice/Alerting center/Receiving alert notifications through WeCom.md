---
title: "Receiving alert notifications through WeCom"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Receiving_alerting_notifications_through_Wecom"
---

VMP supports multiple alert notification methods. You can use the standard WeCom bot to receive alerts generated in VMP. This topic describes the procedure and considerations for receiving alerts by WeCom.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A VMP workspace has been created. For more details, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

* Cloud services or custom businesses are integrated with VMP. For more details, refer to [Integration guide](https://docs.byteplus.com/en/docs/vmp/Monitoring-overview).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya6YWN572u5LyB5Lia5b6u5L-h5py65Zmo5Lq6"></span>
### Step 1: Configure the WeCom robot


1. Log in to WeCom with your account and create or find the group that needs to receive alerts. Click the `...` icon in the upper right corner of the group, and click **Add Group Robot** on the drop\-down menu.

2. Check the definition of the group robot and click **Add Robot**.

3. Click **Create Robot** and specify a name for the group robot. Click **Add Robot** to add the robot to the group and obtain the webhook address of the robot. Click **Copy Address** to copy the webhook address of the robot, which will be used in the subsequent configuration.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more details of the configuration and descriptions of the WeCom group robot, refer to the <a href="https://open.work.weixin.qq.com/help2/pc/14931?person_id=1&is_tencent=">official documentation of WeCom</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you cannot find or add the robot, contact your WeCom administrator.   </div>
   


<span id=".5q2l6aqk5LqM77ya6YWN572u5ZGK6K2m6IGU57O75Lq6"></span>
### Step 2: Configure an alert contact


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the left navigation pane, click **Alert Center \> Alert Notification Policy**. Click the **Notification contact** tab.

3. Click **Create notification contact** to configure the alerting notification contact. Here:

   * Select the **WeCom robot** check box for the **Webhook** parameter.

   * Paste the webhook address of the WeCom robot in the **WeCom robot** field.

   * (Optional) In the **People who need @**  field, enter the IDs of the personnel mentioned when alerts are being triggered and press Enter to confirm. For the method of obtaining the IDs of WeCom users, refer to the [official documentation of WeCom](https://developer.work.weixin.qq.com/document/path/90665#userid).

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_77349b9abd421ec113f8122791d16a87.png) </span>

4. Click **Verify** to check the connectivity between VMP and the WeCom robot. When the verification is passed, the WeCom robot will prompt that the connection is successful in the WeCom group.

5. Click **Add** to complete the configuration.


<span id=".5q2l6aqk5LiJ77ya6YWN572u5ZGK6K2m6IGU57O75Lq657uE"></span>
### Step 3: Configure an alert contact group


1. In the left navigation pane, click **Alert Center \> Alert Notification Policy**. Click the **Notification contact** tab.

2. Click **Create notification contact**. Select **Contact group** for the Object type parameter, configure the alert notification contact group, and add users to this group.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_753de1f458fb55a13636a4d94a1a20d1.png) </span>

3. Click **Add** to complete the configuration.


<span id=".5q2l6aqk5Zub77ya6YWN572u5ZGK6K2m6YCa55-l562W55Wl"></span>
### Step 4: Configure an alert notification policy


1. In the left navigation pane, click **Alert Center \> Alert Notification Policy**. Click the **Policy list** tab.

2. Click **Create notification policy** to configure an alert notification policy. Notification method: Select **WeCom robot**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e8ff7ed92ef6ccd1266b202fad1eca9e.png) </span>

3. Click **Add** to complete the configuration.


<span id=".5q2l6aqk5LqU77ya6YWN572u5ZGK6K2m6KeE5YiZ"></span>
### Step 5: Configure an alert rule


1. In the left navigation pane, click **Alert Center \> Alert Rule**.

2. Click **Create** to configure an alert rule. Here:

   * Select the **workspace** to which the alert rule applies.

   * Configure the query statement. `count(up) by (job)` is used in this example.

   * Configure a trigger policy. You can specify different thresholds for different levels of alerts.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d8544439bce7a45200d1ed4c5583c6a8.png) </span>

   * Configure an alert notification. Specify the **Notify policy** and **Aggregation policy** parameters.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5c64e0cac10fee4d5a88d0d12224796c.png) </span>

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If you have not configured an aggregation policy, you can directly use the system default policy, named "default". For the configuration method of an aggregation policy, see <a href="https://docs.byteplus.com/en/docs/vmp/Creating-alerting-aggregation-rules">Creating alert aggregation policies</a>.      </div>
      

3. Click **Add** to complete the configuration.


<span id=".5p-l55yL57uT5p6c"></span>
## View results

After alert\-related configurations are complete, alert notifications will be sent to WeCom through the WeCom bot when an alert that meets the alert rule is generated. In this case, you can receive the details of alert notifications in the WeCom group.

Click **Alert Details** to go to the **Alert event** page to view the detailed information of the alerts. For more details, refer to [Viewing alerts](https://docs.byteplus.com/en/docs/vmp/Viewing-alerts).
