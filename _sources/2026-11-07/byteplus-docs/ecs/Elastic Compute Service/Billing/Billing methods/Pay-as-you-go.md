---
title: "Pay-as-you-go"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Pay-as-you-go"
---

<span id=".566A5LuL"></span>
## Overview

Pay\-as\-you\-go is a billing method that allows you to use resources first and pay for them afterward. Without paying for a large amount of resources in advance, you can activate and release resources on\-demand at any time. Pay\-as\-you\-go is suitable for short\-term business scenarios that experience significant growth, such as limited\-time shopping events. The BytePlus platform calculates fees based on the actual resources you use. You need to pay for what you use in real time. Instance fees are calculated based on the duration of usage, with charges calculated on a second basis. When you no longer need resources, delete them at any time. Once deleted, these resources will not be billed. This topic describes the billing and settlement rules for pay\-as\-you\-go instances.

<span id=".6LSt5Lmw6KaB5rGC"></span>
## Purchase prerequisites


* Before you buy an ECS instance, your account must undergo real\-name authentication.

* After you purchase a pay\-as\-you\-go instance, you can upgrade or downgrade it, as well as expand volumes. For more information, refer to [Changing instance type](https://docs.byteplus.com/en/docs/ecs/Modify-instance-type).


<span id=".6K6h6LS56LWE5rqQ"></span>
## Billed resources

The billed resources and billing duration for pay\-as\-you\-go instances are shown in the following table, except for service suspension due to unpaid fees.


|Resource type |Billing duration |
|---|---|
|Compute resources (vCPUs, memory, GPU cards) |Billing starts when the instance is created. This resource is released automatically when the instance is released and billing ends.<br><br>> Instances with[ Economical Mode](https://docs.byteplus.com/en/docs/ecs/Economical-mode-for-pay-as-you-go-instances) enabled will not incur charges for compute resources after being stopped. |
|Image |Billing starts when the instance is created. Billing ends when the instance is released. |
|Local volume |Billing starts when the instance is created. This resource is released automatically when the instance is released and billing ends. |
|Root volume |Billing starts when the instance is created. This resource is released automatically when the instance is released and billing ends. |
|Storage volume |Billing starts when the volume is created. Billing ends when the volume is released. Billing continues when the volume is disassociated from the instance but not released. |
|Snapshot |Billing (on an hourly basis) starts when the snapshot is created and ends when the snapshot is released. |
|EIP  |Billing starts when the EIP is created. Billing ends when the EIP is released. For more information, please refer to [EIP billing](https://docs.byteplus.com/en/docs/eip/Pay-as-you-go). |


<span id=".6LWE5rqQ5Lu35qC8"></span>
## Resource price

On the [Price calculator](https://www.byteplus.com/en/pricing?product=ECS&tab=2) page, you can see the instance price and configuration items (such as system volumes, data volumes, and EIPs). The price calculator provides reference prices. The actual costs are the fee results displayed when you order in the [ECS console](https://console.byteplus.com/ecs/region:ecs+cn-shanghai/instance).

<span id=".57uT566X5ZGo5pyf"></span>
## Settlement cycle

Billing for pay\-as\-you\-go ECS instances is settled every hour (UTC+8). After this, the next settlement cycle starts. If the available amount in your account (including account balance and vouchers) is less than the outstanding bill, you will receive a notification via SMS or email regarding insufficient balance.

For example: The unit price of an instance is 0.8 USD/hour. With volume, image, or Elastic IP not being considered, the instance's settlement fee is calculated by usage duration, on a second basis.


* For usage of 30 minutes, the cost is: 0.8 / 3600 \* 30 \* 60 = 0.40 USD

* For usage of 1 hour, the cost is: 0.8 \* 1 = 0.80 USD

* For usage of 1 hour 30 minutes, the cost is: 0.8 \* 1 + 0.8 / 3600 \* 30 \* 60 = 1.20  USD
