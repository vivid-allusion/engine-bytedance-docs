---
title: "Billing of Push to CDN"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1392578"
---

<span id="charging-items"></span>
## Billable items

Additional costs are incurred when you use server\-side capabilities to push RTC streams to CDN:


* **Push to CDN fee**: Billing is determined based on the type of relay (single\-stream or mixed\-stream), task duration, and the type of stream pushed to the CDN. Pricing depends on whether the stream is single or mixed, and audio or video. Different rates also apply based on video specifications. For detailed billing rules, see [Push to CDN fee](https://docs.byteplus.com/docs/byteplus-rtc/docs-1392578#transcode).

* **Bot audio and video call fees**: When a "push to CDN" task is initiated, a bot joins the RTC room and subscribes to the media streams to push them to the CDN. The bot's call costs follow the same rules as those for standard RTC calls. For detailed billing rules, see [Billing of Audio and Video Calls](https://docs.byteplus.com/docs/byteplus-rtc/docs-69871).


<span id="transcode"></span>
## Push to CDN fee

<span id="billing-formula"></span>
### Billing formula

Push to CDN cost = Audio pushing unit price × Audio pushing billing duration + Video pushing unit price for each tier × Video pushing billing duration for each tier

<span id="pricing"></span>
### Pricing


|Billing type |Pricing tier |Resolution/type of stream pushed to CDN |Unit price (USD / 1000 minutes) |
|---|---|---|---|
|Single\-stream |All tiers (no transcoding) |All tiers (no transcoding) |1.29 |
|Mixed\-stream |Audio\-only |High quality audio |1.29 |
||360P |Video resolution of the stream pushed to CDN: no higher than 360P (800 x 360 = 288000) |2.59 |
||720P |Video resolution of the stream pushed to CDN: higher than 360P (800 x 360 = 288000) and not higher than 720P (1600 x 720 = 1152000) |5.19 |
||1080P |Video resolution of the stream pushed to CDN: higher than 720P (1600 x 720 = 1152000) and not higher than 1080P (2400 x 1080 = 2592000) |11 |


<span id="calculating-billing-duration"></span>
### Calculating billing duration

The billing duration for pushing streams to a CDN is calculated as follows:


* For a Push to CDN task, the billing duration is the total time from the start to the end of the push.

* Calculation rules for pricing tiers:

   * When initiating a stream push task, the pricing profile (audio/video) is determined based on the specified transcoding type.

   * If the pushed stream contains both audio and video, the billing duration is calculated using the video pricing profile.

   * For pushing video streams to the CDN, the billing duration is calculated based on the resolution of the pushed video stream.

* When multiple stream push tasks are active in an RTC call, the billing duration is calculated for each task and then aggregated.


<span id="payment-method"></span>
### Payment method


* **Push to CDN package**: Pay before using the Push to CDN service. During settlement, usage is first deducted from the purchased Push to CDN package.

* **Pay\-as\-you\-go**: A billing method that allows users to use services first and pay for them afterwards. Charges are settled on a monthly basis and deducted from the user's account balance.
