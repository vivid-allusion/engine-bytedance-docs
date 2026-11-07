---
title: "Subscription"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/subscription"
---

Subscription is a prepaid billing method where payments are made in advance before a new instance is created. Compared with pay\-as\-you\-go Cloud Search instances, subscription Cloud Search instances offer more favorable prices. This topic introduces the billing and settlement cycle of subscription Cloud Search instances.

<span id="简介"></span>
## Introduction

If you require long\-term use of Cloud Search, you can buy subscription instances by paying for them several months or 3 years at most, in advance. Compared with pay\-as\-you\-go instances, subscription instances have preferential prices. On the BytePlus platform, you can receive annual discounts if you buy subscription instances for more than one year.

<span id="购买时长"></span>
## Subscription duration

Subscription Cloud Search instances offer a variety of subscription durations. You can choose an appropriate duration based on your business needs.


* **Monthly subscription**: Buy an instance for 1 to 9 months.

* **Annual subscription**: Buy an instance for 1 to 3 years.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you buy an instance for one year or longer, you can receive a certain discount. For the specific discount, refer to the actual order page in the console.</div>


<span id="9d9b9dd9"></span>
## Billable items

The billable items of Cloud Search include **node specifications** and **storage capacity**. For more information on billable items, refer to [Billable items](https://docs.byteplus.com/en/docs/cloudsearch/billing-items).

In the subscription billing method, the billing formulas are as follows:


* Node specification fee = Unit price of the node instance type per month × Number of nodes × Subscription duration

* Storage capacity fee = Storage capacity of a single node × Unit price of the storage capacity per month × Number of nodes × Subscription duration


<span id="结算周期"></span>
## Billing cycle

The billing cycle of a subscription Cloud Search instance is its subscription duration (based on UTC +08:00). A billing cycle starts at the time when you buy a resource (accurate to seconds) and ends at 23:59:59 of the expiration day.

For example, if you create a subscription instance at 14:00:00 on July 1, 2021 and the subscription duration is 1 month, the billing cycle is from 14:00:00 on July 1, 2021 to 23:59:59 on August 1, 2021.

<span id="退订实例"></span>
## Unsubscribing from an instance

After you delete a subscription Cloud Search instance to unsubscribe from it, refunds are handled according to the unsubscription and refund rules.

<span id="变更配置"></span>
## Changing specifications

You can change the specifications of a subscription instance at any time. After the node specifications are successfully changed, such as the number of shards and the number of shard nodes, you can view the latest specifications of the instance on the **List of Instances** page.

Currently, you can only upgrade specifications for subscription instances. After the node specifications are successfully changed, fees are settled based on the following rules:

Order cost for upgrading specifications = Discounted price of the new specifications \- Remaining value of the instance


* Discounted price of the new specifications = Unit price of the new specifications per month × [Subscription duration after upgrade ÷ (365 ÷ 12)] × Applicable discount (corresponding to the subscription duration after upgrade)

* Remaining value of the instance = Order amount paid for the original specifications \- Unit price per month at the time of purchase × [Days of use ÷ (365 ÷ 12)] × Applicable discount (corresponding to the actual usage duration before upgrade)


<span id="注意事项"></span>
## Precautions

You can still use all subscription Cloud Search instances that you bought even if you have overdue payments. However, you cannot buy new instances or renew your subscriptions until you have paid the outstanding fees. For more information, refer to [Overdue Payment](https://docs.byteplus.com/docs/cloudsearch/overdue).
