---
title: "Subscription"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ecs_billing_subscription"
---

Subscription, also known as prepaid, is a payment method for Volcano Engine E\-MapReduce (EMR) clusters where you pay for resources in advance before use. This model is suitable for use cases where computing and storage resources are relatively fixed. The minimum purchase duration for EMR Subscription is one month.

<span id="7d89a18b"></span>
## **Limits**


* For Subscription instances, node deletion is not supported before expiration.


<span id="b02150dc"></span>
## **Billing rules**


* The Subscription price in the Johor region is $7.47 USD per core per month, and $89.64 USD per core per year.

* Once Subscription payment is successfully completed, services are provided immediately, and the billing start time is the day the cluster is launched.

* The Subscription amount for a cluster is calculated as unit price × total number of cores in the cluster × purchase duration. If the cluster is expanded during operation, only the Subscription duration fee for the newly added nodes will be charged.


<span id="cb921020"></span>
## **Settlement cycle**

The EMR service Subscription cloud billing cycle is based on the duration you purchase (UTC+8 time). The start of a billing cycle is the time when resources are activated (accurate to the second), and the end is 23:59:59 on the expiration date. For example, if you purchase one month at 00:00:00 on 2022\-04\-10, the expiration time is 23:59:59 on 2022\-05\-09. If you purchase after 00:00:01 on 2022\-04\-10, the expiration time is 23:59:59 on 2022\-05\-10.

The payment type for EMR creation is directly associated with and fully consistent with the payment type for basic resources (ECS, Elastic Block Storage, Public IP).

<span id="46cb16b3"></span>
## **Overdue payments**

There is no concept of overdue payments for Subscription clusters. If your account has overdue payments, you can continue to use purchased EMR clusters that have not yet expired.

However, to expand node disk capacity or change ECS configuration, you must settle any outstanding account payments before performing these operations.

For details, see [Overdue payments](https://docs.byteplus.com/docs/E-MapReduce/109018).

<span id="5fe35ca7"></span>
## Expiration

For details on resource changes after Subscription cluster expiration, see [Expiration instructions](https://docs.byteplus.com/docs/E-MapReduce/109032).

<span id="8bc644e1"></span>
## View bills

During the use of Volcano Engine E\-MapReduce (EMR), if you have questions about EMR consumption, you can view the billing statement and consumption details via **Expense Center**. For details, see [Bill management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-billing-management).
