---
title: "Changing the billing method from pay-as-you-go to subscription"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/changing-billing-method"
---

After a **pay\-as\-you\-go** instance is created, you can change its billing method to **subscription** in the Cloud Search console based on your business needs. This topic describes how to change the billing method of a Cloud Search instance from pay\-as\-you\-go to subscription.

<span id="前提条件"></span>
## **Before you begin**


* Verify that the Cloud Search instance is in the **Running** state.

* Verify that the instance is billed on a **pay\-as\-you\-go** basis.


<span id="注意事项"></span>
## **Precautions**


* When you change from pay\-as\-you\-go to subscription, you need to settle the bill for this pay\-as\-you\-go instance and prepay the amount for the subscription. Please make sure there is sufficient balance in your account.

* Changing the billing method for instance does not affect its operation.

* Currently, only changing from pay\-as\-you\-go to subscription is supported. If you have changed the billing method to subscription, **you cannot change it back to pay\-as\-you\-go again**. Exercise caution when making such a change.


<span id="操作步骤"></span>
## **Procedure**


1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the Region of your instance.

3. On the **List of Instances** page, find the target pay\-as\-you\-go instance, then click  **... \> subscription** in the **Actions** column.

4. On the **Switch to subscription** page, confirm the instance information and configure the following parameters.



|**Parameter** |**Description** |
|---|---|
|Subscription duration |Select a subscription duration for the instance. For more information on subscription, refer to [Subscription](https://docs.byteplus.com/en/docs/cloudsearch/subscription). |
|Automatic renewal |Specify whether to enable the automatic renewal feature.<br><br><br>* Enable **Automatic renewal**: The system automatically renews the subscription on a monthly basis before the instance expires, without the need for manual renewal.<br><br>* Disable **Automatic renewal**: You must manually renew your instance before it expires. Otherwise, the instance is automatically released upon expiration. |



5. Read and agree to the relevant agreement, then click **Confirm order**.

6. On the **Confirm order information** page, confirm the payment details and click **Next step**.

7. On the **Submit payment information** page, select a payment method and click **Buy now**.

   After completing the payment, you can click **Go to Product Console** to return to the **List of Instances** page and see if the **Billing type** of the target instance is displayed as **Subscription**.
