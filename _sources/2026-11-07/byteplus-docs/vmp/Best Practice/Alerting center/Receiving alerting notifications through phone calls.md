---
title: "Receiving alerting notifications through phone calls"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Receiving-alerting-notifications-through-mobile-phone"
---

VMP supports multiple alert notification methods. You can use your phone number to receive alerts generated in VMP. This topic describes the procedure and considerations for receiving alerts by phone.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Alert notifications are received only by phone for alerts of the P0 level.</div>


* <div data-tips="true" data-tips-type="warning">Only phone numbers in China's mainland are supported.</div>



<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A VMP workspace has been created. For more details, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

* Cloud services or custom businesses have been integrated with VMP. For more details, see [Integration guide](https://docs.byteplus.com/en/docs/vmp/Monitoring-overview).

* You have a phone number in China's mainland with voice and data services activated.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya6YWN572u5ZGK6K2m6IGU57O75Lq6"></span>
### Step 1: Configure an alert contact


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the left navigation pane, click **Alert Center \> Alert Notification Policy**. Click the **Notification contact** tab.

3. Click **Create notification contact** to configure the alerting notification contact. In the **cell phone** section, enter the phone number of the alert contact.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_de853d764feb1aab7a0e603d51999b5b.png) </span>

4. Click **Add** to complete the configuration.


<span id=".5q2l6aqk5LqM77ya5a6M5oiQ5omL5py66aqM6K-B"></span>
### Step 2: Complete phone number verification

After you save the alert contact, the system will automatically send a verification text message to the phone number you configured. Procedure:


1. Use your phone number to receive the verification text message.

2. Click the link in the text message to verify the phone number. After verification is complete, you can view the verification result of the phone number in the contact list. If the mobile phone number column displays<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5d8cda5ce832705b9cf10c52aeb6e484.png) </span>, it indicates that the phone number passed the verification.


<span id=".5q2l6aqk5LiJ77ya6YWN572u5ZGK6K2m6IGU57O75Lq657uE"></span>
### Step 3: Configure an alert contact group


1. In the left navigation pane, click **Alert Center \> Alert Notification Policy**. Click the **Notification contact** tab.

2. Click **Create notification contact**. Select **Contact group** for the Object type parameter, configure the alert notification contact group, and add users to this group.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_753de1f458fb55a13636a4d94a1a20d1.png) </span>

3. Click **Add** to complete the configuration.


<span id=".5q2l6aqk5Zub77ya6YWN572u5ZGK6K2m6YCa55-l562W55Wl"></span>
### Step 4: Configure an alert notification policy


1. In the left navigation pane, click **Alert Center \> Alert Notification Policy**. Click the **Policy list** tab.

2. Click **Create notification policy** to configure an alert notification policy. Here:

   * **Alert level**: Select P0.

   * **Notifier**: In the **All contact groups** section, select the check boxes before the names of the contact groups that need to receive alerts to add them to the **Selected contact group** section on the right side.

   * **Notification method**: Select **Telephone**.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f9d99dc4da5233cf853ff0b41204854f.png) </span>

3. Click **Add** to complete the configuration.


<span id=".5q2l6aqk5LqU77ya6YWN572u5ZGK6K2m6KeE5YiZ"></span>
### Step 5: Configure an alert rule


1. In the left navigation pane, click **Alert Center \> Alert Rule**.

2. Click **Create** to configure an alert rule. Here:

   * **Workspace**: Select the workspace to which the alert rule applies.

   * **Query statement**: Use PromQL to configure the query statement. `count(up) by (job)` is used in this example.

   * **Trigger policy**: Specify the trigger thresholds for different levels of alerts. You can specify different thresholds for different levels of alerts.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d8544439bce7a45200d1ed4c5583c6a8.png) </span>

   * Configure an alert notification. Specify the **Notify policy** and **Aggregation policy** parameters.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5c64e0cac10fee4d5a88d0d12224796c.png) </span>

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If you have not configured an aggregation policy, you can directly use the system default policy, named "default". For the configuration method of an aggregation policy, see <a href="https://docs.byteplus.com/en/docs/vmp/Creating-alerting-aggregation-rules">Creating alert aggregation policies</a>.      </div>
      

3. Click **Add** to complete the configuration.


<span id=".5p-l55yL57uT5p6c"></span>
## View results

After alert\-related configurations are complete, the system will make an alert phone call to your verified phone number when an alert that meets the alert rule is generated.
