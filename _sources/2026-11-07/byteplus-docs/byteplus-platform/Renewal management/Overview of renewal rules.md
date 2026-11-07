---
title: "Overview of renewal rules"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-of-renewal-rules"
---

You can renew your subscriptions after successfully activating monthly or annual subscription resources. BytePlus supports three types of renewal: manual renewal (and the setting of a unified expiration day), auto\-renewal (and the setting of an auto\-renewal billing date), and non\-renewal upon expiration.

<span id="ba4710df"></span>
## **Renewal rules**


1. Manual renewal, auto\-renewal, and non\-renewal upon expiration can all take effect before the release of the expiring annual or monthly subscription instance.

2. Annual or monthly subscription instances in "Running" status support setting the renewal type to manual renewal, auto\-renewal, or non\-renewal upon expiration. Instances in "To be terminated/Terminated/Refunded" status only support switching to manual renewal.

3. "Running" reserved instances support manual renewal, auto\-renewal, or non\-renewal before expiration. Reserved instances in "To be terminated/Terminated/Refunded" status cannot be renewed.

4. Instances in "Refunded" status will have auto\-renewal disabled and only support manual renewal before final release.

5. Resource instances with a strong binding relationship (such as a cloud server and its system disk) must be renewed together. On the other hand, instances with a weak binding relationship (such as a public IP bound to a cloud server) can be renewed either separately or in conjunction.

6. For instances that are temporarily upgraded, renewal fees will be calculated based on the original configuration, and their validity period will be extended accordingly.

7. When renewing the fully prepaid savings plan, credit is not supported. Please ensure sufficient available balance beyond credit to avoid renewal failure

8. Explanation of instance status in the renewal list



|**Status** |**Explanation** |
|---|---|
|Running |An instance that has not expired is in Running status. |
|To be terminated |The instance has expired but yet to be terminated. |
|Terminated |The instance has been terminated due to subscription expiration. |
|Refunded |Instances of some products come with a retention period after unsubscribing, during which they can be reinstated through manual renewal. |


<span id="bf68e6b3"></span>
## **Renewal restrictions**


1. On\-demand resources, spot instances, tier\-based resource packages, one\-time resources, and reserved storage capacity packages do not support renewal.

2. Renewal is not supported for resources that are undergoing changes (such as upgrading, renewing, and unsubscribing).

3. Renewal is not supported for released resources.

4. Products that have been discontinued do not support renewal.


<span id="8fab5fbb"></span>
## **Detailed illustration of renewal (using annual/monthly subscription cloud resources as an example)** 


1. Lifecycle of annual/monthly subscription cloud resource instances: Manual renewal is available before instance expiration or recovery upon unsubscription.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/564e925a864f4ab8b0ed2212ed9e2126~tplv-goo7wpa0wc-image.image" width="1956px" /></div>



2. Auto\-renewal of annual/monthly subscription cloud resource instances: By default, the auto\-renewal process starts at 00:00 AM, seven days prior to the expiration date (the date/time can be customized). If a renewal attempt fails, repeated attempts will be made every six hours, continuing until either the renewal is confirmed or the resource is released.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d034f1d955648e58f6543c89d11e5c2~tplv-goo7wpa0wc-image.image" width="1950px" /></div>



3. Expiration notifications

   1. Pre\-expiration warning: The specified recipients will receive alerts through their preferred communication channels—emails or site messages—at intervals of seven, three, and one day before the expiration date, and once again on the actual day of expiration. Set the recipient and preferred communication methods in the [Message Center](https://console.byteplus.com/user/message/setting).

   2. Post\-termination notification: Upon the expiration and subsequent termination of your instance, automated notifications including emails and site messages, will be sent by default. Set the recipients and preferred communication methods in the [Message Center](https://console.byteplus.com/user/message/setting).

   3. Pre\-release warning: One day before instance release upon expiration, email and site message notifications will be sent by default. You can set the recipients and preferred communication methods in the [Message Center](https://console.byteplus.com/user/message/setting).

   4. Post\-release notification: Upon the expiration and subsequent release of your instance, automated notifications including emails and site messages, will be sent by default. Set the recipients and preferred communication methods of such notifications in the [Message Center](https://console.byteplus.com/user/message/setting).
