---
title: "Pay-as-you-go"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/pay-as-you-go"
---

Post Paid is a billing method with which you use first and pay later. This billing method is best when you don't need to buy a large quantity of resources in advance, but purchase and release them on demand at any time.

<span id="introduction"></span>
## Introduction

Post paid billing is applicable to scenarios that expect a substantial increase in business in the short term, e\-commerce businesses that offer flash sales. BytePlus platform calculates the expenses based on the resources you actually use, which truly achieves pay\-as\-you\-go billing, and instance fees are charged according to the duration of use, calculated in seconds. When you don't need certain resources, you can delete them at any time and billing will stop.

<span id="purchase-prerequisites"></span>
## Purchase prerequisites


* A BytePlus account has been registered and completed verification. For the detailed method, refer to [Sign Up and Verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* As per the regulations in the Chinese mainland, you must have completed real name registration before you can activate and use cloud services on regions in the Chinese mainland through BytePlus. For more details, refer to [Real name registration](https://docs.byteplus.com/en/docs/byteplus-platform/docs-real-name-registration).

* After purchasing a post paid instance, you can perform Modify Instance Spec to change the instance specification temporarily. For more information, refer to [Modifying specifications](https://docs.byteplus.com/en/docs/RDS_for_MySQL/standard_instance_specification_modification).


<span id="billing-duration"></span>
## Billing duration

If shutdown due to arrears is not considered, the billing duration of an RDS for MySQL post paid billing instance starts when the instance is created and ends when the instance is released.

<span id="settlement-cycle"></span>
## Settlement cycle

For a post paid instance, fees are settled hourly (subject to UTC+8), and then the next settlement cycle starts. If your account balance (including cash coupons) is less than the amount specified in the bill to be settled, you will receive an SMS or email reminder about the insufficient balance.

For example, assume the unit price of an instance of a certain specification is USD 0.80/hour, and the settlement fee of the instance is charged based on the duration of use, calculated in seconds.


* Duration: 30 min, fee: USD 0.8/hour ÷ 3,600 seconds × 60 seconds × 30 minutes = USD 0.4

* Duration: 1 hour and 30 min, fee: USD 0.8/hour ÷ 3,600 seconds × 60 seconds × 90 minutes = USD 1.2


<span id="modify-the-specification"></span>
## Modify the specification

For a post paid instance, real\-time modification to another instance specification of the same architecture and type is supported. After the instance specification is modified successfully, the latest specification is displayed for the target instance in the instance list and the instance functions according to the new specification.

For a post paid instance, the fee settlement rules for Modify Instance Spec are shown below:


* The price of modifying instance specification is the price of the current target specification, which is the specification actually paid for. The prices in different periods may differ slightly, and the specific price is subject to the actual operation.

* The amount of modifying instance specification order is calculated in hours, and the price is accurate to two decimal places.
