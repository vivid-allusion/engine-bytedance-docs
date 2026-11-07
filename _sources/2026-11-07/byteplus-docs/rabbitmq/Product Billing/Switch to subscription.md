---
title: "Switch to subscription"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Switch_to_subscription"
---

After creating a pay\-as\-you\-go instance, you can change the billing mode to **Subscription** in the console based on business needs. This section describes the steps for switching pay\-as\-you\-go instances to subscription instances.

<span id="前提条件"></span>
## Prerequisites


* The status of the RabbitMQ instance is **Running**.

* The billing method for the instance is **Pay\-as\-you\-go**.


<span id="注意事项"></span>
## Notes


* When switching from pay\-as\-you\-go to subscriptions, you need to settle the pay\-as\-you\-go instance and prepay for the annual and monthly fees. Please ensure there is sufficient balance in your account.

* Switching the billing method of the instance will not affect the operation of the instance.

* Currently, only the switch from pay\-as\-you\-go to subscription is supported. Once it is completed, it can not be reversed. Please proceed with caution.


<span id="操作步骤"></span>
## Operation steps


1. Log in to the [Message Queue for RabbitMQ console](https://console.byteplus.com/rabbitmq).

2. Select a region in the top navigation bar.

3. In the **Instances**, find the pay\-as\-you\-go instance that needs a billing method change, expand the dropdown menu in its corresponding **Actions** column, and click **Switch to subscription**.

4. Confirm the selected instance information, and choose the duration of subscription in **Subscription duration**.

5. Choose whether to enable auto\-renewal.

   * Enable **Automatic renewal**: Before the instance expires, the platform automatically renews monthly, without the need for manual renewal.

   * Disable **Automatic renewal**: Before the instance expires, it requires manual renewal. Otherwise, the instance will be automatically released.

6. Read and agree to the relevant agreements, then click **Confirm order**.

7. Follow the page prompts to confirm and pay the bill.


<span id="执行结果"></span>
## Execution result

After the pay\-as\-you\-go instance is successfully converted to a subscription instance, the **Instances** in the console will show the **Billing method** as **Subscription**, and also display the due date of the subscribed instance.
