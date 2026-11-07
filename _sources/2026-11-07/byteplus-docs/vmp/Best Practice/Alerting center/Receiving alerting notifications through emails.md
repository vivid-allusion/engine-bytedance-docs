---
title: "Receiving alerting notifications through emails"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Receiving-alerting-notifications-through-email"
---

VMP supports multiple alert notification methods. You can receive alerts generated in VMP through emails. This topic describes the procedure and considerations for receiving alerts by email.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A VMP workspace has been created. For more details, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

* Cloud services or custom businesses have been integrated with VMP. For more details, see [Integration guide](https://docs.byteplus.com/en/docs/vmp/Monitoring-overview).

* An email address used for receiving alerts is created.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya6YWN572u5ZGK6K2m6IGU57O75Lq6"></span>
### Step 1: Configure an alert contact


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the left navigation pane, click **Alert Center \> Alert Notification Policy**. Click the **Notification contact** tab.

3. Click **Create notification contact** to configure the alerting notification contact. Enter the email address that is used for receiving alerts in the **Email** field.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a5d92241361fd7f7b3fefbcdeea16496.png) </span>

4. Click **Add** to complete the configuration.


<span id=".5q2l6aqk5LqM77ya5a6M5oiQ6YKu566x6aqM6K-B"></span>
### Step 2: Complete email address verification

After you save the alert contact, the system will automatically send a verification email to the email address you configured. Procedure:


1. Log in to your email account and find the verification email sent to you.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_03a9d4f0a19967596b3de1160b870640.png) </span>

2. Click the link in the email to verify the email address.


<span id=".5q2l6aqk5LiJ77ya6YWN572u5ZGK6K2m6IGU57O75Lq657uE"></span>
### Step 3: Configure an alert contact group


1. In the left navigation pane, click **Alert Center \> Alert Notification Policy**. Click the **Notification contact** tab.

2. Click **Create notification contact**. Select **Contact group** for the Object type parameter, configure the alert notification contact group, and add users to this group.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_753de1f458fb55a13636a4d94a1a20d1.png) </span>

3. Click **Add** to complete the configuration.


<span id=".5q2l6aqk5Zub77ya6YWN572u5ZGK6K2m6YCa55-l562W55Wl"></span>
### Step 4: Configure an alert notification policy


1. In the left navigation pane, click **Alert Center \> Alert Notification Policy**. Click the **Policy list** tab.

2. Click **Create notification policy** to configure an alert notification policy. Notification method: Select **Mail**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_685e6d23e7497cf68f552c7dcd2b72e9.png) </span>

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

After alert\-related configurations are complete, alert notifications will be sent to the email address when an alert that meets the alert rule is generated. You can log in to the email account to view the details of alert notifications.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you do not receive an alert email as expected, check the spam box to confirm whether the alert email was mistakenly classified as spam.</div>
