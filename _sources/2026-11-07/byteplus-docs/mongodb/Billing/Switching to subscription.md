---
title: "Switching to subscription"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/switch-to-subscription"
---

Document Database for MongoDB offers two billing methods: pay\-as\-you\-go and yearly or monthly subscription, and supports the conversion between the two billing methods. This topic introduces how to convert the billing method of a MongoDB instance from pay\-as\-you\-go to yearly or monthly subscription.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The instance status must be **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).

* The instance billing method is **Pay\-as\-you\-go**. For more information about instance billing methods, refer to [Billing method](https://docs.byteplus.com/en/docs/mongodb/billing-method).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* After successfully changing the billing method for an instance, the instance is immediately billed by subscription.

* After changing the billing method from pay\-as\-you\-go to subscription for an instance, you can restore it to pay\-as\-you\-go. For specific procedures, refer to [Switching to pay-as-you-go](https://docs.byteplus.com/en/docs/mongodb/switch-to-pay-as-you-go).


<span id=".5Y2V5a6e5L6L6L2s5YyF5bm05YyF5pyI"></span>
## Switching to subscription for single instance


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, you can choose any of the following methods to switch billing method.

   * **Method 1**

      Locate the target instance, and in the **Actions** column on the right, select  **... \> Switch to subscription**.

   * **Method 2**

      1. Click the target instance name.

      2. Under the **Summary** tab, click **Switch to subscription** under the **Billing information** section.

5. On the **Switch to subscription** page, set the following configurations.

   
   |Parameter |Description |
   |---|---|
   |Subscription duration |Select the subscription duration for the instances. |
   |Automatic renewal |Whether to enable the automatic renewal function. If you check **Automatic renewal**, the system will automatically renew the instance before it expires.<br><br>For more details on automatic renewal rules, refer to [Auto-renewal rules](https://docs.byteplus.com/en/docs/byteplus-platform/docs-auto-renewal-rules). |
   |Agreement |Read and check the relevant agreements. |
   

5. In the lower\-right corner of the page, click **Confirm order**.

6. On the **Confirm order information** page, confirm the order details, then click **Next step** to complete the payment.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the payment is completed, you can return to the Instances page to view whether the target instance's <strong>Billing method</strong> has been successfully converted to <strong>Subscription</strong>.   </div>
   

<span id=".5om56YeP6L2s5YyF5bm05YyF5pyI"></span>
## Switching to Subscription for multiple instances


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instances page, select the target instances to be switched in batch, then click **Switch to subscription** at the lower\-left corner of the list.

5. On the **Switch to subscription** page, reconfirm the selected instance information and configure the following settings.

   
   |Parameter |Description |
   |---|---|
   |Subscription duration |Select the subscription duration for the instances. |
   |Automatic renewal |Whether to enable the automatic renewal function. If you check **Automatic renewal**, the system will automatically renew the instance before it expires.<br><br>For more details on automatic renewal rules, refer to [Auto-renewal rules](https://docs.byteplus.com/en/docs/byteplus-platform/docs-auto-renewal-rules). |
   |Agreement |Read and check the relevant agreements. |
   

6. In the lower\-right corner of the page, click **Confirm order**.

7. On the **Confirm order information** page, confirm the order details, then click **Next** **step** to complete the payment.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the payment is completed, you can return to the Instances page to view whether the target instance's <strong>Billing method</strong> has been successfully converted to <strong>Subscription</strong>.   </div>
   

<span id=".55u45YWzLWFwaQ=="></span>
## Relevant APIs


|API |Description |
|---|---|
|[ModifyDBInstanceChargeType](https://docs.byteplus.com/en/docs/mongodb/modifydbinstancechargetype) |Call the ModifyDBInstanceChargeType API to modify the billing method of the target instance. |
