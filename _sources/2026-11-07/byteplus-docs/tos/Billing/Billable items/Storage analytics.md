---
title: "Storage analytics"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Storage-analytics"
---

You pay to use Storage Lens, a storage analytics solution in TOS, with advanced metrics. This topic explains how you are charged for storage analytics.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This topic only provides a description of billable items. For specific prices, see <a href="https://www.byteplus.com/en/pricing?product=TOS&tab=1">TOS pricing details</a>.</div>


<span id="131cda64"></span>
## Notes


* You only pay for Storage Lens dashboards with advanced metrics enabled.

* Each dashboard incurs a monitoring fee. These charges are based on the number of objects monitored by the dashboard. To avoid duplicate charges across multiple dashboards, consolidate monitoring of similar metrics within a single dashboard.

* The number of monitored objects on each dashboard is equal to the total number of objects in all buckets added to that dashboard.


<span id="bbcd7029"></span>
## Billing cycle

TOS generates charges after each dashboard finishes collecting statistics. Each dashboard typically runs statistics once per day at most and incurs one charge per day.

As shown in the [TOS pricing details](https://www.byteplus.com/en/pricing?product=TOS&tab=1), the storage analytics pricing unit is  **$/one million objects/month**. For actual bills, TOS converts  **$/one million objects/month** into  **$/one million objects/day**, using the following formula: Daily rate = Monthly rate ÷ 30 (days).

<span id="b9bd2f7f"></span>
## Billable item


|**Billable item** |**Description** |**Billing method** |
|---|---|---|
|Storage analytics |The cost of using Storage Lens dashboards with advanced metrics is calculated based on the number of objects monitored by each dashboard. |**Pay\-as\-you\-go**: Storage analytics cost = Number of monitored objects × Unit price ÷ 1,000,000 |


<span id="0685c629"></span>
## Example

You created three dashboards with advanced metrics, each monitoring 1,000,000 objects. Your daily charges will be calculated as follows:

3 × 1,000,000 ÷ 1,000,000 × (0.2 $ **/one million objects/month** ÷ 30) = 0.02 $
