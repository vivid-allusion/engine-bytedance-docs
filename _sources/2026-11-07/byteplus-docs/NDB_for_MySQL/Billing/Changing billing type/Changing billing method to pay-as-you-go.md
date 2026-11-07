---
title: "Changing billing method to pay-as-you-go"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Changing_billing_method_to_Pay-as-you-go"
---

NDB for MySQL provides Pay\-as\-you\-go and Subscription billing methods, and supports conversion between the two. This topic describes how to change the billing method of the NDB for MySQL instance from yearly or monthly subscription to pay\-as\-you\-go.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance has been created with the Calculate billing type of subscription and is in the **Running** state. For more details, refer to [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1).

* The instance currently has no **pending** configuration change events. You can search and view them by instance ID in the **Planned event** list. For steps, see [Viewing event list](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Viewing_event_list).

* The account balance is greater than or equal to 100 yuan.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* To change the billing method to Pay\-as\-you\-go in bulk, you can only select instances that have the same storage type and use **Subscription** for both compute and storage billing. You can select a maximum of 50 instances at a time.

* When changing an instance's billing method to Pay\-as\-you\-go, the system first calculates the remaining value of the instance according to the standard refund policy for unsubscribing (the balance will be refunded to the original payment method). Once the billing method is successfully changed, the instance is immediately billed on a Pay\-as\-you\-go basis. For more information on the standard refund policy for unsubscribing, refer to [Standard unsubscription rules](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management).


<span id=".5Y2V5a6e5L6L6L2s5oyJ6YeP6K6h6LS5"></span>
## Single instance switch to pay\-as\-you\-go


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instance list** page, find the target instance and select  **...**  \> **Change billing method** in the **Actions** column.

4. On the **Change billing method** page, set the following configuration.

   
   |Parameter |Description |
   |---|---|
   |Calculate billing type |Choosing **Pay\-as\-you\-go** means changing the yearly or monthly subscription instance to a pay\-as\-you\-go instance. |
   |Storage billing type |The storage billing type for Pay\-as\-you\-go instances only supports **Pay\-as\-you\-go**. |
   |Agreement |Read and check the terms of service. |
   

5. In the lower\-right corner of the page, click **Confirm order**.

6. On the **Confirm order** page, confirm the order details and click **Next** to complete the payment.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the payment is complete, return to the <strong>Instance list </strong>page to check if the <strong>Calculate billing type</strong> and <strong>Storage billing type</strong> for the target instance have been successfully changed. The billing method update may be delayed. Refresh to confirm after a while.   </div>
   

<span id=".5om56YeP6L2s5oyJ6YeP6K6h6LS5"></span>
## Batch switch to pay\-as\-you\-go


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instance list** page, select the target instances to be changed to Pay\-as\-you\-go in batches, and click **Change billing method** in the lower\-left corner of the list.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can only select instances with the same Calculate billing type and Storage billing type for batch conversion to Pay\-as\-you\-go.   </div>
   

4. On the **Change billing method** page, set the following configuration.

   
   |Parameter |Description |
   |---|---|
   |Calculate billing type |Choosing **Pay\-as\-you\-go** means changing the yearly or monthly subscription instance to a pay\-as\-you\-go instance. |
   |Storage billing type |The storage billing type for Pay\-as\-you\-go instances only supports **Pay\-as\-you\-go**. |
   |Agreement |Read and check the terms of service. |
   

5. In the lower\-right corner of the page, click **Confirm order**.

6. On the **Confirm order** page, confirm the order details and click **Next** to complete the payment.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[ModifyDBInstanceChargeType](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBInstanceChargeType) |Call the ModifyDBInstanceChargeType API to modify the instance's billing method. |
