---
title: "Subscription cancellation or instance specification modification"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/fees_for_modification_of_instance_specification"
---

This topic describes the fees for modifying configuration and unsubscribing from PostgreSQL instances.

<span id=".5Y-Y6YWN6LS555So6K-05piO"></span>
## Modify configuration fee description


* Pay\-as\-you\-go

   Pay\-as\-you\-go instances are billed by the hour. After modifying configuration, billing follows the new configuration price per hour.

* Subscription

   Subscription instance configuration modifications are divided into resource upgrade and resource downgrade.

   * Upgrade: when the new configuration list price (hourly list price) is \>= the old configuration list price (hourly list price) during resource specification modification. The system calculates the price difference you need to pay between the new and old configurations based on the upgrade formula.

   * Downgrade: when the new configuration list price (hourly list price) is < the old configuration list price (hourly list price) during resource specification modification. The system calculates the price difference between the old and new specifications based on the downgrade refund formula and refunds it to your account balance. If you downgrade and renew, the system first calculates according to the downgrade refund formula. If the result is a refund, the price difference between the old and new specifications will be refunded to your account balance; if it results in a charge, the upgrade formula will be applied to recalculate, and you need to pay the price difference between the old and new specifications.

   
   |Type of specification modification |Fee description |
   |---|---|
   |Upgrade |Upgrade order fee<br><br>= new specification fee \- remaining value of old specification<br><br>= new specification list price ( hours) \* remaining duration ( hours) \* discount \- old specification list price ( hours) \* remaining duration ( hours) \* discount |
   |Downgrade |Downgrade order fee<br><br>= new specification fee \- refundable residual value of old specification<br><br>= new specification price (hours) \* remaining hours \* discount \- order actual value / order subscription duration \* remaining hours<br><br>= new specification price (hours) \* remaining hours \* discount \- (order actual value \- order actual value \* used hours / order subscription duration \* downgrade refund coefficient)<br><br>= new specification price (hours) \* remaining hours \* discount \- (order actual value \- order actual value \* used hours / order subscription duration) \* downgrade refund coefficient |
   


For detailed information on the fees for specification modification, refer to [Billing Rules for Resource Subscription Change](https://docs.byteplus.com/en/docs/byteplus-platform/Billing_Rules_for_Resource_Subscription_Change).

<span id=".6YCA6K6i6LS555So6K-05piO"></span>
## Unsubscription fee description


* Deleting a pay\-as\-you\-go instance does not involve unsubscription, with no refund involved.

* Subscription instances support unsubscription without reason within non\-7 days. For refund rules, refer to [Unsubscription Management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management).
