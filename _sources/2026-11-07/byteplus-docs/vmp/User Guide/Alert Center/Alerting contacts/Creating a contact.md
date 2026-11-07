---
title: "Creating a contact"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Creating-alerting-receivers"
---

When the matching rule of an alert notification policy is triggered, notifications will be sent to the specified contact. This topic describes how to create an alert contact.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The VMP service is activated.

* The alert reception channel is specified and the relevant address is obtained. Addresses include email addresses, webhook addresses, and other addresses.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus).

2. On the top navigation bar, select the target region.

3. On the left navigation bar, click **Alert center \> Alerting notification policy**. Click the **Notification contact** tab.

4. Click **Create notification contact** to configure the alert notification contact.

   * Specify the basic information of the alert notification contact.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a0e8688ae788b196ba078789b7cc8fb7.png) </span>

      
      |**Parameter** |**Description** |
      |---|---|
      |Object type |Select the type of alerttification object. For this example, select **Contact person**. |
      |Name |Specify the name of the alerttification contact. |
      |Email |Configure the email address of the alerttification contact for receiving alert notifications.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After you configure the email address, the system will automatically send a confirmation email to your email address. You need to log in to your email account and confirm within 24 hours. In this way, you can use this email address to receive alert notifications as expected.</div><br> |
      |cell phone |Specify the mobile number of the alert notification contact.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Alert notifications are received only by phone for alerts of the P0 level.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Only mobile numbers in the Chinese mainland are supported.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After you configure the mobile number, the system will automatically send a confirmation message to your mobile phone. You need to click the link in the message and confirm within 24 hours to use the mobile number to receive alerts as expected.</div><br> |
      |Feishu group |Configure the Feishu group that receives alert notifications when you use a Feishu application robot. If you cannot search for the Feishu group, click To authorize to go to the Feishu authorization page. |
      

   * (Optional) Configure the webhook authentication information.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ce12fed33bd20561f6539a861af8f12d.png) </span>

      
      |**Parameter** |**Description** |
      |---|---|
      |Webhook |Select the method of receiving alert notifications based on the webhook. You can select multiple options. Valid values:<br><br><br>* **Generic webhook**: Alert notifications are received by standard webhook.<br><br>* **Larkbot**: Alert notifications are received by Larkbot.<br><br>* **DingTalk robot**: Alert notifications are received by DingTalkBot.<br><br>* **WeCom robot**: Alert notifications are received by WeCom robot. |
      |Generic webhook |Configure the standard webhook address for receiving alert notifications.<br><br><br>* **Token**: (Optional) Specify whether token authentication is required. When you select this option, you need to configure the token used for authentication.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">In the Generic webhook field, you cannot enter the webhook addresses of the Larkbot, DingTalkBot, or WeCom robot. Alert notifications may not be received as expected due to different formats. For the format of the generic webhook, refer to <a href="https://docs.byteplus.com/en/docs/vmp/general-webhook-format">Generic webhook format description</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Click <strong>Verify</strong> to check whether the configured webhook address is available.</div><br> |
      |Larkbot |Configure the webhook address of Larkbot for receiving alert notifications.<br><br><br>* **bot key**: (Optional) Specify whether secret key authentication is required. When you select this option, you need to configure the secret key of Larkbot.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Click <strong>Verify</strong> to check whether the webhook address configured for Larkbot is available.</div><br> |
      |DingTalk robot |Configure the webhook address of DingTalkBot for receiving alert notifications.<br><br><br>* **bot key**: (Optional) Specify whether secret key authentication is required. When you select this option, you need to configure the **signing** information about DingTalkBot.<br><br>* **People who need @** : (Optional) Specify alert contacts. Valid values:<br><br>   * **Mobile phone number input**: If you select this option, you can specify alert contacts by using mobile numbers. You can enter multiple contacts. After you enter a mobile number, press Enter to confirm the entry and then enter the next mobile number.<br><br>   * **user ID input**: If you select this option, you can specify alert contacts by using DingTalk user IDs. You can enter multiple contacts. After you enter a user ID, press Enter to confirm the entry and then enter the next user ID.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Click <strong>Verify</strong> to check whether the webhook address configured for DingTalkBot is available.</div><br> |
      |WeCom robot |Configure the webhook address of the WeCom robot for receiving alert notifications.<br><br><br>* **bot ket**: (Optional) Specify whether secret key authentication is required. When you select this option, you need to configure the secret key of the WeCom robot.<br><br>* **People who need @** : (Optional) Specify alert contacts. Valid values:<br><br>   * **Mobile phone number input**: If you select this option, you can specify alert contacts by using mobile numbers. You can enter multiple contacts. After you enter a mobile number, press Enter to confirm the entry and then enter the next mobile number.<br><br>   * **user ID input**: If you select this option, you can specify alert contacts by using WeCom user IDs. You can enter multiple contacts. After you enter a user ID, press Enter to confirm the entry and then enter the next user ID.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">For the method of obtaining WeCom user IDs, refer to the <a href="https://developer.work.weixin.qq.com/document/path/90665#userid">official documentation of WeCom</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Click <strong>Verify</strong> to check whether the webhook address configured for the WeCom robot is available.</div><br> |
      

   * (Optional) Configure the contact group. Add the contact to one or more target contact groups.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_41e01696c874c7f1aace89bc201f95cc.png) </span>

      
      |**Parameter** |**Description** |
      |---|---|
      |Contact group |In the **All contact groups** section, select the check boxes before the names of the target contact groups to add the groups to the **Selected contact group** section.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The system allows you to configure alert notification policies only by using contact groups. Therefore, a contact can receive alert notifications only after it is added to a contact group.</div><br> |
      

5. Click **OK** to complete the configuration.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

When you receive alert notifications by email or phone, you must first verify your email address or mobile number to receive alert notifications as expected. For more details, refer to the following topics:


* [Receiving alert notifications by email](https://docs.byteplus.com/en/docs/vmp/Receiving-alerting-notifications-through-email)

* [Receiving alert notifications by phone](https://docs.byteplus.com/en/docs/vmp/Receiving-alerting-notifications-through-mobile-phone)
