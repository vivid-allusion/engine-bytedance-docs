---
title: "Traffic Mirror billing"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Traffic-mirror-billing"
---

Traffic Mirror currently supports pay\-as\-you\-go billing.

<span id=".6K6h6LS55YWs5byP"></span>
## Billing formula

Traffic Mirror is billed based on mirror sessions.

**The cost of a single mirror session = Instance Fee + Traffic Processing Fee**


* Instance fee = Active duration of the Traffic Mirror session (hours) × Instance unit price (USD/hour)

* Traffic processing fee = Amount of used traffic (GB) × Traffic unit price (USD/GB)


If a traffic mirror session is active for less than 1 hour, it will be billed as 1 hour. The following table lists related unit prices:


|Name |Cost |
|---|---|
|Example unit price |0.014 USD/hour |
|Traffic unit price |0.007 USD/GB |


Billing Cycle & Settlement Cycle: Both are based on calendar hours.

On the hour (UTC+8), the platform settles fees, issues bills and deducts payments. 

<span id=".6LS555So56S65L6L"></span>
## Fee example

Mr. A created a mirror session at 10:30:00 on December 1, 2023, and deleted it at 17:00:00 on the same day. The traffic usage is shown in the chart below:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_28cd005d440d3c983069188c522f3a27.png) </span>

Assuming the instance unit price was  (approximately 0.014 USD/hour) and the traffic unit price was  (approximately 0.007 USD/GB). The cost for each specific billing cycle is as follows:


|Billing cycle |Instance fee |Traffic usage (GB) |Traffic processing fee |Cost of the Mirror Session |
|---|---|---|---|---|
|10:00:00 ～ 11:00:00 | 0.0140 x 1 = 0.0140 |0 |0 |0.0140 |
|11:00:00 ～ 12:00:00 | 0.0140 x 1 = 0.0140 |36 |0.007 x 36 = 0.252 |0.266 |
|12:00:00 ～ 13:00:00 | 0.0140 x 1 = 0.0140 |72 |0.007 x 72 = 0.504 |0.518 |
|13:00:00 ～ 14:00:00 | 0.0140 x 1 = 0.0140 |80 |0.007 x 80 = 0.56 |0.574 |
|14:00:00 ～ 15:00:00 | 0.0140 x 1 = 0.0140 |40 |0.007 x 40 = 0.28 |0.294 |
|15:00:00 ～ 16:00:00 | 0.0140 x 1 = 0.0140 |15 |0.007 x 15 = 0.105 |0.119 |
|16:00:00 ～ 17:00:00 | 0.0140 x 1 = 0.0140 |14 |0.007 x 14 = 0.098 |0.112 |
|Total ||||1.897 |


<span id=".5qyg6LS56K-05piO"></span>
## Arrears

An overdue account balance will lead to the suspension of Traffic Mirror services and may even result in resource release. The platform has set a grace period for resources. Within the grace period, the resources are retained and you can continue using the resources after you recharge your account and clear overdue payments. No impact on the features of resources. If the payment overdue period is exceeded, Traffic Mirror resources will be forcibly reclaimed, and all related data will be permanently irrecoverable. Regardless of whether your instances are suspended or released, you shall settle the issued bills based on the actual. 

After payment becomes overdue, the operational and billing status of Traffic Mirror resources is shown in the following diagram:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4303c2674081f2714b2c948196f96010.png) </span>

Based on Your settings, the platform will send you reminders via SMS, email, or internal message during stages such as Traffic Mirror arrears, service suspension due to arrears, and resource release due to arrears. The specific suspension time is subject to the actual situation.
