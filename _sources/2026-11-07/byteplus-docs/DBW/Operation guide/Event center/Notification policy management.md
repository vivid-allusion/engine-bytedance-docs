---
title: "Notification policy management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Notification_policy_management"
---

Notification policies define the notification channels, recipients, and sending rules after an alarm is triggered. They support configuring notification time periods and escalation rules to ensure that abnormal information reaches the relevant personnel accurately, preventing missed alarms or notification fatigue, and ensuring efficient and timely operations response. This topic describes how to configure contacts, contact groups, and callback URLs for event notifications.

<span id="pMKFpSfs"></span>
## Prerequisite


* Contacts and contact groups have been created. For detailed operations, see [a contact](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-contact-and-an-alarm-contact-group?lang=en)[a contact](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-contact-and-an-alarm-contact-group?lang=en) or [a contact group](https://docs.byteplus.com/en/docs/cloudmonitor/Editing-an-alarm-contact?lang=en)[a contact group](https://docs.byteplus.com/en/docs/cloudmonitor/Editing-an-alarm-contact?lang=en).

* When using a bot for notifications, you need to configure a callback URL. For detailed operations, see [Callback URL](https://docs.byteplus.com/en/docs/cloudmonitor/Managing-callback-address?lang=en).


<span id="WFGb1gpz"></span>
## Precautions

Among notification methods, Feishu group messages, DingTalk bots, and WeCom bots are mutually exclusive. You can select only one of these channels at a time.

<span id="9ejrbhmc"></span>
## Procedure


<Tabs>
<Tab zoneid="zr1IyxqkYD" title="Create notification policy">
<TabTitle>Create notification policy</TabTitle>

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. In the left navigation bar, select **Event center** \> **Notification policy**.

4. In the **Create notification policy** dialog box, configure the following information.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Policy name** |Customize the policy name. The length must not exceed 64 characters. |
   |**Policy description** |(Optional) Configure the policy purpose as needed. It is recommended to align it closely with your business. |
   |**Alert level configuration methods** |Supports **Tiered configuration** and**Global configuration**. |
   |**Level notification** |When **Alert level configuration methods** is set to **Tiered configuration**, this parameter can be configured. The levels include **Serious**, **Warning**, and **Notification**. |
   |**Notification policy** |When **tiered configuration** is selected, you need to configure a corresponding notification policy for each alarm level. When **global configuration** is selected, all alarm levels share the same notification policy. The parameter configuration of the notification policy is the same.<br><br><br>* **Notification method**: You can select **Feishu group message**, **Email**, **SMS**, **Telephone**, **DingTalk**, or **WeCom**.<br><br>   * Feishu group message, DingTalk bot, and WeCom bot are mutually exclusive; you cannot select more than one of these three channels at the same time.<br><br>   * Email notifications require the contact's email address, while telephone and SMS notifications require the contact's mobile number.<br><br>* **Notification object**: When Email, SMS, or Telephone is selected under Notification method**Email**, **SMS**, or **Telephone** is selected under Notification method, you can configure the notification object. The notification object supports two receiving methods: **Contact group** and **Contact**.<br><br><br>Contacts and contact groups are maintained by Cloud Monitoring. For more information, see [Create](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-contact-and-an-alarm-contact-group?lang=en) [Contact](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-contact-and-an-alarm-contact-group?lang=en) or [Create](https://docs.byteplus.com/en/docs/cloudmonitor/Editing-an-alarm-contact?lang=en) [Contact group](https://docs.byteplus.com/en/docs/cloudmonitor/Editing-an-alarm-contact?lang=en).<br><br><br>* **Callback URL**: Select a callback URL from the drop\-down list.<br><br><br>When Feishu group message, DingTalk, or WeCom is selected under Notification method, you need to configure the corresponding callback URL. The callback URL is maintained by Cloud Monitoring and can be selected from the dropdown list. For detailed operations, see [Callback URL](https://docs.byteplus.com/en/docs/cloudmonitor/Managing-callback-address?lang=en). |
   

5. Click **OK**.


</Tab>
<Tab zoneid="JcsWIz8wgU" title="View notification policy">
<TabTitle>View notification policy</TabTitle>

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. In the left navigation bar, select **Event center** \> **Notification policy**.

4. On the **Notification policy** page, view the notification policy list and details:

   * View the notification policy list, including the **Policy name**, **Notification level**, and **Notification channel**.

   * View notification policy details: click **Details** in the **Actions** column of the target policy. On the **Notification policy details** page, view the following information:

      * Basic information: includes the **Policy name**, **Policy ID**, **State**, **Creation time**, **Modification time**, and **Description**.

      * Notification configuration: includes the **Notification method**, **Callback URL**, **Notification object**, and other information.


</Tab>
<Tab zoneid="dhIRxO1lq8" title="Edit notification policy">
<TabTitle>Edit notification policy</TabTitle>

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. In the left navigation bar, select **Event center** \> **Notification policy**.

4. On the **Notification Policy** page, click **Edit** in the **Actions** column of the target policy.

5. In the **Edit Notification Policy** dialog box, configure the following information.

6. 
|**Parameter** |**Description** |
|---|---|
|**Policy name** |Customize the policy name. The length must not exceed 64 characters. |
|**Policy description** |(Optional) Configure the policy purpose as needed. It is recommended to align it closely with your business. |
|**Alert level configuration methods** |Supports **Tiered configuration** and**Global configuration**. |
|**Level notification** |When **Alert level configuration methods** is set to **Tiered configuration**, this parameter can be configured. The levels include **Serious**, **Warning**, and **Notification**. |
|**Notification policy** |When **tiered configuration** is selected, you need to configure a corresponding notification policy for each alarm level. When **global configuration** is selected, all alarm levels share the same notification policy. The parameter configuration of the notification policy is the same.<br><br><br>* **Notification method**: You can select **Feishu group message**, **Email**, **SMS**, **Telephone**, **DingTalk**, or **WeCom**.<br><br>   * Feishu group message, DingTalk bot, and WeCom bot are mutually exclusive; you cannot select more than one of these three channels at the same time.<br><br>   * Email notifications require the contact's email address, while telephone and SMS notifications require the contact's mobile number.<br><br>* **Notification object**: When **Email**, **SMS**, or **Telephone** is selected under **Notification method**, you can configure the notification object. The notification object supports two receiving methods: **Contact group** and **Contact**.<br><br><br>Contacts and contact groups are maintained by Cloud Monitoring. For more information, see [Create](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-contact-and-an-alarm-contact-group?lang=en) [Contact](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-contact-and-an-alarm-contact-group?lang=en) or [Create](https://docs.byteplus.com/en/docs/cloudmonitor/Editing-an-alarm-contact?lang=en) [Contact group](https://docs.byteplus.com/en/docs/cloudmonitor/Editing-an-alarm-contact?lang=en).<br><br><br>* **Callback URL**: Select a callback URL from the drop\-down list.<br><br><br>When Feishu group message, DingTalk, or WeCom is selected under Notification method, you need to configure the corresponding callback URL. The callback URL is maintained by Cloud Monitoring and can be selected from the dropdown list. For detailed operations, see [Callback URL](https://docs.byteplus.com/en/docs/cloudmonitor/Managing-callback-address?lang=en). |


7. Click **OK**.


</Tab>
<Tab zoneid="Ymcsf8w0NP" title="Delete notification policy">
<TabTitle>Delete notification policy</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Once a notification policy is deleted, it cannot be recovered. Proceed with caution.</div>



1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. In the left navigation bar, select **Event center** \> **Notification policy**.

4. On the **Notification policy** page, find the target policy and click  **...**  in the **Actions** column. \> **Delete**.

5. In the **Delete notification policy** dialog box, click **OK**.


</Tab>
</Tabs>
