---
title: "Pay-as-you-go"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Pay-as-you-go"
---

Post Paid is a billing method with which you use first and pay later. This billing method is best when you don't need to buy a large quantity of resources in advance, but purchase and release them on demand at any time. Pay\-as\-you\-go instance means that both the calculation billing type and the storage billing type are pay\-as\-you\-go.

<span id=".566A5LuL"></span>
## Brief introduction

Post paid billing is applicable to scenarios that expect a substantial increase in business in the short term, e\-commerce businesses that offer flash sales. BytePlus platform calculates the expenses based on the resources you actually use, which truly achieves pay\-as\-you\-go billing, and instance fees are charged according to the duration of use, calculated in seconds. You can delete resources at any time when they are not needed. After deletion, billing stops immediately.

<span id=".6LSt5Lmw6KaB5rGC"></span>
## Purchase prerequisites


* A BytePlus account has been registered and completed verification. For the detailed method, refer to [Sign Up and Verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* When you purchase an instance that uses the post paid billing method, the total value of your account balance (that is, cash balance) and cash coupons must be at least USD 100.00.

* After purchasing a post paid instance, you can perform Modify Instance Spec to change the instance specification temporarily. For more information, refer to [Modify instance spec](https://www.volcengine.com/docs/NDB_for_MySQL/Changing_node_specifications).


<span id=".6K6h6LS55pe26ZW_"></span>
## Billing duration

If shutdown due to arrears is not considered, the billing duration of the post paid billing instance starts when the instance is created and ends when the instance is released.

<span id=".57uT566X5ZGo5pyf"></span>
## Settlement cycle

For a post paid instance, fees are settled hourly (subject to UTC+8), and then the next settlement cycle starts. If your account balance (including cash coupons) is less than the amount specified in the bill to be settled, you will receive an SMS or email reminder about the insufficient balance.

For example, assume the unit price of an instance of a certain specification is USD 0.80/hour, and 2 nodes are used. The settlement fee of the instance is charged based on the duration of use, calculated in seconds.


* Duration: 30 min, fee: (USD 0.80/hour/node ÷ 3,600 seconds × 60 seconds × 30 minutes) × 2 nodes = USD 0.80

* Duration: 1 hour and 30 min, fee: (USD 0.80/hour ÷ 3,600 seconds × 60 seconds × 90 minutes) × 2 nodes = USD 2.40


<span id=".5Y-Y5pu06YWN572u"></span>
## Modify the specification

For a post paid instance, real\-time modification to another instance specification of the same architecture and type is supported. After the instance specification is modified successfully, the latest specification is displayed for the target instance in the instance list and the instance functions according to the new specification.

For a post paid instance, the fee settlement rules for Modify Instance Spec are shown below:


* The prices in different periods may differ slightly, and the specific price is subject to the actual operation.

* The amount of modifying instance specification order is calculated in hours, and the price is accurate to two decimal places.
