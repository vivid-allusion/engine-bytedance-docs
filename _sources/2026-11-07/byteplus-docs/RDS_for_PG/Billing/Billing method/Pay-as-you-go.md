---
title: "Pay-as-you-go"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/pay_as_you_go"
---

Pay\-as\-you\-go is a post\-paid billing method. You don't need to purchase a large quantity of resources in advance, but can purchase and release them on demand at any time.

<span id=".566A5LuL"></span>
## Introduction

Pay\-as\-you\-go billing is applicable to scenarios featuring massive business growth within a short time, such as flash sales. Under this billing mode, BytePlus charges fees based on the resources you actually consumed and enables instant payments upon use. Instance expenses are collected based on duration of use and accurate to seconds. You can delete resources at any time when they are no longer needed, and billing stops immediately after deletion.

<span id=".6LSt5Lmw6KaB5rGC"></span>
## Purchase requirements


* A BytePlus account has been registered and completed verification. For the detailed method, refer to [Sign Up and Verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* As per the regulations in the Chinese mainland, you must have completed real name registration before you can activate and use cloud services in regions in the Chinese mainland through BytePlus. For more details, refer to [Real name registration](https://docs.byteplus.com/en/docs/byteplus-platform/docs-real-name-registration)..

* After you purchase a pay\-as\-you\-go instance, you can modify the instance configuration at any time. For more information, refer to [Modifying instance configuration](https://docs.byteplus.com/en/docs/RDS_for_PG/standard_instance_specification_modification).


<span id=".6K6h6LS55pe26ZW_"></span>
## Billing duration

Excluding the situation where the instance is shut down due to arrears, the billing for a pay\-as\-you\-go RDS for PostgreSQL instance starts from instance creation and ends at instance release.

<span id=".57uT566X5ZGo5pyf"></span>
## Payment cycle

For pay\-as\-you\-go PostgreSQL instances, the expenses are collected on the hour (in UTC+8 time) and the next payment cycle follows. If your account balance (including cash balance and value of coupons) is less than the payable amount, you will receive an SMS or email notification on insufficient balance.

For example, if an instance specification is charged at USD 0.80/hour, the payment cycle of the instance is based on the duration of use and accurate to seconds.


* If the instance is used for 30 minutes, the expense is: USD 0.80/hour ÷ 3600 (number of seconds) × 60 (number of seconds) × 30 (number of minutes) = USD 0.40

* If the instance is used for 30 minutes, the expense is: USD 0.80/hour ÷ 3600 (number of seconds) × 60 (number of seconds) × 30 (number of minutes) = USD 0.40


<span id=".5Y-Y5pu06YWN572u"></span>
## Change Configuration

The specifications of pay\-as\-you\-go instances can be modified in real time within the same architecture and type. After a successful instance specification modification, the latest specification is displayed for the target instance in the instance list and implemented internally.

The billing rules for specification modifications of a pay\-as\-you\-go instance are as follows:


* The specification modification expense is based on the target specification and collected in real time. The price may vary in different periods. See the specific specification modification for details.

* Expenses of specification modification orders are collected hourly and accurate to two decimal places.
