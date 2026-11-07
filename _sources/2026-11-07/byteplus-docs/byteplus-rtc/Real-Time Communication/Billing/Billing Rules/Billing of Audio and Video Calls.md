---
title: "Billing of Audio and Video Calls"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69871"
---

Audio and video call charges refers to the fees incurred by users for subscribing to audio and video streams while utilizing the BytePlus RTC service. Billing is determined based on the type of stream subscribed to and the subscription duration, with charges calculated according to the cumulative subscription time within a calendar day, measured in minutes.

<span id="billing-formula"></span>
## Billing formula

Audio & video call fee = Audio call unit price × Audio duration + Video call unit price × Video durations of different specifications

<span id="pricing"></span>
## Pricing


|Billing type |Pricing tier |Stream specification |Unit price (USD / 1000 minutes) |
|---|---|---|---|
|Audio\-only |Audio\-only |High quality audio |0.99 |
|Video |360P |Video resolution up to 360P (800 x 360 = 288000) |1.99 |
||720P |Video resolution higher than 360P (800 x 360 = 288000); up to 720P (1600 x 720 = 1152000) |3.99 |
||1080P |Video resolution: higher than 720P (1600 x 720 = 1152000); but not higher than 1080P (2400 x 1080 = 2592000) |8.99 |
||2K |Video resolution: higher than 1080P (2400 x 1080 = 2592000), but up to 2K (3200 x 1440 = 4608000) |15.99 |
||4K |Video resolution of the public stream: higher than 2K (3200 x 1440 = 4608000), but no higher than 4K (4800 x 2160 = 10368000) |35.99 |


<span id="calculating-the-billing-duration"></span>
## Calculating the billing duration

When serving your end users, the audio and video usage durations of each user are accumulated and included in your bill. The audio and video billing durations are calculated separately based on the following rules:


* Video billing duration: This refers to the actual duration of all received video streams, accumulated by pricing profiles.

   The duration of a received video stream is measured from when a user starts receiving it until they stop. If a user receives multiple video streams, the duration of each stream is calculated and summed up.

* Audio billing duration: This is the duration of a user in the room without receiving video streams.

   The Audio Billing Duration is calculated when a user joins the RTC room and does not receive any video streams, regardless of whether they are receiving audio streams or not. The duration remains the same regardless of the number of audio streams the user is receiving.

* Special cases

   * If a user subscribes to a video stream but does not receive it (for example, if the sender has turned off their camera), only the audio billing duration is counted.

   * When a user receives a video stream, only the video billing duration is counted. The audio billing duration will not be counted, regardless of whether the video stream contains an audio stream or not.

   * Billing duration starts immediately when a user joins the RTC room, even if they are the only user in the room.

   * If a user joins and leaves the same room multiple times, the duration of each session is calculated and added to the total.

   * When calculating the overall cost of a room, you need to sum the costs for each user in the room.


Here is an example: A user joins the RTC room at T0 and leaves the room at T6. During this period, there are several status changes.

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/pricing/34bfd08-.png) </span>

The audio and video billing duration for the user is as follows:


|Time period |Audio subscription |Video reception |Audio billing duration |Video billing duration by resolution |
|---|---|---|---|---|
|T0 \- T1 |/ |/ |T0 ~ T1 |/ |
|T1 \- T2 |Subscribe to the following audio streams at the same time:<br><br><br>* Audio Stream 1<br><br>* Audio Stream 2 |/ |T1 ~ T2 |/ |
|T2 \- T3 |Audio Stream 2 |Video Stream 1: 360P |/ |360P Video: T2 ~ T3 |
|T3 \- T4 |Audio Stream 2 |Receive the following video streams at the same time:<br><br><br>* Video Stream 1: 360P<br><br>* Video Stream 2: 720P |/ |Video streams from different pricing tiers are billed simultaneously:<br><br>360P Video: T3 ~ T4<br><br>720P Video: T3 ~ T4 |
|T4 \- T5 |Audio Stream 2 |Receive the following video streams at the same time:<br><br><br>* Video Stream 1: 360P<br><br>* Video Stream 2: 720P<br><br>* Video Stream 3: 1080P |/ |Video streams from different pricing tiers are billed simultaneously:<br><br>360P Video: T4 ~ T5<br><br>720P Video: T4 ~ T5<br><br>1080P Video: T4 ~ T5 |
|T5 \- T6 |Audio Stream 2 |/ |T5 ~ T6 |/ |


<span id="payment-method"></span>
## Payment method

Billing is settled monthly, with the following methods available to offset audio and video call fees, in order of priority: 10,000\-minute Free package \> Call package \> Pay\-as\-you\-go.


* **10,000\-minute free package**: Each RTC application (App ID) automatically receives a 10,000\-minute package of free minutes per month. During monthly billing, this free package is applied first to cover your usage (audio and video calls generated by WeChat Mini Programs are excluded).

* **Call package**: This is a prepaid option for purchasing service minutes in bulk. Once the free package is exhausted, your purchased call package is used to cover any remaining usage.

* **Pay\-as\-you\-go**: A billing method that allows users to use services first and pay for them afterwards. Charges are settled on a monthly basis and deducted from your account balance.
