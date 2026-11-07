---
title: "Expiration"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Expiration"
---

Before a Subscription VPN gateway expires, the platform sends reminders via SMS, email, or internal messages based on the specified notification method. You will receive reminders on four different dates: 7 days before expiration, 3 days before expiration, 1 day before expiration, and on the expiration date. To avoid disruption to your business, renew your bandwidth package promptly when receiving the notification.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can set message subscription and notification methods. Before the Subscription resources expire, the platform will send reminders according to your settings. For specific actions, see <a href="https://docs.byteplus.com/en/docs/message_center/Message-Subscription-and-Notification-Methods">Message Subscription and Notification Methods</a>.</div>


<span id=".5Yiw5pyf6K-05piO"></span>
## Expiration

The platform reserves a resource retention period for you, which is 15 days after the expiration. During this period, you can renew the subscription to continue to use the VPN gateway, or unsubscribe to release the VPN gateway immediately. If no action is performed during the retention period, the VPN gateway and related resources will be forcibly withdrawn after this period. The withdrawn resources cannot be recovered.

See the diagram below for the status of resources related to the expired VPN gateway.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_799b7dbccf6ab490ad3ec3e6ba4ec30c.png) </span>

<span id=".5Yiw5pyf6YCA6K6i"></span>
## Unsubscription

Subscription VPN gateways support unsubscripition. Before the resource expires, you can apply for unsubscribing the resource on the Billing center \> Unsubscription management page in the console and then release it. After the resource expires, you can directly delete the resource in the product console to release it.


|Unsubscription type |Description |Related action |
|---|---|---|
|**Pre\-expiration unsubscription** |* 7\-day unconditional unsubscription: For resources that are eligible for the 7\-day unconditional unsubscription, you can request an unsubscription without being asked any questions within 7 days (≦ 7 × 24 hours) after you pay the resource order. After your request is approved, the platform refunds the total paid amount to your account balance. Used coupons cannot be refunded. For more information, see [Seven-day unconditional refund rules](https://docs.byteplus.com/en/docs/6269/81013#.5LiA44CB5LiD5aSp5peg55CG55Sx6YCA6K6i6K-05piO).<br><br>* Excluded from 7\-day unconditional unsubscription: For resources that are excluded from the 7\-day unconditional unsubscription, after the unsubscription application is approved, the amount actually consumed will be deducted based on the used duration and monthly (or yearly) unit price; and the remaining actual payment will be refunded to the account balance. Used coupons cannot be refunded. For more information, see [Non-seven-day unconditional unsubscribe rules](https://docs.byteplus.com/en/docs/6269/81013#.5LqM44CB6Z2e5LiD5aSp5peg55CG55Sx6YCA6K6i6K-05piO). |* [Unsubscribing a VPN gateway via Billing Center](https://docs.byteplus.com/en/docs/6269/81013#.5Zub44CB5pON5L2c5q2l6aqk)<br><br>* [Unsubscribing VPN gateway via VPN Gateway console](https://docs.byteplus.com/en/docs/vpn/Unsubscribe-VPN-gateway)<br><br><br> |
|**Post\-expiration unsubscription** |For an expired Subscription VPN gateway that is still within the retention period, if you are certain that you will not use the VPN gateway any more, you can directly delete the VPN gateway in the VPN gateway console. Related resources are released right after the deletion and cannot be restored. |[Deleting a VPN gateway](https://docs.byteplus.com/en/docs/vpn/Deleting-a-VPN-gateway) |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The platform reserves the right to reject unsubscription requests that appear to be suspicious or malicious.</div>


<span id=".5Yiw5pyf57ut6LS5"></span>
## Renewal

Before a Subscription VPN gateway expires, the platform sends reminders via SMS, email, or internal messages based on the specified notification method. You will receive reminders on four different dates: 7 days before expiration, 3 days before expiration, 1 day before expiration, and on the expiration date. To avoid affecting your business, please renew in a timely manner after receiving the reminder.


* Modifying the Bandwidth of VPN gateway during the renewal is not supported. If necessary, you can modify it after renewal.

* For a yearly Subscription VPN gateway, if its usage duration is less than one year, no annual discount is offered for new billing items incurred by configuration modifications.

* The renewal start time is the original expiration time if you renew within 12 hours (exclusive) after the expiration. If you renew from 12 hours (inclusive) up to 15 days (exclusive) after the expiration, the renewal start time is the actual renewal time.


<span id=".5omL5Yqo57ut6LS5"></span>
### Manual renewal

Manual renewal is available for a resource at any point between its successful purchase and its scheduled release.


1. Log in to the VPN gateway console.

2. In the top menu bar, select a target region and project.

3. In the VPN gateway list, click Renewal in Actions column of the VPN gateway to be renewed. The page then navigates to the Billing center \> Renewal page.

4. In the lower\-left section of the Renew page, specify the renewal period and then click Pay in the lower\-right corner.

5. After confirming the order information is correct, complete the payment according to the interface prompts.

   After submitting the payment information, complete the payment within the specified time. Otherwise, the order will be canceled.


<span id=".6Ieq5Yqo57ut6LS5"></span>
### Automatic renewal

The platform supports automatic renewal. After enabling automatic renewal, the system automatically deducts the renewal fee from your balance 7 days before the expiration. When purchasing a Subscription VPN gateway, you can check the Automatic renewal option or change manual renewal to automatic renewal.

You can actively enable automatic renewal before the resource expiration. After enabling automatic renewal, the system will prioritize using available vouchers during renewal.


1. Log in to [the Billing center console](https://console.byteplus.com/finance/accountOverview/).

2. In the left navigation pane, click **Renewal Management**.

3. On the **Manual renewal** tab of the Renewal Management page, click  **··· \> Enable auto\-renewal** in Actions column of the resource to be renewed.

   > You can change manual renewal to automatic renewal only before the VPN gateway instance expires.   
   

4. On the **Auto\-renewal** page, specify the interval for auto\-renewal in the lower\-left section, set the auto\-renewal time, and then click **Enable** to enable automatic renewal.

   > If you do not select Custom for auto\-renewal times, automatic renewal is permanently effective. The system performs automatic renewal each time the resource expires based on the interval for auto\-renewal set for the single automatic renewal.
