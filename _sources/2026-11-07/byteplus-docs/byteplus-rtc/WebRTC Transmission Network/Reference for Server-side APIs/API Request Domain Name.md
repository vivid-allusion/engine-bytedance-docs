---
title: "API Request Domain Name"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/wtn-domain"
---

WTN provides several domain names for creating/destroying/setting publishing and subscribing resources.

The available domain names are listed below:


|Domain Name |Service Region |
|---|---|
|`wtn-va.rtcplus.com` |North America |
|`wtn-sg.rtcplus.com` |Asia\-Pacific |
|`wtn-fr.rtcplus.com` |Europe |
|`wtn.rtcplus.com`(Recommended) |Global (excluding Mainland China) |


When using `wtn.rtcplus.com`, WTN will automatically route to the nearest data center according to the user's location. For example, a request initiated in Singapore will automatically route to the data center in Singapore, which is the same as specifying `wtn-sg.rtcplus.com`.

If a request fails due to a connection error or a `5xx` HTTP status code, retry it using the same or a different domain name. If you receive a `4xx` status code, verify that your request is valid by checking details like the parameter format and token validity.
