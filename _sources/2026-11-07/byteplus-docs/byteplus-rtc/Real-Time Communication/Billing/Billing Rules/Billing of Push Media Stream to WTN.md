---
title: "Billing of Push Media Stream to WTN"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1392587"
---

<span id="billing-items"></span>
## Billing Items

When using the [Pushing RTMP Streams to WTN or RTC Rooms](https://docs.byteplus.com/docs/byteplus-rtc/docs-1627491) feature to push local media files or audio and video captured by audio\-video devices to WTN, the following fees will be incurred:


* **Pushing\-Stream Fee**: Charged based on the streaming type (audio or video), streaming specifications, and duration. The unit prices differ for audio and video, and also vary by video specification. For billing rules, please refer to [Pushing-Stream Fee](https://docs.byteplus.com/docs/byteplus-rtc/docs-1392587#wtn).

* **Playing\-Stream Fee**: Charged based on the playback type (audio or video), playback specifications, and duration. The unit prices differ for audio and video, and also vary by video specification. For billing rules, please refer to  [WTN Fees](https://docs.byteplus.com/en/docs/byteplus-rtc/pricing-wtn).


<span id="wtn"></span>
## Pushing\-Stream Fee

<span id="billing-formula"></span>
### Billing Formula

The fee for pushing a stream to WTN = Audio streaming unit price × Audio streaming billing duration + Unit price of each video tier × Billing duration of each video tier

<span id="unit-price"></span>
### Unit Price


|Billing Type |Pricing Tier |Corresponding Streaming Type/Specification |Unit Price (USD/Thousand Minutes) |
|---|---|---|---|
|Audio Call |Pure Audio |Pure audio |1.29 |
|Video Call |360P Video |Video resolution not higher than 360P (800 x 360 = 288000) |2.59 |
||720P Video |Video resolution higher than 360P (800 x 360 = 288000) but not higher than 720P (1600 x 720 = 1152000) |5.19 |
||1080P Video |Video resolution higher than 720P (1600 x 720 = 1152000) but not higher than 1080P (2400 x 1080 = 2592000) |11 |
||2K Video |Video resolution higher than 1080P (2400 x 1080 = 2592000) but not higher than 2K (3200 x 1440 = 4608000) |20.59 |
||4K Video |Video resolution higher than 2K (3200 x 1440 = 4608000) but not higher than 4K (4800 x 2160 = 10368000) |46.29 |


<span id="billing-duration"></span>
### Billing Duration

The billing duration for each WTN video stream is tiered, and the durations of multiple streams are aggregated.


* Duration of each WTN stream actually received: The duration from when a user successfully pulls the stream until they stop receiving it.

* Tiered Pricing: Streams are classified into pricing tiers based on their resolution, with each tier having a different unit price.


<span id="playing-stream-fee"></span>
## Playing\-Stream Fee

Refer to [WTN Fees](https://docs.byteplus.com/en/docs/byteplus-rtc/pricing-wtn) for playback billing details.

<span id="payment-methods"></span>
### Payment Methods


* **Pay\-as\-you\-go**: Use first, pay later, and settle monthly. A bill for the previous month is issued at the beginning of each month, and the fee is deducted from your account balance.


<span id="billing-example"></span>
## Billing Example

Assume that a 10\-minute 1080P video is pushed, and User A pulls a 1080P video WTN stream for 10 minutes. Then the billed amount is:

Video pushing\-stream fee (1080P) + Video pulling\-stream fee (1080) = 0.011 \* 10 + 0.00899 \* 10 = 0.1009 USD.
