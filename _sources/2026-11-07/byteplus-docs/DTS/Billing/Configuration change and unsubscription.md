---
title: "Configuration change and unsubscription"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/modification_of_instance_specification_or_subscription_cancellation"
---

This topic describes the specifications for changing the configuration and unsubscribing from Database Transmission Service (DTS) tasks.

<span id=".5Y-Y6YWN6LS555So6K-05piO"></span>
## Specification for configuration change fees

DTS provides two link specifications: Compact and Standard. Resource specification changes are divided into two types: upgrade and downgrade. The specific resource specification changes for both types are as follows:


* Resource upgrade: Upgrade refers to changing the task's link specification from Compact to Standard.

* Resource downgrade: Downgrade refers to changing the task's link specification from Standard to Compact.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Currently, only data migration and synchronization tasks support specification changes.</div>


* <div data-tips="true" data-tips-type="tip">After changing the link specification of a migration or synchronization task, BytePlus will recalculate billing based on the new specification. For pay\-as\-you\-go tasks, the new billing will take effect at the next full hour after the specification changes. Additionally, no further specification changes can be made to the task until the previous change is fully effective.</div>



DTS offers two billing methods: pay\-as\-you\-go and subscription. After a DTS task's specification is changed, the fee changes vary depending on the billing method, as detailed below:


* Pay\-as\-you\-go

   Pay\-as\-you\-go resources are billed after usage. The cost for modifying specifications is subject to the bill amount.

* Subscription

   Subscription task resource changes are divided into two types: resource upgrades and resource downgrades, as detailed below:

   * Upgrade: When changing resource specifications, if the publish price (hourly publish price) of the new specification is greater than or equal to the publish price of the old specification, the system will calculate the price difference between the new and old specifications using the upgrade formula.

   * Downgrade: When changing resource specifications, if the publish price (hourly publish price) of the new specification is less than the publish price of the old specification, the system will calculate the price difference between the new and old specifications using the downgrade refund formula and credit the amount to your account balance. If you downgrade the specification and renew your instance, the system gives priority to the downgrade formula when calculating the refund. If the calculation result is a refund, the system refunds the price difference between the new and old specifications to your account balance. If the calculation result is a charge, the system re\-calculates it according to the upgrade formula, and you also need to pay the price difference between the new and old specifications.

   The detailed fees for resource specification changes of subscription tasks are shown in the table below:



|**Type of specification change** |**Fee description** |
|---|---|
|Upgrade |Total payable amount of upgrade order<br><br>= New specification cost \- residual value of old specification<br><br>= Publish price of new specification (hourly) \* remaining time (hour) \* discount \- publish price of old specification (hourly) \* remaining time (hour) \* discount |
|Downgrade |Total payable amount of downgrade order<br><br>= New specification cost \- refundable residual value of old specification<br><br>= Publish price of new specification (hourly) \* remaining time (hour) \* discount \- true value of order/purchase duration of order \* remaining time<br><br>= Publish price of new specification (hourly) \* remaining time (hour) \* discount \- (true value of order \- true value of order \* duration used/purchase duration of order \* degrading refund coefficient)<br><br>= Publish price of new specification (hourly) \* remaining time (hour) \* discount \- (true value of order \- true value of order \* duration used/purchase duration of order) \* degrading refund coefficient |


For more information on specification change fees, refer to the [Billing rules for resource changes](https://docs.byteplus.com/en/docs/6269/438722).

<span id=".6YCA6K6i6LS555So6K-05piO"></span>
## **Specification for unsubscription fees**


* Pay\-as\-you\-go tasks are unsubscribed upon deletion, and no refunds are involved.

* Subscription instances support non\-7\-day unconditional unsubscription. For details on refund rules, refer to [Unsubscription management](https://docs.byteplus.com/en/docs/6269/81013).
