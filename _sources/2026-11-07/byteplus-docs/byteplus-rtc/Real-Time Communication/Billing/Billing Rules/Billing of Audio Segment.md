---
title: "Billing of Audio Segment"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1392579"
---

<span id="charging-items"></span>
## Billable items

Additional costs are incurred when utilizing RTC services to segment audio streams:


* **Audio segment fee**: Billing is based on the total duration of all generated audio segments. For detailed billing rules, see [Audio segment fee](https://docs.byteplus.com/docs/byteplus-rtc/docs-1392579#segment).

* **Audio and video call fees of the audio segmentation bot**: When a "audio segmentation" task is initiated, the audio segmentation bot joins the RTC room and subscribes to the media streams that require segmentation. The bot's call costs follow the same rules as those for standard RTC calls. For detailed billing rules, see [Billing of Audio and Video Calls](https://docs.byteplus.com/docs/byteplus-rtc/docs-69871).


<span id="segment"></span>
## Audio segment fee

<span id="billing-formula"></span>
### Billing formula

Audio segment fee = Audio segment unit price × Billing duration

<span id="pricing"></span>
### Pricing


|Billing type |Unit price (USD / 1000 minutes) |
|---|---|
|Audio segment |0.29 |


<span id="calculating-billing-duration"></span>
### Calculating billing duration


* The billing duration is the total usage time of the audio segmentation service.

* If a stream publisher mutes their microphone during the segmentation process, the duration of the resulting silent audio segments is also included in the billed duration.


<span id="payment-method"></span>
### Payment method

Pay\-as\-you\-go: A billing method that allows users to use services first and pay for them afterwards. Charges are settled on a monthly basis and deducted from the user's account balance.
