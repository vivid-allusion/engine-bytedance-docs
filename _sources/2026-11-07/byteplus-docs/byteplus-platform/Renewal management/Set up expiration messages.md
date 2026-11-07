---
title: "Set up expiration messages"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/message"
---

<span id="nIlJUjeP"></span>
## **What are expiration messages?** 

BytePlus Message Center provides resource expiration reminders. Expiration messages notify you through in\-site messages and emails when your resources are about to expire or have already expired. This allows you to renew, recharge, or repurchase in a timely manner to avoid service interruptions or resource reclamation due to forgetting to process the expiration. The preset reminder times are as follows (some products may not involve shutdown/release):


* **Pre\-expiration warning:**  By default, warnings are sent 7 days, 3 days, 1 day, and on the day before the instance expires. You can also cancel reminders for certain renewal types or dates. For specific operations, refer to the Set up expiration warning messages section below.

   * Expiration warnings are not sent for one\-time resource packages that have been used up or for adjusted reserved instances.

* **Post\-expiration notification:**  Reserved instances and reserved storage capacities are reminded the day after the instance expires (including adjusted expiration and original expiration), which cannot be modified.

* **Post\-expiration shutdown notification**: Reminders are sent on the day the instance expires and cannot be modified.

* **Pre\-Expiration Recycling Warning**: Reminds you one day before the instance is due to be recycled and cannot be modified.

* **Post\-Expiration Recycling Notification**: Reminds you on the day the instance is due to be recycled and cannot be modified.

   * One\-time instances, reserved instances, and reserved storage capacity packages do not send expiration shutdown notifications, pre\-expiration recycling warnings, or post\-expiration recycling notifications.


&nbsp;

<span id="B9B170QM"></span>
## Set Expiration Warning Messages


1. Log in to the BytePlus Console, and go to Billing center [Renewal management page](https://console.byteplus.com/finance/renew).

2. On the right, click the Renewal settings dropdown button and click set expiration warning message button.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_5db799a19291543f020c13d090ce1b0d.png) </span>


3. In the Set Expiration Warning Message pop\-up window, you can modify the renewal types and dates you need to subscribe to.

4. To avoid losses caused by unexpected shutdowns, you are not allowed to cancel the expiration warning message for manually renewed instances separately. Cancellation is not allowed 1 day before expiration.

5. After modifying, click OK to complete the settings.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_d12abb55f29b18c303c9697c3ce948dc.png) </span>
