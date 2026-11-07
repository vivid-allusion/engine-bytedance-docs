---
title: "Contacts"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Contacts"
---

When configuring a notification policy, if notification messages need to be received via the email, phone, or SMS channels associated with a contact, you need to create a contact. This topic describes how to create and manage a contact.

<span id="7vNFIPZB"></span>
## Limits


* You can create up to 300 contacts.

* Each contact can be associated with up to 10 contact groups.


<span id="RV0lYxc2"></span>
## Create contacts


1. Log in to the [Observability Platform console](https://console.byteplus.com/observe).

2. In the left navigation pane, select "**Alert Center \-\> Notification configuration**" to go to the "Notification configuration" page.

3. On the **Notification object** tab, select **Contacts** to access the contact management page.

4. Click **Create contacts** and configure the relevant parameters as needed.

   
   |Parameter |Description |
   |---|---|
   |Name |Specify a name for the contact as a unique identifier. Duplicate names are not allowed. |
   |Email |The email address to associate with the contact, which is used to receive notification messages sent via the email channel. |
   |Lark username |The Feishu user to associate with the contact, which is used to send notifications via the Feishu group bot and Feishu application bot channels, and @mention or mark as urgent for this account when notifications are sent.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If authorization is missing before associating a Feishu user, click <strong>To authorize</strong> to complete Feishu user authentication and authorization. For more information, see <a href="https://docs.byteplus.com/en/docs/Observability_Platform/Feishu_user_authentication_and_authorization">Feishu user authentication and authorization</a>.</div><br> |
   |Mobile phone number |The phone number to associate with the contact, which is used to receive notification messages sent via the SMS and phone channels, and to @mention this account when notifications are sent via the DingTalk channel. |
   |WeCom account |The WeCom account to associate with the contact, which is used to send notification messages via the WeCom channel, and @mention this account when notifications are sent. |
   |Contact group |The contact group of the contact, which can be used to categorize or batch manage contacts. |
   

4. Return to the contact management page, click **Send verification** next to the email address or phone number, and complete the verification within 24 hours by clicking the link in the message or entering the verification code. Otherwise, alert or event notifications may not be received as expected.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Each email address can receive 1 verification email per minute, and the system can send at most 100 verification emails per minute per account. If either limit is exceeded, the contact is created successfully, but the activation email cannot be received. To receive the activation email, you need to update the email address for the contact later.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Each phone number can receive 1 verification SMS message per minute, and the system can send at most 100 verification SMS messages per minute per account. If either limit is exceeded, the contact is created successfully, but the activation SMS message cannot be received. To receive the activation SMS message, you need to update the phone number for the contact later.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Cloud Monitor will send an email address verification email by using <code>no-reply@notice.volcengine.com</code> and send an alert notification email by using <code>monitor@monitor.volces.com</code>. Therefore, make sure these email addresses are added to the allowlist or related policies of the contact email address to prevent emails from not being received or from being sent to the spam folder due to permission issues.   </div>
   


<span id="CwxAiAEt"></span>
## Manage contacts

Click a button in the "Actions" column to the right of the target contact to perform the corresponding operation. The currently supported management operations are as follows:


|Actions |Description |
|---|---|
|Edit |Edit the configuration information of an existing contact.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">After the email address or phone number of a contact is updated, the system will send a verification message again to the specified email address or phone number. After receiving the verification message, you need to click the link in the message within 24 hours to complete verification. Otherwise, you will not be able to receive alert or event notifications.</div><br> |
|Delete |Delete a contact that is no longer needed.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If a contact is already associated with contact groups or notification policies, deleting the contact will also disassociate the contact groups or notification policies.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If contacts are synchronized by importing VMP notification configuration data, we recommend that you manually delete the contacts from the VMP contact menu in advance. Otherwise, deleted contacts will be recreated. For more information, see <a href="https://docs.byteplus.com/en/docs/Observability_Platform/Importing_VMP_notification_configuration_data">Importing VMP notification configuration data</a>.</div><br> |
