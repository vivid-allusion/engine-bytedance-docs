---
title: "Pricing"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/pricing-wtn"
---

When using WTN services, you are required to pay for your WTN subscription connections and WTN streams subscribed.

Usage and expense data on the RTC console and in the bill are calculated on a monthly basis. Daily expenses can also be reviewed on the console. Please note that due to minute\-level accuracy and rounding up, there might be a slight difference between the monthly bill and the sum of daily charges on the console. The charges on your monthly bill are final.

<span id="pricing-scheme"></span>
## Pricing Scheme

`WTN cost = (Audio subscription unit price * (WTN subscription connection billing duration + Audio stream subscription billing duration)) + (Video subscription unit price × Video stream subscription billing duration)`

<span id="stream-subscription-unit-price"></span>
### Stream Subscription Unit Price

WTN stream subscription pricing depends on the stream type (audio or video) and video specifications.


|Pricing Type |Pricing Profile |Specifications |Unit Price (USD / 1000 Minutes) |
|---|---|---|---|
|Connection established without stream subscription |Audio |High Quality Audio |0.99 |
|WTN Audio Stream Subscription |Audio |High Quality Audio |0.99 |
|WTN Video Stream Subscription |360P |Video resolution: no higher than 360P (800 x 360) |1.99 |
||720P |Video resolution: higher than 360P (800 x 360), but no higher than 720P (1600 x 720 = 1152000) |3.99 |
||1080P |Video resolution: higher than 720P (1600 x 720 = 1152000), but no higher than 1080P (2400 x 1080 = 2592000) |8.99 |
||2K |Video resolution: higher than 1080P (2400 x 1080 = 2592000), but no higher than 2K (3200 x 1440 = 4608000) |15.99 |
||4K |Video resolution: higher than 2K (3200 x 1440 = 4608000), but no higher than 4K (4800 x 2160 = 10368000) |35.99 |


<span id="calculating-the-billing-duration"></span>
### Calculating the Billing Duration

The billing duration for WTN is calculated based on the subscribed stream types.


|Subscribed Stream Type |Pricing Type |
|---|---|
|Connection established without stream subscription |Audio Call |
|Audio Streams |Audio Call |
|Video Streams |Video Call |
|Audio & Video Streams |Video Call |
