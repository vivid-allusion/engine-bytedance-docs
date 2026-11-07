---
title: "Billing of Cloud Recording"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1392577"
---

<span id="charging-items"></span>
## Billable items

When you record RTC calls on the cloud, additional costs are incurred:


* **Recording fee**: Billed based on the recording type (single\-stream or mixed\-stream), the type of recording file generated (audio or video), and duration. Rates vary by recording type (single\-stream or mixed\-stream), media type (audio or video), and video resolution. For detailed billing rules, see [Recording fee](https://docs.byteplus.com/docs/byteplus-rtc/docs-1392577#cloudrecording).

* **Call fees for the recording bot**: When a "cloud recording" task is initiated, the recording bot joins the RTC room and subscribes to the media streams to record. The bot's call costs follow the same rules as those for standard RTC calls. For detailed billing rules, see [Billing of Audio and Video Calls](https://docs.byteplus.com/docs/byteplus-rtc/docs-69871).


<span id="cloudrecording"></span>
## Recording fee

<span id="billing-formula"></span>
### Billing formula

Recording fees = Audio recording unit price x Audio recording billing duration + Video recording unit price for each tier x Video recording billing duration for each tier

<span id="pricing"></span>
### Pricing


|Billing type |Pricing tier |Recorded file specification |Unit price (USD / 1000 minutes) |
|---|---|---|---|
|Single\-stream |Audio |High Quality Audio |0.49 |
||360P |Video resolution: no higher than 360P (800 x 360 = 288000) |0.99 |
||720P |Video resolution \> 360P (288,000 total pixels) and ≤ 720P (1,152,000 total pixels) |1.99 |
||1080P |Video resolution: higher than 720P (1600 x 720 = 1152000); but not higher than 1080P (2400 x 1080 = 2592000) |4.99 |
||2K |Video resolution: higher than 1080P (2400 x 1080 = 2592000), but no higher than 2K (3200 x 1440 = 4608000) |7.99 |
||4K |Video resolution of the public stream: higher than 2K (3200 x 1440 = 4608000), but no higher than 4K (4800 x 2160 = 10368000) |13.99 |
|Mixed\-stream |Audio |High Quality Audio |1.29 |
||360P |Video resolution: no higher than 360P（800 x 360 = 288000） |2.59 |
||720P |Video resolution: higher than 360P (800 x 360 = 288000); but not higher than 720P (1600 x 720 = 1152000) |5.19 |
||1080P |Video resolution: higher than 720P (1600 x 720 = 1152000); but not higher than 1080P (2400 x 1080 = 2592000). |11 |
||2K |Video resolution of the public stream: higher than 1080P (2400 x 1080 = 2592000) , but no higher than 2K (3200 x 1440 = 4608000) |20.59 |
||4K |Video resolution of the public stream: higher than 2K (3200 x 1440 = 4608000), but no higher than 4K (4800 x 2160 = 10368000) |46.29 |


<span id="calculating-billing-duration"></span>
### Calculating billing duration

The billing duration for cloud recording is calculated using the following rules:


* The billing duration is calculated based on the time slots of the files recorded on the cloud. Even if a video stream is not received during the recording process (e.g., if the user turns off the camera), the billing duration will still be counted.

* The pricing tier is determined by the specified recording type (audio or video) when you initiate a cloud recording task. For video recording, the pricing tier is determined by the resolution of the recorded video file.

* When multiple files are recorded, the billing duration is calculated for each file separately and then summed up.


<span id="payment-method"></span>
### Payment method


* **Cloud recording package**: Pay before using the cloud recording service. During settlement, usage is first deducted from your purchased cloud recording package.

* **Pay\-as\-you\-go**: A billing method that allows users to use services first and pay for them afterwards. Charges are settled on a monthly basis and deducted from the user's account balance.
