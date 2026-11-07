---
title: "Certificate messages"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/certificate-messages"
---

Certificate messages are sent by the BytePlus Certificate Center and include notifications, alerts, and other messages related to your SSL certificates. This article introduces the recipients, delivery methods, and specific content of certificate messages, as well as how to manage certificate message subscriptions.

<span id="who-will-receive-certificate-messages"></span>
## Who will receive certificate messages

BytePlus Certificate Center sends certificate messages via **Inbox** messages and **Email** to the following three types of contacts.


|Type |Description |Related operations |
|---|---|---|
|Account contact |* When registering a BytePlus account, you can specify an account contact.<br><br>* Account contacts can receive all SSL certificate messages from BytePlus Certificate Center by default. |Subscribe/unsubscribe to certificate messages |
|Message recipient |* You can add message recipients in the [BytePlus Message Center console](https://console.byteplus.com/user/message/person).<br><br>* After subscribing to certificate messages, message recipients can receive all SSL certificate messages from BytePlus Certificate Center. |* Add/remove message recipients<br><br>* Subscribe/unsubscribe to certificate messages |
|Certificate contact |* When submitting a certificate request (in BytePlus Certificate Center), you can specify a certificate contact for the certificate.<br><br>* Certificate contacts are specified through the "information template" parameter and are not applicable to certificates uploaded to BytePlus Certificate Center.<br><br>* Certificate contacts can only receive messages related to their own SSL certificates and cannot unsubscribe from certificate messages. |None |


<span id="topics-covered-by-certificate-messages"></span>
## Topics covered by certificate messages

Certificate messages mainly include the following topics.


|Type |Message topic |Sending condition |Sent to |
|---|---|---|---|
|Notification |SSL Certificate Activation Notification |After you successfully purchase an SSL certificate in BytePlus Certificate Center, BytePlus Certificate Center sends you an SSL certificate activation notification. |Account contact |
||SSL Certificate Order Cancellation Success Notification |After you successfully cancel a certificate order in BytePlus Certificate Center, BytePlus Certificate Center sends you an order cancellation notification. |* Account contact<br><br>* Message recipient<br><br>* Certificate contact |
||SSL Certificate Domain Validation Notification |After the CA returns domain validation requirements, BytePlus Certificate Center sends you a domain validation reminder. ||
||SSL Certificate Issuance Success Notification |After your SSL certificate is successfully issued, BytePlus Certificate Center sends you a certificate issuance notification. ||
||SSL Certificate Issuance Failure Notification |After your SSL certificate issuance fails, BytePlus Certificate Center sends you a certificate issuance failure notification. ||
|Alert |SSL Certificate Revocation Reminder |When your SSL certificate is revoked, BytePlus Certificate Center sends you a certificate revocation reminder. ||
||SSL Certificate Expiration Reminder |30 days, 15 days, 7 days, and 3 days before your SSL certificate expires, BytePlus Certificate Center sends you an expiration reminder.<br><br>If different certificates expire on the same day, reminders are sent together.<br><br>> Example:<br><br>> Suppose you have 2 certificates expiring on the same day. 30 days, 15 days, 7 days, and 3 days before the certificates expire, you will receive an expiration reminder. The reminder message will include these 2 certificates. |* Account contact<br><br>* Message recipient |


<span id="modify-certificate-messages-reception-settings"></span>
## Modify certificate messages reception settings

<span id="applicable-scenarios"></span>
### Applicable scenarios

You can add a new message recipient and subscribe to certificate messages, or modify the subscription status of existing message recipients.

<span id="operation-steps"></span>
### Operation steps


1. Log in to the [BytePlus Message Center console.](https://console.byteplus.com/user/message).

2. In the left navigation bar, click **Settings**.

3. On the **Basic Receive Configuration** page, find **Certificate Notification** under the **Service** category.

4. Modify the reception settings for **Certificate Notification**:

   1. Click **Edit** under the **Actions** column.

   2. In the **Modify message recipient** dialog box, select the message recipients who will receive certificate messages.

      * You can click **Add recipient** to add new message recipients.

      * Account contact is selected by default. If you deselect account contact, the account contact will no longer receive certificate messages.

   3. Click **OK**.


After completing the configuration, the **Message recipient** information for **Certificate Notification** will be updated.

<span id="AKxtRaVT"></span>
## **Disable/Enable certificate expiration alerts**

<span id="CM6wizBi"></span>
### **Applicable scenarios**

If you have a large number of SSL certificates under your BytePlus account, the account contacts and message recipients who have subscribed to certificate messages may frequently receive certificate expiration reminders. To avoid unnecessary disruptions, you can disable expiration alerts for a specific certificate (the BytePlus Certificate Center will no longer send expiration reminders for that certificate).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">Disabling certificate expiration alerts may cause a certificate to expire without being detected in time. Proceed with caution.</div>


<span id="kvqXDXDi"></span>
### **Steps**


1. Log in to the [BytePlus Certificate Center console](https://console.byteplus.com/certificate-center/ssl/overview).

2. In the left navigation bar, select **SSL Certificate** \> **Certificates**.

3. Above the certificate list, click the **Expire soon** card.

   Only certificates that are about to expire trigger expiration alerts and support manually disabling or enabling the alerts.

4. Locate your certificate, and click **Disable expiration alarm** or **Enable expiration alarm** in the **Operations** column.

   * **Disable expiration alarm** applies to certificates for which expiration alerts are currently enabled.

   * **Enable expiration alarm** applies to certificates for which expiration alerts are currently disabled.

5. In the dialog box that appears, click **Confirm**.
