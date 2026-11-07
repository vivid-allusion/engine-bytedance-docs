---
title: "Billing of WTN (Public Stream)"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1392583"
---

<span id="charging-items"></span>
## Billable items

Additional costs are incurred when utilizing server\-side services to combine one or more audio and video streams in a room into one WTN stream for users to subscribe to:


* **Transmuxing and transcoding fee**: Only single\-stream transmuxing is supported, and it is billed based on the task duration. For detailed billing rules, see [Transmuxing and transcoding fee](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1392583?lang=en#transcoding).

* **Audio and video call fees for the cloud processing bot**: When a transmuxing or transcoding task is initiated, a bot joins the RTC room and subscribes to the necessary transcoding or transmuxing audio and video streams. The bot's call costs follow the same rules as those for standard RTC calls. For detailed billing rules, see [Billing of Audio and Video Calls](https://docs.byteplus.com/docs/byteplus-rtc/docs-69871).

* **WTN stream subscription fee**: This fee applies when users subscribe to the WTN stream. For detailed billing rules, see [WTN stream subscription fee](https://docs.byteplus.com/docs/byteplus-rtc/docs-1392583#subscribepublicstream).


<span id="transcoding"></span>
## Transmuxing and transcoding fee

<span id="billing-formula"></span>
### Billing formula


* Transmuxing fee = Transmuxing unit price × Billing duration

* Transcoding fee = Audio transcoding unit price × Audio transcoding billing duration + Video transcoding unit price for each tier × Video transcoding billing duration for each tier


<span id="pricing"></span>
### Pricing


* Transmuxing: The billing rate is the same. On your bill, this item appears as **Push Audio/Video Single\-stream to RTC**.

* Transcoding: For both single\-stream and mixed\-stream transcoding, the billing rate is the same. On your bill, this item appears as **Push xx Mixed\-stream to RTC xx** (even if the task is single\-stream transcoding).



|Task type (TranscodeMode) |Pricing tier |Generated WTN stream type/resolution |Unit price (USD / 1,000 minutes) |
|---|---|---|---|
|Transmuxing |All tiers |All tiers |1.29 |
|Transcoding |Audio\-only |High\-quality audio |1.29 |
||360P |Video resolution of the WTN stream: no higher than 360P (800 x 360) |2.59 |
||720P |Video resolution of the WTN stream: higher than 360P （800 x 360）, but no higher than 720P (1600 x 720 = 1152000) |5.19 |
||1080P |Video resolution of the WTN stream: higher than 720P (1600 x 720 = 1152000), but no higher than 1080P (2400 x 1080 = 2592000) |11 |


<span id="calculating-billing-duration"></span>
### Calculating billing duration


* The billing duration is the total time from the start to the end of the transcoding task.

* If a WTN stream contains both audio and video, only the video tier is used to calculate the billing duration.

* The pricing tier for video is determined by the resolution of the published WTN stream.


<span id="payment-method"></span>
### Payment method

Pay\-as\-you\-go: A post\-paid billing method where charges are settled monthly based on your account's usage. Charges are settled on a monthly basis and deducted from the user's account balance.

<span id="subscribepublicstream"></span>
## WTN stream subscription fee

<span id="billing-formula"></span>
### Billing formula

Subscription fee per user = Audio subscription unit price × Audio subscription billing duration + Video subscription unit price for each tier × Video subscription billing duration for each tier

<span id="pricing"></span>
### Pricing


|Billing type |Pricing tier |Subscribed stream type/specification |Unit price (USD / 1,000 minutes) |
|---|---|---|---|
|Audio call |Audio |High\-quality audio |0.99 |
|Video call |360P |Video resolution of the WTN stream: no higher than 360P (800 x 360) |1.99 |
||720P |Video resolution of the WTN stream: higher than 360P （800 x 360）, but no higher than 720P (1600 x 720 = 1152000) |3.99 |
||1080P |Video resolution of the WTN stream: higher than 720P (1600 x 720 = 1152000), but no higher than 1080P (2400 x 1080 = 2592000) |8.99 |
||2K |Video resolution of the WTN stream: higher than 1080P (2400 x 1080 = 2592000) , but no higher than 2K (3200 x 1440 = 4608000) |15.99 |
||4K |Video resolution of the WTN stream: higher than 2K (3200 x 1440 = 4608000), but no higher than 4K (4800 x 2160 = 10368000) |35.99 |


<span id="calculating-billing-duration"></span>
### Calculating billing duration

The billing duration depends on the type of subscribed streams:


|Subscribed stream type |Billing type |
|---|---|
|None |Audio call |
|Audio streams |Audio call |
|Video Streams |Video call |
|Audio & Video Streams |Video call |


<span id="payment-method"></span>
### Payment method

Pay\-as\-you\-go: A post\-paid billing method where charges are settled monthly based on your account's usage. Charges are settled on a monthly basis and deducted from the user's account balance.
