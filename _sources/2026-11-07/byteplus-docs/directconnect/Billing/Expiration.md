---
title: "Expiration"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Expiration"
---

At seven days, three days, and one day before, and on the expiration date for Subscription Direct Connect (DC) resources, BytePlus will send text messages, emails, or internal messages based on your settings to notify you that the DC resources are about to expire. To avoid affecting your business, please renew in a timely manner after receiving the reminder.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can set your message subscription and notification preferences. Before Subscription resources expire, BytePlus will send expiration reminders based on your settings. For details, see <a href="https://docs.byteplus.com/en/docs/message_center/Message-Subscription-and-Notification-Methods">Message Subscription and Notification Methods</a>.</div>


<span id=".5Yiw5pyf5LuL57uN"></span>
## Expiration overview

The port occupancy fee of DC Connections is billed on a subscription basis. For up to 22 days after a subscription expires, the associated port resources are retained. During this grace period, you can renew the subscription to continue using the port, or delete it to trigger immediate resource release. If you perform no actions during the grace period, the port will be forcibly released after this period. The configuration and data related to the port will be deleted and is irrecoverable.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_923ce590c982348fc418e8dafc742496.png) </span>


|Time elapsed since expiration |Resource status |Action description |
|---|---|---|
|From the expiration date until 11:59 on the 16th day |Expired but not suspended |* The resource remains the same as it was before expiration. It is still fully operational and subject to billing.<br><br>* Renewal is supported during this period. The renewed term is backdated to start from the original expiration date, thereby including the current interim period in the new term.<br><br>* The resource expires. Deletion is available. |
|From noon on the 16th day until the end of 22nd day |Expired and suspended |* The resource is suspended. Its dependent configurations are preserved, but the resource itself is frozen and non\-operational. However, because it continues to occupy the port resource, billing still applies.<br><br>* If the resource has Cloud Monitor configured, monitoring is suspended during this period. You cannot create new DC Virtual Interfaces with this resource.<br><br>* Renewal is supported during this period. After renewal, the resource status becomes Available. The renewed term is backdated to start from the original expiration date, thereby including the current interim period in the new term.<br><br>* The resource expires. Deletion is available. |
|After the end of the 22nd day |Resource released |Renewal is no longer supported. DC Connection port resources, dependent DC Virtual Interfaces, and other resources (except DC Gateways) are permanently deleted and cannot be recovered. |


<span id=".5Yiw5pyf6YCA6K6i"></span>
## Unsubscription

Subscription port resources support cancellation. Before the resource expires, you can request an unsubscription through the "Billing center \> Cancellation" page in the BytePlus console. After expiration, you can simply delete the port resource in the Direct Connect console to release it.


|Unsubscription type |Unsubscription description |Related actions |
|---|---|---|
|Pre\-expiration unsubscription |The port occupancy fee for DC Connection is not eligible for the 7\-day free cancellation policy. Upon approval of your unsubscription request, the system will calculate a pro\-rated refund based on your actual usage duration. The remaining balance will be credited to your account, while any coupons used are non\-refundable. For more information, see [Unsubscription Management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management). |* [Unsubscribe DC Connection via Billing center](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management#iv-unsubscription-procedure)<br><br>* [Unsubscribe DC Connection via Direct Connect Connection console](https://docs.byteplus.com/en/docs/directconnect/Unsubscribing_a_Direct_Connect_Connection) |
|Post\-expiration unsubscription |For expired Subscription port resources that are still within the grace period, you can access the Direct Connect Connection console and simply delete any port resources that you have confirmed are no longer needed. The deletion instantly releases the port resources and is irreversible. |[Delete a DC Connection](https://docs.byteplus.com/en/docs/directconnect/Managing-Direct-Connect-connections#.5Yig6Zmk54mp55CG5LiT57q_) |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If suspicious or malicious unsubscription occurs, BytePlus reserves the right to deny your request.</div>


<span id=".5Yiw5pyf57ut6LS5"></span>
## Renewal

At seven days, three days, and one day before, and on the expiration date for Subscription port resources, BytePlus will send text messages, emails, or internal messages based on your settings to notify you that the port resources are about to expire. To avoid affecting your business, please renew in a timely manner after receiving the reminder. For more information, see [Overview of renewal rules](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-of-renewal-rules).


* You cannot modify the port specification when renewing.

* Renewal is supported within 22 days (inclusive) after expiration. The renewed term will be backdated to start from the original expiration date. After 22 days (exclusive) post\-expiration, renewal is not supported and any associated resources will be released.


<span id=".5omL5Yqo57ut6LS5"></span>
## Manual renewal

Manual renewal is available for a resource at any point between its successful purchase and its scheduled release.

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to [the Direct Connect console](https://console.byteplus.com/dc/PhysicalConnection).

2. In the top menu bar, select your target region.

3. In the DC Connection list, click **Renew** in the **Actions** column of the target DC Connection to redirect to the **Billing center \> Renew** page.

4. In the lower\-left section of the Renew page, specify the renewed period and then click **Pay** in the lower\-right corner.

5. After confirming that the order information is correct, click **Next step**.

6. Select a payment method, then click **Pay**.

7. Make the payment by the selected method. After submitting the payment information, complete the payment within the specified time. Otherwise, the order will be canceled.


<span id=".6Ieq5Yqo57ut6LS5"></span>
## Automatic renewal

BytePlus supports automatic renewal. After activating automatic renewal, the system will automatically deduct the renewal fee from your balance 7 days before resource expiration. If there are available coupons in your account, the system will prioritize coupons for payment.


* You can enable automatic renewal by checking **Automatic renewal** when paying the port occupancy fee.

* You can manually switch manual renewal to automatic renewal after paying the port occupancy fee.


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to [the Billing center console](https://console.byteplus.com/finance/accountOverview/).

2. In the left navigation pane, click **Renewal Management**.

3. On the **Manual renewal** tab of the Renewal Management page, click  **··· \> Enable auto\-renewal** in Actions column of the resource to be renewed.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Only DC Connections unexpired support switching manual renewal to automatic renewal for the payment of the port occupancy fee.   </div>
   

4. On the **Auto\-renewal** page, specify the interval for auto\-renewal in the lower\-left section, set the auto\-renewal time, and then click **Enable** to enable automatic renewal.

   If you do not select Custom for auto\-renewal times, automatic renewal is permanently effective. The system performs automatic renewal each time the resource expires based on the interval for auto\-renewal set for the single automatic renewal.
