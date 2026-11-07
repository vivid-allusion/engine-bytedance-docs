---
title: "Pay-as-you-go"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/pay-as-you-go"
---

Pay\-as\-you\-go is a billing method that allows you to use resources first and pay for them later. You do not need to buy a large number of resources in advance. Instead, you can buy and release resources as needed at any time.

<span id="简介"></span>
## Introduction

The pay\-as\-you\-go billing method is suitable for scenarios in which traffic bursts in a short period, for example, a flash sale. BytePlus calculates instance costs based on the resources you used, rendering you a genuine pay\-for\-what\-you\-use experience. Instances are billed in seconds according to the usage duration. When the resources you bought are no longer needed, you can delete them at any time. The billing process stops immediately after you delete a resource.

<span id="注意事项"></span>
## Precautions


* You must finish enterprise real\-name authentication for your BytePlus account before buying Kafka instances.

* When you buy a pay\-as\-you\-go Kafka instance, the total value of your cash balance and vouchers must not be less than CNY 100.00.

* After you buy a pay\-as\-you\-go instance, you can upgrade it. For more information, refer to [Changing instance specifications](https://docs.byteplus.com/en/docs/kafka/upgrading-instance-specifications).


<span id="计费时长"></span>
## Billing duration

If you always have sufficient balance in your BytePlus account, the billing duration of a pay\-as\-you\-go Kafka instance throughout its lifecycle is as follows:

The billing duration starts when you create an instance and ends when you release the instance.

<span id="结算周期"></span>
## Settlement cycle

A Kafka instance is billed every hour on the hour based on the time of UTC +08:00. After the billing hour, the resources used are billed in the next settlement cycle. If the available balance in your account, including the cash balance and vouchers, falls below the amount of bills to be settled, you will receive a text message or email that reminds you of insufficient balance.

For example, the unit price of an instance type is CNY 0.80 per hour. The instance is billed in seconds according to the usage duration.


* If you use the instance for 30 minutes, the instance cost is: CNY 0.8 per hour ÷ 3,600 seconds × 60 seconds × 30 minutes = CNY 0.4

* If you use the instance for 1 hour and 30 minutes, the instance cost is: CNY 0.8 per hour ÷ 3,600 seconds × 60 seconds × 90 minutes = CNY 1.2


<span id="变更配置"></span>
## Changing instance specifications

You can change the instance specifications at any time for pay\-as\-you\-go instances. After you change the specifications for an instance, the instance specifications displayed on the instance list page and the instance details page are all up to date.

The billing rules for changing specifications for a pay\-as\-you\-go instance are as follows:


* The instance whose specifications are changed is billed based on the price of the new instance specifications. Instance prices vary over time. All billable items are billed based on the actual specifications.

* The amount of a configuration change order is calculated in hours, and the displayed price is accurate to two decimal places.
