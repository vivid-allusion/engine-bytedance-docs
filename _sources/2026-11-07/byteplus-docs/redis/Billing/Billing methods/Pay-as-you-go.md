---
title: "Pay-as-you-go"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/pay-as-you-go"
---

Pay\-as\-you\-go is a postpaid billing method. You don't need to purchase a large quantity of resources in advance, but can purchase and release them on demand at any time.

<span id=".566A5LuL"></span>
## Introduction

Pay\-as\-you\-go is suitable for scenarios with rapidly growing businesses in the short term, such as limited\-time flash sale shopping businesses. The system charges you by the second based on your actual resource usage and deducts payments hourly from your account, truly achieving pay\-as\-you\-go. If purchased resources are no longer in use, you can delete them at any time, and billing stops immediately after deletion.

<span id=".6LSt5Lmw6KaB5rGC"></span>
## Purchase requirements


* A BytePlus account has been registered and completed verification. For the detailed method, refer to [Sign up and verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* As per the regulations in the Chinese mainland, you must have completed real name registration before you can activate and use cloud services in regions in the Chinese mainland through BytePlus. For more details, refer to [Real name registration](https://docs.byteplus.com/en/docs/byteplus-platform/docs-real-name-registration).

* When purchasing pay\-as\-you\-go Redis instance, the total value of your account balance (that is, cash balance) and vouchers must be at least USD 0.

* Pay\-as\-you\-go Redis instances support specification upgrades and downgrades at any time. For more details about changing instance configurations, refer to [Changing instance configurations](https://docs.byteplus.com/en/docs/redis/solutions-for-spec-modification).


<span id=".6K6h6LS55pe26ZW_"></span>
## Billing duration

The billing time of a pay\-as\-you\-go Redis instance throughout its lifecycle, without taking into account service suspension due to insufficient balance, is as follows: The billing begins when the instance is created and ends when the instance is released.

<span id=".57uT566X5ZGo5pyf"></span>
## Payment cycle

Pay\-as\-you\-go Redis instances incur charges per second, with an hourly billing cycle. The system settles charges once every hour on the hour (based on UTC+8 time). If your available credit (including account balance and vouchers) is less than the pending bill, you will receive an SMS or email notification about the insufficient balance.

<span id=".5Yig6Zmk5a6e5L6L"></span>
## Delete instance

Billing for Pay\-as\-you\-go Redis instances stops immediately upon deletion. For specific procedures, refer to [Deleting instance](https://docs.byteplus.com/en/docs/redis/delete-instance).

<span id=".5Y-Y5pu06YWN572u"></span>
## Modify configuration

Pay\-as\-you\-go instances support real\-time modification of instance configurations. After the instance specifications (such as number of shards, number of shard nodes) are successfully changed, you can view the latest instance specification configuration information on the **Instances** page. For more details about changing instance configurations, refer to [Changing instance configurations](https://docs.byteplus.com/en/docs/redis/solutions-for-spec-modification).

For more information on billing rules when the configuration of pay\-as\-you\-go instances is changed, refer to [Change Pay-as-you-go specifications](https://docs.byteplus.com/en/docs/byteplus-platform/Billing_Rules_for_Resource_Subscription_Change#iv-change-pay-as-you-go-specifications).
