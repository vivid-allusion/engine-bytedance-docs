---
title: "Pay-as-you-go"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Pay_as_you_go"
---

Pay\-as\-you\-go is a billing method where you pay after using the resources. You don't need to buy large amounts of resources in advance. You can enable and release resources anytime as needed.

<span id=".566A5LuL"></span>
## Overview

Pay\-as\-you\-go suits scenarios where short\-term business surges, such as limited\-time flash sales. BytePlus calculates fees based on your actual resource usage for pay\-as\-you\-go billing. Instance charges are based on usage time, billed by the second. You can delete resources no longer needed at any time, and billing stops immediately upon deletion.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* Your account must complete enterprise real\-name verification before purchasing message queue for RabbitMQ instances.

* When purchasing Pay\-as\-you\-go message RabbitMQ version instances, the total volume of your account balance (cash balance) and vouchers must be at least USD 100.00.

* The Pay\-as\-you\-go instance supports upgrading after purchasing. For more details, see [Modify instance information](https://docs.byteplus.com/en/docs/rabbitmq/Modify_instance_information).


<span id=".6K6h6LS55pe26ZW_"></span>
## Billing duration

If you disregard service suspension due to non\-payment, the billing duration for the pay\-as\-you\-go RabbitMQ instance spans its entire lifecycle:

Billing starts once the instance is created and ends when it is released.

<span id=".57uT566X5ZGo5pyf"></span>
## Settlement period

The message queue for RabbitMQ instance settles charges every hour (based on UTC+8 time), then enters the next settlement period. If the available credit in your account (including balance and vouchers) is less than the pending bill, you will receive a notification via SMS or email about insufficient funds.

For example, if the unit price of an instance is 0.80 Yuan/hour, the settlement cost of the instance is calculated based on the usage duration, billed to seconds.


* For 30 minutes of use, the cost is: 0.8 Yuan/hour ÷ 3600 seconds × 60 seconds × 30 minutes = 0.4 Yuan

* For 1 hour and 30 minutes of use, the cost is: 0.8 Yuan/hour ÷ 3600 seconds × 60 seconds × 90 minutes = 1.2 Yuan


<span id=".5Y-Y5pu06YWN572u"></span>
## Change configuration

For instances under pay\-as\-you\-go billing model, real\-time configuration changes are supported. After changing the instance specifications, the target instance in the instance list will display the latest specifications' configuration; once the instance changes configuration successfully, the internal settings are also updated to the latest configuration.

The settlement rules for changing instance specifications on a pay\-as\-you\-go basis are as follows:


* The price for changing configurations is based on the current target specification's price, and actual payments are made for the actual changes, with prices varying slightly at different times. The specific price is determined by the actual change.

* The bill amount for changing configurations is calculated hourly, with prices precise to two decimal places.
