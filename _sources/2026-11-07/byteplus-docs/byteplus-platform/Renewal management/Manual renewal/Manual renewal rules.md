---
title: "Manual renewal rules"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/docs-manual_renewal_rules"
---

<span id="ad7afe99"></span>
### Rules


1. "Running" annual/monthly subscription instances set to "manual renewal" allow manual renewal, batch renewal, and switching to auto\-renewal or non\-renewal upon expiration. Instances in "To be terminated/Terminated/Refunded" status only support manual and batch renewal.

2. "Running" reserved instances set to "manual renewal" allow manual renewal, batch renewal, and switching to auto\-renewal or non\-renewal upon expiration. Expired reserved instances cannot be renewed.

3. When making a manual renewal, you can select an applicable coupon on the order confirmation page to enjoy a discount.

4. Resource instances with a strong binding relationship (such as a cloud server and its system disk) must be renewed together. On the other hand, instances with a weak binding relationship (such as a public IP bound to a cloud server) can be renewed either separately or in conjunction.

5. For instances that are temporarily upgraded, renewal fees will be calculated based on the original configuration, and their validity period will be extended accordingly.

6. Explanation of instance status in the renewal list



|**Status** |**Explanation** |
|---|---|
|Running |An instance that has not expired is in Running status. |
|To be terminated |The instance has expired but yet to be terminated. |
|Terminated |The instance has been terminated due to subscription expiration. |
|Refunded |Instances of some products come with a retention period after unsubscribing, during which they can be reinstated through manual renewal. |


<span id="b6dd911e"></span>
### Steps


1. Go to Billing Center \> Renewal Management \> Manual Renewal.

2. Renew a single instance or perform batch renewal as needed.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_aca969b6b5dcb84e9a4e517aeaaf86bf.png) </span>


3. On the renewal confirmation page that appears, set the renewal duration, click "Pay", and proceed with the payment to complete the renewal.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_54f77e000269bf8ac1e4f94a07b0a7f5.png) </span>


4. Before the expiration date, you can also enable auto\-renewal for one or more instances or set them to non\-renewal upon expiration as needed. After successful operation, the instances will be automatically listed under the Auto\-Renewal or Non\-Renewal Upon Expiration tab.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_37b7706c21b57bac8bfaf5a54f2f3bdd.png) </span>
