---
title: "Changing billing method to yearly or monthly subscription"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Changing_billing_method_to_Subscription"
---

NDB for MySQL provides Pay\-as\-you\-go and Subscription billing methods, and supports conversion between the two. This topic describes how to change the billing method of the NDB for MySQL instance from pay\-as\-you\-go to yearly or monthly subscription.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The instances cannot have unpaid orders for conversion to yearly/monthly subscription.

* The instance currently has no **pending** configuration change events. You can search and view them by instance ID in the **Planned event** list. For steps, see [Viewing event list](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Viewing_event_list).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* To change the billing method to Subscription in bulk, you can only select instances that have the same storage type and use **Pay\-as\-you\-go** for both compute and storage billing. You can select a maximum of 50 instances at a time.

* The billing method for compute nodes can only be changed from Pay\-as\-you\-go to Subscription.

* If an instance has an unpaid order to change its billing method to Subscription, and you upgrade the instance's specification, that order will become invalid. You must first cancel the order on the order page, and then restart the process of changing the billing method to Subscription.


<span id=".5Y2V5a6e5L6L6L2s5YyF5bm05YyF5pyI"></span>
## Single instance switch to subscription


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instance list** page, find the target instance and select  **...**  \> **Change billing method** in the **Actions** column.

4. On the **Change billing method** page, set the following configuration.

   
   |Parameter |Description |
   |---|---|
   |Calculate billing type |Choosing the **Subscription** option means changing the pay\-as\-you\-go instance to a yearly/monthly subscription instance. |
   |Storage billing type |The storage billing type for a Subscription instance can be **Pay\-as\-you\-go ** or **Subscription**, and they are mutually convertible.<br><br>To modify the storage billing type, refer to [Modifying storage billing type](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_storage_billing_type). |
   |Specify storage space |If the storage billing type is Subscription, you must select whether to specify the storage space size.<br><br><br>* Select **No** (default): You do not need to select a storage space size. It defaults to the `currently used space` + `15 GB`.<br><br>* Select **Yes**: customize the storage space size. It is recommended to choose a size larger than the currently used storage space. If you choose a size smaller than the currently used space, the excess usage will be billed on a pay\-as\-you\-go basis. |
   |Storage space |Select the storage space size. The supported storage space size varies by instance specification. For details, refer to [Product specifications](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Product_specifications). |
   |Purchase duration |Select the purchase duration. Support monthly purchases (can purchase 1~9 months) and yearly purchases (can purchase 1~3 years). |
   |Automatic renewal |Select whether to enable automatic renewal. After selecting **Automatic renewal**, the system automatically renews the instance before it is due. For more information about automatic renewal rules, refer to [Overview of renewal rules](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-of-renewal-rules). |
   |Agreement |Read and check the terms of service. |
   

5. In the lower\-right corner of the page, click **Confirm order**.

6. On the **Confirm order** page, confirm the order details and click **Next** to complete the payment.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the payment is complete, return to the <strong>Instance list </strong>page to check if the <strong>Calculate billing type</strong> and <strong>Storage billing type</strong> for the target instance have been successfully changed. The billing method update may be delayed. Refresh to confirm after a while.   </div>
   

<span id=".5om56YeP6L2s5YyF5bm05YyF5pyI"></span>
## Batch switch to subscription

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Only Pay\-as\-you\-go instances can be switched to Subscription in a batch. Batch changing the storage billing type for Subscription instances is not supported.</div>



1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **instance list** page, select the target instances that you want to switch to Subscription, and then click **Change billing method** at the lower\-left corner of the list.

4. On the **Change billing method** page, set the following configuration.

   
   |Parameter |Description |
   |---|---|
   |Calculate billing type |Choosing the **Subscription** option means changing the pay\-as\-you\-go instance to a yearly/monthly subscription instance. |
   |Storage billing type |The storage billing type for a Subscription instance can be **Pay\-as\-you\-go ** or **Subscription**, and they are mutually convertible.<br><br>To modify the storage billing type, refer to [Modifying storage billing type](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_storage_billing_type). |
   |Specify storage space |If the storage billing type is Subscription, you must select whether to specify the storage space size.<br><br><br>* Select **No** (default): You do not need to select a storage space size. It defaults to the `currently used space` + `15 GB`.<br><br>* Select **Yes**: Customize the storage space size. It is recommended to select a size larger than the maximum storage space used among all instances. If the size is smaller than the maximum storage space currently used, the excess capacity of some instances will be charged on a pay\-as\-you\-go basis. |
   |Storage space |Select the storage space size. In a batch scenario, the default minimum storage space is the maximum used storage space among all instances. |
   |Purchase duration |Select the purchase duration. Support monthly purchases (can purchase 1~9 months) and yearly purchases (can purchase 1~3 years). |
   |Automatic renewal |Select whether to enable automatic renewal. After selecting **Automatic renewal**, the system automatically renews the instance before it is due. For more information about automatic renewal rules, refer to [Overview of renewal rules](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-of-renewal-rules). |
   |Agreement |Read and check the terms of service. |
   

5. In the lower\-right corner of the page, click **Confirm order**.

6. On the **Confirm order** page, confirm the order details and click **Next** to complete the payment.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[ModifyDBInstanceChargeType](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBInstanceChargeType) |Call the ModifyDBInstanceChargeType API to modify the instance's billing method. |
