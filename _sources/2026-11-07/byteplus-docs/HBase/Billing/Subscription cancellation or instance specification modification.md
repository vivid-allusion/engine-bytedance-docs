---
title: "Subscription cancellation or instance specification modification"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Subscription_cancellation_or_instance_specification_modification"
---

This topic describes the fee description for Modify Instance Spec and unsubscription of a HBase instance.

<span id="iwTgtC2r"></span>
## Fee description for Modify Instance Spec


* Post paid billing

   A post paid billing instance is charged by the hour. After Modify Instance Spec, it is charged by hour based on the new specification price.

* Yearly/monthly subscription

   The modification of a yearly/monthly subscription instance specification can upgrade or downgrade the resource specification.n

   * Upgrade: When the resource specification is modified, the publish price of the new specification (hourly publish price) is =\> publish price of old specification (hourly publish price). At this time, the system calculates the price difference between the new and old specifications you need to pay according to the upgrade formula.

   * Downgrade: When the resource specification is modified, the publish price of the new specification (hourly publish price) is =< publish price of old specification (hourly publish price). At this time, the system calculates the price difference between the new and old specifications according to the downgrade formula and refunds it to your account balance. If you downgrade the specification and renew your instance, the system gives priority to the downgrade formula when calculating the refund. If the calculation result is a refund, the system refunds the price difference between the new and old specifications to your account balance. If the calculation result is a charge, the system re\-calculates it according to the upgrade formula, and you also need to pay the price difference between the new and old specifications.

   
   |**Modification Type** |**Fee Description** |
   |---|---|
   |Upgrade |Upgrade order cost<br><br>= new specification cost \- residual value of old specification<br><br>= publish price of new specification (hourly) \* remaining time (hour) \* discount \- publish price of old specification (hourly) \* remaining time (hourly) \* discount |
   |Downgrade |Downgrade order cost<br><br>= new specification cost \- refundable residual value of old specification<br><br>= publish price of new specification (hourly) \* remaining time (hour) \* discount \- true value of order/purchase duration of order \* remaining time<br><br>= publish price of new specification (hourly) \* remaining time (hour) \* discount \- (true value of order \- true value of order \* duration used/purchase duration of order\* degrading refund coefficient)<br><br>= publish price of new specification (hourly) \* remaining time (hour) \* discount \- (true value of order \- true value of order \* duration used/purchase duration of order \*degrading refund coefficient |
   


<span id="zKEmSSxh"></span>
## Fee description for unsubscription


* Deleting a post paid billing instance does not involve unsubscription, with no refund involved.

* Non\-7\-day unconditional subscription cancellation is supported for yearly/monthly subscription instances. For details on refund rules, refer to [Unsubscription Management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management).
