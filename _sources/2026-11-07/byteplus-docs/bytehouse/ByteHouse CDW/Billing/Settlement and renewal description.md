---
title: "Settlement and renewal description"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/settlement-and-renewal-description"
---

<span id="2712a71e"></span>
## Settlement description

<span id="d0b28a5c"></span>
### Pay\-as\-you\-go

Billing duration: If non\-payment shutdown is not considered, the billing period for the ByteHouse cloud data warehouse edition instance runs from instance creation completion to instance release at the end of its life cycle.

Settlement and Billing: ByteHouse cloud data warehouse edition settles costs every hour on the hour (based on UTC+8 time), and then enters the next billing period.

ByteHouse issues bills daily (with bills issued around 9:00am the next day), followed by real\-time settlement and deduction. If the available credit in your account (including account balance and vouchers) is smaller than the bill pending settlement, you will be considered in arrears, and you will receive a reminder via SMS or email about the insufficiency of funds.

<span id="c65aacfd"></span>
### Annual and Monthly Subscription

The billing period for the ByteHouse annual and monthly subscription instance is the duration you purchased (based on UTC+8 time), with the starting point being the time resources are activated (accurate to seconds) and the endpoint being the expiration date at 23:59:59.

For example, creating an annual and monthly Cluster on July 1st, 2021 at 14:00:00, with a purchase duration of one month, the billing period would be: July 1st, 2021 14:00:00 \- August 1st, 2021 23:59:59.

<span id="cffa3c3f"></span>
## Renewal

You can renew the cluster before the instance expires. Currently, both automatic and manual renewal methods are supported.

<span id="128c1347"></span>
### Manual Renewal

On the [renewal management](https://console.byteplus.com/finance/renew) page, view ByteHouse services that support manual renewal, select the renewal duration and amount, and then purchase.

<span id="fd704ba9"></span>
### Automatic Renewal


* When opening a ByteHouse instance, you can select the automatic renewal option to activate automatic renewal. Support for cancelling is also available on the renewal management page after activation.

* After purchasing the instance, support is also available on the **renewal management** page, under the **manual renewal** tab, where you can select the resources to be renewed and click the **More \> Activate automatic renewal** button in the Actions column.


After activating automatic renewal, if your account has available vouchers, the system will prioritize using the vouchers for renewal.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you do not check<strong>the preset automatic renewal count</strong>, it means the automatic renewal will permanently activate, and the system will perform automatic renewal actions every time a resource expires based on the duration of a single automatic renewal. For more details, refer to <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-of-renewal-rules">renewal management</a>.</div>
