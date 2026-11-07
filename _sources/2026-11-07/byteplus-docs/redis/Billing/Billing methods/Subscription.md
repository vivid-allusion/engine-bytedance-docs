---
title: "Subscription"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/subscription"
---

Subscription is a billing method where payment is made in advance when creating new instance. Compared to pay\-as\-you\-go, purchasing Redis instances with a subscription is more cost\-effective.

## Introduction

The subscription billing method is suitable for scenarios where the business is stable or requires long\-term use of Cache for Redis services. You can prepay for several months or years of service based on the instance's expected usage duration.

## Subscription duration

Subscription Redis instances offer various subscription duration options. Choose the appropriate subscription duration based on your business usage. Among which:

* **Monthly subscription**: Purchase for 1 to 9 months.

* **Yearly subscription**: Purchase for 1 to 3 years.

   > **tip**

   > If the purchase duration is 1 year or longer, you will receive a discount. The specific discount is subject to the actual order page on the console.

## Payment cycle

The payment cycle of a subscription Redis instance is the instance's purchase duration (subject to UTC+8 time). A payment cycle starts at the time of resource activation (accurate to seconds) and ends at 23:59:59 on the expiration date.

## Unsubscribe instance

After unsubscribing from yearly or monthly subscription Redis instances, the refund is returned to the account balance. For how to unsubscribe subscription instance, refer to [Unsubscription management.](https://docs.byteplus.com/en/docs/redis/unsubscribe-instance)

For details on refund calculation rules, refer to [Unsubscription management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management#2a09ed89).

## Modify configuration

Subscription instances support real\-time modification of instance configurations. After the instance specifications (such as number of shards, number of shard nodes) are successfully changed, you can view the latest instance specification configuration information on the **Instances** page. For more details about changing instance configurations, refer to [Changing instance configurations](https://docs.byteplus.com/en/docs/redis/solutions-for-spec-modification).

After changing the specifications of subscription instances, you may receive a refund or have to pay the difference. For detailed billing rules for changing the configuration of subscription instances, refer to [Changing specifications of subscription resources](https://docs.byteplus.com/en/docs/byteplus-platform/Billing_Rules_for_Resource_Subscription_Change#i-change-specifications-of-an-annual-or-monthly-subscription).

## Precautions

Even if your account is in arrears, you can still use the subscription Redis instances you have purchased normally. However, you cannot purchase new instances or perform renewals before paying outstanding fees. For more details, refer to [Arrears](https://docs.byteplus.com/en/docs/redis/arrear-and-expiration#.5qyg6LS56K-05piO).
