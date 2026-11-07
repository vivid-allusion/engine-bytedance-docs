---
title: "Billing of WebRecord"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1392582"
---

When using the server\-side webrecord service to relay the content of a specified webpage to an RTC room for users to watch, fees are calculated based on the duration of the task.

<span id="billing-formula"></span>
## Billing formula

Webrecord cost = Webrecord unit price × Billing duration

<span id="pricing"></span>
## Pricing


|Pricing tier |Resolution |Unit price (USD / 1000 Minutes) |
|---|---|---|
|360P |Video resolution: no higher than 360P (800 x 360) |4.9 |
|720P |Video resolution: higher than 360P （800 x 360）, but no higher than 720P (1600 x 720 = 1152000) |9.9 |
|1080P |Video resolution: higher than 720P (1600 x 720 = 1152000), but no higher than 1080P (2400 x 1080 = 2592000) |15 |


<span id="calculating-billing-duration"></span>
## Calculating billing duration


* The billing duration is the total time from a task's start to its end.

* For the same page, if multiple tasks are enabled, the cost will be charged for each task.


<span id="payment-method"></span>
## Payment method

Pay\-as\-you\-go: A billing method that allows users to use services first and pay for them afterwards. Charges are settled on a monthly basis and deducted from the user's account balance.
