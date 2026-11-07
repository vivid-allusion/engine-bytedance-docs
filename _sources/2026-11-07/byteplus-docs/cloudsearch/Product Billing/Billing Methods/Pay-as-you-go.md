---
title: "Pay-as-you-go"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/pay-as-you-go"
---

Pay\-as\-you\-go is a postpaid billing method that allows you to use resources first and pay later. You do not need to buy a large number of resources in advance. Instead, you can buy and release resources as needed at any time.

<span id="简介"></span>
## Introduction

Pay\-as\-you\-go is suitable for scenarios with significant business growth in the short term. The system generates charges based on the actual resources used and deducts the costs from your account on an hourly basis. This renders you a genuine pay\-for\-what\-you\-use experience. If you no longer use the purchased resources, you can delete them at any time. The billing process stops immediately after you delete a resource.

<span id="购买要求"></span>
## Before you buy


* Create a BytePlus account and ensure that you have completed enterprise real\-name authentication for your account.

* Make sure that the combined value of the available balance in your account, including cash balance and vouchers, is no less than CNY 100.

* You can change the configurations and storage capacity for pay\-as\-you\-go Cloud Search instances at any time.


<span id="0d47d4af"></span>
## Billable items

The billable items of Cloud Search include **node specifications** and **storage capacity**. For more information on billable items, refer to [Billable items](https://docs.byteplus.com/en/docs/cloudsearch/billing-items).

In the pay\-as\-you\-go billing method, the billing formulas are as follows:


* Node specification fee = Unit price of the node instance type per hour × Number of nodes × Usage duration

* Storage capacity fee = Storage capacity of a single node × Unit price of the storage capacity per hour × Number of nodes × Usage duration


<span id="结算周期"></span>
## Billing cycle

Pay\-as\-you\-go Cloud Search instances are billed on an **hourly** basis, with charges settled every hour on the hour (UTC +08:00).

If the available balance in your account, including the cash balance and vouchers, falls below the amount of bills to be settled, you will receive a text message or email that reminds you of an insufficient balance.

<span id="变更配置"></span>
## Changing specifications

You can change node specifications and storage capacity for pay\-as\-you\-go Cloud Search instances at any time. After the specifications are changed, you can view the latest node specifications on the **List of Instances** page. The billing rules for changing specifications for a pay\-as\-you\-go instance are as follows:


* The instance whose specifications are changed is billed based on the price of the new node specifications. Instance prices vary over time. For specific prices, refer to the buy page in the console.

* During the current settlement cycle in which the specification change occurs, instance fees are settled at the price before the change. Starting from the next settlement cycle after the change, the instance fees are settled at the price corresponding to the new specifications. For example, if you change the specifications of a Cloud Search instance at 12:30, the price before the change still applies in the 12:00–13:00 settlement cycle. After 13:00, the new price applies.
