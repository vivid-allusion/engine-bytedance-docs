---
title: "Convert a pay-as-you-go Logstash instance to subscription"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Convert_a_pay-as-you-go_Logstash_instance_to_a_subscription"
---

After you confirm that the created pay\-as\-you\-go Logstash instance meets the requirements, you can change its billing type to subscription. This article describes how to convert a pay\-as\-you\-go Logstash instance to a subscription.

<span id="IW0eMxLv"></span>
## Prerequisites

A Logstash instance has been created with a **status** of **Running** and a **billing type** of **Pay\-as\-you\-go**. For the procedure, refer to [Create a Logstash instance](https://docs.byteplus.com/en/docs/cloudsearch/Create_a_Logstash_instance).

<span id="aitYAwhY"></span>
## **Notice**


* When you convert a pay\-as\-you\-go instance to a subscription, you must settle the bill for the pay\-as\-you\-go instance and prepay the subscription amount. Ensure that your account has a sufficient balance.

* Changing the billing type of a Logstash instance will not affect its operation.

* Only converting from pay\-as\-you\-go to subscription is supported. This action is irreversible, so proceed with caution.


<span id="aitYAwhY"></span>
## Operation steps


1. Log in to the [Cloud Search console](https://console.byteplus.com/es).

2. In the upper\-left corner of the top menu bar, select the project and region of the Logstash instance.

3. In the left navigation pane, select **Data processing** \> **Logstash**.

4. In the list of Logstash instances, click  **...**  in the **actions** column of the target Logstash instance \> **Convert to subscription**.

5. On the **Convert pay\-as\-you\-go to subscription** page, select the purchase duration, select automatic renewal as needed, read and select **Terms of service for database products**, and then click **Confirm order**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When confirming the order, individual users also need to select <strong>Unsubscription or change fee instructions</strong>. To use an enterprise account, complete the enterprise verification.   </div>
   

6. On the **Confirm order information** page, confirm the changes and the amount, and click **Next**.

7. On the Submit payment information page, confirm the payment details, select a payment method, and click **Go to pay** to complete the payment as prompted.
