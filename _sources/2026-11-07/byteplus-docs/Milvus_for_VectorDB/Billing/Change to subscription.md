---
title: "Change to subscription"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Change_to_subscription"
---

Milvus for VectorDB offers pay\-as\-you\-go and subscription billing methods, supporting conversion between the two. After creating a pay\-as\-you\-go Dedicated instance, you can change the billing method to subscription in the console based on your business needs. This article explains how to switch the billing method of a Dedicated instance from pay\-as\-you\-go to subscription.

<span id="IrBhhquh"></span>
## **Prerequisites**


* Created Dedicated instances with status **Running**. For more information about how to create an instance, see [Create an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_an_instance).

* The billing method of the instance is **Pay\-as\-you\-go**. For more information about billing methods, see [Billing methods](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Billing_methods).


<span id="QmgqIxCy"></span>
## **Precautions**


* When changing from pay\-as\-you\-go to subscription, you need to settle the bill for this pay\-as\-you\-go instance and prepay the subscription fees. Ensure sufficient balance in your account.

* After changing from pay\-as\-you\-go to subscription, you can change the billing method back to pay\-as\-you\-go. For detailed steps, see [Change to pay-as-you-go](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Change_to_pay-as-you-go).

* Instances with enabled elastic scaling do not support subscription changes. For details, see [Elastic scaling](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Elastic_scaling).


<span id="9U2ACh6M"></span>
## **Procedure**


1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. In the top navigation bar, select the project and region where you want to create an instance.

3. In the **Instances** list, select the **Dedicated** tab, then click **Change to subscription** under the **Actions** column of the target pay\-as\-you\-go instance.

4. On the **Switch to subscription** page, confirm the instance information, then configure the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |Purchase duration |Select the purchase duration for the subscription instance. Enjoy a 50% discount when the purchase duration is one year or longer. For more information about subscription, see [Subscription](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Subscription). |
   |Automatic renewal |Specify whether to enable automatic renewal. The automatic renewal rules are as follows:<br><br><br>* Enable **automatic renewal**: Before the instance expires, the platform automatically renews it monthly without manual renewal.<br><br>* Disable **automatic renewal**: You need to manually renew the instance before it expires. Otherwise, the instance will be automatically released. |
   

5. After configuring the parameters, read and agree to the relevant agreement, then click **Confirm order**.

6. On the **Confirm order information** page, review the payment details and click **Next step**.

7. On the **Submit payment information** page, select a payment method and click **Pay**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After completing the payment, you can click <strong>Go to the console</strong> to return to the <strong>Instance list</strong> page and check whether the target instance's <strong>Billing type</strong> is <strong>Subscription</strong>.   </div>
