---
title: "Auto-renewal rules"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/docs-auto-renewal-rules"
---

<span id="02a082a9"></span>
### Rules


1. Enabling auto\-renewal prevents service disruption due to instance expiration. Instances set to "auto\-renewal" will be displayed on the Auto\-Renewal tab.

2. "Running" instances set to "auto\-renewal" allow manual renewal, batch renewal, modifying auto\-renewal settings, and switching to manual renewal or non\-renewal upon expiration.

3. Instances that are set to "auto\-renewal" and in "To be terminated/Terminated" status only support manual renewal, batch renewal, and switching to manual renewal.

4. Instances in "Refunded" status will have auto\-renewal disabled. They will be displayed in the Manual Renewal tab and only support manual renewal.

5. After auto\-renewal is enabled, if no auto\-renewal billing date is set, the system will start charging seven days before resource expiration at 00:00 AM by default. If renewal fails, the system will retry renewing every six hours until the resource is finally released. Please ensure there is sufficient balance in your account. If an auto\-renewal billing date is set, the system will initiate auto\-renewal on the set date at 00:00 AM. If renewal fails, the system will retry renewing every six hours until the resource is finally released.

6. Resources with auto\-renewal enabled can be manually renewed at any time. The auto\-renewal settings will remain effective after a successful manual renewal.

7. During auto\-renewal, the system will automatically apply any applicable coupons available in your account to the payment.

8. Explanation of instance status in the renewal list



|**Status** |**Explanation** |
|---|---|
|Running |An instance that has not expired is in Running status. |
|To be terminated |The instance has expired but yet to be terminated. |
|Terminated |The instance has been terminated due to subscription expiration. |
|Refunded |Instances of some products come with a retention period after unsubscribing, during which they can be reinstated through manual renewal. |


<span id="51c99a70"></span>
### Steps


1. **Enable auto\-renewal**

   1. Go to Billing Center \> Renewal Management \> Manual Renewal/Non\-Renewal Upon Expiration. Select the target instances and click Enable Auto\-Renewal.

   2. Set the single auto\-renewal duration and number of renewals. The number is "Unlimited" by default, but it can be customized. Once the specified number of auto\-renewals has been exhausted, the instance will switch to manual renewal.

   3. Click Enable to complete the setup.

      <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_98a9902f8ed0b2778218931967aa555a.png) </span>

      <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_7edd14bacf056c114b93210ce87b5c6a.png) </span>

2. Go to Billing Center \> Renewal Management \> Auto\-Renewal.

3. **To manually renew an instance set to auto\-renewal:**  Select the instance and click Renew or Batch Renew to proceed to the renewal page. There, set the renewal duration, click Pay, and proceed with the payment to complete the manual renewal.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_ee9e1e05b0427e8cfae787bb6579e897.png) </span>


4. You can switch one or more instances to manual renewal or non\-renewal upon expiration (only before they expire), or modify their auto\-renewal settings (only before they expire) as needed. Upon successful update of the renewal mode, the instances will be automatically listed under the Manual Renewal, Auto\-Renewal, or Non\-Renewal Upon Expiration tab.
