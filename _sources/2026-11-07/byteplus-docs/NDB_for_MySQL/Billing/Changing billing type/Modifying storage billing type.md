---
title: "Modifying storage billing type"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_storage_billing_type"
---

NDB for MySQL supports two storage billing types: Pay\-as\-you\-go and Yearly or monthly subscription. This topic describes how to modify the storage billing type of a subscription instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance has been created with the Calculate billing type of subscription and is in the **Running** state. For more details, refer to [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1).

* The instance currently has no **pending** configuration change events. You can search and view them by instance ID in the **Planned event** list. For steps, see [Viewing event list](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Viewing_event_list).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limitations


* You can only modify the storage billing type of instances whose calculate billing type is subscription.

* You cannot change the Storage billing type of a Subscription instance by calling an API. You can only change it through the console.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instance list** page, find the target instance and select  **...**  \> **Change billing method** in the **Actions** column.

4. On the **Change billing method** page, set the following configuration.

   
   |Parameter |Description |
   |---|---|
   |Calculate billing type |The default selection is **Subscription**, indicating no change to the calculate billing type. |
   |Storage billing type |The storage billing type for a Subscription instance can be **Pay\-as\-you\-go** or **Subscription**, and they are mutually convertible.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When you change the storage billing type from Subscription to Pay\-as\-you\-go, the System issues a refund calculated based on the refund rules. When changing from Pay\-as\-you\-go to Subscription, the System recalculates the fee based on the subscription duration and storage space, and you will need to pay for the new configuration. For more details, refer to <a href="https://docs.byteplus.com/en/docs/byteplus-platform/Billing_Rules_for_Resource_Subscription_Change">Billing Rules for Resource Subscription Change</a>.</div><br> |
   |Specify storage space |When changing the storage billing type from Pay\-as\-you\-go to Subscription, you need to select whether to specify the storage space size.<br><br><br>* Select **No** (default): you do not need to select a storage space size; it defaults to the `currently used space` + `15 GB`.<br><br>* Select **Yes**: customize the storage space size. It is recommended to choose a size larger than the currently used storage space. If you choose a size smaller than the currently used space, the excess usage will be billed on a pay\-as\-you\-go basis. |
   |Storage space |Select the storage space size. The supported storage space size varies by instance specification. For details, refer to [Product specifications](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Product_specifications). |
   |Agreement |Read and check the terms of service. |
   

5. In the lower\-right corner of the page, click **Confirm order**.

6. On the **Confirm order information** page, confirm the order details, and click **Next step**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the payment is complete, you can return to the <strong>instance list</strong> page to check whether the <strong>Storage billing type</strong> for the target instance has been successfully changed.   </div>
