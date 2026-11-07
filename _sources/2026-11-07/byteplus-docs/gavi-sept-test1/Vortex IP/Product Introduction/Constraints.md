---
title: "Constraints"
product: "Vortex IP"
product_code: "gavi-sept-test1"
source: "https://docs.byteplus.com/en/docs/gavi-sept-test1/Constraints"
---

<span id=".6YWN6aKd6ZmQ5Yi2"></span>
## Quota


|Limit Item |Upper Limit |Quota description |
|---|---|---|
|Number of Virtual Private Clouds (VPC) Attached by a single Vortex IP instance |1 Gateway |Cannot be adjusted |
|Number of inbound allowlist entries that a single internet access mode Vortex IP instance can add |20 |Please contact your account manager. |


<span id=".5oCn6IO96ZmQ5Yi2"></span>
## Performance limits


|Billing method  |New Connections Per Second |Max Connections |Maximum Bandwidth When Purchasing an EIP (Mbps) |Maximum Bandwidth When Changing Specifications (Mbps) |Can Maximum Bandwidth Be Increased |
|---|---|---|---|---|---|
|Pay\-as\-you\-go |200 ～ 20000<br><br>New Connections Per Second = 10 × Bandwidth Limit |1000 ～ 100000<br><br>Max Connections = 50 × Bandwidth Limit |20 ～ 2000 |20 ～ 2000 |Please contact your account manager. |



* When purchasing Vortex IP, you need to specify the bandwidth limit (the outbound and inbound bandwidth limits are consistent with the values you set), and the platform will calculate the fee based on actual traffic.

* Vortex IP adopts a distributed high availability deployment architecture. When the number of connections is too low, the bandwidth limit of the instance cannot be reached. It is recommended that you configure it reasonably.


<span id=".5L2_55So6ZmQ5Yi2"></span>
##  Limits

Vortex IPs of the **Dynamic Residential Proxy** Service Type are not supported to access the following websites:


|Type  |Website |
|---|---|
|Entertainment and social category |Spotify, Netflix, Twitch, Disney, Playstation, Steam |
|Platform category |LinkedIn, Google, Microsoft, and websites related to the domain names of these three platforms |
|Banking and financial sectors |Paypal, Stripe, Binance |
|Ticketing\-related |Ticketmaster, Eventim, SeatGeek |
|Email category |Yahoo, Outlook |
|Advertisement\-related |Doubleclick, Pubmatic, Google Tag Manager, Google Ads Services |
|Government sectors |All government\-related websites |
