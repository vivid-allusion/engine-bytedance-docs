---
title: "Billing overview"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/billing-overview"
---

This article helps you quickly understand the main billing information of Vital Managed Service for Prometheus, including billing components, cycles, and methods.

<span id=".6K6h6LS56K-05piO"></span>
## Billing description

Vital Managed Service for Prometheus supports the **pay\-as\-you\-go** billing method, helping enterprises significantly reduce resource costs and expenses. The billing methods are shown in the table below.


|Instance type |Billing method |Billing Items |Descriptions |
|---|---|---|---|
|Standard Edition |[Pay as you go](https://docs.byteplus.com/en/docs/vmp/pay-as-you-go) |Reported metric volume |Postpaid: Cumulative tiered billing is applied based on the reported metric volume (number of metric samples). Bills are generated per settlement cycle (settled hourly), and corresponding fees are deducted from your account balance. |
|||Written metric volume |Postpaid: Cumulative billing is applied based on the written metric volume (metric data size). Bills are generated per settlement cycle (settled daily), and corresponding fees are deducted from your account balance. |
||[Package](https://docs.byteplus.com/en/docs/vmp/Resource-packages) |Package Specifications |Prepaid: You purchase a resource package in advance. During fee settlement, usage is first offset by the quota offered by the resource package. For usage that exceeds the resource package quota or occurs after the resource package expires, settlement will be performed according to the rules for billing by reported volume.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Currently, resource packages can be applied only to standard workspaces billed by reported volume. The resource package to apply to a workspace must have the same duration as the storage retention period of the workspace.</div><br> |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For billing items and price details of different instance specifications, please refer to <a href="https://docs.byteplus.com/en/docs/vmp/pay-as-you-go">Pay\-as\-you\-go</a> and <a href="https://docs.byteplus.com/en/docs/vmp/Resource-packages">Package</a>.</div>


<span id=".57uT566X5ZGo5pyf"></span>
## Billing cycle


* For billing by reported volume, the settlement cycle is **hourly**, meaning bills are generated based on the resource usage within each hour.

* For billing by written volume, the settlement cycle is **daily**, meaning bills are generated based on the resource usage of each calendar day.


<span id=".5Ye66LSm5pe26Ze0"></span>
## Billing time

The bill fees are automatically deducted from your account. You can view the bill details in the [Cost Center](https://console.byteplus.com/finance/bill/detail).


* For billing by reported volume, bills are generated per **hourly** settlement cycle, with **USD** as the settlement unit.

* For billing by written volume, bills are generated per **daily** settlement cycle, with **USD** as the settlement unit.


<span id=".6YCA6K6i5ZKM5pu06YWN"></span>
## Cancellation and configuration change


* Pay\-as\-you\-go does not involve cancellation and configuration change.

* Packages support 7\-day no\-reason cancellation and refund, and support package specification configuration change. For details, please refer to [Cancellation and Configuration Change](https://docs.byteplus.com/en/docs/vmp/Unsubscribing-from-a-resource-package-and-changing-the-specification).
