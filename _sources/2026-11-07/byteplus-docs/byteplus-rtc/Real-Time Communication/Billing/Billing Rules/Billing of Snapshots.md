---
title: "Billing of Snapshots"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1392580"
---

<span id="charging-items"></span>
## Billable items

Additional costs are incurred when utilizing RTC services capture snapshots of video streams:


* **Snapshot fee**: Billed based on task duration. For detailed billing rules, see [Snapshot fee](https://docs.byteplus.com/docs/byteplus-rtc/docs-1392580#snapshot).

* **Audio and video call fees for the snapshot bot**: When a "snapshot" task is initiated, the snapshot bot joins the RTC room and subscribes to the media streams that require snapshot capture. The bot's call costs follow the same rules as those for standard RTC calls. For detailed billing rules, see [Billing of Audio and Video Calls](https://docs.byteplus.com/docs/byteplus-rtc/docs-69871).


<span id="snapshot"></span>
## Snapshot fee

<span id="billing-formula"></span>
### Billing formula

Snapshot fee = Snapshot unit price × Billing duration

<span id="pricing"></span>
### Pricing


|Pricing tier |Unit price (USD / 1000 minutes) |
|---|---|
|Snapshot |0.59 |


<span id="calculating-billing-duration"></span>
### Calculating billing duration

The billing duration for the snapshot service is the total time spent capturing snapshots.

<span id="payment-method"></span>
### Payment method

Pay\-as\-you\-go: A billing method that allows users to use services first and pay for them afterwards. Charges are settled on a monthly basis and deducted from the user's account balance.
