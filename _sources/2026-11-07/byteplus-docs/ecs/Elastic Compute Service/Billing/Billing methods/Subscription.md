---
title: "Subscription"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Subscription"
---

<span id=".566A5LuL"></span>
## Overview

Subscription is a billing method where you pay in advance, then use the service. It helps you save expenses. In scenarios where long\-term use of Elastic Compute Service (ECS) instances is required, you can purchase subscription instances by prepaying for multiple months or years. This billing method offers more favorable prices compared to the pay\-as\-you\-go method. When you use an ECS instance over one year, you can enjoy an annual discount provided by the platform. For long\-term stable business needs, the subscription mode is your first choice for ECS. This topic describes the billing and settlement rules for subscription instances.

After you purchase Subscription instances, you can still use the compute resources and volumes associated with the instances even if outstanding fees exist in your account. However, if you want to buy new instances or modify the instance configuration, the outstanding fees must be settled when you place new orders.

<span id=".6K6h6LS55LuL57uN"></span>
## Billing overview

Subscription instances can be purchased on a monthly basis (1\-9 months) or a yearly basis (1\-5 years). Refer to the actual order settlement page for specific discounts. Each resource (instance, images, volumes, etc.) is billed separately, and a total cost is generated. Once you have paid for subscription\-based resources, you can use them.

You are allowed to upgrade or downgrade the configurations of subscription instances. For more information, refer to [Changing instance type of subscription instances](https://docs.byteplus.com/en/docs/ecs/Modify-instance-type).

<span id=".6K6h6LS56LWE5rqQ"></span>
## Billed resource


|Resource |Description |
|---|---|
|Compute resources (vCPUs and memory) |When you create an instance, you need to determine whether to use the subscription billing method for the resources. |
|Image |Created when the subscription instance is created. The billing method is subscription and can not be changed. |
|System volume and local volume |Created when the subscription instance is created. The billing method is subscription and can not be changed. |
|Data volume |Subscription applies to data volumes created along with a subscription instance.<br><br>> After you create an instance, you can associate existing pay\-as\-you\-go data volumes with the instance. |
|Elastic IP Address (EIP) |Subscription and pay\-as\-you\-go are available. For more information, refer to [Billing overview](https://docs.byteplus.com/en/docs/eip/Billing-overview). |


<span id=".6LWE5rqQ5Lu35qC8"></span>
## Resource price

On the [Price calculator](https://www.byteplus.com/en/pricing?product=ECS&tab=2) page, you can see the instance price and configuration items (such as system volumes, data volumes, and EIPs). The price calculator provides reference prices. The actual costs are the fee results displayed when you order in the [ECS console](https://console.byteplus.com/ecs/region:ecs+cn-shanghai/instance).

<span id=".57uT566X5ZGo5pyf"></span>
## Settlement cycle

The billing cycle for subscription instances is based on the duration you paid for (UTC+8 time). A billing cycle starts when the resources are provisioned (accurate to the second), and ends at 23:59:59 on the expiration date.

For example, you create a subscription instance on July 1, 2021, at 14:00:00, with a duration of 1 month. The billing cycle will be from 14:00:00 on July 1, 2021 to 23:59:59 on August 1, 2021.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* Subscription instances cannot be deleted before the expiration date. If you want to delete an instance in advance, you can apply to unsubscribe the instance. For information on how to unsubscribe instances, please refer to [Unsubscription description](https://docs.byteplus.com/en/docs/ecs/Renewal-and-unsubscription#.6YCA6K6i6K-05piO).

* Once a subscription\-based data volume is created, it must be associated with a subscription instance and can not be dissociated.
