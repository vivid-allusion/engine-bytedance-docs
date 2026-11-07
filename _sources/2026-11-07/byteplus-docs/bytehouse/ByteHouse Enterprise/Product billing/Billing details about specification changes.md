---
title: "Billing details about specification changes"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/billing-details-about-specification-changes"
---

<span id="集群升级"></span>
# Cluster upgrade

<span id="结算规则"></span>
## Settlement rules

For annual and monthly clusters undergoing configuration upgrades, the settlement rules are as follows:


* The billing duration is by days, and the change in configuration charges on the selected day is attributed to the new configuration purchase.

* The settlement price is accurate to two decimal places.

* The expiration time of the changed resources is consistent with the original purchase resources expiration time.

* The upgrade cost for annual and monthly clusters is the difference between the remaining price of the original cluster and the discounted price of the new cluster, namely: upgrade cost = new cluster configuration discounted price \- original cluster configuration remaining price

   * New cluster configuration discounted price = new cluster monthly unit price \* [upgrade duration (i.e., total days) / (365/12)] \* applicable discount

   * Original cluster configuration remaining price = (upgrade duration (i.e., total days) / original order purchase duration) \* original order discounted price

> Duration matches the remaining unused duration of the original cluster.


<span id="费用计算示例"></span>
## Example of cost calculation

The following content is the calculation process for upgrading the configuration of an annual and monthly cluster. Suppose a cluster was purchased on Oct 1st, 2022, with specifications of 4 cores 16 GiB, 2 nodes, and storage capacity of 100 GB for 3 months, with a total list price of 1808.4 dollars. The discount is 10%, and the actual order price is 1627.56 dollars.

On Nov 1st, 2022, the storage capacity of this cluster will need to be expanded to 200 GB. Total list price is: 645.6/month. The discount is 10%, and the actual price is 581.04 dollar/month.

Then:


* The original order duration was 31 days,

* The purchase duration of the original order was 92 days.

* Updated duration is 61 days.


Therefore:

The remaining price for the original cluster configuration = (61/92)\*1627.56 = 1079.14 dollars

The discounted price for the new cluster configuration = 581.04 \* 61/(365/12)= 1165.26 dollars

In conclusion:

Upgrade cost = 1165.26 \- 1079.14 = 86.12 dollars

<span id="集群降配"></span>
# Cluster downgrade

**Settlement Rules**

When the specifications of the annual or monthly instance exceed your business needs, you can reduce the instance specifications in real\-time (subject to support on the product console). When downgrading, we will calculate refund costs for you, please see [Billing Console-Downgrade](https://docs.byteplus.com/en/docs/byteplus-platform/Billing_Rules_for_Resource_Subscription_Change#downgrade) for specific rules.
